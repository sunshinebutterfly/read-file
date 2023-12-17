## ts基本命令与用法



------



### 优势

1. 优势1:编译时静态类型检测:函数或方法传参或变量赋值不匹配时，会出现编译错误提示，规避了开发期间的大量低级错误，省时，省力。
2. 优势2: 自动提示更清晰明确
3. 优势3: 引入了泛型和一系列的 TS 特有的类型。
4. 强大的 d.ts 声明文件: 声明文件像一个书的目录一样，清晰直观展示了依赖库文件的接口，type类型，类，函数，变量等声明。
5. 优势5: 轻松编译成JS 文件: 即使 TS 文件有错误，绝大多数情况也能编译出JS 文件
6. 优势6: 灵活性高:尽管 TS 是一门 强类型检查语言，但也提供了 any 类型 和 as any 断言，这提供了 TS 的灵活度。





------



### 基本命令

```shell
npm install typescript -d     创建node  typescript

tsc --init  生成tsconfig 配置文件

outDir     编译完成输出目录

rootDir     需要编译的目录

tsc命令， 生成dist 文件

tsc --noEmitOnError       编译文件有错的时候不生成目录

ts-node XXX    编译和执行代码一次执行

```





------



### 用法

```ts
// 联合类型
let str2: string | number | boolean = 'aa'
str2 = true


// 交叉类型
type obj1 = {name: string}
type obj2 = {age: number}
let obj3: obj1 & obj2 = {name:'ww',age:40}


//字面量数据类型
type inFlag = 0 | 1
function isUp(increase: inFlag){
	if(increase){}
}
```





------



### typescript 的枚举

枚举的好处：

1. 有默认值和可以自增值，节省编码时间
2. 语义更清晰，可读性增强

```ts
// 数字枚举 
enum weeknum {
	Mondy = 1,
	tuesday
}

// 数字枚举的双向映射
var weeknum;
(function (weeknum) {
    weeknum[weeknum["Mondy"] = 1] = "Mondy";
    weeknum[weeknum["tuesday"] = 2] = "tuesday";
})(weeknum || (weeknum = {}));

//字符串枚举
enum week {
	Mondy = 'Mondy',
	tuesday = 'tuesday'
}

var week;
(function (week) {
    week["Mondy"] = "Mondy";
    week["tuesday"] = "tuesday";
})(week || (week = {}));
```





------



### any，unknown的区别和应用场景

1. 相同点: any 和 unknown 可以是任何类的父类，所以任何类型的变量都可以赋值给 any 类型或 unknown类型的变量。
2. 不同点1: any 也可以是任何类的子类，但 unknown 不可以，所以 any 类型的变量都可以赋值给 其他类型的变量。
3. 不同点2:不能拿 unknown 类型的变量来获取任何属性和方法，但 any 类型的变量可以获取任意名称的属性和任意名称的方法.
