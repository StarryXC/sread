> Thinking

```

```

> Memory

```
val mSharedPreferences = context.getSharedPreferences("", Context.MODE_PRIVATE)
        mSharedPreferences.edit() {
            putBoolean("boo",false)
        }

        val mView: View = View(context)
        mView.doOnLayout {
        }
        mView.setOnClickListener({v -> })
        mView.setOnClickListener {  }

        val string = "baidu.com"
//        string.javaClass.simpleName
        val uri = string.toUri()

        val mIntent = Intent(context, MyAppCompatActivity::class.java)
        context.startActivity(mIntent)


//        var stackTrace : Array<StackTraceElement>  = Thread.currentThread().stackTrace
//        var stackTraceElement : StackTraceElement = stackTrace[3]
```

