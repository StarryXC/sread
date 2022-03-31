> Thinking

```
BaseMovementMethod MovementMethod
    ScrollingMovementMethod
        LinkMovementMethod
    ArrowKeyMovementMethod

TextView
    EditText
        AutoCompleteTextView
    Button
        CompoundButton
            CheckBox
            RadioButton
            ToggleButton
            Switch
```

> Memory

```
TextView textView = new TextView(context);
textView.getText(); textView.setText(""); textView.append("");
textView.getTextSize(); textView.setTextSize(12);
textView.getTextColors(); textView.setTextColor(Color.BLACK);
textView.getHintTextColors(); textView.setHintTextColor(Color.BLACK);
textView.getLinkTextColors(); textView.setLinkTextColor(Color.BLACK);
textView.isSingleLine(); textView.setSingleLine(true);
textView.setTextAppearance(android.R.attr.textAppearanceLarge);
textView.setAllCaps(true);textView.isAllCaps();
textView.setSelectAllOnFocus(true);
textView.getShowSoftInputOnFocus(); textView.setShowSoftInputOnFocus(true);
textView.isTextSelectable(); textView.setTextIsSelectable(true);
textView.setMovementMethod(LinkMovementMethod.getInstance());
textView.addTextChangedListener(new TextWatcher() {
    @Override
    public void beforeTextChanged(CharSequence s, int start, int count, int after) { }
    @Override
    public void onTextChanged(CharSequence s, int start, int before, int count) { }
    @Override
    public void afterTextChanged(Editable s) { }
});
textView.setFilters(new InputFilter[]{new InputFilter.LengthFilter(20)});
textView.setInputType(InputType.TYPE_TEXT_VARIATION_VISIBLE_PASSWORD);
textView.setInputType(InputType.TYPE_TEXT_VARIATION_PASSWORD | InputType.TYPE_CLASS_TEXT);
textView.setCompoundDrawablesWithIntrinsicBounds(ContextCompat.getDrawable(context, R.mipmap.ic_shenghuo_shoucang), null, null, null);


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

radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(RadioGroup radioGroup, int i) {
    }
});

AutoCompleteTextView autoCompleteTextView = new AutoCompleteTextView(context);
autoCompleteTextView.setThreshold(0);// 使得在输入1个字符之后便开启自动完成
autoCompleteTextView.dismissDropDown();// 当用户中途输入非法字符时，关闭下拉提示框
// autoCompleteTextView.performFiltering 该方法会在用户输入文本之后调用
// replaceText 当我们在下拉框中选择一项时 文本来填充文本域 重新replace逻辑，将用户输入的部分与后缀合并




```

