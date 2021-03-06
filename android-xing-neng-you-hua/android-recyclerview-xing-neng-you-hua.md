# Android - RecyclerView 性能优化 - 刷新数据

![](../.gitbook/assets/image%20%284%29.png)

1. recycleView刷新方式分析； 
2. DiffUtil各种使用姿势； 
3. Myers差分算法； 
4. DiffUtil还不够，AsyncListDiff来了

## 全局刷新

优点：简单

缺点：每个可见的item都会被重新绘制，不管数据有没有变化；不会触发item的动画

```text
notifyDataSetChanged();
```

## 局部刷新

通过指定position刷新指定的item，解决全局刷新的问题

缺点：当不知道刷新那些position的时候，就无法使用；场景就是：当下拉刷新的时候，无法确定哪些数据需要刷新，只能全局刷新。

```text
notifyItemInserted();        // 增
notifyItemRemoved();         // 删
notifyItemChanged();         // 改
notifyItemMoved();           // 移
```

## 对比刷新：DiffUtil

Google 最早在 Support-v7:24:2.0 提供了DiffUtils 类，但是目前support库已经不再维护了，而是使用AndroidX版本（androidx.recyclerview.widget.DiffUtil）

作用：对比两个数据集，发现哪些数据变化了，哪些需要更新，哪些不需要更新，主要通过RecylerView提供的方法去刷新。

```text
// DiffUtil.Callback

public abstract static class Callback {
   
    // 旧列表数据的长度
    public abstract int getOldListSize();

    // 新列表数据的长度
    public abstract int getNewListSize();

    // 判断是否是同一个item    
    public abstract boolean areItemsTheSame(int oldItemPosition, int newItemPosition);

    // 如果是同一个item，也就是areItemsTheSame方法返回true，则继续判断内容是否相同
    public abstract boolean areContentsTheSame(int oldItemPosition, int newItemPosition);
 
    // 果item相同，内容不同，用 payLoad 记录这个 ViewHolder 中，具体需要更新那个View
    public Object getChangePayload(int oldItemPosition, int newItemPosition) {
        return null;
    }
}
```

 

## DiffereUtil 的算法

![](../.gitbook/assets/image%20%286%29.png)

![](../.gitbook/assets/image%20%281%29.png)

DiffUtil源码里有效率的测试：

100个item，有10个item修改，平均消耗0.39ms，中位数是0.35ms

![](../.gitbook/assets/image%20%287%29.png)

