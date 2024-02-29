## ts基本命令与用法



------



### 优势

1. 编译时静态类型检测：函数或方法传参或变量赋值不匹配时，会出现编译错误提示，规避了开发期间的大量低级错误，省时，省力。
2. 自动提示更清晰明确
3. 引入了泛型和一系列的 `TS` 特有的类型。
4. 强大的 `d.ts` 声明文件，声明文件像一个书的目录一样，清晰直观展示了依赖库文件的接口，`type`类型，类，函数，变量等声明。
5.  轻松编译成`JS` 文件，即使 `TS` 文件有错误，绝大多数情况也能编译出`JS` 文件
6. 灵活性高:尽管 TS 是一门 强类型检查语言，但也提供了 `any` 类型 和  `as any` 断言，这提供了 TS 的灵活度。





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



### 一些基本类型

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

1. 相同点: `any` 和 `unknown` 可以是任何类的父类，所以任何类型的变量都可以赋值给 `any` 类型或 `unknown`类型的变量。
2. 不同点1: `any` 也可以是任何类的子类，但 `unknown` 不可以，所以 `any` 类型的变量都可以赋值给 其他类型的变量。
3. 不同点2:不能拿 `unknown` 类型的变量来获取任何属性和方法，但 `any` 类型的变量可以获取任意名称的属性和任意名称的方法.



------





### 接口 interface



使用`interface` 定义接口



接口应用场景

1. 提供方法的对象类型参数时使用
2. 为多个同类别的类提供统一的方法
3. 继承接口

```ts
interface Pet{
	name: string,
	love: number
	toHealth(): void
}

// 接口可以继承
interface Dog extends Pet{
	strain: string,
	guradHome(): void
}


//接口合并，当出现2个同样接口名称，则会自动合并
一般接口合并用作底层源码 添加新属性
interface Product{
	 name:string
}
interface Product{
	account: number
}

```

 

`implements` 类的接口实现，接口只能包含方法

```ts
interface Car{
	color(): void
}
class Benz implements Car{
	name:string
	age:number
	constructor(name:string,age:number){
		this.name = name,
		this.age = age
	}
	// 具体方法的实现
	color(): void {
		throw new Error("Method not implemented.")
	}
}

```



可索引签名

```ts
interface Pet{
	name: string,
	love: number,
	[x:string]: any
}
let pc:Pet={
	name:'ok',
	love: 100,
    // 此处定义X 后 可以不加任何东西
}

// 如果添加新属性，可以如下， 当X可索引类型为string，下面代码都不报错
let pc:Pet={
	name:'ok',
	love: 100,
	account: 100,
	desc:'ok',
	[Symbol('s')]:1000,
	100:'90',
	true:'100'
}
```



### 函数的几种表达方式

```ts
function info(name:string,age:number):number{
	return 3
}

type InfoType = (number:string,age:number) => number
const info :(name:string,age:number)=>number = function(){
	return 3
}
// 简写
const info :InfoType = function(){
	return 3
}

//es6
const info =(name:string,age:number):number =>{
	return 3
}
```



### 元组

```ts
let cust:[string,number,string,...any[]] = [
	'张三',
	11,
	'广州',
	'微信',
	'qq',
]

// 可变元组解构
let [name,age,address,...rest]:[string,number,string,...any[]] = [
	'张三',
	11,
	'广州',
	'微信',
	'qq',
]
// 元组除了可以用数组下标取值，也可以结构取值
console.log(name);
console.log(rest);

// 元组添加tag 标签
let [name,age,address,...rest]:[name:string,age:number,address:string,...rest:...any[]] = [
	'张三',
	11,
	'广州',
	'微信',
	'qq',
]
```



### 类，静态属性等

```ts
class People{
	name:string
	age:number
	addr:string
	static num:number   // 静态属性：一般用作对象共有的属性，所有对象访问值都一样
	count?: string  // 属性必须赋值，如果不在类体里面赋值，那么就必须在构造函数中赋值,或者写成可选 ?:  !:
	constructor(_name: string,_age:number,_addr:string){
		this.name = _name
		this.age = _age
		this.addr = _addr
		People.num++
	}

	doEat(){}
}
let p = new People('张三',10,'cc')
```



### 单列模式

单例模式属于创建模式的一种。通过单例模式创建的类只有一个实例。这种模式使得类的对象成为系统的唯一实例。而我们在系统中多次调用这个类的实例的时候，并不会去覆盖这个类，也可以我们在开发的过程中避免变量覆盖。



> 它的核心概念：限制类的实例化次数并且只能实例化一次，一个类只能存在一个实例，并提供一个全局的访问点。



以下代码实现一个最简单的单列模式，在`People`类里面`new`一个`newpeople`对象，使得该对象可以调用类的方法。

```ts
class People {
	// 单列模式
	static newpeople = new People()
	private constructor() {
		
	}
	eat() { }
	playGame() { }
}
let peo = People.newpeople
let peo1 = People.newpeople
console.log(peo === peo1);   // true


//***************以上代码有一个问题就是会初始化一次constructor，如下代码可以解决初始化问题，保证在调用的时候才会创建对象


class People {
	// 单列模式
	static people: People
	static getInstance(){
		if(!this.people){
			this.people = new People()
		}
		return this.people
	}
	private constructor() {

	}
	eat() { }
	playGame() { }
}
let peo = People.getInstance()
let peo1 = People.getInstance()
console.log(peo === peo1);   // true



```



`set` 和 `get` 

```ts
class User {
    //  get、set方法的成员变量命名时建议在前面加 _
  private _fullName: string;
    //get 的用法
    get fullName(): string{ 
        return this._fullName;
    }

    // "set" 访问器必须正好具有一个参数    可以处理数据修改
    set fullName(fullName: string) {
        this._fullName = fullName;
    }
}

const c = new User();
// set 不需要调用方法 直接对象属性赋值
c.fullName = "GT";
// get 直接对象属性赋值
console.log(c.fullName)
```



### 拦截器

拦截器的理解和总结

1. 生成新的数据属性 `dataprop`.
2.  保存 `dataprop.value` ，以保留原来的方法
3.  然后修改 `dataprop.value` 的指向，指向新的空间，创建了一个内存地址赋值给了`value`
4. 然后通过 `Object.defineProperty` 把修改了value指向 的`dataprop` 绑定到 原来的方法上
5. 执行原来方法，就会找到 `dataprop.value` 的指向的方法来执行

```ts
class People {
	name: string
	age: number
	addr: string
	static count = 0
	constructor(_name:string,_age:number,_addr:string){
		this.name = _name
		this.age = _age
		this.addr = _addr
	}
	doEat(who:string,where:string) {
		console.log(`who${who}，where${where}`);
			
	}
	playGame() { }
} 

//-------------拦截器实现方法
const dataProp = Object.getOwnPropertyDescriptor(People.prototype,'doEat')
const targetMethod = dataProp?.value
dataProp!.value = (...arg:any[]) =>{
	console.log('前置拦截');
	targetMethod.apply(this,arg)
	console.log('arg:',arg);
	console.log('后置拦截');
}
//dataProp?.value('小明','王府井')
Object.defineProperty(People.prototype,'doEat',dataProp!)
let p = new People('张三',100,'王府井')
p.doEat('小明','北京')

// ————————————————————————封装拦截器
// 封装拦截器
enum interceptor{
	AJAX = 'ajax',
	REG = 'reg'
}
const axiso = (classProtype:Object,method:string,p:string) =>{
	const prop = Object.getOwnPropertyDescriptor(classProtype,method)
	const propMethod = prop?.value
	prop!.value = (...arg:any[]) =>{
		if(interceptor.AJAX == p){
			console.log('进入ajax');
		}
		if(interceptor.REG == p){
			console.log('进入正则表达式');
		}
		propMethod.apply(this,arg)
		console.log('后置拦截');
	}
	Object.defineProperty(classProtype,method,prop!)
}
axiso(People.prototype,'doEat','reg')
let p = new People('张三',100,'王府井')
p.doEat('小明','北京')


```

## tsconfig.json配置详解

```ts
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */

    /* Projects */
    // "incremental": true,                              /* Save .tsbuildinfo files to allow for incremental compilation of projects. */
    // "composite": true,                                /* Enable constraints that allow a TypeScript project to be used with project references. */
    // "tsBuildInfoFile": "./.tsbuildinfo",              /* Specify the path to .tsbuildinfo incremental compilation file. */
    // "disableSourceOfProjectReferenceRedirect": true,  /* Disable preferring source files instead of declaration files when referencing composite projects. */
    // "disableSolutionSearching": true,                 /* Opt a project out of multi-project reference checking when editing. */
    // "disableReferencedProjectLoad": true,             /* Reduce the number of projects loaded automatically by TypeScript. */

    /* Language and Environment */
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    // "lib": [],                                        /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    // "jsx": "preserve",                                /* Specify what JSX code is generated. */
    // "experimentalDecorators": true,                   /* Enable experimental support for legacy experimental decorators. */
    // "emitDecoratorMetadata": true,                    /* Emit design-type metadata for decorated declarations in source files. */
    // "jsxFactory": "",                                 /* Specify the JSX factory function used when targeting React JSX emit, e.g. 'React.createElement' or 'h'. */
    // "jsxFragmentFactory": "",                         /* Specify the JSX Fragment reference used for fragments when targeting React JSX emit e.g. 'React.Fragment' or 'Fragment'. */
    // "jsxImportSource": "",                            /* Specify module specifier used to import the JSX factory functions when using 'jsx: react-jsx*'. */
    // "reactNamespace": "",                             /* Specify the object invoked for 'createElement'. This only applies when targeting 'react' JSX emit. */
    // "noLib": true,                                    /* Disable including any library files, including the default lib.d.ts. */
    // "useDefineForClassFields": true,                  /* Emit ECMAScript-standard-compliant class fields. */
    // "moduleDetection": "auto",                        /* Control what method is used to detect module-format JS files. */

    /* Modules */
    "module": "commonjs",                                /* Specify what module code is generated. */
    "rootDir": "./src",                                  /* Specify the root folder within your source files. */
    // "moduleResolution": "node10",                     /* Specify how TypeScript looks up a file from a given module specifier. */
    // "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    // "paths": {},                                      /* Specify a set of entries that re-map imports to additional lookup locations. */
    // "rootDirs": [],                                   /* Allow multiple folders to be treated as one when resolving modules. */
    // "typeRoots": [],                                  /* Specify multiple folders that act like './node_modules/@types'. */
    // "types": [],                                      /* Specify type package names to be included without being referenced in a source file. */
    // "allowUmdGlobalAccess": true,                     /* Allow accessing UMD globals from modules. */
    // "moduleSuffixes": [],                             /* List of file name suffixes to search when resolving a module. */
    // "allowImportingTsExtensions": true,               /* Allow imports to include TypeScript file extensions. Requires '--moduleResolution bundler' and either '--noEmit' or '--emitDeclarationOnly' to be set. */
    // "resolvePackageJsonExports": true,                /* Use the package.json 'exports' field when resolving package imports. */
    // "resolvePackageJsonImports": true,                /* Use the package.json 'imports' field when resolving imports. */
    // "customConditions": [],                           /* Conditions to set in addition to the resolver-specific defaults when resolving imports. */
    // "resolveJsonModule": true,                        /* Enable importing .json files. */
    // "allowArbitraryExtensions": true,                 /* Enable importing files with any extension, provided a declaration file is present. */
    // "noResolve": true,                                /* Disallow 'import's, 'require's or '<reference>'s from expanding the number of files TypeScript should add to a project. */

    /* JavaScript Support */
    // "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
    // "checkJs": true,                                  /* Enable error reporting in type-checked JavaScript files. */
    // "maxNodeModuleJsDepth": 1,                        /* Specify the maximum folder depth used for checking JavaScript files from 'node_modules'. Only applicable with 'allowJs'. */

    /* Emit */
    // "declaration": true,                              /* Generate .d.ts files from TypeScript and JavaScript files in your project. */
    // "declarationMap": true,                           /* Create sourcemaps for d.ts files. */
    // "emitDeclarationOnly": true,                      /* Only output d.ts files and not JavaScript files. */
    // "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    // "inlineSourceMap": true,                          /* Include sourcemap files inside the emitted JavaScript. */
    // "outFile": "./",                                  /* Specify a file that bundles all outputs into one JavaScript file. If 'declaration' is true, also designates a file that bundles all .d.ts output. */
     "outDir": "./dist",                                   /* Specify an output folder for all emitted files. */
    // "removeComments": true,                           /* Disable emitting comments. */
    // "noEmit": true,                                   /* Disable emitting files from a compilation. */
    // "importHelpers": true,                            /* Allow importing helper functions from tslib once per project, instead of including them per-file. */
    // "importsNotUsedAsValues": "remove",               /* Specify emit/checking behavior for imports that are only used for types. */
    // "downlevelIteration": true,                       /* Emit more compliant, but verbose and less performant JavaScript for iteration. */
    // "sourceRoot": "",                                 /* Specify the root path for debuggers to find the reference source code. */
    // "mapRoot": "",                                    /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSources": true,                            /* Include source code in the sourcemaps inside the emitted JavaScript. */
    // "emitBOM": true,                                  /* Emit a UTF-8 Byte Order Mark (BOM) in the beginning of output files. */
    // "newLine": "crlf",                                /* Set the newline character for emitting files. */
    // "stripInternal": true,                            /* Disable emitting declarations that have '@internal' in their JSDoc comments. */
    // "noEmitHelpers": true,                            /* Disable generating custom helper functions like '__extends' in compiled output. */
    // "noEmitOnError": true,                            /* Disable emitting files if any type checking errors are reported. */
    // "preserveConstEnums": true,                       /* Disable erasing 'const enum' declarations in generated code. */
    // "declarationDir": "./",                           /* Specify the output directory for generated declaration files. */
    // "preserveValueImports": true,                     /* Preserve unused imported values in the JavaScript output that would otherwise be removed. */

    /* Interop Constraints */
    // "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    // "verbatimModuleSyntax": true,                     /* Do not transform or elide any imports or exports not marked as type-only, ensuring they are written in the output file's format based on the 'module' setting. */
    // "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    // "preserveSymlinks": true,                         /* Disable resolving symlinks to their realpath. This correlates to the same flag in node. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */

    /* Type Checking */
    "strict": true,                                      /* Enable all strict type-checking options. */
    // "noImplicitAny": true,                            /* Enable error reporting for expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,                         /* When type checking, take into account 'null' and 'undefined'. */
    // "strictFunctionTypes": true,                      /* When assigning functions, check to ensure parameters and the return values are subtype-compatible. */
    // "strictBindCallApply": true,                      /* Check that the arguments for 'bind', 'call', and 'apply' methods match the original function. */
    // "strictPropertyInitialization": true,             /* Check for class properties that are declared but not set in the constructor. */
    // "noImplicitThis": true,                           /* Enable error reporting when 'this' is given the type 'any'. */
    // "useUnknownInCatchVariables": true,               /* Default catch clause variables as 'unknown' instead of 'any'. */
    // "alwaysStrict": true,                             /* Ensure 'use strict' is always emitted. */
    // "noUnusedLocals": true,                           /* Enable error reporting when local variables aren't read. */
    // "noUnusedParameters": true,                       /* Raise an error when a function parameter isn't read. */
    // "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
    // "noImplicitReturns": true,                        /* Enable error reporting for codepaths that do not explicitly return in a function. */
    // "noFallthroughCasesInSwitch": true,               /* Enable error reporting for fallthrough cases in switch statements. */
    // "noUncheckedIndexedAccess": true,                 /* Add 'undefined' to a type when accessed using an index. */
    // "noImplicitOverride": true,                       /* Ensure overriding members in derived classes are marked with an override modifier. */
    // "noPropertyAccessFromIndexSignature": true,       /* Enforces using indexed accessors for keys declared using an indexed type. */
    // "allowUnusedLabels": true,                        /* Disable error reporting for unused labels. */
    // "allowUnreachableCode": true,                     /* Disable error reporting for unreachable code. */

    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* Skip type checking .d.ts files that are included with TypeScript. */
    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
  }
}

```



### ts继承



1. 借用构造函数继承
2. 原型继承
3. 寄生组合继承





类型断言，类型守卫，类型转换



`typeof` 的局限性，`typeof` 和类型守卫

自定义守卫类型







### ts 泛型
