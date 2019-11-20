---
title: Use `mmap` to create shared objects 
date: 2019-11-20 11:01:00
tags: [unix, network programming, mmap, shared memory, shared object]
---

當我們有很多 processes 時，並想用實現 shared memory 處理共用資料時，就可以使用 shared memory，來實作。建立 shared memory 可以使用 `mmap` 或是 System V `shmget`，但根據 Stack Overflow 「[How to use shared memory with Linux in C](https://stackoverflow.com/questions/5656530/how-to-use-shared-memory-with-linux-in-c)」回答，`shmget` 已經有點過時，`mmap` 則比較新和彈性。

Shared memory 讓我們可以建立一塊共用的記憶體空間，`mmap` 會回傳一塊記憶體空間的指標，型別是 `void *`，如果我們想要放資料進去，可以用 `memcpy` 將物件、字串或任何東西拷貝進去。我們也可以直接將 `void *` 轉型成物件指標，這樣就建立 shared object，不同 process 可以直接對 process 存取物件。

<!-- more -->

實作範例：

```shell
$ g++ mmap.cc -std=c++17
```

```c++
// mmap.cc 

#include <memory>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/mman.h>
#include <unistd.h>

template <typename T> T *create_shared_memory() {
  // 可讀、可寫
  int protection = PROT_READ | PROT_WRITE;

  // MAP_SHARED 代表分享給其他 process，MAP_ANONYMOUS 讓使其只被自己和 child 可見
  int visibility = MAP_SHARED | MAP_ANONYMOUS;

  // 詳細參數使用見 man mmap
  // 為啥要放 -1 可以看這篇 https://stackoverflow.com/questions/37112682/
  void *ptr = mmap(NULL, sizeof(T), protection, visibility, -1, 0);

  // 將記憶體轉型成 T 物件指標
  return reinterpret_cast<T *>(ptr);
}

struct Bar {
  int a;
  int b;
  Bar(int a, int b) : a(a), b(b) {}
};

struct Foo {
  Bar bar[30];
};

int main() {

  // 建立 Foo * 在 shared memory 中
  auto *foo = create_shared_memory<Foo>();

  auto print = [=]() {
    for (auto i = 0; i < 3; i++) {
      printf("%d: %d, %d\n", i, foo->bar[i].a, foo->bar[i].b);
    }
    // 印出 Foo 的地址，檢驗 parent 和 child 是共用
    printf("Foo: %p\nFoo.bar: %p\n---\n", foo, foo->bar);
  };

  // 初始化
  foo->bar[0] = Bar(0, 0);
  foo->bar[1] = Bar(0, 0);
  foo->bar[2] = Bar(0, 0);
  
  printf("data before fork: \n");
  print();

  if (!fork()) {  // child

    printf("Child read:\n");
    print();

    // 改動 shared object
    foo->bar[1].a = 2;
    foo->bar[1].b = 3;

    printf("Child wrote:\n");
    print();

  } else { // parent
    printf("Parent read:\n");
    print();

    sleep(1);

    printf("After 1s, parent read:\n");
    print();
  }
}
```

不過要注意的是，shared object 不能放 STD container，因為 container 產生的指標只能在當下那個 process 所用，其他 process 讀不到。

我想到兩種解法可以處理，一種是自己實作 STD container 的 allocator；另一種是將大物件的 container 裡面的小物件都先建立在 shared memory 中，大物件初始化的時候再把小物件一個一個塞回 container。

第二種實作大概像這樣：

```c++
struct Foo {
  std::vector<std::unique_ptr<Bar>> bars;
};

void main() {
  std::vector<Bar *> bars;
  for(int i = 0; i < 10; i++) {
    auto *bar = create_shared_memory<Bar>();
    bars.push_back(bar);
  }

  if(!fork()) {
    // 生成新的 process 才建立 Foo
    Foo foo1;

    // 把 foo 中的 bar 們一個一個塞回來
    for(size_t i = 0; i < bars.size(); i++) {
      std::unique_ptr<Bar> u_bar;
      u_bar.reset(bars.at(i));
      foo1.push_back(std::move(u_bar));
    }

    // 接下去 foo1 都會另一個 process 的 foo2 共用資料
  } else {
    Foo foo2;

    // 一樣把 bar 塞回來
    // ...
  }
  // ...
}
```
