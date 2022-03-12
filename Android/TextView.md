> Thinking

```
textView.append(content);
textView.setMovementMethod(LinkMovementMethod.getInstance());
```

> Memory

```
TextView
	android:textAppearance="?android:attr/textAppearanceLarge"
TextView
	android:autoLink="web"
	android:textColorLink="@color/result_text"
	android:textIsSelectable="true"
	android:selectAllOnFocus="true"
	android:textAppearance="?android:attr/textAppearanceSmall"

<CheckBox
        android:id="@+id/check_no_tip"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:buttonTint="@color/common_hint"
        android:text="不再提示"
        android:textColor="@color/common_hint" />

<RadioGroup
        android:id="@+id/trade_type_group"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:checkedButton="@id/check_buy"
        android:orientation="horizontal"
        android:paddingLeft="@dimen/common_margin"
        android:paddingRight="@dimen/common_margin">
radioGroup.setOnCheckedChangeListener { _, i ->







```

