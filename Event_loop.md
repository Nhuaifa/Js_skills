### 并发模型与事件循环
>>Javascript执行引擎的主线程运行的时候，产生堆（heap）和栈（stack），程序中代码依次进入栈中等待执行，若执行时遇到异步方法，该异步方法会被添加到用于回调的队列（queue）中【即JavaScript执行引擎的主线程拥有一个执行栈/堆和一个任务队列】
>>>栈（stack） : 函数调用会形成了一个堆栈帧
堆（heap） : 对象被分配在一个堆中，一个用以表示一个内存中大的未被组织的区域。
队列（queue） ： 一个 JavaScript 运行时包含了一个待处理的消息队列。每一个消息都与一个函数相关联。当栈为空时，则从队列中取出一个消息进行处理。这个处理过程包含了调用与这个消息相关联的函数（以及因而创建了一个初始堆栈帧）。当栈再次为空的时候，也就意味着该消息处理结束。
![Alt text](https://link.juejin.im/?target=https%3A%2F%2Fmdn.mozillademos.org%2Ffiles%2F4617%2Fdefault.svg)
---
#### Macrotasks 和 Microtasks-- 宏任务与微任务

  - Macrotasks: setTimeout, setInterval, setImmediate, I/O, UI rendering
  - Microtasks: process.nextTick, Promises, Object.observe(废弃), MutationObserver
---
js执行宏任务与微任务的顺序：
- microtask会优先macrotask执行
- microtasks会被循环提取到执行引擎主线程的执行栈，直到microtasks任务队列清空，才会执行macrotask
---
#### Macrotasks 和 Microtasks有什么区别？
```
console.log('1');
setTimeout(function() {
  console.log('2');
}, 0);
Promise.resolve().then(function() {
  console.log('3');
}).then(function() {
  console.log('4');
});
console.log('5');
//输出结果：
//1
//5
//3
//4
//2
```
>原因是Promise中的then方法的函数会被推入 microtasks 队列，而setTimeout的任务会被推入 macrotasks 队列。在每一次事件循环中，macrotask 只会提取一个执行，而 microtask 会一直提取，直到 microtasks 队列清空。
