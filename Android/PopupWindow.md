> Thinking

```

```

> Memory

```
PopupWindow popupWindow = new PopupWindow(ViewGroup.LayoutParams.FILL_PARENT, ViewGroup.LayoutParams.WRAP_CONTENT);
popupWindow.setAnimationStyle(R.style.popup_anim_report);
popupWindow.setFocusable(true);
popupWindow.setContentView(new View(context));
popupWindow.setBackgroundDrawable(new ColorDrawable(Color.WHITE));
popupWindow.setOutsideTouchable(true);
popupWindow.showAsDropDown(layout, 0, 2);
```

