# `Swift`  #
***by Younni Baak***
 ***
 ***2022.11.11***
 ***
**1. Variabl (`var`)&Constant (`let`)**
```swift
/* When defining variables,the initial of the variable type should be capitalized in Swift */
/* Add an space in front and behind of "=" when you assignment */

var a:String = "Hello World" //Character string
var b:Character = "A" 
//Single character, multiple characters will error.
var c:Int = 23 
//integer，also include Int8、Int16、Int32...
var d:Float = 2.3
var e:Double = 20.23
var f:Bool = true
var g:UInt = 2023 
/* UInt expressed POSTIVE Integer,but not recommended if necessary */

/* Constant:change “var” to “let”,but To be Notice after that the data can't changed */

//Other
var a = "GoodBye World" //This method can be inferred by Xcode.
/* Now if there is " a = 12 " at below,it is error,beacuse "a" has already inferred a type:(String) */
```
**2. Function of `type`<br>**
`The function of type is a function that can infer the type of data.`
```swift
/*Method od Using(Usually the Xcode will auto association when you input ty...,it will appear at below) */
var a:String = "Hello World"
var c:Int = 23
print(a,c)
print(type(of: a),type(of: c),type(of: true))

//Output
Hello World 23
String Int Bool
```
**3. `print` Statement**
```swift
var a = "Hello"
var b = "World"
var c = 23
print("Hello World")
print(a,b)
print(a + b)
print(a + b + " \(c)")

//Output
Hello World
Hello World
HelloWorld
HelloWorld 23
```
**4. Type Alias:  `typealias` Statement**
```swift
typealias I = Int //Now you can use "I" express Int.

var a: I = 23
```
**5. Type Transformation**
```swift
var a = 23
var b = "Hello World"
var c = "23"
var TransA = Double(a) ?? 0  /* “??” means if "a" can comform to Int,return Int(a),if can't return the value of behind of "??" */
var TransB = Int(b) ?? 0
var TransB_2 = Double(b) ?? 0
var TransC = Int(c)
print("This is " + String(a))
print(TransA,TransB,TransB_2)
print(TransC)

//Output
This is 23
23.0 0 0.0
Optional(23)
```
**6. Optionals**(Means Optional Type)
```swift
var a:Int? = nil
var b:Int? = 23
print(a,b,b!) /* "!" means take the data out in b.Of course,because of "nil", "a!" is error. */

//Output
nil Optional(23) 23 
```
**7. Tuple**<br>
Difference to Python,a part of the tuple in Swift *can be changed*.
```swift
//Definition of tuple
var Tuple_1 = (1,2,3,"Hello")
let Tuple_2 = (4,5,6) //let tuple can't be changed
var Tuple_3 = Tuple_1 //Verify the tuple passed by value or by reference.
var Tuple_4 = (name1:1,name2:2,3)//We can defined name to all of the data.
var Tuple_5:(name1: Int,name2: String,Int?) = (1,"2",3) 
//Using this method of definition must defined all of data.

print(Tuple_1.3)
Tuple_1.3 = "Hello World"
 /* The data of var tuple can be changed,but its type can't
Such as" Tuple_1.3 = 23 ",when we defined the tuple,the data at lacation has already type:(String),so we can't change it to type:(Int) */

print(Tuple_1.0,Tuple_2.1)
print(Tuple_1.3)
Tuple_3.2 = 23
print(Tuple_1,Tuple_3)

print(Tuple_4)
print(Tuple_4.name1)
print(Tuple_4.0)

print(Tuple_5)
print(Tuple_5.name1)
print(Tuple_5.0)

//Output
Hello
1 5
Hello World
(1, 2, 3, "Hello World") (1, 2, 23, "Hello")
//So the data in tuple is passed by value nor by reference
(name1: 1, name2: 2, 3)
1
1
(name1: 1, name2: "2", Optional(3))
2
1
```
**8. Basic Operators**<br>
Basically the same as C  <br>
Plus Subtraction Multiplication Division,comparation,and or not,? :<br>
But it also has its own,such as mentioned in before” ?? “ “ ! ”
***
**9.`if` Statement**<br>
```swift
//for example
if (condition) {
    //code
}
else if (condition) {
    //code
}
else {
    //code
}

/* Notice,front&behind of "condition" is necessary. */
```
**`if` Statement Extensions**<br>
Optionals Binding of `if` 
```swift
//for example
//Optionals Binding
var Original:Int? = nil

if let a = Original {
    print("a is\(a)")
}
else{
    print("Nothing in a.")
}

//Output
Nothing in a
/* if " var Original:Int? = 2023 ",then output " a is 2023 " */
/* It is worth noting that although the "Original" is a type of Optional ,we needn't add "!" behind Original */
```
**10. Implicitly Unwrapped Optionals**
*(It's a little hard to understand)*<br>
In "6" we mentioned the *Optionals*,you can regard the "Int?" as a type of data.It is (Optional)Int.
Optionals hint the data(Variable & Constant) maybe a nil,it can use the `if` Statement to judge wheather exist a value.But if we assigned a value to a Variable or Constant,so after that it always exist a value.If we used the Optionals that Swift will judge it in every time, this is very inefficient.<br>
Implicitly unwrapped optionals is just an Optionals that always exist a value.<br>
```swift
//Optionals
var a:Int? = 100
var b = a!
print(a,b)
//Implicitly Unwrapped Optionals
var c:Int! = 2023
var d = c! //Notice,it must add an "!",otherwise return Optional(2023)
print(c,d)

var e:Int! = 2023
e = nil
print(e)

//Output
Optional(100) 100
Optional(2023) 2023
nil
/* If you replace " var e:Int = 2023 " in it then it will return an error. */
/* Thus it can be seen Implicitly unwrapped optionals can improve the effiecient of Optionals */
```
**11. `Switch-Case` Statement**<br>
In Swift, the `Switch-Case` Statement is same as other language.But it's worth noting that `Switch-Case` in Swift doesn't have a fallthrough effect.
For example, in C ,we often write as follows.
```c
switch a{
    case 1:
    case 2: printf("good"); break;
    default: printf("failure"); break;
} 
```
But in Swift, it can't be identify. So the "break" is unmeaningful. In Swift, implement completly a "case" will break immediately.<br>
It must rewrite as follows.<br>
```swift
switch a{
    case 1: printf("good")
    case 2: printf("good")
    default: printf("failure")
} 
```
**`fallthrough`**<br>
If you want to realize the effect of C. You can add a "`fallthrough`"
```swift
var a = 1
switch a{
    case 1，2，3: fallthrough //It will match multiple situations.
    case 4，5: printf("good"); 
    default: printf("failure");
} 

//Output
good
```
**`where` Statement**<br>
It can put in behind of switch in order to judge if establish ，this case can be executed.
```swift
var IELTS = 9,GPA = 4
switch IELTS{
    case 8...10 where GPA >= 4: print("Good")
    case 6...10: print("Pass")
    default: print("False")
}

//Output
Pass
```
**Combine Tuple**
```swift
var a = ("hello",10)
switch a{
    case var("hello",x): print("x = \(x)")
    case ("hello",20): print("Pass")
    default: print("False")
}

//Output
x = 10
```
**12. Range Operator**
```swift
var closedRge = 1...2023 //[1,2023]
var Rge = 1..<2023 //[1,2023)
var closedRgeDou = (1.5)...2023 //"()" is unecessary
var ParRgeFrm = 1... //[1,+∞）
var ParRgeThr = ...2023

print(type(of: closedRge))
print(type(of: Rge))
print(type(of: closedRgeDou))
print(type(of: ParRgeFrm))
print(type(of: ParRgeThr))

//Output
ClosedRange<Int>
Range<Int>
ClosedRange<Double>
PartialRangeFrom<Int>
PartialRangeThrough<Int>
```
***
**2022.11.13**
***
**13. `For-in` Loop**<br>
You can combine the *Range Operator* with the `For-in` Loop. Such as follows.
```swift
for index in 0...3 {
    print(index)
}

//Output
0
1
2
3
```
**The function of `stride`**<br>
In `For-in` Loop, we may not just need range of step size of 1, in this case, we can quote a function : `stride`. It seems like range function in Python.
```swift
//Programm Structure
stride(from: Strideable, to: Strideable, by: Comparable & SignedNumeric)

//for example
for index in stride(from: 0, to: 6, by: 2) {
    print(index)
}

//Output
0
2
4
```
Of course, you can change "*to*" to "*through*" in order to include "6"
```swift
//Programm Structure
stride(from: Strideable, through: Strideable, by: Comparable & SignedNumeric)
//For example
for index in stride(from: 0, to: 6, by: 2) {
    print(index)
}
//Besides, you can also use the Double in stride.
for index in stride(from: 0, through: 4.8, by: 2.4) {
    print(index)
}

//Output
0
2
4
6
0.0
2.4
4.8
```
**`reversed`**: You can use "reversed" function to reversing the range.
```swift
for index in stride(from: 0, through: 4.8, by: 2.4) {
    print(index)
}

//Output
4.8
2.4
0.0
```
Similarly, you can also use it in an Array or range operator.
```swift
var list = [1,2,3,4]
let Ary:Array = list.reversed()
print(Ary)

//Output
[4,3,2,1]
```
**`Continue & Break`**<br>
We mentioned above `break` is unmeaningful in `switch-case` but that's not mean it is useless. It still have been used for other sentence. Same as other Language,break means stop; continue means stop this round.

**14. `while` Loop**
```swift
//Programm Structure
while (Relational Expression){
    //code
}//Same as "if" Statement ,"()" is still unnecessary.

//For example(Rewrite 13.1)
var index = 0
while (index <= 3){
    print(index)
    index += 1
}
//or
var index = 0
while true {
    if(index <= 3){
       print(index)
       index += 1 
    }else{
        break
    }
}
/* This is an infallible method. Write "if" statement first ,finally add a "while (true)", this may make your logic clearer. */
```
**`repeat-while` Loop**<br>
`repeat-while` Loop is same as the *`do-while`* Loop in other language. But we don't know why did Apple use "repeat" to defined it.
```swift
//Programm Structure
repeat{
    //code
}while(Relational Expression)
```
**15.String's Operation**<br>
First, there are lots of developer feedback the string's operation in Swift is suck.It likes shit. When you finished your learn, you may think same as it.<br>
**·(1) String Index**<br>
String.Index correspond every character in a string.
```swift
var string = "Hello World"

print(string.count) //Include space
print(string[string.startIndex])

/* NOTICE! Please don't use such as "string[string.endIndex]", string.endIndex means the postion of stop in String, so this method crossed the String's border*/

//You can use the other "str.index"
print(string[string.index(before: string.endIndex)])
print(string[string.index(string.startIndex, offsetBy: 2)]) //"string.startIndex" means 0
print(string[(string.index(string.startIndex, offsetBy: 2))...(string.index(string.startIndex, offsetBy: 4))])
//You can short it
var a = string.index(string.startIndex, offsetBy: 2)
var b = string.index(string.startIndex, offsetBy: 4)
print(string[a...b])

var c = string.firstIndex(of: "o")  ?? string.endIndex //If it isn't exist "o", return "string.endIndex"
print(string[string.startIndex...c])

print(string.prefix(5))
var d = string.index(string.endIndex, offsetBy: -5)

print(string[(d..<string.endIndex)])

print(string[string.index(after: string.startIndex)])  //Easily, after "string.startIndex"

//Output
11
H
d
l
llo
llo
Hello
Hello
World
e
```
***
***2022.11.16***
***
**·(2)Others Operator**
```swift
var str = "ABCDEF"

print(str.contains("X"))
print(str.contains("A"))

print(str.contains(where: String.contains("BG")))
/* Although It's not exist "G", but because exist "B" so return "true" */

print("Prefix : " + String(str.hasPrefix("AB")))
print("Suffix : " + String(str.hasSuffix("EF")))

str.append("+GHIJ")
print(str)

str.insert(contentsOf: "-Hello-", at: str.index(str.startIndex, offsetBy: 3))
print(str)

let index_1 = str.index(str.startIndex, offsetBy: 4)
let index_2 = str.index(str.startIndex, offsetBy: 8)
let range = index_1...index_2
str.replaceSubrange(range, with: "HELLO")
print(str)

str.remove(at: str.index(str.startIndex, offsetBy: 17))
print(str)

for x in str {
    print(x)
}

var MultilineText = """
                        Hello
                            world
                                !!!
                    """
print(MultilineText)

var EscChar = #""hello""#
print(EscChar)

//Output
false
true
true
Prefix : true
Suffix : true
ABCDEF+GHIJ
ABC-Hello-DEF+GHIJ
ABC-HELLO-DEF+GHIJ
ABC-HELLO-DEF+GHI
A
B
C
-
H
E
L
L
O
-
D
E
F
+
G
H
I
    Hello
        world
            !!!
"hello"
```
The part of String's Operation can be find in our document.<br>
Although it is so complex in string, you needn't remember it completely.<br>
***
***2022.11.17***
***
**16.Array**
```swift
//Defination
var Ary_1 = [1,2,3,4]
print(Ary_1)
print(type(of: Ary_1))

var Ary_2:[String] = ["Hello","world"]
print(Ary_2)
print(type(of: Ary_2))

var Ary_3:Array<Float> = [1.2,11,1.33]
print(Ary_3)
print(type(of: Ary_3))
//Visit
print(Ary_1[0],Ary_2[1],Ary_3[2])
//Change
Ary_1[3] = 100
print(Ary_1)
//Of course, you can't change any data in "let" array.

//Add Data
Ary_1 = Ary_1 + [4,5,6]
Ary_1 += [7,8,9]
print(Ary_1)

Ary_2.append("2023")
print(Ary_2)

//Insert Data
Ary_3.insert(100, at: 1) //Before "Ary_3[1]"
print(Ary_3)

//Search Data
print(Ary_1.contains(3))
print(Ary_2.contains("swift"))

//Replace Data
Ary_1.replaceSubrange(3...9, with: [4,5,6,7,8,9,0])
print(Ary_1)

//Delet Data
Ary_2.remove(at: 2)
print(Ary_2)

//Output
[1, 2, 3, 4]
Array<Int>
["Hello", "world"]
Array<String>
[1.2, 11.0, 1.33]
Array<Float>
1 world 1.33
[1, 2, 3, 100]
[1, 2, 3, 100, 4, 5, 6, 7, 8, 9]
["Hello", "world", "2023"]
[1.2, 100.0, 11.0, 1.33]
true
false
[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
["Hello", "world"]
```
Comparing with Tuple, there is same type in an array.Such as follows is not be allow.
```swift
var Ary = [1,"2",3]
```
**Foreach**
```swift
//Foreach
//Method 1
var Array = [1,2,3,4,5]
for data in Array{
    print(data)
}

//Method 2
for index in (0..<(Array).count){
    print(Array[index])
}
for data in Array[0...]{
    print(data)
}
//Output
1
2
3
4
5
1
2
3
4
5
1
2
3
4
5
```
**17.Set**
```swift
var Set_1:Set = [1,2,3,4]
print(Set_1)

var Set_2:Set<String> = ["Hello","World"]
print(Set_2)

//Operation
print(Set_1.count)
Set_1.remove(4)
print(Set_1)
Set_2.insert("2023")
print(Set_2)
print(Set_2.contains("Hello"))
print(Set_2.contains("hello"))

var Set_3:Set = ["Swift","iOS","Hello"]
print(Set_2.union(Set_3))  //Only in same type Set

print(Set_2.intersection(Set_3)) //Only in same type Set

print(Set_2.symmetricDifference(Set_3)) //Only in same type Set

print(Set_2.subtracting(Set_3)) //Only in same type Set

//Output
[2, 4, 1, 3]
["Hello", "World"]
4
[2, 1, 3]
["Hello", "2023", "World"]
true
false
["Hello", "2023", "World", "Swift", "iOS"]
["Hello"]
["2023", "World", "iOS", "Swift"]
["World", "2023"]
```
**18.Dictionary**
```swift
var Dic_1:Dictionary = ["1":"A","b":"B"]
print(Dic_1)

var Dic_2:Dictionary<String,String> = ["a":"A","b":"B"]
print(Dic_2)

var Dic_3:[Int:String] = [1:"A",2:"B"]
print(Dic_3)

var Dic_4 = ["a":"A","b":"B"]
print(Dic_4)

print(Dic_1["1"]!)

print(Dic_2["a"] ?? "unkown")
print(Dic_2["c"] ?? "unkown")

//Change
Dic_1["1"] = "a"
Dic_1["3"] = "c"
print(Dic_1)
Dic_1.updateValue("d", forKey: "3")
print(Dic_1)
Dic_2.removeValue(forKey: "a")
print(Dic_2)

//Optionals Binding of if
if var value = Dic_3[1]{ //Dic_3[1] = "A"
    print(value)
}else{
    print("unkwon")
}

if var value = Dic_3[3]{ //Dic_3[3] is unkwon
    print(value)
}else{
    print("unkwon")
}

//Output
["b": "B", "1": "A"]
["b": "B", "a": "A"]
[1: "A", 2: "B"]
["b": "B", "a": "A"]
A
A
unkown
["b": "B", "3": "c", "1": "a"]
["b": "B", "3": "d", "1": "a"]
["b": "B"]
A
unkwon
```
***
***2022.11.20***
***
**Traversal Dictionar**
```swift
var dic = ["a":"A","b":"B","c":"C"]
for (key,value) in dic{
    print("Key = \(key) | Value = \(value)")
}//The "key"&"value" in "for-in" statement can be customized.

//Output
Key = a | Value = A
Key = c | Value = C
Key = b | Value = B
```
**19.Filter**<br>
It can be used in many type, include Set Dictionary Array and so on.In order to filter **value**.
```swift
var dic = [ "a":"A","b":"B","c":"C" ]

var new_dic = dic.filter({(key,value) -> Bool in
    if value != "B" {
        return true
    }else{
        return false
    }
})//The "key"&"value" in "filter" statement can be customized.

print(new_dic)

//Output
["a":"A","c":"C"]
```
**20.Use Function**<br>
In "C", we can use this method as follows to define a function.
```c
void test(int a,int b){
    printf("%d",a - b);
}
```
But in swift
```swift
func test(name:(a:Int,b:Int)) -> Void {
    print(name.a - name.b)
}
```
**Inname & Outname**
```swift
func test(Outname Inname:(a:Int,b:Int)) -> Void {
    print(Inname.a + 100)
    print(Inname.b - 10)   
}

test(Outname: (100,30)) //You must use the "Outname" 

//Output 
200
20
```
You can also use the "_".<br>
Its effect is to default to no Outname & Inname.
```swift
//No define Outname
func test(_ Inname1:Int,_ Inname2:Int) -> Void {
    print(Inname1 + 100)
    print(Inname2 - 10)
    
}
var a = 100,b = 30
test(a,b)
/* No define Inname,but use this method you must be sure the key in Outname same as the inside of function */
func test(Outname _:(a:Int,b:Int)) -> Void {
    print(a + 100)
    print(b - 10)   
}
var a = 100,b = 30
test(Outname: (a,b))
//No define Out & In name
func test(_ _:(a:Int,b:Int)) -> Void {
    print(a + 100)
    print(b - 10)   
}
var a = 100,b = 30
test((a,b))

//Output 
200
20
200
20
200
20
```
If you don't add outname at all. It will use the inname as its outname.As follows.
```swift
func test(Inname:(a:Int,b:Int)) -> Void {
    print(Inname.a + 100)
    print(Inname.b - 10)
    
}
var a = 100,b = 30
test(Inname: (a,b))
```
**`inout`**
It can change the function passed method. Using `inout`, pass to function's value will from value to laction.
```swift
func test(name: inout Int)
{
    name *= 2
    
    print(name)
    
}
var a = 10
test(name: &a) //Notice, you must use "&" to get it location.

//Output
20
```
If you don't use the "inout", the programm won't run.<br>
**assert**<br>
If you use the assert statement, the programm will stop its run.
```swift
assert(false ,the programm will stop)
//The statment in "()" ,will print in the consoles.
```
***
***2022.11.21***
***
**21. `guard-else` Statement**
```swift
//Guard Statement
func gud(gudTest:Int)
{
    guard gudTest <= 10 else{
        print("Guard ")
        return
    }
    print(gudTest)
}
gud(gudTest: 9)
gud(gudTest: 11)
/* If gudTest > 10, the guard will stop function and run inside "guard-else" */
```
Simularily, `guard-else` statement also exist a operation of Optional Binding. Here won't repeat it.
