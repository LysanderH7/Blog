# 面试题：实现一个LazyMan

> 实现一个LazyMan，可以按照以下方式调用:
>
> LazyMan(“Hank”)输出:<br>
> Hi! This is Hank!
>
> LazyMan(“Hank”).sleep(10).eat(“dinner”)输出<br>
> Hi! This is Hank!<br>
> //等待10秒..<br>
> Wake up after 10<br>
> Eat dinner~
>
> LazyMan(“Hank”).eat(“dinner”).eat(“supper”)输出<br>
> Hi This is Hank!<br>
> Eat dinner~<br>
> Eat supper~
>
> LazyMan(“Hank”).sleepFirst(5).eat(“supper”)输出<br>
> //等待5秒<br>
> Wake up after 5<br>
> Hi This is Hank!<br>
> Eat supper
>
> 以此类推。

## 思路

### 链式调用

可以看出需求是需要实现链式调用的，这就要求：
1. `LazyMan()` 需要返回一个对象，这个对象包含了 `eat` `sleep` `sleepFirst` 这些api
2. 所有的方法（`eat` 等）调用，都仍需要返回这个对象（返回 `this` )

### 异步执行

每个方法都是要做一些事情的，但是因为 `sleep` 会等待一段时间再继续做后面的事情，所以这些事情不能在方法调用的时候就直接做。而且 `sleepFirst` 其实是会改变做事情的顺序的，所以应该在调用方法的时候确定做事情的顺序，在调用结束之后，再按照确定好的顺序依次做这些事情。

我选择用一个数组记录这些要做的事情，每调用一个方法的时候，就往数组里 `push` 一个函数，遇到 `sleepFirst` 就在数组前面 `unshift` 一个函数。在调用完成之后，再按顺序依次执行数组中的函数，并且是一个事情做完之后（包括等待）再去调用下一个函数。

## 我的代码

```js
function LazyMan(name) {
  let taskList = [];
  let api = {
    eat: function(food) {
      taskList.push(function() {
        console.log('Eat '+food+'~')
        next()
      })
      return this
    },
    sleep: function(seconds) {
      taskList.push(function() {
        console.log('Wake up after '+seconds)
        setTimeout(next, seconds*1000)
      })
      return this
    },
    sleepFirst: function(seconds) {
      taskList.unshift(function() {
        console.log('Wake up after '+seconds)
        setTimeout(next, seconds*1000)
      })
      return this
    }
  }
  let next = function() {
    let fn = taskList.shift()
    fn && fn()
  }
  taskList.push(function() {
    console.log('Hi! This is ' + name)
    next()
  })
  setTimeout(next, 0)
  return api
}
LazyMan('Hank').sleepFirst(3).sleep(2).eat('dinner').sleep(10).sleep(5).eat('supper')
```