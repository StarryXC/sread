> Thinking

```
Layout
    StaticLayout
    DynamicLayout
    BoringLayout

CharSequence
    Spanned
        Spannable
            SpannableString
            SpannableStringBuilder
    Editable
    GetChars
Appendable

CharacterStyle
    ForegroundColorSpan
    ClickableSpan
        URLSpan
    MetricAffectingSpan
        StyleSpan

Html
```

> Memory

```
Layout layout = new StaticLayout("", new TextView(context).getPaint(), 100 , Layout.Alignment.ALIGN_NORMAL, 1.0f, 0.0f, false);
layout.getWidth(); layout.getHeight();
layout.getPaint();
layout.getLineCount();
layout.getLineWidth(1);

Spannable spannable = new SpannableString();
ForegroundColorSpan foregroundColorSpan = new ForegroundColorSpan(0x111111);
spannable.setSpan(foregroundColorSpan, 1, 20, Spanned.SPAN_EXCLUSIVE_INCLUSIVE);

new ForegroundColorSpan(Color.BLUE)
new StyleSpan(Typeface.BOLD)

Editable editable = new SpannableStringBuilder();
editable.insert(1, "");
editable.delete(1, 12);
editable.append("");
editable.clearSpans();
editable.replace(1, 1, "");
editable.getFilters(); editable.setFilters(new InputFilter[1]);

Html.fromHtml("", Html.FROM_HTML_MODE_COMPACT);
```

