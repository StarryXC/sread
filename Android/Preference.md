> Thinking

```

```

> Memory

```

<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
  <PreferenceCategory android:title="@string/preferences_scanning_title">
    <CheckBoxPreference
        android:key="preferences_decode_PDF417"
        android:defaultValue="false"
        android:title="@string/preferences_decode_PDF417_title"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_actions_title">
    <CheckBoxPreference
        android:key="preferences_supplemental"
        android:defaultValue="true"
        android:title="@string/preferences_supplemental_title"
        android:summary="@string/preferences_supplemental_summary"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_general_title">
    <ListPreference
        android:entries="@array/preferences_front_light_options"
        android:entryValues="@array/preferences_front_light_values"
        android:key="preferences_front_light_mode"
        android:defaultValue="OFF"
        android:title="@string/preferences_front_light_title"
        android:summary="@string/preferences_front_light_summary"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_result_title">
    <EditTextPreference
        android:key="preferences_custom_product_search"
        android:title="@string/preferences_custom_product_search_title"
        android:summary="@string/preferences_custom_product_search_summary"/>
    <ListPreference
        android:key="preferences_search_country"
        android:defaultValue="-"
        android:entries="@array/country_codes"
        android:entryValues="@array/country_codes"
        android:title="@string/preferences_search_country"/>
  </PreferenceCategory>
  <PreferenceCategory android:title="@string/preferences_device_bug_workarounds_title">
    <CheckBoxPreference
        android:key="preferences_disable_continuous_focus"
        android:defaultValue="false"
        android:title="@string/preferences_disable_continuous_focus_title"
        android:summary="@string/preferences_disable_continuous_focus_summary"/>
    <CheckBoxPreference
        android:key="preferences_disable_exposure"
        android:defaultValue="true"
        android:title="@string/preferences_disable_exposure_title"/>
  </PreferenceCategory>
</PreferenceScreen>

```

