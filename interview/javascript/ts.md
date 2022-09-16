## `interface` 和 `type`的区别

相同点

- 都可以表示一个对象或者函数
- 都可以拓展，`interface`可以继承 `type`,`type`也可以继承` interface`,但是两者继承的表达不同

```ts
interface A {
  name: string;
}
interface B {
  age: number;
}
interface C extends A, B {}

type A = {
  name: string;
};
type B = {
  age: number;
};
type C= A&B
```

不同点
- `type` 可以声明基本类型别名，联合类型，元组等
- `interface`可以合并声明

## `in`
- in用于取联合类型的值。主要用于数组和对象的构造。

```ts
type name = 'firstName' | 'lastName';
type TName = {
  [key in name]: string;
};
```
## `infer`实例
```ts
// 实现Parameters
type Parameters<T extends (...args: any) => any => T extends (
    ...args: infer P
  ) => any
    ? P
    : never; 

// 实现 returnType
type ReturnType<T extends (...args: any) => any => T extends (
    ...args: any
  ) => infer R
    ? R
    : any;
```
