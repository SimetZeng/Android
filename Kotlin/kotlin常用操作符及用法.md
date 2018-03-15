<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [kotlin常用操作符及用法](#kotlin常用操作符及用法)
	- [?](#)
	- [?:](#)
	- [!!](#)
	- [.. in !in](#-in-in)
	- [downTo()函数](#downto函数)
	- [step()函数](#step函数)
	- [::](#)
	- [@](#)
	- [as?](#as)
	- [is](#is)
	- [$](#)

<!-- /TOC -->

# kotlin常用操作符及用法
## ?
- 表示这个对象可能为空
  - <span style="color:red">var name: String? = "zhangsan"  </span>
  - <span style="color:red">b?.length //如果 b非空，就返回 b.length ，否则返回 null </span>

## ?:
- 如果?:左侧表达式非空，则返回其左侧表达式，反之返回右侧表达式。当且仅当左侧为空时，才会对右侧表达式求值
  - <span style="color:red">val l = b?.length ?: -1 </span>

## !!
- 返回一个非空的b值或者如果b为空就会抛出空指针异常
  - <span style="color:red">val l = b!!.length</span>

## .. in !in
- x..y：代表从x到y，包含x和y(闭区间运算符)
- until：代表从x到y，包含x但不包含y，
- in代表在一个区间中，!in代表不在一个区间中

## downTo()函数
- 倒叙遍历，区间内循环
```javascript
for (i in 4 downTo 1){
    print(i)
}
//输出4321
```

## step()函数
- 可以进行任意数量的迭代，而不是每次变化都是1
```javascript
for (i in 1..4 step 2) print(i) // prints "13"
for (i in 4 downTo 1 step 2) print(i) // prints "42"
```

## ::
- 得到类的Class对象
- <span style="color:red">startActivity(Intent(this@KotlinActivity, MainActivity::class.java))</span>

## @
- 限定this的类型
```javascript
class User {
    inner class State{
        fun getUser(): User{
            return this@User //返回User
        }
        fun getState(): State{
            return this@State //返回State
        }
    }
}
```
- 作为标签
  - 跳出多层for循环
  ```javascript
  loop@ for (itemA in arraysA) {
    var i : Int = 0
    for (itemB in arraysB) {
      i++
      if (itemB > 2) {
        break@loop
      }
      println("itemB:$itemB")
    }
  }
  ```
  - 命名函数自动定义标签
  ```javascript
  fun fun_run(){
      run {
          println("lambda")
      }
      var i: Int = run {
          return@run 1
      }
      println("$i")
      //匿名函数可以通过自定义标签进行跳转和返回
      i = run (outer@{
          return@outer 2
      })
      println(i)
  }
  ```
  - 从forEach函数跳出
  ```javascript
  fun forEach_label(ints: List<Int>) {
        var i =2
        ints.forEach {
            //forEach中无法使用continue和break;
            //if (it == 0) continue //编译错误
            //if (it == 2) break //编译错误
            print(it)
        }
         run outer@{
             ints.forEach {
                 if (it == 0) return@forEach //相当于在forEach函数中continue,实际上是从匿名函数返回
                 if (it == 2) return@outer //相当于在forEach函数中使用break,实际上是跳转到outer之外
             }
         }
        if (i == 3) {
            //每个函数的名字代表一个函数地址，所以函数自动成为标签
            return@forEach_label //等同于return
        }
    }
  ```

## as?
- 安全转型，当转型不成功时，会返回null

## is
- 判断某个实例是否是某个类型

## $
- 字符串可以包含模板表达式，及一小段代码，会求值并把结果包含到字符串中
- <span style="color:red">val value:Int=5;</span>
- <span style="color:red">val str:String="the value is $value"</span>
- <span style="color:red">var userInfo = "name:${user.name},  age:$age"</span>
