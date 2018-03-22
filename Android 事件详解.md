

# 概述
Android里的事件大致分三大类：**onTouch**、**onLongClick**、**onClick**

# onTouch
带一个Boolear返回值。如果返回true，就不会再分发下去，如果返回false，就会分发下去

# onLongClick
- 带一个Boolear返回值。如果返回true，则表示不用再分发事件到下一级，如果返回false，则表示要分发到下一级，就是点击事件onClick。<span style="color:grey">此事件的上一层是onTouch事件</span>
- 常用事件
  - ACTION_DOWN: 表示按下了屏幕，第一个执行也是必然执行的方法
  - ACTION_MOVE: 表示移动手势，会不断的执行直到触摸停止
  - ACTION_UP: 表示为离开屏幕，触摸停止的时候执行
  - ACTION_CANCEL: 表示取消手势，不会由用户产生，而是由程序产生的
- 参数
  - View
    - 收到Touch事件的view对象
  - MotionEvent
    - 包含事件的详细信息。如：触摸点的信息，触摸事件类型的信息等
- 常用方法
  - getRowX：触摸点相对屏幕的坐标
  - getX：触摸点相对于view的坐标
  - getLeft：按钮左上角相对与父view(LinearLayout)的x坐标
  - getTop：按钮左上角相对与父view(LiearLayout)的y坐标

# onClick

# 实现事件
- **匿名内部类（建议使用这种）**
  - onTouch
  ```kotlin
  btn_login.onTouch { view, motionEvent ->
      Log.d("MainActivity", "you're onTouch")
      return@onTouch false
  }
  ```
  - onLongClick
  ```kotlin
  btn_login.onLongClick {
      Log.d("MainActivity", "you're onLongClick")
      return@onLongClick false
  }
  ```
  - onClick
  ```kotlin
  btn_login.onClick {  //btn_login: 界面上的某个控件id
      Log.d("MainActivity", "You're onClick the login button!")
  }
  ```

- **全局实现OnClickListener接口**
  - onTouch
  ```kotlin
  btn_login.setOnTouchListener { view, motionEvent ->
       Log.d("MainActivity", "you're onTouch")
       return@setOnTouchListener false
  }
  ```
  - onLongClick
  ```javascript
  btn_login.onLongClick {
      Log.d("MainActivity", "you're onLongClick")
      return@onLongClick false
  }
  ```
  - onClick
  ```javascript
  btn_login.setOnClickListener(this)
  ```
