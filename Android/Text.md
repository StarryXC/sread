> Thinking

```
SpannableString spannableString = new SpannableString("");
ForegroundColorSpan foregroundColorSpan = new ForegroundColorSpan(0x111111);
spannableString.setSpan(foregroundColorSpan, 1, 20, Spanned.SPAN_EXCLUSIVE_INCLUSIVE);;

SpannableStringBuilder spannableStringBuilder = new SpannableStringBuilder();
spannableStringBuilder.append("append");

Editable
    append insert delete replace clear
    clearSpans
	getFilters setFilters

Layout

Html.fromHtml(title)
```

> Memory

```
StaticLayout # new StaticLayout(text, new TextView(getContext()).getPaint(), boundedWidth , Layout.Alignment.ALIGN_NORMAL, 1.0f, 0.0f, false);
	getHeight
	getLineCount
	getLineWidth
	getDesiredWidth

Spannable styled = new SpannableString(contents.toString());
      styled.setSpan(new StyleSpan(Typeface.BOLD), 0, namesLength, 0);
Spannable content = new SpannableString(newText + "\n\n");
content.setSpan(new URLSpan(linkURL), linkStart, linkEnd, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);

```

