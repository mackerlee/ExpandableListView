# ExpandableListView

Lesson 87 ExpandableListView

1.ExpandableListView:ListView的扩展，一个视图显示垂直滚动两级列表中的条目，与普通列表视图ListView区别在于，它允许两个层次，组织单                      独可以扩展为显示其子项,即每一个列表项下面还可以包含一个列表项（二级列表）.
  --使用方法：
    --1.要给ExpandableListView设置适配器，必须先设置数据源;
    --2.数据源，就是此处的适配器类ExpandableAdapter，此方法继承类BaseExpandableListAadapter,它是ExpandableListView的一个子类，需     要重写里面的多个方法;数据源中，用到类自定义的view布局，此时根据自己的需求，来设置组和子项的布局样式;
