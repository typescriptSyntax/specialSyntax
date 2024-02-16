### typescript的特殊性:
1. 裝飾器
```
function enumerable(value: boolean) {
  return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.enumerable = value;
    console.log(target);
  };
}
```
```
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
 
  @enumerable(false)
  greet() {
    return "Hello, " + this.greeting;
  }
}
class NounGreeter {
  greeting: int;
  constructor(message: int) {
    this.greeting = int;
  }
 
  @enumerable(false)
  greet() {
    return this.greeting;
  }
}
``` 
3. type 與interface 
#### type 不支持聯合聲明
```
interface Point {
  x: number;
}

interface Point {
  y: number;
}

const point: Point = { x: 10, y: 30 };
```

```
// 报错：Duplicate identifier 'Point'.
type Point = {
  x: number;
}

// 报错：Duplicate identifier 'Point'.
type Point = {
  y: number;
}
```

3. infer的用法(提取陣列、遞迴)
### 提取元素
```
type Arr=['a','b','c'] 
或者 type Arr=Array<string>

type First<T extends any[]> = T extends [infer one,...any[]]?one:[]

type Last<T extends any[]> = T extends [...any[],infer Last]?Last:[]

type pop<T extends any[]> = T extends [...infer Rest,unknown]?Rest:[]

得取剩餘陣列值
type shift<T extends any[]> = T extends [unknown,...infer Rest]?Rest:[]
得取剩餘陣列值
type a=Last<Arr>

```
### 遞迴
```
type Arr=[1,2,3,4] or type Arr=Array<number>
type ReverArr<T extends any[]> = T extends [infer First,...infer rest]? [...ReverArr<rest>,First]:T

type Arrb = ReverArr<Arr>
```