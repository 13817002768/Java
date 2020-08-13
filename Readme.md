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

<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-io</artifactId>
    <version>1.3.2</version>
</dependency>
```



```java
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

