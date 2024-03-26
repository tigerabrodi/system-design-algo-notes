# Concurrency in JavaScript

When running JavaScript in a browser, it may appear that JavaScript is multi-threaded, but it's not. JavaScript is a single-threaded programming language, which means it has a single call stack and can only execute one task at a time. When a script is running, it blocks other scripts from running until it completes.

So, why can it appear that JavaScript is multi-threaded?

The answer lies in the JavaScript Runtime Environment.

# JavaScript Engine

Let's start by taking a look at the JavaScript engine. The JavaScript engine is responsible for executing JavaScript code. It consists of two main components:

1. **Call Stack**: The call stack is a data structure that stores the execution context of the running code. It follows the Last In, First Out (LIFO) principle, meaning that the last function added to the stack is the first one to be executed.
2. **Heap**: The heap is a memory space where objects are stored. And to remind you, arrays are also objects in JavaScript.

Let's take a look at a simple example to understand how the call stack works:

```javascript
function bark() {
  console.log("Woof!");
}

function meow() {
  console.log("Meow!");
}

function speak() {
  console.log("Speaking");
  bark();
  meow();
  console.log("Done speaking");
}

speak();
```

1. `speak` function is called, and it's added to the call stack.
2. `speak`'s first console log is added to the call stack and executed. When the console log is executed, it's removed from the call stack.
3. `bark` function is called and added to the call stack.
4. `bark`'s console log is added to the call stack and executed.
5. `bark` is removed from the call stack.
6. `meow` function is called and added to the call stack.
7. `meow`'s console log is added to the call stack and executed.
8. `meow` is removed from the call stack.
9. `speak`'s last console log is added to the call stack and executed.
10. `speak` is removed from the call stack.

That's the entire process when calling the `speak` function.

# JavaScript Runtime Environment

Assume we want to run `setTimeout(foo, 500)`, what would happen if we pushed it to the call stack?

```javascript
function foo() {
  console.log("Hello");
}

setTimeout(foo, 500);
```

If we pushed `setTimeout(foo, 500)` to the call stack, it would block the call stack for 500 milliseconds. This is not what we want. Instead, we want to run `foo` after 500 milliseconds. But how do we keep track of when to run `foo` if we can't use the call stack?

The JavaScript Engine isn't running code in complete isolation. It's running it in what we call a JavaScript Runtime Environment. This environment provides a set of extra functionality on top of JavaScript called Web APIs. These APIs include:

- Timers (setTimeout, setInterval)
- HTTP requests (fetch)
- DOM manipulation functions

When we call `setTimeout(foo, 500)`, the `setTimeout` function is pushed to the call stack. The `setTimeout` function is then removed from the call stack and sent to the Web API environment to handle the timer. But how does the JavaScript Engine know when to run `foo`?

This is where the callback queue comes in. The callback queue is a FIFO (First In, First Out) data structure that stores callback functions. Once the timer is complete, the Web API environment pushes the callback function (`foo`) to the callback queue.

The event loop is responsible for checking the call stack and callback queue. If the call stack is empty, it pushes the first function in the callback queue to the call stack. Once that's done, it checks the callback queue again for the next function. This process continues until the callback queue is empty.

The process of the Event Loop:

1. Dequeue the first function in the callback queue.
2. Enqueue the function to the call stack.
3. Execute the function.
4. Render any changes to the DOM.
5. Remove the function from the call stack.
6. Repeat the process until the callback queue is empty.

# setTimeout(func, 0)

You might think that `setTimeout(func, 0)` runs the function immediately, but that's not the case.

As we mentioned earlier, `setTimeout` is a part of the Web API environment. When you call `setTimeout(func, 0)`, the function is sent to the Web API environment to handle the timer. The timer is set to 0 milliseconds, but it doesn't mean the function will run immediately. The function is still sent to the callback queue, and the event loop will run it when the call stack is empty.

Let's look at some code:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Inside setTimeout");
}, 0);

console.log("End");
```

1. `console.log("Start")` is added to the call stack and executed.
2. `setTimeout` is added to the call stack and sent to the Web API environment to handle the timer.
3. `console.log("End")` is added to the call stack and executed.
4. The event loop checks the call stack and callback queue. Since the call stack is empty, it dequeues the function from the callback queue and adds it to the call stack.
5. `console.log("Inside setTimeout")` is added to the call stack and executed.

# Microtask Queue

When promises were added to JavaScript, they introduced a new queue called the microtask queue. The microtask queue has a higher priority than the callback queue. When a promise is resolved or rejected, the callback function is added to the microtask queue.

Let's look at some code to understand how everything works together:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Inside setTimeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Inside Promise");
});

console.log("End");
```

Just to remind you, whenever something is "executed" in the call stack, it's removed from the call stack.

1. `console.log("Start")` is added to the call stack and executed.
2. `setTimeout` is added to the call stack and sent to the Web API environment to handle the timer.
3. `Promise.resolve().then` is added to the call stack and executed. The callback function (`console.log("Inside Promise")`) is added to the microtask queue.
4. `console.log("End")` is added to the call stack and executed.
5. The event loop checks the call stack, microtask queue, and callback queue. Since the call stack is empty, it dequeues the function from the microtask queue and adds it to the call stack.
6. `console.log("Inside Promise")` is added to the call stack and executed.
7. The event loop does its job again and sees that microtask queue is empty. It then dequeues the function from the callback queue and adds it to the call stack.
8. `console.log("Inside setTimeout")` is added to the call stack and executed.

Pseudo code of the event loop may look something like:

```javascript
while (true) {
  if (callStack.isEmpty()) {
    if (!microtaskQueue.isEmpty()) {
      callStack.push(microtaskQueue.dequeue());
    } else if (!callbackQueue.isEmpty()) {
      callStack.push(callbackQueue.dequeue());
    }
  } else {
    // This would execute the last function added to the call stack
    // And then remove it from the call stack
    callStack.execute();
  }
}
```
