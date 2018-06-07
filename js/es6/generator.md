# Generator
Generator 是ES6提供的一种异步编程的解决方案


# Genrator 特征
Generator 函数是一个普通函数，有如下特征。
* function关键字与函数名之间有一个星号；
* 函数体内部使用yield表达式，定义不同的内部状态（yield在英语里的意思就是“产出”）
* 执行 Generator 函数会返回一个遍历器对象(Iterator )

# Genrator 使用

```js
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```
注： 调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，这里并不是返回“ending”。而是一个指向内部状态的指针对象，也就是上面说的遍历器对象（Iterator Object）。 因此此处 hw 是一个遍历器对象；
必须调用遍历器对象（hw）的next方法，使得指针移向下一个状态。也就是说，每次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个yield表达式（或return语句）为止。

```js
hw.next()
// { value: 'hello', done: false }
hw.next()
// { value: 'world', done: false }
hw.next()
// { value: 'ending', done: true }
hw.next()
// { value: undefined, done: true }
```
（hw）遍历器对象，代表 Generator 函数的内部指针。以后，每次调用遍历器对象的next方法，就会返回一个有着value和done两个属性的对象。value属性表示当前的内部状态的值，是yield表达式后面那个表达式的值；done属性是一个布尔值，表示是否遍历结束。

注：ES6 没有规定，function关键字与函数名之间的星号，写在哪个位置。这导致下面的写法都能通过。
```js
function * foo(x, y) { ··· }
function *foo(x, y) { ··· }
function* foo(x, y) { ··· }
function*foo(x, y) { ··· }
```
由于 Generator 函数仍然是普通函数，所以一般的写法是上面的第三种，即星号紧跟在function关键字后面。

# yield 表达式 
上文提到：由于 Generator 函数返回的遍历器对象，只有调用next方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数。yield表达式就是暂停标志。

* 遇到yield表达式，就暂停执行后面的操作，并将紧跟在yield后面的那个表达式的值，作为返回的对象的value属性值。
* 下一次调用next方法时，再继续往下执行，直到遇到下一个yield表达式。
* 如果没有再遇到新的yield表达式，就一直运行到函数结束，直到return语句为止，并将return语句后面的表达式的值，作为返回的对象的value属性值。
* 如果该函数没有return语句，则返回的对象的value属性值为undefined


Generator 函数可以不用yield表达式，这时就变成了一个单纯的暂缓执行函数。
```js
function* f() {
  console.log('执行了！')
}

var generator = f();

setTimeout(function () {
  generator.next()
}, 2000);
```
上面代码中，函数f如果是普通函数，在为变量generator赋值时就会执行。但是，函数f是一个 Generator 函数，就变成只有调用next方法时，函数f才会执行。