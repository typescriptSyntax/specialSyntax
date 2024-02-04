### typescript的特殊性:
1. 裝飾器
2. type 與interface 
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