---
layout: post
title: Activity 跳转最佳实践
tags: [android]
---

> 今天你听到防空警报了吗？

有的时候，我们需要跳转到下一个 Activity 的同时，把数据也传递过去。我们通常使用下面这种写法：

#### 起始 Activity

    public class OriginActivity extends Activity {
    
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_origin);
    
            findViewById(R.id.btn).setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    // 发送数据
                    Intent intent = new Intent(OriginActivity.this, TargetActivity.class);
                    intent.putExtra(TargetActivity.EXTRA_KEY, "data");
                    OriginActivity.this.startActivity(intent);
                }
            });
        }
    
    }

#### 目标 Activity

    public class TargetActivity extends Activity {
    
        public static final String EXTRA_KEY = "com.owen.demo.TargetActivity.key";
    
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_target);
    
            // 接收数据
            String data = getIntent().getStringExtra(EXTRA_KEY);
        }
    
    }
    
这种写法是比较常见的写法。但是有个可以优化的地方：

> 目前 App 开发是团队合作，也许这个起始 Activity 是你写的，而目标 Activity 是另外一个人写的。当向目标 Activity 传递数据时，还要查看目标 Activity 的代码，才能知道 `putExtra()` 方法的 Key 值要写什么。
  那么有没有办法可以不写 Key 值，直接传递 value 值呢？答案是有的。

在目标 Activity 下添加一个静态方法 `actionStart`

    public static void actionStart(Context context, String data) {
        Intent intent = new Intent(context, TargetActivity.class);
        intent.putExtra(EXTRA_KEY, data);
        context.startActivity(intent);
    }
    
这样写就可以不写 Key 值，而且也避免少传数据而带来的空指针等异常，代码更优雅了。

下面是优化的代码：

#### 起始 Activity

    public class OriginActivity extends Activity {
    
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_origin);
    
            findViewById(R.id.btn).setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    // 发送数据缩短为一行代码
                    TargetActivity.actionStart(OriginActivity.this, "data");
                }
            });
        }
    
    }
    
#### 目标 Activity

    public class TargetActivity extends Activity {
    
        // KEY 可以改为 private，不用设为 public
        private static final String EXTRA_KEY = "com.owen.demo.TargetActivity.key";
    
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_target);
    
            // 接收数据的写法不变
            String data = getIntent().getStringExtra(EXTRA_KEY);
        }
    
        // 添加一个静态方法以供调用
        public static void actionStart(Context context, String data) {
            Intent intent = new Intent(context, TargetActivity.class);
            intent.putExtra(EXTRA_KEY, data);
            context.startActivity(intent);
        }
    
    }