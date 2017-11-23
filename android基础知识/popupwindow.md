
settouchable(ture);
该方法设置为true的时候，响应点击事件；为false的时候，popupwindow不响应点击事件，透传到popupwindow之外的控件，有其他控件响应。

setfocusable(true);
setFocusable 使能控件获得焦点，设置为true时，并不是说立刻获得焦点，要想立刻获得焦点，得用requestFocus，这个时候，popupwindow中的eidttext能够获取
到焦点；为false的时候，edittext不能获得焦点，并且popupwindow显示的时候，不能拦截返回键，点击返回键，不是popupwindow消失，而是直接返回上一页。

setBackgroundDrawable(new BitmapDrawable());必须要设置这个才能实现点击popupwindow外部，popupwindow消失的效果。
setOutsideTouchable


点击外部区域,弹窗不消失,但是点击事件会向下面的activity传递,看了源码，这个Flag的设置与否是由一个叫mNotTouchModal的字段控制，但是设置该字段的set方法被标记为@hide。
　　所以要通过反射的方法调用：
/**
     * Set whether this window is touch modal or if outside touches will be sent
     * to
     * other windows behind it.
     *
     */
    public static void setPopupWindowTouchModal(PopupWindow popupWindow,
            boolean touchModal) {
        if (null == popupWindow) {
            return;
        }
        Method method;
        try {

            method = PopupWindow.class.getDeclaredMethod("setTouchModal",
                    boolean.class);
            method.setAccessible(true);
            method.invoke(popupWindow, touchModal);

        }
        catch (Exception e) {
            e.printStackTrace();
        }

    }
    
    然后在程序中：　　

UIUtils.setPopupWindowTouchModal(popupWindow, false);


问题：切换界面，但是PopupWindow暂时不需要dismiss的情况，如何处理：

链接地址：http://blog.csdn.net/u010929231/article/details/53445132

摘要：解决方案就是在Activity onPause的时候，手动取消PopupWindow的动画：

    @Override
    public void onPause() {
        super.onPause();
        if (mPopupWindow != null && mPopupWindow.isShowing()) {
            mPopupWindow.setAnimationStyle(0);
            mPopupWindow.update()
        }
    }
但是切换回来，我们应该再次把动画效果加上：

    @Override
    public void onResume() {
        super.onResume();
        if (mPopupWindow != null) {
            mHandler.postDelayed(new Runnable() {
                @Override
                public void run() {
                    mPopupWindow.setAnimationStyle(R.style.PopupWindowFilter);
                    mPopupWindow.update();
                }
            }, 200);
        }
    }

onResume()方法里之所以要延时200ms操作，是因为要在onResume行为结束后再将动画加上，否则会因为太早导致切换回来PopupWindow还会再次执行显示的动画。



