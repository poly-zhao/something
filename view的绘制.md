

```java
// spec参数   表示父View的MeasureSpec 
// padding参数    父View的Padding+子View的Margin，父View的大小减去这些边距，才能精确算出 子View的MeasureSpec的size 
// childDimension参数  表示该子View内部LayoutParams属性的值（lp.width或者lp.height） 可以是wrap_content、match_parent、一个精确指(an exactly size),  
public static int getChildMeasureSpec(int spec, int padding, int childDimension)
```



上面方法**用于获取测量子view的测量规范**，返回值见下表更直观

| 子view尺寸\|父view测量规范 | MeasureSpec.EXACTLY | MeasureSpec.AT_MOST | MeasureSpec.UNSPECIFIED |
| ------------------ | ------------------- | ------------------- | ----------------------- |
| match_parent (-1)  | EXACTLY + 父size     | AT_MOST + 父size     | UNSPECIFIED + 0         |
| wrap_content (-2)  | AT_MOST + 父size     | AT_MOST + 父size     | UNSPECIFIED + 0         |
| 确切值 (>=0)          | EXACTLY + 确切值       | EXACTLY + 确切值       | EXACTLY + 确切值           |





---





```
/**
 * <p>
 * This is called to find out how big a view should be. The parent
 * supplies constraint information in the width and height parameters.
 * </p>
 *
 * <p>
 * The actual mesurement work of a view is performed in
 * {@link #onMeasure(int, int)}, called by this method. Therefore, only
 * {@link #onMeasure(int, int)} can and must be overriden by subclasses.
 * </p>
 *
 *
 * @param widthMeasureSpec Horizontal space requirements as imposed by the
 *        parent
 * @param heightMeasureSpec Vertical space requirements as imposed by the
 *        parent
 *
 * @see #onMeasure(int, int)
 */
public final void measure(int widthMeasureSpec, int heightMeasureSpec) {
    if ((mPrivateFlags & FORCE_LAYOUT) == FORCE_LAYOUT ||
            widthMeasureSpec != mOldWidthMeasureSpec ||
            heightMeasureSpec != mOldHeightMeasureSpec) {
。。。
        // measure ourselves, this should set the measured dimension flag back
        onMeasure(widthMeasureSpec, heightMeasureSpec);
。。。
        }
    }

    mOldWidthMeasureSpec = widthMeasureSpec;
    mOldHeightMeasureSpec = heightMeasureSpec;
}
```



```
/**
 * <p>
 * Measure the view and its content to determine the measured width and the
 * measured height. This method is invoked by {@link #measure(int, int)} and
 * should be overriden by subclasses to provide accurate and efficient
 * measurement of their contents.
 * @param widthMeasureSpec horizontal space requirements as imposed by the parent.
 *                         The requirements are encoded with
 *                         {@link android.view.View.MeasureSpec}.
 * @param heightMeasureSpec vertical space requirements as imposed by the parent.
 *                         The requirements are encoded with
 /
     protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        setMeasuredDimension(getDefaultSize(getSuggestedMinimumWidth(), widthMeasureSpec),
                getDefaultSize(getSuggestedMinimumHeight(), heightMeasureSpec));
    }
 
```



获取view宽度最小值和backgroud最小值中的最大值

```
/**
 * Returns the suggested minimum width that the view should use. This
 * returns the maximum of the view's minimum width)
 * and the background's minimum width
 *  ({@link Drawable#getMinimumWidth()}).
 * <p>
 * When being used in {@link #onMeasure(int, int)}, the caller should still
 * ensure the returned width is within the requirements of the parent.
 *
 * @return The suggested minimum width of the view.
 */
protected int getSuggestedMinimumWidth() {
    int suggestedMinWidth = mMinWidth;

    if (mBGDrawable != null) {
        final int bgMinWidth = mBGDrawable.getMinimumWidth();
        if (suggestedMinWidth < bgMinWidth) {
            suggestedMinWidth = bgMinWidth;
        }
    }

    return suggestedMinWidth;
}
```

设置view的宽度最小值， 哪里在调用这个方法还需要查

```
/**
 * Sets the minimum height of the view. It is not guaranteed the view will
 * be able to achieve this minimum height (for example, if its parent layout
 * constrains it with less available height).
 *
 * @param minHeight The minimum height the view will try to be.
 */
public void setMinimumHeight(int minHeight) {
    mMinHeight = minHeight;
}
```





```
/**
 * Utility to return a default size. Uses the supplied size if the
 * MeasureSpec imposed no constraints. Will get larger if allowed
 * by the MeasureSpec.
 *
 * @param size Default size for this view
 * @param measureSpec Constraints imposed by the parent
 * @return The size this view should be.
 */
public static int getDefaultSize(int size, int measureSpec) {
//size表示的是View想要的尺寸信息，比如最小宽度或最小高度
    int result = size;
    int specMode = MeasureSpec.getMode(measureSpec);
    int specSize = MeasureSpec.getSize(measureSpec);

    switch (specMode) {
    //如果mode是UNSPECIFIED，表示View的父ViewGroup没有给View在尺寸上设置限制条件，直接用自己最小值作为宽或高
    case MeasureSpec.UNSPECIFIED:
        result = size;
        break;
    //此处mode是AT_MOST或EXACTLY时，View就用其父ViewGroup指定的尺寸作为量算的结果
    case MeasureSpec.AT_MOST:
    case MeasureSpec.EXACTLY:
        result = specSize;
        break;
    }
    return result;
}
```





```
保存测量到的宽高到mMeasuredWidth和mMeasuredHeight中
protected final void setMeasuredDimension(int measuredWidth, int measuredHeight) {
    mMeasuredWidth = measuredWidth;
    mMeasuredHeight = measuredHeight;

    mPrivateFlags |= MEASURED_DIMENSION_SET;
}
```

在更高版本中上面方法还会调用setMeasuredDimensionRaw(measuredWidth, measuredHeight);}来保存view的测量宽高





