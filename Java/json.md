> Thinking

```
orgJson
Gson
Fastjson
```

> Memory

```
org.json
JSONObject topLevel = (JSONObject) new JSONTokener(contents.toString()).nextValue();
      JSONArray items = topLevel.optJSONArray("items");
authorsArray.isNull(0)

Gson https://github.com/google/gson
Gson # toJson fromJson
TypeToken # type rawType
import com.google.gson.annotations.SerializedName
implementation 'com.google.code.gson:gson:2.8.5'

data class Order(
    @SerializedName("side") val side: String
):Serializable

Fastjson https://github.com/alibaba/fastjson
JSON # parse
JSONObject
JSONObject
	parse
	getString
	getJSONObject
val data = JSONObject.parseObject(message) alibaba
```

