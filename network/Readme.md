###### 向服务器上传文件

所用依赖

```xml
<dependency>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>jackrabbit-webdav</artifactId>
    <version>2.21.3</version>
</dependency>

<dependency>
    <groupId>org.kie.modules</groupId>
    <artifactId>org-apache-commons-httpclient</artifactId>
    <version>6.2.0.CR2</version>
    <type>pom</type>
</dependency>

```



上传文件

```java
String url = "https://www.xxx.com"
public static void uploadFile(String url){
    File f = new File("C://Users/lyz/Desktop/123.txt");

    try{
        HttpClient client = new HttpClient();
        Credentials creds = new UsernamePasswordCredentials("username", "password");
        client.getState().setCredentials(AuthScope.ANY, creds);

        PutMethod method = new PutMethod(url + "/" + f.getName());
        RequestEntity requestEntity = new InputStreamRequestEntity(
                new FileInputStream(f));
        method.setRequestEntity(requestEntity);
        client.executeMethod(method);
        System.out.println(method.getStatusCode() + " " + method.getStatusText());
    }
    catch(HttpException ex){
        // Handle Exception
    }
    catch(IOException ex){
        // Handle Exception
    }
}
```

下载文件

```java
String url = "https://www.xxx.com/test.txt"
public static void downloadFile(String url){
    File f = new File("C://Users/lyz/Desktop/123.txt");

    try{
        HttpClient client = new HttpClient();
        Credentials creds = new UsernamePasswordCredentials("admin", "1qazXSW@");
        client.getState().setCredentials(AuthScope.ANY, creds);

        GetMethod method = new GetMethod(url);
        //PutMethod method = new PutMethod(url + "/" + f.getName());

        client.executeMethod(method);

        System.out.println(method.getStatusCode() + " " + method.getStatusText());
        System.out.println(method.getResponseBody());
        String s = method.getResponseBodyAsString();
        FileOutputStream outputStream = new FileOutputStream("1234.txt");
        outputStream.write(s.getBytes());
        outputStream.close();

    }
    catch(HttpException ex){
        // Handle Exception
    }
    catch(IOException ex){
        // Handle Exception
    }
}
```

