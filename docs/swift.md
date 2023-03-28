## Swift的字符串操作

### 关于字符串的索引

**Swift中字符串的索引下标的数据类型为String.Int**
**因此str[0]等操作无效**
```swift
str.startIndex

str.endIndex
```
这两个是最常用的字符串索引
其中`str.endIndex`指向的是`\n`
因此返回字符串的最后一个元素通常用
```swift
str.index(before:str.endIndex)
```
来表示

**还有支持下标位移的函数**
```swift
str.index(str.startIndex,offsetBy:2) <=>str[2]
```
两者等价
还可以向前位移
```swift
str.index(endIndex,offsetBy:-2) <=> str[str.length()-2]
```
两者等价
**另外字符串还支持区间运算符**
```swift
var a = str.index(str.startIndex,offsetBy:2)

var b = str.index(str.endIndex,offsetBy:-1)

print(str[a...b])

print(str[a..<b])
```

### 关于字符串的查找修改
#### 查看字符串是否包含某个字符或字符串
```swift
str.contains("x")

str.contains("abc")
```
返回值为`Bool`

#### 判断字符串是否含有前后缀
```swift
str.hasPrefix("ABCD")

str.hasSuffix("EF")
```
返回值也为`Bool`

#### 追加字符串
```swift
str.append()
```

#### 插入字符串
```swift
str.insert(contentsOf:"hello", at: str.startIndex)

str.insert(contentsOf:"hello:, at: 

str.index(str.startIndex,offsetBy:2)
```
将插入的字符串的字一个字符放到索引的位置，然后依次顺延

#### 字符串的修改
**区间修改**
```swift
let index1 = str.index(str.startIndex,offsetBy:1)

let index2 = str.index(str.startIndex,offsetBy:3)

let range = index1...index2

str.replaceSubrange(range,with: "123123")

```
**字符串修改**
```swift
str.replacingOccurences(of:"BC", with: "123")
```

**索引删除**
```swift
str.remove(str.index(str.startIndex,offsetBy:2))
```
**区间删除**
```swift
str.removeSubrange(range)
```

### 关于字符串的遍历
可以直接把字符串中的字符取出来
```swift
for i in str {
    print(i)
}
```
可以用索引值
```swift
for i in 0..<str.count {
    print(str[str.index(str.startIndex, offsetBy: i)])
}
```
**还可以用`.reversed()`**

### 多行本文输入
```swift
var str = """
        hello
    word
                    world
          """
```  
可以原封不动地打出文本，但是一定要注意**上下引号对齐**     

输出引号
```swift
var str =  #""hello""#

print(str)
```
输出"hello"



## 下标语法
```swift
struct Person{

    private var array:[String] = ["swift","ios","macos"]
    
    subscript(index:Int,param:String) -> String{
    
        set(newValue){
        
            array.insert(newValue + param, at: index)
            
        }
        
        get{
        
            return array[index]
            
        }
    }
}

var person = Person()

person[1,"A"] = "hello"

print(person[1,"sdf"])
```


## 数组
### 数组的定义方式
**直接定义**
```swift
var a = [1,2,3,4]

let b = ["hello", "world"]
```

**类型定义**
```swift
var a:[Int] = [1,2,3,4]
```

**结构体定义**
```swift
var a:Array<Int> = [1,2,3,4]
```
数组可以空定义
**初始化器定义**
```swift
var arr = [Int]()

arr.append(1)

arr.append(2)

arr.append(3)

var arr2 = Array(repeating:-1, count: 3)
```

### 数组操作
常规修改方式
```swift
arr.append()

arr.insert(  , at: )

arr.replaceSubrange(range, with: )

arr.contains()

arr.remove(at: )
```

### 数组排序
```swift
arr.sort(by: {(s1, s2) -> Bool in

    if(s1 > s2){
    
        return true
        
    } else {
    
        return false
        
    }
    
})
```

### 数组过滤
```swift
var arr = [1,2,3,4]

var new_arr = arr.filter({(i) -> Bool in
    if i != 2 {
    
        return true
        
    }else {
    
        return false
        
    }
    
})

//new_arr = [1,3,4]
```
### 数组遍历
```swift
for i in arr{// <=>arr[0...]

    print(i)
    
}

for i in arr[0...2]{

    print(i)
    
}

for i in 0...arr.count{

    print(arr[i])
    
}

## 匿名函数简写方式
### 无参数无返回值
```swift
func test(param:() -> Void){

    param()
    
}

test(param:{() -> Void in

    print("nmsl")
    
})

test{

    print("nmsl")
    
}
```
### 单个参数无返回值
```swift
func test(param:(Int) -> Void){

    param(10)
    
}

test(param:{(value:Int) -> Void in

    print(value)

})

test(param:{(value) -> Void in

    print(value)

})

test{ (value) in

    print(value)
    
}
```
### 有参数有返回值
```swift
func test(param:{(item1:Int,item2:Int) -> Int}){

    print(param(10,20))
    
}

test(param:{(item1,item2) -> Int in

    return item1+item2

})

test(param:{return $0 + $1})

test(param: {$0 + $1})
```

## 类与结构体

### 拷贝构造
**结构体是值传递**
**结构体是引用传递**

### 常量修改
**结构体常量不能修改成员变量**
```swift
struct Student{

    var name = "hello"
    
}

let s1 = Student()

s1.name = "world"
```
报错

**类的常量可以修改成员变量**
```swift
class Student{

    var name = "hello"
    
}

let s1 = Student()

s1.name = "world"
```
可以执行

## 类的重写
### 重写成员变量
用于改变子类对父类成员调用产生的效果
**要求父类成员外部可以调用**
关键字`override`
```swift
class Person{

    var name:String
    
    var age:Int
    
    init(name:String,age:Int){
    
        self.name = name
        
        self.age = age
        
    }
}

class Student:Person{

    override var name:String{
    
        set{
        
            super.name = super.name + " ----- student"
            
        }
        
        get{
        
            return super.name
            
        }
    }
    
    override init(name:String,age:Int){
    
        super.init(name:name,age:age)
        
        self.name = name
        
    }
}
```
### 重写接口
如果父类的成员变量为私有，可以通过重写接口达到目的
```swift
class Person{

    private var name:String
    
    private var age:Int
    
    init(name:String,age:Int){
    
        self.name = name
        
        self.age = age
        
    }
    
    func setName(name:String){
    
        self.name = name
        
    }
    
    func setAge(age:Int){
    
        self.age = age
        
    }
    
    func getName() -> String{
    
        return self.name
        
    }
}

class Student:Person{

    override init(name:String,age:Int){
    
        super.init(name:name,age:age)//一定要先初始化父类
        
    }
    
    override func getName() -> String{
    
        return super.getName() + " ---- Student"
        
    }
    
    override func setAge(age:Int){
    
        super.setAge(age:age-10)
        
    }
}
```
#### 新建接口
```swift
func getName_ultra() -> String{

    return super.getName() + " ---- Student"
    
}
```

#### 重写初始化器
```swift
override init(name:String,age:Int){

    super.init(name:name,age:age-10)
    
}

### 类的继承

#### 语法
```swift
class Person{

    ...
    
}

class Student:Person{

    ...
    
}
```
如果不允许一个类被继承就加关键字`final`
```swift
final class Person{

    ...
    
}
```
#### 用法
子类会继承父类的所有属性，并可以拥有自己的属性
```swift
class Person{

    private var name:Stirng
    
    private var age:Int
    
    init(name:String,age:Int){
    
        self.name = name
        
        self.age = age
        
    }
    
    func getAge() -> Int{
    
        return self.age
        
    }
    
    func getName() ->String{
    
        return self.name
        
    }
    
    func setAge(age:Int){
    
        self.age = age
        
    }
    
    func setName(name:String){
    
        self.name = name
        
    }
    
}

class Student:Person{

    func play(param:String){
    
        print(param)
        
    }
    
var a = Person(name:"A",age:30)

var b = Student(name:"B",age:18)

print(b.getName())

b.setAge = 19

print(b.getAge())

b.play("nmsl")    
```
### 向下类型转换
子类继承父类可以看作一个父类的引用指向子类
```swift
class Student:Person{}

var a:Person = Student()

a.setName(name:"hehe")

print(type(of:a))
```
结果是Student

但不可以作为**Any**的引用
```swift
var b:Any = student()

b.setName(name:"sb")
```
结果报错，不能执行
因此可以做一个类型转换
```swift
var c = b as? Student

c.setName(name:"sd")

print(c.getName())
```
通过了类型转换后，c是一个`Student`的**可选**类型，此时还是不能执行成员函数
因此可以有以下几种方法
#### 确定转换
```swift
var d = b as! Student

d.setName(name:"lhr")
```
#### 常量接收(可选项绑定)
```swift
if let d = b as? Student{

    d.setName(name:"lhr")
    
}
```
#### 类型解析
```swift
var d = b as? Student

d!.setName(name:"lhr")
```

## 结构体
### 结构体的构造函数
结构体中写**init**函数相当于构造函数
```swift
struct Student{

    var name:String
    
    init(name:String){
    
        self.name = name
    
    }
}


var a = Student(name:"sb")
``` 
## 多态调用方法
一个实例调用方法是会根据它的类型去找
```swift
class B:A{

    override func printName(){
    
        print("this is B " + name)
        
    }
    
    func play(){
    
        print("this is B play")
        
    }
}

var s2:A = B(name:"b")

s2.play()
```
调用不成功，因为A类中没有`play`方法
因此可以做强制类型转换
```swift
var s3 = s2 as! A
```
或者在A中补写`play`方法