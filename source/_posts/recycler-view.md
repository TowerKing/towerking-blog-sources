---
title: "RecyclerView的使用入门"
layout: post
date: 2016-01-13
updated: 2016-07-02
categories: Android
comments: true
---

不应该放弃学习的，更不应该放弃学习新知识。因为有时候新的知识点能够帮助我们更好的工作，并提高一定的工作效率。对于Android开发来说，RecyclerView就是这么个控件。它能够完成ListView与GridView的功能，而且还可以完成瀑布流的功能，关键是切换起来非常方便。

官网中有段英文说明是说RecyclerView是一个更高级与灵活的ListView版本。能够高效加载大量数据，同时我们还可以灵活的自定义该组件。我这只是简单的翻译，完整的可以参考[官方网址](http://developer.android.com/training/material/lists-cards.html#RecyclerView)(访问需要翻墙的)。

现在说明一下其简单的使用方法，下面将会是些代码片段，具体的看到效果还得自己写代码去看看。这里主要用到的组件有RecyclerView与CardView控件（这个比较简单的，就可以和LinearLayout使用方法差不多），然后依然使用前一篇文章使用的Butter Knife开源库。所以gradle配置文件需要涵盖下面的内容。

```
 dependencies {
     compile 'com.android.support:cardview-v7:23.1.1'
     compile 'com.android.support:recyclerview-v7:23.1.1'
     compile 'com.jakewharton:butterknife:7.0.1'
 }

```

gradle引用完jar包，就可以在项目中正常使用RecyclerView与CardView了，首先在MainActivity对应的layout文件中包含RecyclerView控件。

```
<android.support.v7.widget.RecyclerView
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/recycler_view" />
```

像ListView一样，我们需要为RecyclerView中的container添加一个新的layout文件以及对应的Adapter。其对应的layout文件如下，取名为`view_book_intro`。

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- A CardView that contains a TextView -->
    <android.support.v7.widget.CardView
        xmlns:card_view="http://schemas.android.com/apk/res-auto"
        android:id="@+id/card_view"
        android:layout_gravity="center"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        card_view:cardCornerRadius="4dp">
        <TextView xmlns:android="http://schemas.android.com/apk/res/android"
            android:id="@+id/book_intro_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
    </android.support.v7.widget.CardView>
</LinearLayout>
```

对应的Adapter（我取名是BookIntroAdapter）需要集成RecyclerView.Adapter，然后重写其三个方法，完整代码如下

```
 public class BookIntroAdapter extends RecyclerView.Adapter<BookIntroAdapter.ViewHolder> {
    private String[] mDataSet;

    public static class ViewHolder extends RecyclerView.ViewHolder {
    	// 获取到RecyclerView的container下的TextView组件信息
        @Bind(R.id.book_intro_title) TextView mTextView;
        public ViewHolder(View view) {
            super(view);
            // 别忘记这句，否则TextView就没有初始化
            ButterKnife.bind(this, view);
        }
    }

    public BookIntroAdapter(String[] bookDataSet) {
        this.mDataSet = bookDataSet;
    }

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate
                (R.layout.view_book_intro, parent, false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
    	// 这里是为控件赋值
        holder.mTextView.setText(mDataSet[position]);
    }

    @Override
    public int getItemCount() {
        return mDataSet.length;
    }
 }
```

看看这段代码是不是要比实现ListView的Adapter更简单呢？

接下来我们就可以在MainActivity中调用RecyclerView组件，MainActiviy的代码片段如下。

```
@Bind(R.id.recycler_view) RecyclerView recyclerView;
...	// 表示其他代码
@Override
protected void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ButterKnife.bind(this);
    ...

    // 1. 这可以实现ListView的功能
    recyclerView.setLayoutManager(new LinearLayoutManager(this));

    // 2. 这可以实现GridView功能，其中2表示一行显示两个元素
    recyclerView.setLayoutManager(new GridLayoutManager(this, 2));

    // 3. 这是瀑布流形式的调用方法，如果想看出效果，可以在初始化字符串时多给几个\n
    recyclerView.setLayoutManager(new StaggeredGridLayoutManager(2,
                StaggeredGridLayoutManager.VERTICAL));

    recyclerView.setAdapter(new BookIntroAdapter(new String[]{"Java", "Android", "C#"}));
 }
```

注意：上述代码片段中的1、2、3就是不同呈现方式需要的代码，在实际项目中根据实际情况任意选一个就好。看到这么便利的组件，难道不想试一试嘛？
