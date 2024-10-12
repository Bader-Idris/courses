# WHAT IS TYPESCRIPT ?

- TypeScript Is A Strongly Typed Programming Language That Builds On JavaScript
- TypeScript Developed And Maintained By Microsoft
- TypeScript Is JavaScript With Types
- Typescript Add Features To JavaScript Without Changing It

---

## WHY WE NEED TYPESCRIPT ?

- Detect Errors Without Running The Code `Static Type Checking`
- Analyze The Code As You Type
- Save Some Unit Tests As The Error Show While Writing
- Every JS File Is Valid TS File
- Will Help You When You Write React, Vue, Angular Apps
- Gives You The Missing Features In JS Like `Interfaces, Generics, Decorators`

---

## HOW TYPESCRIPT WORKS ?

- TypeScript Compiler Compile TS Code Into JavaScript Code `This's Called Transpilation`
- How About The New Features? `Workaround`

---

## Requirements

- **JavaScript Concepts**

- Variables
- Arrays
- Objects
- Functions
- Conditions

---

---

## How to run Ts in your machine?

- `nodejs` is required
- then install its package by: `npm i typescript`, if globally add `-g` as `npm i -g blab`
- then check if it's installed in the project as: `tsc -v`

[Check its website](https://www.typescriptlang.org/)

- You can check installing it in the project [here](https://www.typescriptlang.org/download)

- `npm install typescript --save-dev` for projects

---

- **🔴 Compile Ts Files 🔴**
- to compile 'em use: `tsc fileName.ts`
- `tsc -h` to get help information
- `tsc -w` is to watch migrating ts to js files, which is awesome, even if you delete the `dist` folder where you put every compiled js from TS, it'll re-create it when enabling watch mode
- 🔴 we can remove comments in js migrated files
- to install typescript configuration use: `tsc --init`

#### inside tsconfig.json

- `target` it targets es2016 you can change it to `2020 one`
- an  example of `dist` DIR is [scss](https://github.com/twbs/bootstrap) it compiles scss to css
- so you put the ts in `src` DIR, and make it compile into `dist` DIR, stands for `distribution`
- `rootDir` is to set our src DIR, for TS files to be compiled
- `outDir` is where compiled as JS files go, even if not exists, it creates it
- `removeComments` removes comments as its name, in some projects, comments `are bad code`
- `sourceMap` is for debugging, Osama will explain more in future
- when you type: `tsc` it **runs** tsconfig
- when watch, it does its job on saving, as nodemon do with node

---

## Statically Typed Language Like [Rust, C, C++]

- Variables Types Are Static, , Once You Declare
- Type Of A Variable Is Known At Compile Time
- Have Better Performance At Run-Time Due To
- Error Detected Earlier
- It You Cannot Change
- `Do Type Checking At Compile-Time`
- Not Needing To Check Types Dynamically

## Dynamically Typed Language Like [PHP, Python, JavaScript]

- Variables Types Are Dynamic, You Can Always Change It
- `Type Checking At Execution-Time`
- Error Can Be Detected After Execution

- side note: python does not combine int and str types when printing

### 05- Type Annotations And Any Data Type

- **Type Annotations || Signature** في اللغات الأخرى

  - - Indicates The Data Type Of variables
  - - Indicates The Data Type Of Functions Input/Output
  - - Objects, etc.

  - - Why Do We Use It?
  - - Is It Mandatory?
  - - What Happens If We Didn't Use It?

---

```typescript
// three types of variables, Var: data type, value
let theName: string = "Elzero";//s != S
let theAge: number = 40;
let hire: boolean = true;
// as static typed langs, can't assign int to str
```

- We do this action of setting data type to force var to its type
- it's optional, not mandatory
- - **what to do with unknown values?**
- we use 1st ts data type: `any`

```typescript
let all: any = "little String";//even null as let all any;
all = 100;// accepts it
```

- see this js func

```javascript
const add = (n1, n2) => n1 + n2;
console.log(add(10, 20));//normal number
console.log(add(10, "20"));//functionality destroyed
// it'll concatinate it
// even setting param as Number doesn't work, only inside it
```

- so we make it as 🔽 in tsc

```typescript
function add(n1: number, n2: number ) { n1 + n2};
console.log(add(10, 20));
console.log(add(10, "20"));// string is an error it'll response
```

### 06- Type Annotations With Arrays

- we can use regExp approach of `if or` with data anatotation as 

```typescript
let all: (string | number | boolean) = 'first value';// () => allowed
all = "hello";
all = 100;
all = true;
```

- when you add strings to array, it'll return string[], use this: 

```typescript
let myParts = ["hand", "leg", "head", "whatnot", 10]
// when you add numbers to it it'll become (string | number)
```

- let's add a for loop with some bugs

```typescript
// check index.ts file
for (let i = 0; i < myParts.length; i++) {
  console.log(myParts[i].repeat(3)); // bug because only works with string
  // you can fix the number | add string[] as we did
}
```

### 07 - Type Annotations With Multidimensional Arrays

- it's simple logic and easily perceived

```ts
let arrayFour: (string| number| (number|string)[] | boolean[])[] = [ 1, 2, "A", "B", [ 3, 4,"C","D"], [true, false]];
```

### 08 - Type Annotations With Function

1. noImplicitAny
2. noImplicitReturns
3. noUnusedLocals
4. noUnusedParameters

```ts
let showMsg = true;
function showDetails(name, age, salary) {
  if (showMsg) {
    return `Hello ${name}, Age Is ${age}, Salary is`//ts will help us instead of explicit this salary!
  }
}
console.log(showDetails("Osama", 40, 5000));
```

Because we see an error appearing our type any, we can disable that with 1st `noImplicitAny`: disable, it'll become as quick fix, which is awesome! it can also detect on usage, 😲

2nd option: `noImplicitReturns` will throw an error when a function doesn't have a default option you create with no conditions!

As adding this at last of our function:

```ts
function priorFn(a,b) : string {
  // prior conditions
  return 'some text'
}
// : string means, only returning string! useful lessing XSS
```

If we add an unused var, we can use an error for showing it, called: `noUnusedLocals`, same with params via: `noUnusedParameters`

### 09 - Function Optional and Default Parameters

When we use default values with parameters as (a = 'hi'), to get that without passing any value with ts, we use the undefined when running the Fn, view:

```ts
function showDetails(name: string = "Pedro", age: number, salary: number) {
  if (showMsg) {//so we put it after datatype, in ts
    return `${name} - ${age} - ${salary}`;
  }
}
console.log(showDetails(undefined, 40, 5000));
```

> to make that param optional, we use the regExp question mark, as salary? : string = 50

Logically, optionals will be at last descending!

### 10 - Function Rest Parameter

```ts
function addAll(...nums: number[]) : number {//array of numbers, so only numbers!
  let result = 0;
  for (let i = 0; i < nums.length ; i++) {
    result += nums[i]
  }
  // can use forEach instead
  return result;
}
console.log(addAll(10, 20, 30, 100))//adding float is number in ts
```

Now, we command: `tsc` to extract files -> node  ourFile.js

### 11 - Type Annotations With Anonymous And Arrow Function

little small video, 2m

```ts
const add = function(num1: number, num2: number) : number {
  return num1 + num2;
};
console.log(add(10,20));

const addWithArrow = () : number => num1 + num2;
console.log(addWithArrow(10,20));
```

then command: `tsc` => node fileName

### 13 - Data Types - Type Alias Advanced

We use this when possessing many types for same param:

```ts
type Buttons = {
  up: string,
  right: string,
  down: string,
  left: string,
};
// this namedLast will be added to getAction Fn
type Last = Buttons &&  {x?: boolean}//put ? to be optional, as we learned

function getActions(btns: Last) {//made btns as Last instead of only Buttons
  console.log(`Action for Button up Is: ${btns.up}`);
  console.log(`Action for Button right Is: ${btns.right}`);
  console.log(`Action for Button down Is: ${btns.down}`);
  console.log(`Action for Button left Is: ${btns.left}`);
};
getActions({
  up: `Jump`,
  right: `go right`,
  down: `get down`,
  left: `go left`,
})
```

### 14 - Data Types - Literal Types

Data Types -> literal Types:

```ts
type nums = 0 | 1 | -1;

function compare(num1: number, num2: number) : nums {//🔴 instead of adding many constainet types, we added an Obj called nums 🔴
  if (num1 === num2) {
    return 0;
  } else if ( num1 > num2 ) return 1;
  else return -1;
}
console.log(compare(20,20))//0
console.log(compare(20,15))//1
console.log(compare(20,30))//-1
```

we can use these things with measurement degrees, range units, it's as mapping in backend, I said.
awesome for preventing attackers to add more headers to post bodies for ie!

### 15 - Data Types - Tuple

This Tuple will be useful with frameworks, it's similar to arrays, but it's too specific, and preset to both length and type, I believe it's same as stack then!

consider we're having an article, it has id, title, status: public | private;

```ts
// let article: [number, string, boolean];//can use it directly as is! or initializing its values
let article: readonly [number, string, boolean]; = [11, "Title One", true];
article[0].//adding this will appear string data, as its type was string
article = [12, "Title Two", false];

// to prevent issues as appending/depending to our array, there isn't any restriction in ts for push, shift etc methods, but we can do following:
article.push(100);//added readonly after article setting above!🔴

// destructuring
const [id, title, status] = article;
console.log(id);
console.log(title);
console.log(status);
```

### 16 - Data Types - Void And Never

```ts
/*
  Data Types
  - Void
  --- Function That Will Return Nothing
  --- Function In JavaScript That Not Return A Value Will Show undefined
  --- undefined is not void
  - Never
  --- Return Type Never Returns
  --- The Function Doesn't Have A Normal Completion
  --- It Throws An Error Or Never Finishes Running At All "Infinite Loop"
*/

function logging(msg: string) : void {
  console.log(msg);
  return;
}

console.log(logging("Iam A Message"));
console.log("Test");

const fail = (msg: string) => {
  throw new Error(msg);
  // return 10;
}

function alwaysLog(name: string) : never {
  while(true) {
    console.log(name);
  }
}

alwaysLog("Osama");
// console.log("Test");
```

### 17 - Data Types - Enums Part 1

```ts
/*
  Data Types
  - Enums => Enumerations
  --- Allow Us To Declare A Set Of Named Constants
  --- Used For Logical Grouping Collection Of Constants "Collection Of Related Values"
  --- It Organize Your Code
  --- By Default Enums Are Number-Based, First Element Is 0
  --- Theres A Numeric Enums
  --- Theres A String-Based Enums
  --- Theres Heterogeneous Enums [String + Number]
*/

const KIDS = 15;
const EASY = 9;
const MEDIUM = 6;
const HARD = 3;

enum Level {
  Kids = 15,
  Easy = 9,
  Medium = 6,
  Hard = 3
}

let lvl: string = "Easy";

if (lvl === "Easy") {
  console.log(`The Level Is ${lvl} And Number Of Seconds Is ${Level.Easy}`);
}
```

in tsconfig, we uncommented this and made it to false:`"allowUnreachableCode": false,`, to make it as a warning!


### 18 - Data Types - Enums Part 2

in tsconfig we uncommented this: `"preserveConstEnums": true,`, so it preserves enum with `const enum {}`, instad of only compiling its result

```ts
/*
  Data Types
  - Enums => Enumerations
  --- Enum Can Refer To Other Enum
  --- Enum Can Refer To Same Enum
  --- Enum Can Have Calculations
  --- Enum Can Have Functions
*/

function getHardSeconds() : number {
  return 3;
}

enum Kids {
  Five = 25,
  Seven = 20,
  Ten = 15
}

enum Level {
  Kid = Kids.Ten,//referred from above kids
  Easy = 9,
  Medium = Easy - 3,//from same enum
  Hard = getHardSeconds()
}

let lvl: string = "Easy";

if (lvl === "Easy") {
  console.log(`The Level Is ${lvl} And Number Of Seconds Is ${Level.Hard}`);
}
```

### 19 - Data Types - Type Assertions

```ts
/*
  Data Types
  - Type Assertions
  --- Sometime Compiler Doesnt Know The Information We Do
  --- TypeScript Is Not Performing Any Check To Make Sure Type Assertion Is Valid
*/

// let myImg = document.getElementById("my-img") as HTMLImageElement;
let myImg = <HTMLImageElement> document.getElementById("my-img");
console.log(myImg.src);

let data: any = 1000;
console.log((data as string).repeat(3));
```

### 20 - Data Types - Union And Intersection Type

```ts
/*
  Data Types
  - Union And Intersection Types
  --- Union Type
  ------ The | Symbol Is Used To Create The Union => "Or"

  --- Intersection Type
  ------ Is A Type That Combines Several Types Into One
  ------ The & Symbol Is Used To Create An Intersection => "And"

  --- If A Union Is An OR, Then An Intersection Is An AND.
*/

// let all: number | string = 100;

type A = {
  one: string,
  two: number,
  three: boolean
}

type B = A & {
  four: number
}

type C = {
  five: boolean
}

type mix = A & C;

function getActions(btns: mix) {
  console.log(`Hello ${btns.one}`);
  console.log(`Hello ${btns.two}`);
  console.log(`Hello ${btns.three}`);
  console.log(`Hello ${btns.five}`);
}

getActions({ one: "String", two: 100, three: true, five: true });
```

### 21 - Type Annotations With Object

```ts
/*
  Type Annotations With Object
*/

let myObject: { //this obj is the Annotations options
  readonly username: string,
  id: number,
  hire?: boolean,
  skills: {//nested {}
    one: string,
    two: string
  }
} = {
  username: "Elzero",
  id: 100,
  hire: true,
  skills: {
    one: "HTML",
    two: "CSS"
  }
};

// myObject.username = "Osama";
myObject.id = 101;
myObject.hire = false;

console.log(myObject.username);
console.log(myObject.id);
console.log(myObject.hire);
console.log(myObject.skills.one);
```

🔴 check object define property, in js which is similar to ts annotations 🔴

### 22 - Interface Declaration

```ts
/*
  Interface
  - Interface Declaration
  --- Serve Like Types
  --- The Interface Describes The Shape Of An Object
  --- It Defines The Syntax To Follow

  --- Use With Object
  --- Use With Function
  --- Use Read Only And Optional Operator
*/

interface User {
  id?: number,
  readonly username: string,
  country: string
}

let user: User = {
  id: 100,
  username: "Elzero",
  country: "Egypt"
}

user.country = "Syria";

console.log(user);

function getData(data: User) {
  console.log(`Id Is ${data.id}`);
  console.log(`Username Is ${data.username}`);
  console.log(`Country Is ${data.country}`);
}

getData({ id: 200, username: "Osama", country: "KSA" });
```

### 23 - Interface Method And Parameters

```ts
/*
  Interface
  - Interface Method And Parameters
*/

interface User {
  id: number;// can be comma as semicolon between properties
  username: string;
  country: string;
  sayHello() : string;
  sayWelcome: () => string;
  getDouble(num: number) : number;
}

let user: User = {
  id: 100,
  username: "Elzero",
  country: "Egypt",
  sayHello() {
    return `Hello ${this.username}`;
  },
  sayWelcome: () => {
    return `Welcome ${user.username}`;
  },
  getDouble(n) {
    return n * 2;
  }
}

console.log(user.id);
console.log(user.sayHello());
console.log(user.sayWelcome());
console.log(user.getDouble(100));
```

### 24 - Interface Reopen And Use Cases

```ts
/*
  Interface
  - ReOpen The Interface And Use Cases
*/

// Homepage
interface Settings {
  readonly theme: boolean;// 🔴⚠️ good when disabling user from changing it⚠️🔴
  font: string;
}

// Articles Page
interface Settings {
  sidebar: boolean;
}

// Contact Page
interface Settings {
  external: boolean;
}

let userSettings: Settings = {
  theme: true,
  font: "Open Sans",
  sidebar: false,
  external: true
}
```

### 25 - Interface Extend

```ts
/*
  Interface
  - Extending Interfaces
*/

interface User {
  id: number;
  username: string;
  country: string;
}

interface Moderator {
  role: string | number;
}

interface Admin extends User,Moderator {//extends as super in js => oop
  protect?: boolean;
}

let user: Admin = {
  id: 100,
  username: "Elzero",
  country: "Egypt",
  role: "Mod",
  protect: true
}

console.log(user.id);
```

### 26 - Interface Final Discussion

```ts
/*
  Interface
  - Interface vs Type Aliases
  - Take A Look On HTMLElement Interface
*/

let el = document.getElementById("id") as HTMLElement;//🔴 discover other interfaces via this HTMLElement

// Homepage
type Settings {
  readonly theme: boolean;
  font: string;
  sidebar: boolean;
  external: boolean;
}//interface doesn't duplicate as this type {}, we can use many interfaces as in prior lesson, which is the most important difference from using type {}

let userSettings: Settings = {
  theme: true,
  font: "Open Sans",
  sidebar: false,
  external: true
}
```

### 27 - Class Type Annotations

```ts
/*
  Type Annotations With Class
*/

class User {
  u: string;
  s: number;
  msg: () => string;
  constructor(username: string, salary: number) {
    this.u = username;
    this.s = salary;
    this.msg = function () {
      return `Hello ${this.u} Your Salary Is ${this.s}`;
    }
  }
  sayMsg() {
    return `Hello ${this.u} Your Salary Is ${this.s}`;
  }
}

let userOne = new User("Elzero", 6000);

console.log(userOne.u);
console.log(userOne.s);
console.log(userOne.msg());
console.log(userOne.sayMsg());
```

### 28 - Class Access Modifiers And Parameters Properties

```ts
/*
  Class
  - Data Access Modifiers & Parameters Properties
  --- Public
  ------ All Members Of A Class In TypeScript Are Public
  ------ All Public Members Can Be Accessed Anywhere Without Any Restrictions
  --- Private
  ------ Members Are Visible Only To That Class And Are Not Accessible Outside The Class
  --- Protected
  ------ Same Like Private But Can Be Accessed Using The Deriving Class

  - TypeScript Is A Layer On Top Of JavaScript
  - It Should Remove All Annotations And Although Access Modifiers "Private For Example"
*/

class User {
  msg: () => string;
  constructor(private username: string, protected salary: number,public readonly address: string) {
    this.msg = function () {
      return `Hello ${this.username} Your Salary Is ${this.salary}`;
    }
  }
  sayMsg() {
    return `Hello ${this.username} Your Salary Is ${this.salary}`;
  }
}

let userOne = new User("Elzero", 6000, "Cairo");

// console.log(userOne.username);
// console.log(userOne.salary);
console.log(userOne.msg());
console.log(userOne.sayMsg());
```

### 29 - Class Get And Set Accessors

```ts
/*
  Class
  - Get And Set Accessors
  or getters and setters
*/

class User {
  public get username(): string {
    return this._username;
  }
  public set username(value: string) {
    this._username = value;
  }
  msg: () => string;
  constructor(private _username: string, public salary: number, public readonly address: string) {
    this.msg = function () {
      return `Hello ${this._username} Your Salary Is ${this.salary}`;
    }
  }
  sayMsg() {
    return `Hello ${this._username} Your Salary Is ${this.salary}`;
  }
  // get username() : string {
  //   return this._username;
  // }
  // set username(value: string) {
  //   this._username = value;
  // }
}

let userOne = new User("Elzero", 6000, "Cairo");

console.log(userOne.username);
userOne.username = "Ahmed";
console.log(userOne.username);
console.log(userOne.salary);
console.log(userOne.msg());
console.log(userOne.sayMsg());
```

### 30 - Class Static Members

```ts
/*
  Class
  - Static Members
  --- Don't Use "name, length, call"
*/

class User {
  private static created: number = 0;
  static getCount() : void {
    console.log(`${this.created} Objects Created`);
  }
  constructor(public username: string) {
    User.created++;
  }
}

let u1 = new User("Elzero");
let u2 = new User("Web");
let u3 = new User("School");
// console.log(User.created);
User.getCount();
```

### 31 - Class Implements Interface

```ts
/*
  Class
  - Implement Interface
*/

interface Settings {
  theme: boolean;
  font: string;
  save(): void;
}

class User implements Settings {
  constructor(public username: string, public theme: boolean, public font: string) {}
  save(): void {
    console.log(`Saved`);
  }
  update(): void {
    console.log(`Updated`);
  }
}

let userOne = new User("Elzero", true, "Open Sans");

console.log(userOne.username);
console.log(userOne.font);

userOne.save();
userOne.update();
```

### 32 - Abstract Classes And Members

```ts
/*
  Class
  - Abstract Classes And Members
  --- We Cannot Create An Instance Of An Abstract Class
*/

abstract class Food {
  constructor(public title: string) {}
  abstract getCookingTime() : void;
}

class Pizza extends Food {
  constructor(title: string, public price: number) {
    super(title);
  }
  getCookingTime() : void {
    console.log(`Cooking Time For Pizza Is 1 Hour`);
  }
}

class Burger extends Food {
  constructor(title: string, public price: number) {
    super(title);
  }
  getCookingTime() : void {
    console.log(`Cooking Time For Burger Is Half Hour`);
  }
}

let pizzaOne = new Pizza("Awesome Pizza", 100);

console.log(pizzaOne.title);
console.log(pizzaOne.price);
pizzaOne.getCookingTime();
```

### 33 - Polymorphism And Method Override

```ts
/*
  Class
  - Polymorphism & Method Override

  - Polymorphism
  --- Classes Have The Same Methods But Different Implementations

  - Method Override
  --- Allowing Child Class To Provide Implementation Of A Method In Parent Class
  --- A Method In Child Class Must Have Same Name As Parent Class

  --- noImplicitOverride
*/

class Player {
  constructor(public name: string) {}
  attack() : void {
    console.log("Attacking Now");
  }
}

class Amazon extends Player {
  constructor(name: string, public spears: number) {
    super(name);
  }
  override attack(): void {
    // super.attack();
    console.log("Attacking With Spear");
    this.spears -= 1;
  }
}

class Barbarian extends Player {
  constructor(name: string, public axeDurability: number) {
    super(name);
  }
  override attack(): void {
    // super.attack();
    console.log("Attacking With Axe");
    this.axeDurability -= 1;
  }
}

let barOne = new Barbarian("Elzero", 100);

console.log(barOne.name);
barOne.attack();
console.log(barOne.axeDurability);
```

### 34 - Generics Introduction

```ts
/*
  Generics
  - Help Write A Reusable Code
  - Allow To Pass Type As A Parameter To Another Type
  - You Will Be Able To Deal With Multiple Types Without Using ": Any Type"
  - We Can Create:
  --- Generic Classes
  --- Generic Functions
  --- Generic Methods
  --- Generic Interfaces
*/

function returnNumber(val: number) : number {
  return val;
}
function returnString(val: string) : string {
  return val;
}
function returnBoolean(val: boolean) : boolean {
  return val;
}

console.log(returnNumber(100));
console.log(returnString("Elzero"));
console.log(returnBoolean(true));

function returnType<T>(val: T) : T {// T is an alias to GenericType
  return val;
}

console.log(returnType<number>(100));
console.log(returnType<string>("Elzero"));
console.log(returnType<boolean>(true));
console.log(returnType<number[]>([1, 2, 3, 4]));
```

### 35 - Generics Multiple Types

```ts
/*
  Generics
  - Arrow Function
  - Multiple Types
  - Discussion
*/

function returnType<T>(val: T): T {
  return val;
}

console.log(returnType<number>(100));
console.log(returnType<string>("Elzero"));

const returnTypeArrowSyntax = <T>(val: T): T => val;

console.log(returnTypeArrowSyntax<number>(100));
console.log(returnTypeArrowSyntax<string>("Elzero"));

function testType<T>(val: T): string {
  return `The Value Is ${val} And Type Is ${typeof val}`;
}

console.log(testType<number>(100));
console.log(testType<string>("Elzero"));

function multipleTypes<T, S>(valueOne: T, valueTwo: S): string {
  return `The First Value Is ${valueOne} And Second Value ${valueTwo}`;
}

console.log(multipleTypes<string, number>("Osama", 100));
console.log(multipleTypes<string, boolean>("Elzero", true));
```

### 36 - Generics Classes

```ts
/*
  Generics
  - Classes
*/

class User<T = string> {
  constructor(public value: T) {}
  show(msg: T) : void {
    console.log(`${msg} - ${this.value}`);
  }
}

let userOne = new User<string>("Elzero");
console.log(userOne.value);
userOne.show("Message");

let userTwo = new User<number | string>(100);
console.log(userTwo.value);
userTwo.show("Message");
```

### 37 - Generics And Interfaces

```ts
/*
  Generics
  - Classes And Interfaces
*/

interface Book {
  itemType: string;
  title: string;
  isbn: number;
}

interface Game {
  itemType: string;
  title: string;
  style: string;
  price: number;
}

class Collection<T> {
  public data: T[] = [];
  add(item: T) : void {
    this.data.push(item);
  }
}

let itemOne = new Collection<Book>();
itemOne.add({ itemType: "Book", title: "Atomic Habits", isbn: 150510 });
itemOne.add({ itemType: "Book", title: "Follow Your Heart", isbn: 650650 });
console.log(itemOne);

let itemTwo = new Collection<Game>();
itemTwo.add({ itemType: "Game", title: "Uncharted", style: "Action", price: 150 });
console.log(itemTwo);
```

### 38

How To Continue

- Practice
- Other Topics Not In The Course
- [JSDocs](https://www.typescriptlang.org/docs/handbook/jsdoc-supported-types.html)
- TsConfig

---

# FreeCodeCamp Full TS Course

check the [video](https://www.youtube.com/watch?v=30LWjhZzg50), with our teacher: **Hitesh Choudhary**

Index:

```txt
⭐️ Contents ⭐️
⌨️ (0:00:00) Why to learn TypeScript
⌨️ (0:07:08) TypeScript is not what you think
⌨️ (0:15:25) How to install TypeScript
⌨️ (0:27:33) Your first intro to TypeScript docs
⌨️ (0:39:21) Number, boolean, and type inference
⌨️ (0:39:21) Number, boolean, and type inference
⌨️ (0:46:52) Don't use ANY
⌨️ (0:51:30) Do you really know functions
⌨️ (1:02:55) A better way to write function
⌨️ (1:15:38) Bad behavior of objects
⌨️ (1:25:14) Type Aliases
⌨️ (1:32:28) READONLY and optional
⌨️ (1:42:13) Array
⌨️ (1:50:03) Union Types in TS
⌨️ (2:04:46) Tuples
⌨️ (2:14:33) Enums
⌨️ (2:24:03) interface
⌨️ (2:33:52) Interface vs Type
⌨️ (2:39:08) How to setup Typescript for real projects
⌨️ (2:53:44) Classes
⌨️ (3:02:06) Private Public
⌨️ (3:08:12) Getters and Setters
⌨️ (3:15:25) Protected
⌨️ (3:19:34) Why Interface is important
⌨️ (3:26:05) Abstract class
⌨️ (3:35:36) Generics
⌨️ (3:47:58) Generics in Array and Arrow functions
⌨️ (3:56:07) Generic Classes
⌨️ (4:07:16) Type Narrowing
⌨️ (4:17:04) The in operator narrowing
⌨️ (4:22:17) Instanceof and Type Predicates
⌨️ (4:31:35) Discriminated Union and Exhaustiveness Checking with never
⌨️ (4:42:54) TypeScript End
```

## intro

We can put typescript in one context: **Type safety**, same as `Static checking`

to use console it's preferred in docs to use:

```ts
function randomFn (babe) : void {
  console.log("hi" + babe)
};
```

if for errors we use `never` instead as:

```ts
function handleError(errMsg: string): never {
  throw new Error(errMsg);
}
```

to prevent clients from manipulating _ids in mongo, we cna use the keyword `readonly` as:

```ts
type User = {
  readonly _id: string
  name: string
  email: string
  isActive: boolean
  credcardDetails?: number
}
```
