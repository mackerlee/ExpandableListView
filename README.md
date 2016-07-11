# ExpandableListView

Lesson 87-89 ExpandableListView

1.ExpandableListView:ListView的扩展，一个视图显示垂直滚动两级列表中的条目，与普通列表视图ListView区别在于，它允许两个层次，组织单                      独可以扩展为显示其子项,即每一个列表项下面还可以包含一个列表项（二级列表）.
  --使用方法：
    --1.要给ExpandableListView设置适配器，必须先设置数据源;
    --2.数据源，就是此处的适配器类ExpandableAdapter，此方法继承类BaseExpandableListAadapter,它是ExpandableListView的一个子类，需     要重写里面的多个方法;数据源中，用到类自定义的view布局，此时根据自己的需求，来设置组和子项的布局样式;

2.ExpandableListView实例：
  在res->layout->activity_main.xml主布局中新建ExpandableListView组件：
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:paddingBottom="@dimen/activity_vertical_margin"
      android:paddingLeft="@dimen/activity_horizontal_margin"
      android:paddingRight="@dimen/activity_horizontal_margin"
      android:paddingTop="@dimen/activity_vertical_margin"
      tools:context="com.example.mackerlee.android_87.MainActivity">
  
      <ExpandableListView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:id="@+id/expandableListView87"
          android:layout_alignParentTop="true"
          android:layout_alignParentStart="true"
          android:layout_alignParentEnd="true" />
  </RelativeLayout>
  
  在在res->layout->新建一级列表目录group_itm87.xml:
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="horizontal"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:gravity="center_vertical">
  
      <ImageView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:id="@+id/imageView_group87"
          android:src="@drawable/qq"/>
  
      <TextView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:textAppearance="?android:attr/textAppearanceLarge"
          android:text="Large Text"
          android:id="@+id/textView_group87" />
  </LinearLayout>
  
  在res->layout->新建一个二级列表目录child_item87.xml:
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      android:orientation="horizontal"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:gravity="center_vertical">
  
      <ImageView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:id="@+id/imageView_child87"
          android:src="@drawable/yy"/>
  
      <TextView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:textAppearance="?android:attr/textAppearanceMedium"
          android:text="Medium Text"
          android:id="@+id/textView_child87"  />
  
  </LinearLayout>
  
  在主文件java->包名->MainActivity.java中实现配置：
  package com.example.mackerlee.android_87;

  import android.support.v7.app.AppCompatActivity;
  import android.os.Bundle;
  import android.view.View;
  import android.view.ViewGroup;
  import android.widget.BaseExpandableListAdapter;
  import android.widget.ExpandableListView;
  import android.widget.ImageView;
  import android.widget.TextView;
  
  public class MainActivity extends AppCompatActivity {
  
      private ExpandableListView expandableListView;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          expandableListView = (ExpandableListView)findViewById(R.id.expandableListView87);
          expandableListView.setAdapter(new MyExpandableListViewAdapter());
      }
  
      //--自定义ExpandableListView的适配器
      class MyExpandableListViewAdapter extends BaseExpandableListAdapter{
  
          private String[] groups = {"家人","朋友","同事"};
          private String[][] childs = {{"老爸","老妈"},{"宝宝","威哥"},{"科长","副科长"}};
  
          //--返回分组的数量，一共分几组
          public int getGroupCount() {
              return groups.length;
          }
  
          //--里面每一个二级列表的数量,即每一个列表项里面包含的数量
          public int getChildrenCount(int groupPosition) {
              return childs[groupPosition].length;
          }
  
          //--返回每组对象的信息
          public Object getGroup(int groupPosition) {
              return groups[groupPosition];
          }
  
          //--返回每组中的每个子列表项的对象
          public Object getChild(int groupPosition, int childPosition) {
              return childs[groupPosition][childPosition];
          }
  
          //--返回groupid
          public long getGroupId(int groupPosition) {
              return groupPosition;
          }
  
          @Override
          public long getChildId(int groupPosition, int childPosition) {
              return childPosition;
          }
  
          //--每次返回ID是否是固定的
          public boolean hasStableIds() {
              return true;
          }
  
          @Override
          public View getGroupView(int groupPosition, boolean isExpanded, View convertView, ViewGroup parent) {
              if(convertView == null){
                  convertView = getLayoutInflater().inflate(R.layout.group_item87,null);
              }
              ImageView imageView = (ImageView)convertView.findViewById(R.id.imageView_group87);
              TextView textView = (TextView)convertView.findViewById(R.id.textView_group87);
              //imageView.setImageResource(ResId);
              textView.setText(groups[groupPosition]);
              return convertView;
          }
  
          @Override
          public View getChildView(int groupPosition, int childPosition, boolean isLastChild, View convertView, ViewGroup parent) {
              if(convertView==null){
                  convertView = getLayoutInflater().inflate(R.layout.child_item87,null);
              }
              ImageView imageView = (ImageView)convertView.findViewById(R.id.imageView_child87);
              TextView textView = (TextView)convertView.findViewById(R.id.textView_child87);
              //imageView.setImageResource(ResID);
              textView.setText(childs[groupPosition][childPosition]);
              return convertView;
          }
  
          //--子选项是否可选
          public boolean isChildSelectable(int groupPosition, int childPosition) {
              return true;
          }
      }
  }

  

