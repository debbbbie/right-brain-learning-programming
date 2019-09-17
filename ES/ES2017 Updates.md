---
| tags | JavaScript, ES, ES2017 |
记忆类型 | 故事定桩法
date | 2019/09/17
---

ES2017 Updates

## 右脑编码记忆

共享、异步、遍历、填充

老两口共享一个拐杖；老头儿先用，老太婆再异步用；遍历一下他俩，看谁需要填充一下


记忆内容|编码|备注|
----  | ---- |---- |
7|拐杖|ES2017
共享内存|老两口共享|SharedArrayBuffer & Atomic
异步函数|老头儿先用，老婆儿后用 | async & await
对象遍历|遍历一下他俩|Object.values & Object.entries
填充|看看谁饿了| "98".padStart(3, "0") // "098"

## 内容

1. 字符串填充 String.prototype.padStart / String.prototype.padEnd
2. 对象遍历 Object.values / Object.entries
3. 对象的自身属性描述符 Object.getOwnPropertyDescriptors
4. 函数参数列表和调用中的尾逗号
5. 异步函数 async/await
   由 async 关键字定义的函数声明定义了一个可以异步执行的函数，它返回一个 AsyncFunction 类型的对象。异步函数的内在运行机制和 Generator 函数非常类似，但是不能转化为 Generator 函数。
         function fetchTextByPromise() {
   return new Promise(resolve => { 
      setTimeout(() => { resolve("es8"); }, 2000);
   });
   }
   async function sayHello() { 
   const externalFetchedText = await fetchTextByPromise();
   console.log(`Hello, ${externalFetchedText}`); // Hello, es8
   }
   sayHello();
6. 共享内存与原子操作 Atomic
   当内存被共享时，多个线程可以并发读、写内存中相同的数据。原子操作可以确保那些被读、写的值都是可预期的，即新的事务是在旧的事务结束之后启动的，旧的事务在结束之前并不会被中断。这部分主要介绍了 ES8 中新的构造函数 SharedArrayBuffer 以及拥有许多静态方法的命名空间对象 Atomic 。
   Atomic 对象类似于 Math 对象，拥有许多静态方法，所以我们不能把它当做构造函数。 Atomic 对象有如下常用的静态方法：
   • add/sub - 为某个指定的value值在某个特定的位置增加或者减去某个值
   • and/or/xor - 进行位操作
   • load - 获取特定位置的值
   
   并行的下一站: Atomics ，一个有两个方法的全局变量。首先，介绍一下 Atomics 方法要解决的问题：在各方（如 web workers 或 Web页面的主程序）共享 SharedArrayBuffer 时，各方可以随时读取和写入其内存。那么，你如何保持一致性及访问顺序化，确保各方知道要等待其他方完成他们的数据写入？
   Atomics 有 wake 和 load 方法。各方将会“休眠”在等待队列中，等待其他方完成写入数据，所以 Atomics.wake 是一个让各方“醒来”的方法。当你需要读数据的时候，你用 Atomics.load 去从某个地点装载数据，这个位置需要输入两个参数，TypedArray，一类数组机制去访问raw二进制数据（即 SharedArrayBuffer），和一个下标去寻找在 TypedArray 的位置。除了我们刚才介绍的内容之外，还有更多的内容，但这是它的要点。




## 参考链接
https://www.jianshu.com/p/f7a89056d8ad


