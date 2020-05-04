---
title: Programming Servo--The Debug Way
date: 2018-08-26 00:00:00
tags: [ servo, debug, gdb, rust, english,]
---


## Programming Servo: The Debug Way

### Debug Servo and Rust in a modern way

<img class="dz t u gs ak" src="https://miro.medium.com/max/1800/0*O7DEcy3heyrWOYEf.png" role="presentation"><br/>

Servo is a huge project. I have counted the lines of code for you. There are almost a hundred thousand lines of code in the Servo project. To develop such a big project, knowing how to debug in a right way is very important, since you would like to find the bottleneck in a fast and efficient way.

In this article, I will teach you some tips to use GDB developing and debugging your Rust code in the Servo project.

<!-- more --> 

## So, How to Debug?

I assume you are not familiar with software developing, but you have some skills to write codes.

So when you want to know somethings in the box, you might add some lines, such as:

```rust
println!("{:?}", SOMETHING);
```

This is a simple method. Straightforward enough! It does help you to figure out what’s going on about the code.

However, it requires compiling each time when you want to know another variable’s value in the program. Besides, when your program crashes or causes memory leak, it is hard to trace the underlying problem.

The simple way is not helpful enough, which means you need a more powerful tool. It could be GDB in Linux, or LLDB in macOS. (On Windows platform, VS debugger is also a very strong tool, but not in discussion in this article.)

I will talk about how to use GDB then. LLDB is very similar to GDB. Basically, their commands are almost the same, so I would just introduce how to use GDB to debug the Rust and the Servo.

## Introduction to GDB

<span style="font-size: 26px; color: #696969; font-style:italic">“GDB, the GNU Project debugger, allows you to see what is going on ‘inside’ another program while it executes — or what another program was doing at the moment it crashed.” — -from gnu.org</span>

<em class="at">“GDB, the GNU Project debugger, allows you to see what is going on ‘inside’ another program while it executes — or what another program was doing at the moment it crashed.” — -from </em><a href="https://www.gnu.org/software/gdb/" class="dj by in io ip iq" target="_blank" rel="noopener nofollow"><em class="at">gnu.org</em></a>

In other words, GDB allows you to control the program running and to get more information from the inside of the code.

For example, you can stop the program at a certain line in a file, which is called a “breakpoint”. When the program stops at the breakpoint, you can print them to see the values of the variables in the breakpoint scope.

You can also back trace the code from the breakpoint. Backtrace means to print all functions called before the breakpoint. Sometimes a crash in the program is not because of the code where it crashed at. It might happens earlier, and passes an invalid parameter to cause a crash.

There are some other usage, and I will mention them in the following paragraph.

## GDB the Rust

First of all, I would create a simple <a href="https://doc.rust-lang.org/book/second-edition/ch01-03-hello-cargo.html" class="dj by in io ip iq" target="_blank" rel="noopener nofollow">Hello World</a> to demonstrate how to use GDB in a Rust project. You might have installed Rust and Cargo, Haven’t you?

Please follow the <a href="https://doc.rust-lang.org/book/second-edition/ch01-03-hello-cargo.html#creating-a-project-with-cargo" class="dj by in io ip iq" target="_blank" rel="noopener nofollow">steps</a> in “the Rust book” to create a Hello World. Make sure you can compile, run the code, and understand what Cargo are doing.

To create a project:

```rust
cargo new hello_cargo --bin
cd hello_cargo
```

Then, let’s start!

In order to show how to use GDB, I have designed a sample code. Please copy the following code to your <code class="gw ir is it iu b">./src/main.rs</code>:

```rust
fn main() {
    let name = "Tiger";
    let msg = make_hello_string(&name);
    println!("{}", msg);
}

fn make_hello_string(name: &str) -> String {
    let hello_str = format!("Hi {}, how are you?", name);
    hello_str
}
```

To build this code, simply run <code class="gw ir is it iu b">cargo build</code>.

There would be an executable file <code class="gw ir is it iu b">./target/debug/hello_cargo</code>. The build is set as debug mode by default, and we can use the debug build to run with GDB. However, if it is a release build, you cannot run with GDB, since the debug information is lost.

To run the program with GDB:

```rust
gdb target/debug/hello_cargo 
```

That’s it. You would see the interface in GDB like this:

```rust
gdb (Ubuntu 8.1-0ubuntu3) 8.1.0.20180409-git
Copyright (C) 2018 Free Software Foundation, Inc.
...
(gdb)
```

Now you can enter some commands in GDB!

## GDB commands

There are many commands in GDB, but I would only introduce the most important part for you. For my personal case, I usually only use these commands as well.

## break

As I mentioned before, a breakpoint allows you to stop the program at a certain position. There are two way to set the breakpoints.

Use <code class="gw ir is it iu b">break</code> or <code class="gw ir is it iu b">b</code> as the command to set a breakpoint.

In the first case, you can break at a function. (You would need to enter the whole path, like <code class="gw ir is it iu b">mod::mod::function</code> in a big project)

```rust
(gdb) break make_hello_world
Breakpoint 1 at 0x55555555beca: file src/main.rs, line 8.
```

Or, you can add the file path with a line number to define where to stop.

```rust
(gdb) b src/main.rs:9
Breakpoint 2 at 0x55555555bf6a: file src/main.rs, line 9.
```

let’s see whether we have set successfully.

```rust
(gdb) info break
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x000055555555beca in hello_cargo::make_hello_string at src/main.rs:8
2       breakpoint     keep y   0x000055555555bf6a in hello_cargo::make_hello_string at src/main.rs:9
```

But I just want one breakpoint, so I could delete the first one by <code class="gw ir is it iu b">del</code> command.

```rust
(gdb) del 1
(gdb) info break
Num     Type           Disp Enb Address            What
2       breakpoint     keep y   0x000055555555bf6a in hello_cargo::make_hello_string at src/main.rs:9
```

## run

Now there is just one breakpoint. Let’s run the program and see what happens!

Use <code class="gw ir is it iu b">run</code> to start.

```rust
(gdb) run
Starting program: /home/tigercosmos/Desktop/hello_cargo/target/debug/hello_cargo 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 2, hello_cargo::make_hello_string (name=...) at src/main.rs:9
9	    hello_str
```

As you can see, the program has stopped at the position that we want. Then, we could do something at this breakpoint!

## backtrace

If you are wondering what the upstream functions has been called before runnning to this breakpoint, you can use command <code class="gw ir is it iu b">backtrace</code> or <code class="gw ir is it iu b">bt</code>.

```rust
(gdb) backtrace
#0  hello_cargo::make_hello_string (name=...) at src/main.rs:9
#1  0x000055555555bdd5 in hello_cargo::main () at src/main.rs:3
```

Now GDB tells you that it is <code class="gw ir is it iu b">main.rs</code> line 3 (#1), which is <code class="gw ir is it iu b">let msg = make_hello_string(&amp;name);</code>, called <code class="gw ir is it iu b">main.rs</code> line 9 (#0), which is belong to <code class="gw ir is it iu b">make_hello_string</code>.

You might say, that’s really obvious, doesn’t it?

Yep! However, what if you are debugging a big open source project, such as the Servo project, and need to figure out the backtrace for a module? General speaking, there are about thirty to forty function calls before the breakpoint in a module. To find the backtrace by reading the code is super hard, but now we can use GDB to do it.

## frame

A frame is one of the program states in the backtrace. We can switch to a frame we want, and to check some information in that frame.

You can use <code class="gw ir is it iu b">frame</code> or <code class="gw ir is it iu b">f</code> to use this command.

After the previous step, we have already set a breakpoint at <code class="gw ir is it iu b">src/main.rs:9</code>, and there are two frames in the backtrace, which are <code class="gw ir is it iu b">#0</code> and <code class="gw ir is it iu b">#1</code>.

Now I want to check frame <code class="gw ir is it iu b">#1</code>, and see what is the value of <code class="gw ir is it iu b">name</code>, which is at <code class="gw ir is it iu b">src/main.rs:2</code>, in the scope of frame <code class="gw ir is it iu b">#1</code>.

```rust
#1  0x000055555555bdd5 in hello_cargo::main () at src/main.rs:3
3	    let msg = make_hello_string(&name);
(gdb) print name
$1 = "Tiger"
```

So, <code class="gw ir is it iu b">frame</code> let you enter the scope in frame <code class="gw ir is it iu b">#1</code>, and then you can use <code class="gw ir is it iu b">print</code> to print the value of a variable, or you can use <code class="gw ir is it iu b">call</code> to call a function at that scope.

How about switch to frame <code class="gw ir is it iu b">#0</code>, and see what value is <code class="gw ir is it iu b">hello_str</code>?

```rust
(gdb) frame 0
#0  hello_cargo::make_hello_string (name=...) at src/main.rs:9
9	    hello_str
(gdb) print hello_str
$2 = alloc::string::String {vec: alloc::vec::Vec<u8> {buf: alloc::raw_vec::RawVec<u8, alloc::heap::Heap> {ptr: core::ptr::Unique<u8> {pointer: core::nonzero::NonZero<*const u8> (0x7ffff6c22060 "Hi Tiger, how are you?\000"), _marker: core::marker::PhantomData<u8>}, cap: 34, a: alloc::heap::Heap}, len: 22}}
```

## continue

After checking some information we want know, we might want the program to continue. Use <code class="gw ir is it iu b">continue</code> or <code class="gw ir is it iu b">c</code> to continue running the code. The program will keep running until it meets another breakpoints or finish the execution.

```rust
(gdb) c
Continuing.
Hi Tiger, how are you?
```

Since there is just one breakpoint in this example, the program will run to the end.

## Something else

Once you stop at a breakpoint, you could use <code class="gw ir is it iu b">step</code> command to run code line by line.

Once you stop at a breakpoint, you could use <code class="gw ir is it iu b">up</code> and <code class="gw ir is it iu b">down</code> to switch frames instead of using <code class="gw ir is it iu b">frame &lt;number&gt;</code> directly.

If the program is running(you have commanded <code class="gw ir is it iu b">run</code> already), and you can enter <code class="gw ir is it iu b">Ctrl+C</code> to interrupt GDB, then the program will break right now. The process will paused at where it just run to. And the point where it stopped by the interrupt is a manual breakpoint for just once. You can add some other commands here, and once you have done, you can enter <code class="gw ir is it iu b">c</code> to continue the process.

Then, you can call some commands, such as <code class="gw ir is it iu b">break</code>, <code class="gw ir is it iu b">call</code>, <code class="gw ir is it iu b">step</code>, etc.

There are more commands powered by GDB. You can check the document for more information.

## Debug Servo

Almost there. Let’s go to debug the Servo project. I assume you are able to compile Servo.

To build in debug mode:

```rust
$ ./mach build -d
```

Once the build is done, and we want to debug Servo:

```rust
$ ./mach run -d https://google.com --debug
Reading symbols from /home/tigercosmos/servo/target/debug/servo...done.
(gbd)
```

You can debug Servo now!

## Conclusion

The concept in this article can be applied on not only Rust projects but also C++ projects. If you want to debug Firefox or Chromium, you can use the same way to debug them. I will not discuss some detail such as how to apply a complicated setting for GDB, so you might need to search for other advanced articles to learn more skills.

GDB is not a must for developers, but it indeed powers hackers. There are some contributors of Servo who are front-end developers. One of them is my best friend, and he has already contributed many commits for Servo. As a front-end developer, he never use GDB before. However, he gets some troubles while developing Servo recently, I think if he knows how to use GDB, it would be easier to figure out the reasons why there are some weird behaviors by the program.

I’m writing this article for him and all the developers who just become one of the Servo community. I hope this article is helpful for all of you. Have a nice hacking day! :)

---

### Special thanks

Thanks <a href="https://github.com/ko19951231" class="dj by in io ip iq" target="_blank" rel="noopener nofollow">@SouthRa</a> and <a href="https://github.com/cybai" class="dj by in io ip iq" target="_blank" rel="noopener nofollow">@cybai</a> for helping me review the article.
