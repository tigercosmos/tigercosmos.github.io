---
title: Example of Signals by `sigaction` in Unix 
date: 2019-11-24 11:01:00
tags: [unix, network programming, signal, sigaction]
---

Unix 中 processes 之間溝通有很多種，本篇介紹 signal 的簡易使用。可以先閱讀 [Beej 的介紹](http://beej.us/guide/bgipc/html/single/bgipc.html#signals)。顧名思義，signal 就是程序發送和接受訊號，例如我們在使用 Shell 的時候，之所以 `Ctrl-C` 可以中斷程式執行，就是因為 Shell 捕捉到 `Ctrl-C` 發送的 `SIGINT` 訊號，知道有一個 interrupt signal，所以將程式中斷。

發送 signal 可以用 [`sigaction()`](http://man7.org/linux/man-pages/man2/sigaction.2.html) 或 [`signal()`](http://man7.org/linux/man-pages/man7/signal.7.html)，不過建議使用 `sigaction` 因為比較新，詳細差別可以看 Stack Overflow 這篇 「[What is the difference between sigaction and signal?](https://stackoverflow.com/questions/231912/what-is-the-difference-between-sigaction-and-signal)」。

如果想觸發 signal，可以用 [`kill()`](http://man7.org/linux/man-pages/man2/kill.2.html) 或 [`sigqueue()`](http://man7.org/linux/man-pages/man3/sigqueue.3.html)，差別在於後者僅限 Linux，但後者可以藉由傳送 `siginfo` 加一些資訊在 signal 中。此外一些 system call 本身也會觸發 signal，例如如果嘗試 `send()` 到不存在的 `socket`，就會觸發 `SIGPIPE`。

<!-- more -->

以下為簡單範例，如果想知道更詳盡參數設定，還是要去看 man：

<pre><code class="c++">// signal.cc
#include &lt;signal.h&gt;
#include &lt;stdio.h&gt;
#include &lt;stdlib.h&gt;
#include &lt;string.h&gt;
#include &lt;unistd.h&gt;

int main(int argc, char **argv) {
  // 宣告 sigaction 物件
  struct sigaction act;
  memset(&act, 0, sizeof act);

  // 建立 signal handler，應該盡可能簡化 handler 要做的事情
  // 並且要小心 signal 執行時，原程式已經在做了一樣的事情
  act.sa_sigaction = [](int signo, siginfo_t *info, void *context) {
    if (signo == SIGINT) { // 接收 Ctrl-C
      printf("Received SIGINT.\n");
    } else if (signo == SIGUSR1) { // 接收數字
      int int_val = info-&gt;si_value.sival_int;
      printf("recieve: %d\n", int_val);
    } else if (signo == SIGUSR2) { // 接收指標
      void *ptr = info-&gt;si_value.sival_ptr;
      printf("recieve: %p\n", ptr);
    }
  };

  // sa_sigaction 必須搭配 SA_SIGINFO，否則會呼叫 act.sa_handler
  // 但我們要 sa_sigaction 才能接收 siginfo
  //
  // 其他參數：
  //  重新啟動可被中斷的 system call 要設 SA_RESTART
  //  想要有 SIGCHLD 需要設 SA_NOCLDWAIT;
  act.sa_flags = SA_SIGINFO;

  // 設定 SIGUSR1
  if (0 != sigaction(SIGUSR1, &act, NULL)) {
    perror("sigaction () failed installing SIGUSR1 handler");
    return EXIT_FAILURE;
  }
  // 設定 SIGUSR2
  if (0 != sigaction(SIGUSR2, &act, NULL)) {
    perror("sigaction() failed installing SIGUSR2 handler");
    return EXIT_FAILURE;
  }

  // 設定 SIGINT
  if (0 != sigaction(SIGINT, &act, NULL)) {
    perror("sigaction() failed installing SIGUSR2 handler");
    return EXIT_FAILURE;
  }

  // 執行 15 秒，過程中可以嘗試按 Ctrl-C
  for (int i = 1; i &lt;= 15; i++) {
    // 第二秒觸發 SIGUSR1 並送出 123
    if (i == 2) {
      union sigval value;

      // 目標 process 的 pid，這邊要送給自己，為自己的 pid
      int pid = getpid();

      // sigval 是 union，sival_int 或 sival_ptr 只能擇一
      value.sival_int = 123;

      if (sigqueue(pid, SIGUSR1, value) == 0) {
        printf("signal sent successfully!!\n");
      } else {
        perror("SIGSENT-ERROR:");
      }
    }

    // 第二秒觸發 SIGUSR2 並送出 act 的地址
    if (i == 4) {
      union sigval value;
      pid_t pid = getpid();

      value.sival_ptr = &act;
      if (sigqueue(pid, SIGUSR2, value) == 0) {
        printf("signal sent successfully!!\n");
      } else {
        perror("SIGSENT-ERROR:");
      }
    }

    // 第二秒觸發 SIGUSR1 並送出 3333
    if (i == 6) {
      union sigval value;
      int pid = getpid();

      value.sival_int = 3333;
      if (sigqueue(pid, SIGUSR1, value) == 0) {
        printf("signal sent successfully!!\n");
      } else {
        perror("SIGSENT-ERROR:");
      }
    }

    printf("Tick #%d.\n", i);

    sleep(1);
  }

  return EXIT_SUCCESS;
}

</pre></code>

執行結果如下

<pre><code class="shell">$ g++ signal.cc
$ ./a.out
Tick #1.
recieve: 123
signal sent successfully!!
Tick #2.
Tick #3.
^CReceived SIGINT.
recieve: 0x7ffde08e7970
signal sent successfully!!
Tick #4.
Tick #5.
^CReceived SIGINT.
recieve: 3333
signal sent successfully!!
Tick #6.
^CReceived SIGINT.
Tick #7.
Tick #8.
^CReceived SIGINT.
Tick #9.
^CReceived SIGINT.
Tick #10.
Tick #11.
^CReceived SIGINT.
Tick #12.
Tick #13.
Tick #14.
Tick #15.
</pre></code>
