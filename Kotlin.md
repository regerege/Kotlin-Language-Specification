****************************************************************************************************
<div style="text-align: center;font-size:200%">
    目次
</div>

****************************************************************************************************

[1. 基本構文](#1-基本構文)  
　[1-1. パッケージとインポート](#1-1-パッケージとインポート)  
　[1-2. エントリーポイント](#1-2-エントリーポイント)  
　[1-3. 関数](#1-3-関数)  
　[1-4. 変数](#1-4-変数)  
　[1-5. コメント](#1-5-コメント)  
　[1-6. 文字列テンプレート](#1-6-文字列テンプレート)  
　[1-7. 条件式](#1-7-条件式)  
　[1-8. Nullable 値](#1-8-nullable-値)  
　[1-9. 型チェック と スマートキャスト](#1-9-型チェック-と-スマートキャスト)  
　[1-10. for ループ](#1-10-for-ループ)  
　[1-11. while ループ](#1-11-while-ループ)  
　[1-12. when 式](#1-12-when-式)  
　[1-13. 範囲](#1-13-範囲)  
　[1-14. コレクション](#1-14-コレクション)  
　[1-15. 基本的なクラスとインスタンス生成](#1-15-基本的なクラスとインスタンス生成)  
[2. コーディング規約](#2-コーディング規約)

****************************************************************************************************

# 1. 基本構文

## 1-1. パッケージとインポート
```kotlin
package my.demo

import kotlin.text.*
// ...
```

## 1-2. エントリーポイント
```kotlin
fun main() {
    println("Hello world!")
}
```

## 1-3. 関数
引数と戻り値がInt型の関数
```kotlin
fun sum(a:Int, b:Int) : Int {
    return a + b
}
```

関数内の式と戻り値型を省略
```kotlin
fun sum(a:Int, b:Int) = a + b
```

戻り値の型推論
```kotlin
fun printSum(a:Int, b:Int) {
    println("sum of $a and $b is ${a + b}")
}
```

## 1-4. 変数
読み取り専用の変数宣言 `val`
```kotlin
val a : Int = 1     // Int型の読み取り専用変数
var b = 2           // Int型の読み取り専用変数
var c : Int         // Int型の変数 C を宣言
c = 3
```

mutable な変数宣言 `var`
```kotlin
var x = 5
x += 1
```

変数のスコープ
```kotlin
val PI = 3.14
var x = 0

fun incrementX() {
    x += 1
}
```

## 1-5. コメント
```kotlin
// 1行コメント
/* ブロックコメント
　　複数行の記述が可能 */
/* ブロックコメントは
/* コメントのネストが可能 */
最終行 */
```

## 1-6. 文字列テンプレート
```kotlin
var a = 1

val s1 = "a is $a"

a = 2
val s2 = "${s1.replace("is", "was")}, but now is $a"
```
実行結果
```
a was 1, but now is 2
```

## 1-7. 条件式
```kotlin
fun maxOf(a:Int, b:Int) : Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}
```

簡易構文で記載可能
```kotlin
fun maxOf(a:Int, b:Int) = if (a > b) a else b
```

## 1-8. Nullable 値
```kotlin
fun parseInt(str:String) : Int? {
    return str.toIntOrNull()
}

fun printProduct(arg1:String, arg2:String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)

    if (x != null && y != null) {
        println(x * y)
    } else {
        println("'$arg1' or '$arg2' is not a number")
    }    
}


fun main() {
    printProduct("6", "7")
    printProduct("a", "7")
    printProduct("a", "b")
}
```

```kotlin
fun parseInt(str:String) : Int? {
    return str.toIntOrNull()
}

fun printProduct(arg1:String, arg2:String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)
    
    if (x == null) {
        println("Wrong number format in arg1: '$arg1'")
        return
    }
    if (y == null) {
        println("Wrong number format in arg2: '$arg2'")
        return
    }

    println(x * y)
}

fun main() {
    printProduct("6", "7")
    printProduct("a", "7")
    printProduct("99", "b")
}
```

## 1-9. 型チェック と スマートキャスト
```kotlin
fun getStringLength(obj:Any) : Int? {
    if (obj is String) {
        // is 文で型が分かるので、それ以降の構文では String 型として扱われる。
        return obj.length
    }
    return null
}
```

```kotlin
fun getStringLength(obj:Any) : Int? {
    if (obj !is String) return null
    return obj.length
}
```

```kotlin
fun getStringLength(obj:Any) : Int? {
    if (obj is String && obj.length > 0) {
        return obj.length
    }
    return null
}
```

## 1-10. for ループ
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
```

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${item[index]}")
}
```

## 1-11. while ループ
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
var index = 0
while (index < items.size) {
    println("item at $index is ${items[index]}")
}
```

## 1-12. when 式
Switch みたいな物
```kotlin
fun describe(obj:Any) : String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```

## 1-13. 範囲
```kotlin
val x = 10
val y = 9
if (x in 1..y+1) {
    println("fits in range")
}
```

```kotlin
val list = listOf("a", "b", "c")
if (-1 !in 0..list.lastIndex) {
    println("-1 is out of range")
}
if (list.size !in list.indices) {
    println("list size is out of valid list indices range, too")
}
```

```kotlin
for (x in 1..5) {
    print(x)
}
```

```kotlin
for (x in 1..10 step 2) {
    print(x)
}
println()
for (x in 9 downTo 0 step 3) {
    print(x)
}
```

## 1-14. コレクション
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
```

```kotlin
val items = setOf("apple", "banana", "kiwifruit")
when {
    "orange" in items -> println("juicy")
    "apple" in items -> println("apple is fine too")
}
```

```kotlin
val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
  .filter { it.startsWith("a") }
  .sortedBy { it }
  .map { it.toUpperCase() }
  .forEach { println(it) }
```

## 1-15. 基本的なクラスとインスタンス生成
```kotlin
fun main() {
    val rectangle = Rectangle(5.0, 2.0)
    val triangle = Triangle(3.0, 4.0, 5.0)
    println("Area of rectangle is ${rectangle.calculateArea()}, its perimeter is ${rectangle.perimeter}")
    println("Area of triangle is ${triangle.calculateArea()}, its perimeter is ${triangle.perimeter}")
}

abstract class Shape(val sides: List<Double>) {
    val perimeter: Double get() = sides.sum()
    abstract fun calculateArea(): Double
}

interface RectangleProperties {
    val isSquare: Boolean
}

class Rectangle(
    var height: Double,
    var length: Double
) : Shape(listOf(height, length, height, length)), RectangleProperties {
    override val isSquare: Boolean get() = length == height
    override fun calculateArea(): Double = height * length
}

class Triangle(
    var sideA: Double,
    var sideB: Double,
    var sideC: Double
) : Shape(listOf(sideA, sideB, sideC)) {
    override fun calculateArea(): Double {
        val s = perimeter / 2
        return Math.sqrt(s * (s - sideA) * (s - sideB) * (s - sideC))
    }
}
```

# 2. コーディング規約
