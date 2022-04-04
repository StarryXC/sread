> Thinking

```
Java
orgJson
Gson
Fastjson
```

> Memory

### Java

```
org.json
JSONObject jsonObject = new JSONObject();
jsonObject.put("", ""); jsonObject.putOpt("", "");
jsonObject.getString(""); jsonObject.opt("");
jsonObject.keys(); jsonObject.names();
jsonObject.length();
jsonObject.has("");
jsonObject.isNull("");

JSONObject topLevel = (JSONObject) new JSONTokener(contents.toString()).nextValue();
      JSONArray items = topLevel.optJSONArray("items");
authorsArray.isNull(0)

Gson https://github.com/google/gson
implementation 'com.google.code.gson:gson:2.8.9'
Gson # toJson fromJson
new Gson().toJSon
T model = gson.fromJson(jsonString, cls);
TypeToken # type rawType
import com.google.gson.annotations.SerializedName
// 2.8.0
implementation 'com.google.code.gson:gson:2.8.5'

data class Order(
    @SerializedName("side") val side: String
):Serializable

Fastjson https://github.com/alibaba/fastjson
implementation 'com.alibaba:fastjson:1.2.12'
JSON
    JSONObject
    JSONArray
JSONObject jsonObject = (JSONObject) JSON.parse("");
jsonObject.put("", "");
jsonObject.getString("");
jsonObject.getJSONObject("");
jsonObject.getJSONArray("");
jsonObject.toJSONString();

JSONObject jsonObject = JSON.parseObject("");
JSONArray jsonArray = JSON.parseArray("");
JSONArray jsonArray = new JSONArray();
jsonArray.add("");
jsonArray.getInteger(0);
```

### Android

```
JsonReader jsonReader = new JsonReader(new FileReader(""));
jsonReader.beginArray();
jsonReader.endArray();
jsonReader.beginObject();
jsonReader.endObject();

JsonWriter jsonWriter = new JsonWriter(new FileWriter(""));
jsonWriter.beginArray();
jsonWriter.endObject();
jsonWriter.beginObject();
jsonWriter.endObject();
```



### OC

```

```

