> Thinking

```
CalendarContract.Events
_ID
TITLE
CONTENT_URI
DESCRIPTION
EVENT_LOCATION
EXTRA_EVENT_BEGIN_TIME long
EXTRA_EVENT_ALL_DAY boolean

ContactsContract.Contacts
_ID
DISPLAY_NAME
CONTENT_URI
CONTENT_FILTER_URI

ContactsContract.Data
CONTACT_ID
MIMETYPE
DISPLAY_NAME
CONTENT_URI

ContactsContract.CommonDataKinds.Phone
CONTENT_ITEM_TYPE
NUMBER

ContactsContract.PhoneLookup
CONTENT_FILTER_URI

ContactsContract.Intents
SHOW_OR_CREATE_CONTACT

ContactsContract.Intents.Insert
COMPANY
POSTAL

ContactsContract.CommonDataKinds.Phone.CONTENT_URI # URI
ContactsContract.CommonDataKinds.Phone.NUMBER # String 手机号
ContactsContract.PhoneLookup.DISPLAY_NAME # String 姓名
```

> Memory

```
ContactsContract.Contacts.DISPLAY_NAME
ContactsContract.Contacts.HAS_PHONE_NUMBER

ContactsContract.CommonDataKinds.Phone.CONTENT_URI
ContactsContract.CommonDataKinds.Phone.CONTACT_ID
ContactsContract.CommonDataKinds.Phone.NUMBER getString
ContactsContract.CommonDataKinds.Phone.TYPE getInt

ContactsContract.CommonDataKinds.StructuredPostal.CONTENT_URI
ContactsContract.CommonDataKinds.StructuredPostal.CONTACT_ID
ContactsContract.CommonDataKinds.StructuredPostal.FORMATTED_ADDRESS
ContactsContract.Intents.Insert.POSTAL putString

ContactsContract.CommonDataKinds.Email.CONTENT_URI
ContactsContract.CommonDataKinds.Email.CONTACT_ID
ContactsContract.CommonDataKinds.Email.DATA
```

