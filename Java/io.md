> Thinking

```
IO 流
序列化
文件
```

> Memory

```
InputStream inputStream = new FileInputStream("");
byte[] buffer = new byte[1024];
int len;
while ((len = inputStream.read(buffer)) != -1) {
}

BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
String line;
while ((line = bufferedReader.readLine()) != null) {
}

FileWriter fileWriter = new FileWriter("", true);
BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
bufferedWriter.write("asdfasdf");
bufferedWriter.flush();
bufferedWriter.close();

File file = new File("");
file.lastModified(); file.setLastModified(System.currentTimeMillis());
file.getAbsolutePath(); file.getAbsoluteFile(); file.isAbsolute();
file.getParentFile(); file.getParent();
file.getCanonicalFile();
file.getPath();
file.exists();
file.isFile(); file.isDirectory();
file.mkdir(); file.mkdirs();
file.list(new FilenameFilter() {
    @Override
    public boolean accept(File file, String s) { return false; }
});
file.listFiles(new FileFilter() {
    @Override
    public boolean accept(File file) { return false; }
});
file.getFreeSpace();
file.getTotalSpace();
file.getUsableSpace();
file.createNewFile();
file.canRead();
file.canWrite();
file.canExecute();
file.isHidden();
file.length();
```

