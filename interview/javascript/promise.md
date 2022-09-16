```js
async function async1() {
  console.log(1);
  await async2();
  console.log(2);
}
async function async2() {
  console.log(3);
}
async1();

new Promise(resolve => {
  console.log(10);
  resolve();
}).then(() => {
  console.log(20);
}).then(() => {
  console.log(30)
}).then(() => {
  console.log(40)
})
// 1 3 10 2 20 30 40
```


```js
async function async1() {
  console.log(1);
  await async2();
  console.log(2);
}
async function async2() {
  console.log(3);
  return Promise.resolve()
}
async1();

new Promise(resolve => {
  console.log(10);
  resolve();
}).then(() => {
  console.log(20);
}).then(() => {
  console.log(30)
}).then(() => {
  console.log(40)
})

// 1 3 10 20 30 2 40


```