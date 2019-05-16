# Java Client API参考文档 [![Slack](https://slack.min.io/slack?type=svg)](https://slack.min.io)

## 初始化MinIO Client object。

## MinIO

```java
MinioClient minioClient = new MinioClient("https://play.min.io:9000", "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");
```

## AWS S3


```java
MinioClient s3Client = new MinioClient("https://s3.amazonaws.com", "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY");
```

| 存储桶操作 |  对象操作 | Presigned操作  | 存储桶策略/生命周期操作
|:--- |:--- |:--- |:--- |
| [`makeBucket`](#makeBucket)  |[`getObject`](#getObject)   |[`presignedGetObject`](#presignedGetObject)   | [`getBucketPolicy`](#getBucketPolicy)   |
| [`listBuckets`](#listBuckets)  | [`putObject`](#putObject)  | [`presignedPutObject`](#presignedPutObject)  | [`setBucketPolicy`](#setBucketPolicy)   |
| [`bucketExists`](#bucketExists)  | [`copyObject`](#copyObject)  | [`presignedPostPolicy`](#presignedPostPolicy)  | [`setBucketLifeCycle`](#setBucketLifeCycle) |
| [`removeBucket`](#removeBucket)  | [`statObject`](#statObject) |   |  [`getBucketLifeCycle`](#getBucketLifeCycle) |
| [`listObjects`](#listObjects)  | [`removeObject`](#removeObject) |   |  [`deleteBucketLifeCycle`](#deleteBucketLifeCycle) |
| [`listIncompleteUploads`](#listIncompleteUploads)  | [`removeIncompleteUpload`](#removeIncompleteUpload) |   |   |
| [`listenBucketNotification`](#listenBucketNotification) |  |   |   |
| [`setBucketNotification`](#setBucketNotification) |  |   |   |
| [`getBucketNotification`](#getBucketNotification) |  |   |   |

## 1. 构造函数


|  |
|---|
|`public MinioClient(String endpoint) throws InvalidEndpointException, InvalidPortException`   |
| 使用给定的端点（endpoint）以及匿名方式创建一个MinIO client对象。|
| [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-)  |


|   |
|---|
|`public MinioClient(URL url) throws InvalidEndpointException, InvalidPortException`   |
| 使用给定的url以及匿名方式创建一个MinIO client对象。 |
| [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.net.URL-)  |


|  |
|---|
| `public MinioClient(okhttp3.HttpUrl url) throws  InvalidEndpointException, InvalidPortException`  |
|使用给定的HttpUrl以及匿名方式创建一个MinIO client对象。 |
| [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-okhttp3.HttpUrl-)  |

|   |
|---|
| `public MinioClient(String endpoint, String accessKey, String secretKey) throws  InvalidEndpointException, InvalidPortException`  |
|  使用给定的端点（endpoint）、访问密钥（access key）和密钥（secret key）创建一个MinIO client对象。 |
|   [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-java.lang.String-java.lang.String-)|

|   |
|---|
| `public MinioClient(String endpoint, int port,  String accessKey, String secretKey) throws InvalidEndpointException, InvalidPortException`  |
|  使用给定的端点（endpoint）、端口（port）、访问密钥（access key）和密钥（secret key）创建一个MinIO client对象。 |
| [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-int-java.lang.String-java.lang.String-)  |


|   |
|---|
| `public MinioClient(String endpoint, String accessKey, String secretKey, boolean secure) throws InvalidEndpointException, InvalidPortException`  |
| 使用给定的端点（endpoint）、访问密钥（access key）、密钥（secret key）和一个secure选项（是否使用https）创建一个MinIO client对象。 |
|  [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-java.lang.String-java.lang.String-boolean-) |


|   |
|---|
| `public MinioClient(String endpoint, int port, String accessKey, String secretKey, boolean secure) throws  InvalidEndpointException, InvalidPortException`  |
| 使用给定的端点（endpoint）、端口（port）、访问密钥（access key）、密钥（secret key）和一个secure选项创建一个MinIO client对象。  |
|  [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-int-java.lang.String-java.lang.String-boolean-) |

|   |
|---|
| `public MinioClient(okhttp3.HttpUrl url, String accessKey, String secretKey) throws InvalidEndpointException, InvalidPortException`  |
| 使用给定的HttpUrl对象、访问密钥（access key）、密钥（secret key）创建一个MinIO client对象。 |
| [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-com.squareup.okhttp.HttpUrl-java.lang.String-java.lang.String-)  |


|   |
|---|
| `public MinioClient(URL url, String accessKey, String secretKey) throws InvalidEndpointException, InvalidPortException`  |
|  使用给定的URL对象、访问密钥（access key）、密钥（secret key）创建一个MinIO client对象。 |
|  [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.net.URL-java.lang.String-java.lang.String-) |



|   |
|---|
| `public MinioClient(String endpoint, String accessKey, String secretKey, String region) throws InvalidEndpointException, InvalidPortException`  |
|  用给定的URL对象，访问密钥（access key）和密钥（secret key）创建MinIO client对象。|
|  [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-java.lang.String-java.lang.String-java.lang.String-) |



|   |
|---|
| `public MinioClient(String endpoint, int port, String accessKey, String secretKey, String region, boolean secure) throws InvalidEndpointException, InvalidPortException`  |
|  用给定的端点（endpoint），端口（port），访问密钥（access key）、密钥（secret key），区域（region）和安全选项（secure option）来创建MinIO对象。 |
|  [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-int-java.lang.String-java.lang.String-java.lang.String-boolean-) |



|   |
|---|
| `public MinioClient(String endpoint, int port, String accessKey, String secretKey, String region, boolean secure, okhttp3.OkHttpClient httpClient) throws InvalidEndpointException, InvalidPortException`  |
|  用给定的端点（endpoint），端口（port）、访问密钥（access key）、密钥（secret key）、区域（region）和安全选项（secure option）来创建MinIO对象。 |
|  [查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#MinioClient-java.lang.String-int-java.lang.String-java.lang.String-java.lang.String-boolean-) |


__参数__

| 参数  | 类型  | 描述  |
|---|---|---|
| `endpoint`  |  _string_ | endPoint是一个URL，域名，IPv4或者IPv6地址。以下是合法的endpoints: |
| | |https://s3.amazonaws.com |
| | |https://play.min.io:9000 |
| | |localhost |
| | |play.min.io|
| `port` | _int_  | TCP/IP端口号。可选，默认值是，如果是http,则默认80端口，如果是https,则默认是443端口。|
| `accessKey`   | _string_   |accessKey类似于用户ID，用于唯一标识你的账户。 |
|`secretKey`  |  _string_   | secretKey是你账户的密码。|
|`secure`    | _boolean_    |如果是true，则用的是https而不是http,默认值是true。 |
|`url`    | _URL_    |Endpoint URL对象。|
|`url`    | _HttpURL_    |Endpoint HttpUrl对象。 |
|`region`    | _string_    |用于访问端点的服务的区域名称。 |


__示例__


### MinIO


```java
// 1. public MinioClient(String endpoint)
MinioClient minioClient = new MinioClient("https://play.min.io:9000");

// 2. public MinioClient(URL url)
MinioClient minioClient = new MinioClient(new URL("https://play.min.io:9000"));

// 3. public MinioClient(okhttp3.HttpUrl url)
 MinioClient minioClient = new MinioClient(new HttpUrl.parse("https://play.min.io:9000"));

// 4. public MinioClient(String endpoint, String accessKey, String secretKey)
MinioClient minioClient = new MinioClient("https://play.min.io:9000", "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");

// 5. public MinioClient(String endpoint, int port,  String accessKey, String secretKey)
MinioClient minioClient = new MinioClient("https://play.min.io", 9000, "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");

// 6. public MinioClient(String endpoint, String accessKey, String secretKey, boolean insecure)
MinioClient minioClient = new MinioClient("https://play.min.io:9000", "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG", true);

// 7. public MinioClient(String endpoint, int port,  String accessKey, String secretKey, boolean insecure)
MinioClient minioClient = new MinioClient("https://play.min.io", 9000, "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG", true);

// 8. public MinioClient(okhttp3.HttpUrl url, String accessKey, String secretKey)
 MinioClient minioClient = new MinioClient(new URL("https://play.min.io:9000"), "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");

// 9. public MinioClient(URL url, String accessKey, String secretKey)
MinioClient minioClient = new MinioClient(HttpUrl.parse("https://play.min.io:9000"), "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");

// 10. public MinioClient(String endpoint, String accessKey, String secretKey, String region)
MinioClient minioClient = new MinioClient("https://play.min.io:9000", "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG", "us-east-1");

// 11. public MinioClient(String endpoint, int port, String accessKey, String secretKey, String region, boolean secure)
MinioClient minioClient = new MinioClient("play.min.io", 9000, "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG", "us-east-1", true);

// 12. public MinioClient(String endpoint, int port, String accessKey, String secretKey, String region, boolean secure, okhttp3.OkHttpClient httpClient)
MinioClient minioClient = new MinioClient("play.min.io", 9000, "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG", "us-east-1", true, customHttpClient);
```


### AWS S3


```java
// 1. public MinioClient(String endpoint)
MinioClient s3Client = new MinioClient("https://s3.amazonaws.com");

// 2. public MinioClient(URL url)
MinioClient minioClient = new MinioClient(new URL("https://s3.amazonaws.com"));

// 3. public MinioClient(okhttp3.HttpUrl url)
 MinioClient s3Client = new MinioClient(new HttpUrl.parse("https://s3.amazonaws.com"));

// 4. public MinioClient(String endpoint, String accessKey, String secretKey)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY");

// 5. public MinioClient(String endpoint, int port,  String accessKey, String secretKey)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", 80, "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY");

// 6. public MinioClient(String endpoint, String accessKey, String secretKey, boolean insecure)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY", false);

// 7. public MinioClient(String endpoint, int port,  String accessKey, String secretKey, boolean insecure)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", 80, "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY",false);

// 8. public MinioClient(okhttp3.HttpUrl url, String accessKey, String secretKey)
 MinioClient s3Client = new MinioClient(new URL("s3.amazonaws.com"), "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY");

// 9. public MinioClient(URL url, String accessKey, String secretKey)
MinioClient s3Client = new MinioClient(HttpUrl.parse("s3.amazonaws.com"), "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY");

// 10. public MinioClient(String endpoint, String accessKey, String secretKey, String region)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY", "YOUR-BUCKETREGION");

// 11. public MinioClient(String endpoint, int port, String accessKey, String secretKey, String region, boolean secure)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", 80, "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY", "YOUR-BUCKETREGION", false);

// 12. public MinioClient(String endpoint, int port, String accessKey, String secretKey, String region, boolean secure, okhttp3.OkHttpClient httpClient)
MinioClient s3Client = new MinioClient("s3.amazonaws.com", 80, "YOUR-ACCESSKEYID", "YOUR-SECRETACCESSKEY", "YOUR-BUCKETREGION", false, customHttpClient);
```

## 2. 存储桶操作

<a name="makeBucket"></a>
### makeBucket(String bucketName)
`public void makeBucket(String bucketName)`

用默认的区域（region）创建一个新的存储桶

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#makeBucket-java.lang.String-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_ |存储桶名称  |


| 返回值类型	  | 异常	  |
|:--- |:--- |
| ``None``  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 非法的存储桶名称。 |
|        |  ``RegionConflictException`` : 在通过区域时与之前指定的冲突。. |
|        | ``NoSuchAlgorithmException`` : 在签名计算期间没有发现所请求的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常           |
|        | ``InvalidKeyException`` : 无效的访问密钥或密钥。           |
|        | ``NoResponseException`` : 服务器无响应。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败。            |
|        | ``InternalException`` : 内部异常。       |


__示例__


```java
try {
  // 如存储桶不存在，创建之。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    System.out.println("mybucket already exists");
  } else {
    // 创建名为'my-bucketname'的存储桶。
    minioClient.makeBucket("mybucket");
    System.out.println("mybucket is created successfully");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="makeBucket"></a>
### makeBucket(String bucketName, String region)
`public void makeBucket(String bucketName, String region)`

用给定的区域创建对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#makeBucket-java.lang.String-java.lang.String-)

__参数__

| 参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_ | 存储桶名称。  |
| ``region``  | _String_ | 创建存储桶的区域.  |


| 返回类型	  | 异常	  |
|:--- |:--- |
| ``None``  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 非法的存储桶名称。 |
|        |  ``RegionConflictException`` : 在通过区域时与之前指定的冲突。. |
|        | ``NoSuchAlgorithmException`` : 在签名计算期间没有发现所请求的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常           |
|        | ``InvalidKeyException`` : 无效的访问密钥或密钥。           |
|        | ``NoResponseException`` : 服务器无响应。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败。            |
|        | ``InternalException`` : 内部异常。       |



__示例__


```java
try {
  // 如果存储桶不存在，则创建存储桶。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    System.out.println("mybucket already exists");
  } else {
    // 创建存储桶'my-bucketname'。
    minioClient.makeBucket("mybucket","us-east-1");
    System.out.println("mybucket is created successfully");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="listBuckets"></a>
### listBuckets()

`public List<Bucket> listBuckets()`

列出所有存储桶。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listBuckets--)

|返回值类型	  | 异常	  |
|:--- |:--- |
| ``List Bucket``  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 非法的存储桶名称。 |
|        |  ``RegionConflictException`` : 在通过区域时与之前指定的冲突。. |
|        | ``NoSuchAlgorithmException`` : 在签名计算期间没有发现所请求的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取给定长度之前就得到一个EOFException。 | 
|        | ``IOException`` : 连接异常           |
|        | ``InvalidKeyException`` : 无效的访问密钥或密钥。           |
|        | ``NoResponseException`` : 服务器无响应。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败。            |
|        | ``InternalException`` : 内部异常。       |


__示例__


```java
try {
  // 列出所有存储桶
  List<Bucket> bucketList = minioClient.listBuckets();
  for (Bucket bucket : bucketList) {
    System.out.println(bucket.creationDate() + ", " + bucket.name());
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="bucketExists"></a>
### bucketExists(String bucketName)

`public boolean bucketExists(String bucketName)`

检查存储桶是否存在。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#bucketExists-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称  |


|返回值类型	  | 异常	  |
|:--- |:--- |
| ``bolean``  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 非法的存储桶名称。 |
|        |  ``RegionConflictException`` : 在通过区域时与之前指定的冲突。. |
|        | ``NoSuchAlgorithmException`` : 在签名计算期间没有发现所请求的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 | 
|        | ``IOException`` : 连接异常           |
|        | ``InvalidKeyException`` : 无效的访问密钥或密钥。           |
|        | ``NoResponseException`` : 服务器无响应。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败。            |
|        | ``InternalException`` : 内部异常。       |



__示例__


```java
try {
  // 检查'my-bucketname'是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    System.out.println("mybucket exists");
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="removeBucket"></a>
### removeBucket(String bucketName)

`public void removeBucket(String bucketName)`

删除一个存储桶。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#removeBucket-java.lang.String-)

注意: -  removeBucket不会删除存储桶里的对象，你需要通过removeObject API来删除它们。


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |


|返回值类型	  | 异常	  |
|:--- |:--- |
| None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 非法的存储桶名称。 |
|        |  ``RegionConflictException`` : 在通过区域时与之前指定的冲突。. |
|        | ``NoSuchAlgorithmException`` : 在签名计算期间没有发现所请求的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 | 
|        | ``IOException`` : 连接异常           |
|        | ``InvalidKeyException`` : 无效的访问密钥或密钥。           |
|        | ``NoResponseException`` : 服务器无响应。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败。            |
|        | ``InternalException`` : 内部异常。       |

__示例__


```java
try {
  // 删除之前先检查`my-bucket`是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 删除`my-bucketname`存储桶，注意，只有存储桶为空时才能删除成功。
    minioClient.removeBucket("mybucket");
    System.out.println("mybucket is removed successfully");
  } else {
    System.out.println("mybucket does not exist");
  }
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="listObjects"></a>
### listObjects(String bucketName)

`public Iterable<Result<Item>> listObjects(String bucketName)`

列出给定存储桶中的所有对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listObjects-java.lang.String-java.lang.String-boolean-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |


|返回值类型	  | 异常   |
|:--- |:--- |
| ``Iterable<Result<Item>>``: 结果项的迭代器.  | _None_  |


__示例__


```java
try {
  // 检查'mybucket'是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 列出'my-bucketname'里的对象
    Iterable<Result<Item>> myObjects = minioClient.listObjects("mybucket");
    for (Result<Item> result : myObjects) {
      Item item = result.get();
      System.out.println(item.lastModified() + ", " + item.size() + ", " + item.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```
<a name="listObjects"></a>
### listObjects(String bucketName, String prefix)

`public Iterable<Result<Item>> listObjects(String bucketName, String prefix))`

列举给定存储桶和前缀的对象信息。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listObjects-java.lang.String-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``prefix``  | _String_  | 前缀字符串。列举以``prefix``开始的名字的对象。 |

|返回类型	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<Item>>``: 结果项的迭代器.  | _None_  |


__示例__


```java
try {
  // 检查存储桶是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 列举'my-bucketname'的对象'
    Iterable<Result<Item>> myObjects = minioClient.listObjects("mybucket","minio");
    for (Result<Item> result : myObjects) {
      Item item = result.get();
      System.out.println(item.lastModified() + ", " + item.size() + ", " + item.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="listObjects"></a>
### listObjects(String bucketName, String prefix, boolean recursive)

`public Iterable<Result<Item>> listObjects(String bucketName, String prefix, boolean recursive)`

列举
按给定存储桶，前缀和递归标志中的Iterable<Result><Item>的方式列举对象信息。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listObjects-java.lang.String-java.lang.String-boolean-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶的名字。  |
| ``prefix``  | _String_  | 前缀字符串。列举以``prefix``开始的名字的对象。|
| ``recursive``  | _boolean_  | 当为假时，则仿照一个目录结构，其中返回的每个列表都是直到第一个“/”为止的完整对象或对象键的一部分。直到第一个"/"为止的具有相同前缀的所有对象将合并为一个条目。|


|返回类型	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<Item>>``: 结果项的迭代器。  | _None_  |


__示例__


```java
try {
  // 检查存储桶是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 列举'my-bucketname'中的对象。
    Iterable<Result<Item>> myObjects = minioClient.listObjects("mybucket","minio",true);
    for (Result<Item> result : myObjects) {
      Item item = result.get();
      System.out.println(item.lastModified() + ", " + item.size() + ", " + item.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```



<a name="listObjects"></a>
### listObjects(String bucketName, String prefix, boolean recursive, boolean useVersion1)

`public Iterable<Result<Item>> listObjects(String bucketName, String prefix, boolean recursive, boolean useVersion1)`

列出某个存储桶中的所有对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listObjects-java.lang.String-java.lang.String-boolean-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶的名字。  |
| ``prefix``  | _String_  | 前缀字符串。列举以``prefix``开始的名字的对象。|
| ``recursive``  | _boolean_  | 当为假时，则仿照一个目录结构，其中返回的每个列表都是直到第一个“/”为止的完整对象或对象键的一部分。直到第一个"/"为止的具有相同前缀的所有对象将合并为一个条目。|
| ``useVersion1``  | _boolean_  | 当为真时，将使用V1版本的REST API。|


|返回类型	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<Item>>``: 结果项的迭代器。 | _None_  |


__示例__


```java
try {
  // 检查'mybucket'是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 列举'my-bucket'的所有对象。
    Iterable<Result<Item>> myObjects = minioClient.listObjects("mybucket");
    for (Result<Item> result : myObjects) {
      Item item = result.get();
      System.out.println(item.lastModified() + ", " + item.size() + ", " + item.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="setBucketLifeCycle"></a>
### setBucketPolicy(String bucketName, String lifeCycle)
`public void setBucketPolicy(String bucketName, String lifeCycle)`

为某个存储桶设置生命周期。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#setBucketLifeCycle-java.lang.String-java.lang.String-)

__参数__

|参数   | 类型   | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``lifeCycle`` | _String_ | 存储桶的生命周期XML |



| 返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间找不到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常.            |
|        | ``InvalidKeyException`` : 不合法的访问密钥（access key）和密钥（secret key）|
|        | ``NoResponseException`` : 服务器无响应。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部异常。    |
|        | ``InvalidArgumentException`` : 方法传递值非法。  |





__示例__


```java
try {
    /* Amazon S3: */
  MinioClient minioClient = new MinioClient("https://s3.amazonaws.com", "YOUR-ACCESSKEYID",
                                          "YOUR-SECRETACCESSKEY");
  String lifeCycle = "<LifecycleConfiguration><Rule><ID>expire-bucket</ID><Prefix></Prefix>"
                + "<Status>Enabled</Status><Expiration><Days>365</Days></Expiration>"
                + "</Rule></LifecycleConfiguration>";


  minioClient.setBucketLifecycle("lifecycleminiotest", lifeCycle);
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getBucketLifeCycle"></a>
### getBucketLifeCycle(String bucketName)
`public String getBucketLifeCycle(String bucketName)`

得到存储桶的生命周期。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getBucketLifeCycle-java.lang.String-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶的名字。  |

|返回类型	  | 异常	  |
|:--- |:--- |
|  None  | Listed 异常: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 在计算签名期间得不到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : C      |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析相应的XML异常。           |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。       |

__示例__


```java

try {
   /* Amazon S3: */
   MinioClient minioClient = new MinioClient("https://s3.amazonaws.com", "YOUR-ACCESSKEYID",
            "YOUR-SECRETACCESSKEY");
   String lifecycle = minioClient.getBucketLifecycle("my-bucketName" );
   System.out.println(" Life Cycle is : " + lifecycle );
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="deleteBucketLifeCycle"></a>
### deleteBucketLifeCycle(String bucketName)
`private void deleteBucketLifeCycle(String bucketName)`

删除存储桶的生命周期。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#deleteBucketLifeCycle-java.lang.String-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶的名称。  |

|返回类型	  | 异常	  |
|:--- |:--- |
|  None  | Listed 异常: |
|        |  ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行异常。            |
|        | ``InternalException`` : 内部异常。        |

__示例__


```java

try {
   /* Amazon S3: */
   MinioClient minioClient = new MinioClient("https://s3.amazonaws.com", "YOUR-ACCESSKEYID",
            "YOUR-SECRETACCESSKEY");
   minioClient.deleteBucketLifeCycle("my-bucketName" );
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="listenBucketNotification"></a>
### listenBucketNotification(String bucketName, String prefix, String suffix, String[] events, BucketEventListener listener)
`public void listenBucketNotification(String bucketName, String prefix, String suffix, String[] events, BucketEventListener listener)`

监听在特定存储桶下与对象相关的事件。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listenBucketNotification-java.lang.String-java.lang.String-java.lang.String-java.lang.String:A-io.minio.BucketEventListener-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``prefix`` | _String_ | 只监听包含给定前缀的对象。|
| ``suffix`` | _String_ | 只包含给定后缀的对象。 |
| ``events`` | _String[]_ | 只监听指定的事件，例如s3:ObjectCreated:*, s3:ObjectAccessed:*, s3:ObjectRemoved:*, ..  |
| ``listener`` | _BucketEventListener_ | 拥有updateEvent方法的接口。 |

| 返回类型	  | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行异常。            |
|        | ``InternalException`` : 内部异常。        |


__示例__


```java
  try {
    class TestBucketListener implements BucketEventListener {
      @Override
      public void updateEvent(NotificationInfo info) {
        System.out.println(info.records[0].s3.bucket.name + "/"
           + info.records[0].s3.object.key + " has been created");
      }
    }

    minioClient.listenBucketNotification("testbucket", "", "",
        new String[]{"s3:ObjectCreated:*", "s3:ObjectAccessed:*"}, new TestBucketListener());
  } catch (Exception e) {
    System.out.println("Error occurred: " + e);
  }
  ```

  <a name="setBucketNotification"></a>
### setBucketNotification(String bucketName, NotificationConfiguration notificationConfiguration)
`public void setBucketNotification(String bucketName, NotificationConfiguration notificationConfiguration)`

设置存储桶通知配置。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#setBucketNotification-java.lang.String-io.minio.messages.NotificationConfiguration-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``notificationConfiguration`` | _NotificationConfiguration_ | 待设置的通知配置。 |

|返回类型	  | 异常	  |
|:--- |:--- |
|  None  | Listed 异常: |
|        | ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``InvalidObjectPrefixException`` : 对象前缀非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` :  给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行异常。            |
|        | ``InternalException`` : 内部异常。        |


__示例__


```java
 try {
      NotificationConfiguration notificationConfiguration = minioClient.getBucketNotification("my-bucketname");

      // 添加一个新的SQS配置。
      List<QueueConfiguration> queueConfigurationList = notificationConfiguration.queueConfigurationList();
      QueueConfiguration queueConfiguration = new QueueConfiguration();
      queueConfiguration.setQueue("arn:minio:sqs::1:webhook");

      List<EventType> eventList = new LinkedList<>();
      eventList.add(EventType.OBJECT_CREATED_PUT);
      eventList.add(EventType.OBJECT_CREATED_COPY);
      queueConfiguration.setEvents(eventList);

      Filter filter = new Filter();
      filter.setPrefixRule("images");
      filter.setSuffixRule("pg");
      queueConfiguration.setFilter(filter);

      queueConfigurationList.add(queueConfiguration);
      notificationConfiguration.setQueueConfigurationList(queueConfigurationList);

      // 设置更新的通知配置。
      minioClient.setBucketNotification("my-bucketname", notificationConfiguration);
      System.out.println("Bucket notification is set successfully");
    } catch (MinioException e) {
      System.out.println("Error occurred: " + e);
    }
```

  <a name="getBucketNotification"></a>
### getBucketNotification(String bucketName)
`public NotificationConfiguration getBucketNotification(String bucketName)`

获得存储桶通知配置。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getBucketNotification-java.lang.String-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |

|返回类型	  | 异常	  |
|:--- |:--- |
|  ``NotificationConfiguration``:  通知配置    | 异常列表: |
|        | ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``InvalidObjectPrefixException`` : 对象前缀非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` :  给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行异常。            |
|        | ``InternalException`` : 内部异常。        |


__示例__


```java
 try {
      /* play.min.io for test and development. */
      MinioClient minioClient = new MinioClient("https://play.min.io:9000", "Q3AM3UQ867SPQQA43P2F",
                                                "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");
      NotificationConfiguration notificationConfiguration = minioClient.getBucketNotification("my-bucketname");
      System.out.println(notificationConfiguration);
    } catch (MinioException e) {
      System.out.println("Error occurred: " + e);
    }
```



<a name="listIncompleteUploads"></a>
###  listIncompleteUploads(String bucketName)

`public Iterable<Result<Upload>>  listIncompleteUploads(String bucketName)`

列举存储桶中部分上传的对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listIncompleteUploads-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |


|返回类型	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<Upload>>``: 上传的迭代器  | _None_  |


__示例__


```java
try {
  // 检查'mybucket'是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 列举'my-bucketname'中的所有未完成的对象多部分上传。
    Iterable<Result<Upload>> myObjects = minioClient.listIncompleteUploads("mybucket");
    for (Result<Upload> result : myObjects) {
      Upload upload = result.get();
      System.out.println(upload.uploadId() + ", " + upload.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="listIncompleteUploads"></a>
###  listIncompleteUploads(String bucketName, String prefix)

`public Iterable<Result<Upload>>  listIncompleteUploads(String bucketName, String prefix)`

列举给定存储桶和前缀对象的未完成上传。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listIncompleteUploads-java.lang.String-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``prefix``  | _String_  | 前缀字符串。列举名字以``prefix``开始的对象。|


|返回类型	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<Upload>>``: 上传的迭代器。  | _None_  |


__示例__


```java
try {
  // Check whether 'mybucket' exist or not.
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // List all incomplete multipart upload of objects in 'my-bucketname
    Iterable<Result<Upload>> myObjects = minioClient.listIncompleteUploads("mybucket", "minio");
    for (Result<Upload> result : myObjects) {
      Upload upload = result.get();
      System.out.println(upload.uploadId() + ", " + upload.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="listIncompleteUploads"></a>
### listIncompleteUploads(String bucketName, String prefix, boolean recursive)

`public Iterable<Result<Upload>> listIncompleteUploads(String bucketName, String prefix, boolean recursive)`

列举存储桶中部分上传的对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#listIncompleteUploads-java.lang.String-java.lang.String-boolean-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``prefix``  | _String_  | 前缀字符串。列举名字以``prefix``开头的对象。 |
| ``recursive``  | _boolean_  | 当为假时，则仿照一个目录结构，其中返回的每个列表都是直到第一个“/”为止的完整对象或对象键的一部分。直到第一个"/"为止的具有相同前缀的所有对象将合并为一个条目。 |


|返回类型	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<Upload>>``: 上传的迭代器。  | _None_  |


__示例__


```java
try {
  // 检查'mybucket'是否存在。
  boolean found = minioClient.bucketExists("mybucket");
  if (found) {
    // 列举在'my-bucketname'中所有未完成的对象的多部分上传。
    Iterable<Result<Upload>> myObjects = minioClient.listIncompleteUploads("mybucket", "minio", true);
    for (Result<Upload> result : myObjects) {
      Upload upload = result.get();
      System.out.println(upload.uploadId() + ", " + upload.objectName());
    }
  } else {
    System.out.println("mybucket does not exist");
  }
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getBucketPolicy"></a>
### getBucketPolicy(String bucketName)
`public PolicyType getBucketPolicy(String bucketName)`

获得某个存储桶的存储桶通知策略。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getBucketPolicy-java.lang.String-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |


|返回类型	  | 异常	  |
|:--- |:--- |
|  _String_: Bucket policy JSON string. | Listed 异常: |
|        |  ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``InvalidObjectPrefixException`` : 对象前缀非法。        |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行异常。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidBucketNameException `` : 存储桶名称非法。       |
|        | ``BucketPolicyTooLargeException `` : 存储桶策略的大小过大。       |

__示例__


```java
try {
  System.out.println("Current policy: " + minioClient.getBucketPolicy("myBucket"));
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="setBucketPolicy"></a>
### setBucketPolicy(String bucketName, String policy)
`public void setBucketPolicy(String bucketName, String policy)`

设置存储桶的策略。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#setBucketPolicy-java.lang.String-java.lang.String-)

__参数__

|参数   | 类型  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``policy`` | _String_ | 存储桶策略的JSON文件。 |

|返回类型	  | 异常	  |
|:--- |:--- |
|  None  | Listed 异常: |
|        |  ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``InvalidObjectPrefixException`` : 对象前缀非法。        |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行异常。            |
|        | ``InternalException`` : 内部异常。        |

__示例__


```java
try {
  StringBuilder builder = new StringBuilder();
  builder.append("{\n");
  builder.append("    \"Statement\": [\n");
  builder.append("        {\n");
  builder.append("            \"Action\": [\n");
  builder.append("                \"s3:GetBucketLocation\",\n");
  builder.append("                \"s3:ListBucket\"\n");
  builder.append("            ],\n");
  builder.append("            \"Effect\": \"Allow\",\n");
  builder.append("            \"Principal\": \"*\",\n");
  builder.append("            \"Resource\": \"arn:aws:s3:::my-bucketname\"\n");
  builder.append("        },\n");
  builder.append("        {\n");
  builder.append("            \"Action\": \"s3:GetObject\",\n");
  builder.append("            \"Effect\": \"Allow\",\n");
  builder.append("            \"Principal\": \"*\",\n");
  builder.append("            \"Resource\": \"arn:aws:s3:::my-bucketname/myobject*\"\n");
  builder.append("        }\n");
  builder.append("    ],\n");
  builder.append("    \"Version\": \"2012-10-17\"\n");
  builder.append("}\n");
  minioClient.setBucketPolicy("my-bucketname", builder.toString());
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```






## 3. 对象操作

<a name="getObject"></a>
### getObject(String bucketName, String objectName)

`public InputStream getObject(String bucketName, String objectName)`

以流的形式下载一个对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getObject-java.lang.String-java.lang.String-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_ | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |


| 返回值类型	  | 异常   |
|:--- |:--- |
|  ``InputStream``: 包含对象数据的输入流。  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |



__示例__


```java
try {
  // 调用statObject()来判断对象是否存在。
  // 如果不存在, statObject()抛出异常,
  // 否则则代表对象存在。
  // 运行成功。
  minioClient.statObject("mybucket", "myobject");

  // 从"my-bucketname"中获取输入流以获得"my-objectname"的对象。
  InputStream stream = minioClient.getObject("mybucket", "myobject");

  // 读取输入流直到EOF并打印到控制台。
  byte[] buf = new byte[16384];
  int bytesRead;
  while ((bytesRead = stream.read(buf, 0, buf.length)) >= 0) {
    System.out.println(new String(buf, 0, bytesRead));
  }

  // 关闭流。
  stream.close();
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getObject"></a>
### getObject(String bucketName, String objectName, long offset)

`public InputStream getObject(String bucketName, String objectName, long offset)`

从给定偏移处开始读取对象数据，作为给定存储桶的输入流。输入流在使用后必须关闭，否则连接将保持打开状态。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getObject-java.lang.String-java.lang.String-long-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |
| ``offset``  | _Long_  | ``offset`` 是起始字节的位置 |



| 返回值类型	  | 异常   |
|:--- |:--- |
|  ``InputStream`` : 包含对象数据的输入流。 | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |


__示例__


```java
try {

  // 调用statObject()来判断对象是否存在。
  // 如果不存在, statObject()抛出异常,
  // 否则则代表对象存在。
  // 运行成功。
  minioClient.statObject("mybucket", "myobject");

  // Get input stream to have content of 'my-objectname' from 'my-bucketname'
  InputStream stream = minioClient.getObject("mybucket", "myobject", 1024L, 4096L);

  // 读取输入流直到EOF并打印到控制台。
  byte[] buf = new byte[16384];
  int bytesRead;
  while ((bytesRead = stream.read(buf, 0, buf.length)) >= 0) {
    System.out.println(new String(buf, 0, bytesRead));
  }

  // 关闭流。
  stream.close();
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getObject"></a>
### getObject(String bucketName, String objectName, long offset, Long length)

`public InputStream getObject(String bucketName,  String objectName, long offset, Long length)`

以流的形式下载对象指定范围的byte。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getObject-java.lang.String-java.lang.String-long-java.lang.Long-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |
| ``offset``  | _Long_  | ``offset`` 是起始字节的位置。 |
| ``length``  | _Long_  | 将要在流中读取对象的``length``(可选，如果没有指定，将从偏移量处读取文件剩余的部分)。|



| 返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |

__示例__

```java
try {
  // 调用statObject()来判断对象是否存在。
  // 如果不存在, statObject()抛出异常,
  // 否则则代表对象存在。
  // 运行成功。
  minioClient.statObject("mybucket", "myobject");

  // 从"my-bucketname"获取输入流以获得"my-objectname"的内容。
  InputStream stream = minioClient.getObject("mybucket", "myobject", 1024L, 4096L);

  // 读取输入流直到EOF并打印到控制台。
  byte[] buf = new byte[16384];
  int bytesRead;
  while ((bytesRead = stream.read(buf, 0, buf.length)) >= 0) {
    System.out.println(new String(buf, 0, bytesRead));
  }

  // 关闭输入流。
  stream.close();
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getObject"></a>
### getObject(String bucketName, String objectName, String fileName)

`public void getObject(String bucketName, String objectName, String fileName)`

将对象按照文件下载并保存到当地文件系统。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getObject-java.lang.String-java.lang.String-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |
| ``fileName``  | _String_  | 文件名称。 |


| 返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |
|        | ``InvalidAlgorithmParameterException`` : 该算法不存在 |

__示例__

```java
try {
 // 用statObject()检查对象是否存在。
  // 如果没有找到对象，statObject()抛出一个异常，
  // 否则意味着对象存在。
  // 运行成功。
  minioClient.statObject("mybucket", "myobject");

  // 获得对象的数据并把它存储在photo.jpg中。
  minioClient.getObject("mybucket", "myobject", "photo.jpg");

} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getObject"></a>
### getObject(String bucketName, String objectName, ServerSideEncryption sse)

`public InputStream getObject(String bucketName, String objectName, ServerSideEncryption sse)`

按输入流读取给定存储桶的全部对象数据。输入流在使用后必须关闭，否则连接将一直保持开启状态。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getObject-java.lang.String-java.lang.String-io.minio.ServerSideEncryption-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |

| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名称非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。  |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |

__示例__

```java
try {
 // 用statObject()检查对象是否存在。
  // 如果没有找到对象，statObject()抛出一个异常。
  // 否则意味着对象存在。
  // 运行成功。
  minioClient.statObject("mybucket", "myobject");

   InputStream stream = minioClient.getObject("my-bucketname", "my-objectname", sse);
   byte[] buf = new byte[16384];
   int bytesRead;
   while ((bytesRead = stream.read(buf, 0, buf.length)) >= 0) {
   System.out.println(new String(buf, 0, bytesRead));
   }
   stream.close();
} catch (MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="putObject"></a>
### putObject(String bucketName, String objectName, String fileName, String contentType)

`public void putObject(String bucketName, String objectName, String fileName, String contentType)`
将给定存储桶中的给定文件作为对象进行上传。
如果对象大于5MB，客户端将会自动使用多部分的会话。
如果多会话失败，上传的部分将会自动中止。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-long-java.lang.String-)


__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |
| ``fileName``  | _String_  | 上传的文件名字。 |
| ``contentType``  | _String_ | 内容类型。 |


| 返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |


__示例__



```java
try {
  minioClient.putObject("mybucket",  "island.jpg", "/mnt/photos/island.jpg" ,"application/octet-stream")
  System.out.println("island.jpg is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="putObject"></a>
### putObject(String bucketName, String objectName, InputStream stream, String contentType)

`public void putObject(String bucketName, String objectName, InputStream stream, String contentType)`

将给定流中的数据作为对象上传到流大小未知的存储桶中。如果流有多于525MiB的数据，客户端将自动使用一个多部分的会话。

如果多会话失败了，上传的部分会自动中止。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-java.lang.String-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  |  上传的流。 |
| ``contentType``  | _String_ | 流内容的类型。 |

| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

```java
 StringBuilder builder = new StringBuilder();
 for (int i = 0; i < 1000; i++) {
   builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
   builder.append("(29 letters)\n");
   builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
   builder.append("(31 letters)\n");
   builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
   builder.append("NASAs Space Shuttle. (32 letters)\n");
   builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
   builder.append("(39 letters)\n");
   builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
   builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
   builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
   builder.append("computers after System 7.\n");
   builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
   builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
   builder.append("---\n");
 }
 ByteArrayInputStream bais = new ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
// 创建对象
 minioClient.putObject("my-bucketname", "my-objectname", bais, "application/octet-stream");
 bais.close();
 System.out.println("my-objectname is uploaded successfully");
```


<a name="putObject"></a>
### putObject(String bucketName, String objectName, InputStream stream, long size, String contentType)

`public void putObject(String bucketName, String objectName, InputStream stream, long size, String contentType)`

从输入流中上传对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-long-java.lang.String-)



__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  |  上传的流。 |
| ``size``  | _long_  | 从``stream``中读取的将上传的数据大小。 |
| ``contentType``  | _String_ | 流内容的类型。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |


__示例__

单个对象的最大大小被限制在5TB。putObject透明地上传在多部分中大于5MiB的对象。

```java
try {
  StringBuilder builder = new StringBuilder();
  for (int i = 0; i < 1000; i++) {
    builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
    builder.append("(29 letters)\n");
    builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
    builder.append("(31 letters)\n");
    builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
    builder.append("NASAs Space Shuttle. (32 letters)\n");
    builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
    builder.append("(39 letters)\n");
    builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
    builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
    builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
    builder.append("computers after System 7.\n");
    builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
    builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
    builder.append("- --\n");
  }
  ByteArrayInputStream bais = new
  ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
  // 创建一个对象。
  minioClient.putObject("mybucket", "myobject", bais, bais.available(), "application/octet-stream");
  bais.close();
  System.out.println("myobject is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="putObject"></a>
### putObject(String bucketName, String objectName, String fileName)

`public void putObject(String bucketName, String objectName, String fileName)`

将一个文件中的内容上传到objectName中。
[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.lang.String-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |
| ``fileName``  | _String_  | 文件名称。 |


| 返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |


__示例__

单个对象的最大大小被限制在5TB。putObject透明地上传在多部分中大于5MiB的对象。被上传的对象将会被仔细的用MDSSUM签名校验。


```java
try {
  minioClient.putObject("mybucket",  "island.jpg", "/mnt/photos/island.jpg")
  System.out.println("island.jpg is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="putObject"></a>
### putObject(String bucketName, String objectName, InputStream stream, long size, ServerSideEncryption sse)

`public void putObject(String bucketName, String objectName, InputStream stream, long size, ServerSideEncryption sse)`


将给定流中的数据作为对象上传到流大小未知的存储桶中。如果流有多于525MiB的数据，客户端将自动使用一个多部分的会话。

如果多会话失败了，上传的部分会被自动中止。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-long-io.minio.ServerSideEncryption-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |
| ``stream``  | _InputStream_  | 要上传的流。 |
| ``size``  | _long_  | 从``stream``中读取的将上传的数据大小。 |
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |

| 返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。            |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |
| 		 | ``InvalidAlgorithmParameterException`` : 错误的加密算法。 |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |



__示例__


```java
StringBuilder builder = new StringBuilder();
 for (int i = 0; i < 1000; i++) {
   builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
   builder.append("(29 letters)\n");
   builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
   builder.append("(31 letters)\n");
   builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
   builder.append("NASAs Space Shuttle. (32 letters)\n");
   builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
   builder.append("(39 letters)\n");
   builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
   builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
   builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
   builder.append("computers after System 7.\n");
   builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
   builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
   builder.append("---\n");
 }
 ByteArrayInputStream bais = new ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
 // 创建对象。
 minioClient.putObject("my-bucketname", "my-objectname", bais, "application/octet-stream");
 bais.close();
 System.out.println("my-objectname is uploaded successfully");
```

<a name="putObject"></a>
### putObject(String bucketName, String objectName, InputStream stream, Map<String,String> headerMap)

`public void putObject(String bucketName, String objectName, InputStream stream, long size, Map<String,String> headerMap)`

将给定流中的数据作为对象上传到具有指定元数据的给定存储桶中。
如果对象大于5MB，客户端将会自动使用多部分的会话。

如果会话失败了，用户会尝试着通过再次创建完全相同的对象来重传对象。客户端将会自动检查所有当前上传会话的所有部分并尝试着重用这个会话。如果发现不匹配，在上传更多数据前将中止上传。否则，将会在会话退出的部分恢复上传。

如果多会话失败，用户需要恢复或删除这个会话。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.io.InputStream-long-java.util.Map-)


__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  | 上传的流。 |
| ``headerMap``  | _Map<String,String>_  | 个性化/另外的对象元数据。|


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__

```java
 StringBuilder builder = new StringBuilder();
 for (int i = 0; i < 1000; i++) {
   builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
   builder.append("(29 letters)\n");
   builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
   builder.append("(31 letters)\n");
   builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
   builder.append("NASAs Space Shuttle. (32 letters)\n");
   builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
   builder.append("(39 letters)\n");
   builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
   builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
   builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
   builder.append("computers after System 7.\n");
   builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
   builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
   builder.append("---\n");
 }
 ByteArrayInputStream bais = new ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
// 创建对象
 Map<String, String> headerMap = new HashMap<>();
 headerMap.put("Content-Type", "application/octet-stream");
 minioClient.putObject("my-bucketname", "my-objectname", bais, headerMap);
 bais.close();
 System.out.println("my-objectname is uploaded successfully");
```

<a name="putObject"></a>
### putObject(String bucketName, String objectName, InputStream stream, long size, Map<String,String> headerMap)

`public void putObject(String bucketName, String objectName, InputStream stream, long size, Map<String,String> headerMap)`

将给定流中的数据作为对象上传到流大小未知的存储桶中。
如果流有多于525MiB的数据，客户端将自动使用一个多部分的会话。

如果多会话失败了，上传的部分会被自动中止。


[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-long-java.util.Map-)


__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  | 上传的流。 |
| ``size``  | _long_  | 从``stream``中读取的将上传的数据大小。 |
| ``headerMap``  | _Map<String,String>_  | 个性化/另外的对象元数据。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__

```java
 StringBuilder builder = new StringBuilder();
 for (int i = 0; i < 1000; i++) {
   builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
   builder.append("(29 letters)\n");
   builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
   builder.append("(31 letters)\n");
   builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
   builder.append("NASAs Space Shuttle. (32 letters)\n");
   builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
   builder.append("(39 letters)\n");
   builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
   builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
   builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
   builder.append("computers after System 7.\n");
   builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
   builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
   builder.append("---\n");
 }
 ByteArrayInputStream bais = new ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
 // 创建对象
 Map<String, String> headerMap = new HashMap<>();
 headerMap.put("Content-Type", "application/octet-stream");
 minioClient.putObject("my-bucketname", "my-objectname", bais, bais.available(), headerMap);
 bais.close();
 System.out.println("my-objectname is uploaded successfully");
```

<a name="putObject"></a>

### putObject(String bucketName, String objectName, InputStream stream, long size, Map<String, String> headerMap, SecretKey key)

 `public void putObject(String bucketName, String objectName, InputStream stream, long size, Map<String, String> headerMap,
		  SecretKey key)`
 
 
 从给定的流中获取数据，使用一个随机的密钥加密并将其作为对象上传到给帝国的存储桶中。同样，也要上传加密的内容密钥和iv作为加密对象的头。内容密钥使用传递给函数的master密钥进行加密。
 
 任何个性化或额外的元数据也可以同故宫`headerMap`提供。
 如果对象大于5MB，客户端将会自动执行多部分上传。

 MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-long-java.lang.String-javax.crypto.SecretKey-)

__参数__

 |参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  | 上传的流。 |
| ``size``  | _long_  | 从``stream``中读取的将上传的数据大小。 |
| ``headerMap``  | Map<String, String> | 个性化/另外的对象元数据。 |
| ``key``  | _SecretKey_ | An object of type initialized with AES [SecretKey](https://docs.oracle.com/javase/7/docs/api/javax/crypto/SecretKey.html).  |
 | 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
| 		 | ``InvalidAlgorithmParameterException`` : 使用错误的加密算法。 |
|		 | ``BadPaddingException`` :块元素中的错误padding。 |
|		 | ``IllegalBlockSizeException`` :错误的块元素。 |
|		 | ``NoSuchPaddingException`` :指定错误的padding类型。 |

__示例__

 对象用一种随机生成的数据加密密钥进行加密。数据加密密钥使用只被客户端所知的master密钥进行加密（包装在encryptionMaterials对象中）。加密的数据密钥作为对象头与IV和加密的对象一起被上传到远程服务器中。

 ```java
try {
  StringBuilder builder = new StringBuilder();
  for (int i = 0; i < 1000; i++) {
    builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
    builder.append("(29 letters)\n");
    builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
    builder.append("(31 letters)\n");
    builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
    builder.append("NASAs Space Shuttle. (32 letters)\n");
    builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
    builder.append("(39 letters)\n");
    builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
    builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
    builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
    builder.append("computers after System 7.\n");
    builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
    builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
    builder.append("- --\n");
  }
  ByteArrayInputStream bais = new
  ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
  
  // 创建对象
  Map<String, String> headerMap = new HashMap<>();
  headerMap.put("Content-Type", "application/octet-stream");
  headerMap.put("X-Amz-Meta-Key", "meta-data");
  
  //生成对称的256比特的AES密钥。
  KeyGenerator symKeyGenerator = KeyGenerator.getInstance("AES");
  symKeyGenerator.init(256);
  SecretKey symKey = symKeyGenerator.generateKey();
  
  // 创建一个对象。
  minioClient.putObject("mybucket", "myobject", bais, bais.available(), headerMap, symKey);
  bais.close();
  System.out.println("myobject is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="getObject"></a>
### getObject(String bucketName, String objectName, ServerSideEncryption sse, String fileName)

`public void getObject(String bucketName, String objectName, ServerSideEncryption sse, String fileName)`

将一个加密的objectName下载内容到一个给定的文件。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#getObject-java.lang.String-java.lang.String-io.minio.ServerSideEncryption-java.lang.String-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html)。|
| ``fileName``  | _String_  | 下载存入的文件名字。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法的传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__


```java
try {
  KeyGenerator keyGen = KeyGenerator.getInstance("AES");
  keyGen.init(256);
  ServerSideEncryption sse = ServerSideEncryption.withCustomerKey(keyGen.generateKey());
  minioClient.putObject("mybucket",  "island.jpg", sse, "/mnt/photos/island.jpg")
  System.out.println("island.jpg is uploaded successfully");
  minioClient.getObject("mybucket",  "island.jpg", sse, "/mnt/photos/islandCopy.jpg")
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="putObject"></a>
### putObject(String bucketName, String objectName, ServerSideEncryption sse, String fileName)

`public void putObject(String bucketName, String objectName, ServerSideEncryption sse, String fileName)`

将一个文件中内容上传到objectName中并用sse密钥加密。
[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-io.minio.ServerSideEncryption-java.lang.String-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |
| ``fileName``  | _String_  | 文件名称。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__


```java
try {
  KeyGenerator keyGen = KeyGenerator.getInstance("AES");
  keyGen.init(256);
  ServerSideEncryption sse = ServerSideEncryption.withCustomerKey(keyGen.generateKey());
  minioClient.putObject("mybucket",  "island.jpg", sse, "/mnt/photos/island.jpg")
  System.out.println("island.jpg is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="putObject"></a>
### putObject(String bucketName, String objectName, InputStream stream, Map<String,String> headerMap, ServerSideEncryption sse)

`public void putObject(String bucketName, String objectName, InputStream stream, Map<String,String> headerMap, ServerSideEncryption sse)`
将给定流中的数据作为对象上传到具有指定元数据的给定存储桶中。
如果对象大于5MB，客户端将会自动使用多部分的会话。

如果会话失败了，用户会尝试着通过再次创建完全相同的对象来重传对象。客户端将会自动检查所有当前上传会话的所有部分并尝试着重用这个会话。如果发现不匹配，在上传更多数据前将中止上传。否则，将会在会话退出的部分恢复上传。

如果多会话失败，用户需要恢复或删除这个会话。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.util.Map-io.minio.ServerSideEncryption-)


__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  | 上传的流。 |
| ``headerMap``  | _Map<String,String>_  | 个性化/额外的对象元数据。|
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |



| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__

```java
 StringBuilder builder = new StringBuilder();
 for (int i = 0; i < 1000; i++) {
   builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
   builder.append("(29 letters)\n");
   builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
   builder.append("(31 letters)\n");
   builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
   builder.append("NASAs Space Shuttle. (32 letters)\n");
   builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
   builder.append("(39 letters)\n");
   builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
   builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
   builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
   builder.append("computers after System 7.\n");
   builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
   builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
   builder.append("---\n");
 }
 ByteArrayInputStream bais = new ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
 KeyGenerator keyGen = KeyGenerator.getInstance("AES");
 keyGen.init(256);
 ServerSideEncryption sse = ServerSideEncryption.withCustomerKey(keyGen.generateKey());
// 创建对象
 Map<String, String> headerMap = new HashMap<>();
 headerMap.put("Content-Type", "application/octet-stream");
 minioClient.putObject("my-bucketname", "my-objectname", bais, headerMap, sse);
 bais.close();
 System.out.println("my-objectname is uploaded successfully");
```


<a name="putObject"></a>

### putObject(String bucketName, String objectName, String fileName, Long size, Map<String, String> headerMap, ServerSideEncryption sse, String contentType)

`public void putObject(String bucketName, String objectName, String fileName, Long size, Map<String, String> headerMap, ServerSideEncryption sse, String contentType)`

将给定流中的数据作为对象上传到具有指定元数据的给定存储桶中。
如果对象大于5MB，客户端将会自动使用多部分的会话。

如果会话失败了，用户会尝试着通过再次创建完全相同的对象来重传对象。客户端将会自动检查所有当前上传会话的所有部分并尝试着重用这个会话。如果发现不匹配，在上传更多数据前将中止上传。否则，将会在会话退出的部分恢复上传。

如果多会话失败，用户需要恢复或删除这个会话。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.lang.String-java.lang.Long-java.util.Map-io.minio.ServerSideEncryption-java.lang.String)


__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``fineName``  | _String_  | 上传的文件名称。 |
| ``stream``  | _InputStream_  | 上传的流。 |
| ``size``  | _long_  | 文件大小。 |
| ``headerMap``  | _Map<String,String>_  | 个性化/另外的对象元数据。 |
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |
| ``contentType``  | _String_ | 对象的文件内容类型，用户提供。  |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__

```java
try {
  KeyGenerator keyGen = KeyGenerator.getInstance("AES");
  keyGen.init(256);
  ServerSideEncryption sse = ServerSideEncryption.withCustomerKey(keyGen.generateKey());
  Map<String, String> headerMap = new HashMap<>();
  headerMap.put("my-custom-data", "foo");
  minioClient.putObject("mybucket",  "island.jpg", "/mnt/photos/island.jpg",headerMap,sse, "application/octet-stream" );
  System.out.println("island.jpg is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="putObject"></a>

### putObject(String bucketName, String objectName, InputStream stream, Long size, Map<String, String> headerMap, ServerSideEncryption sse, String contentType)

`public void putObject(String bucketName, String objectName, InputStream stream, Long size, Map<String, String> headerMap, ServerSideEncryption sse, String contentType)`



[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#putObject-java.lang.String-java.lang.String-java.io.InputStream-java.util.Map-io.minio.ServerSideEncryption-java.lang.String)


__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``stream``  | _InputStream_  | 上传的流。 |
| ``size``  | _long_  | 从``stream``中读取的将上传的数据大小。 |
| ``headerMap``  | _Map<String,String>_  | 个性化/另外的对象元数据。 |
| ``sse``  | _ServerSideEncryption_  | 服务端加密的格式 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |
| ``contentType``  | _String_ | 对象文件的目录内容，用户提供。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |

__示例__

```java
 StringBuilder builder = new StringBuilder();
 for (int i = 0; i < 1000; i++) {
   builder.append("Sphinx of black quartz, judge my vow: Used by Adobe InDesign to display font samples. ");
   builder.append("(29 letters)\n");
   builder.append("Jackdaws love my big sphinx of quartz: Similarly, used by Windows XP for some fonts. ");
   builder.append("(31 letters)\n");
   builder.append("Pack my box with five dozen liquor jugs: According to Wikipedia, this one is used on ");
   builder.append("NASAs Space Shuttle. (32 letters)\n");
   builder.append("The quick onyx goblin jumps over the lazy dwarf: Flavor text from an Unhinged Magic Card. ");
   builder.append("(39 letters)\n");
   builder.append("How razorback-jumping frogs can level six piqued gymnasts!: Not going to win any brevity ");
   builder.append("awards at 49 letters long, but old-time Mac users may recognize it.\n");
   builder.append("Cozy lummox gives smart squid who asks for job pen: A 41-letter tester sentence for Mac ");
   builder.append("computers after System 7.\n");
   builder.append("A few others we like: Amazingly few discotheques provide jukeboxes; Now fax quiz Jack! my ");
   builder.append("brave ghost pled; Watch Jeopardy!, Alex Trebeks fun TV quiz game.\n");
   builder.append("---\n");
 }
 ByteArrayInputStream bais = new ByteArrayInputStream(builder.toString().getBytes("UTF-8"));
 KeyGenerator keyGen = KeyGenerator.getInstance("AES");
 keyGen.init(256);
 ServerSideEncryption sse = ServerSideEncryption.withCustomerKey(keyGen.generateKey());
// 创建对象
 Map<String, String> headerMap = new HashMap<>();
 headerMap.put("my-custom-data", "foo");
 minioClient.putObject("my-bucketname", "my-objectname", bais, bias.available(), headerMap, sse, contentType);
 bais.close();
 System.out.println("my-objectname is uploaded successfully");
```


<a name="statObject"></a>
### statObject(String bucketName, String objectName)

*`public ObjectStat statObject(String bucketName, String objectName)`*

获取对象的元数据。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#statObject-java.lang.String-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |


| 返回值类型	  | 异常   |
|:--- |:--- |
|  ``ObjectStat``: Populated object meta data. | 异常列表： |
|        |  ``InvalidBucketNameException`` : 不合法的存储桶名称。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 执行失败异常。            |
|        | ``InternalException`` : 内部错误。        |

__示例__


```java
try {
  // 获得对象的元数据。
  ObjectStat objectStat = minioClient.statObject("mybucket", "myobject");
  System.out.println(objectStat);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="statObject"></a>
### statObject(String bucketName, String objectName, ServerSideEncryption sse)

*`public ObjectStat statObject(String bucketName, String objectName, ServerSideEncryption sse)`*

返回在给定存储桶中的给定对象的元数据。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#statObject-java.lang.String-java.lang.String-io.minio.ServerSideEncryption-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``sse``  | _ServerSideEncryption_  | 只被SSE-C要求的加密元数据 [ServerSideEncryption](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |


| 返回类型   | 异常	  |
|:--- |:--- |
|  ``ObjectStat``: Populated object meta data. | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |

__示例__


```java
try {
  // Get the metadata of the object.
  ObjectStat objectStat = minioClient.statObject("my-bucketname", "my-objectname", sse);
  System.out.println(objectStat);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```



<a name="copyObject"></a>
### copyObject(String bucketName, String objectName, String destBucketName)

*`public void copyObject(String bucketName, String objectName, String destBucketName)`*

复制一个源对象到具有相同对象名字的的目的对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#copyObject-java.lang.String-java.lang.String-java.lang.String-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 源存储桶的名称。  |
| ``objectName``  | _String_  | 源存储桶中要复制的对象名称。 |
| ``destBucketName``  | _String_  | 目的存储桶名称。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |


__示例__


```java
minioClient.copyObject("my-bucketname", "my-objectname", "my-destbucketname");
```


<a name="copyObject"></a>
### copyObject(String bucketName, String objectName, String destBucketName, CopyConditions copyConditions)

*`public void copyObject(String bucketName, String objectName, String destBucketName, CopyConditions copyConditions)`*

复制一个原对象到所提供存储桶中具有所提供名字的新对象中。可以随意地选择一个键值CopyConditions并有条件地尝试copyObject。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#copyObject-java.lang.String-java.lang.String-java.lang.String-io.minio.CopyConditions-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 元存储桶地名称。  |
| ``objectName``  | _String_  | 在源存储桶中被复制的源存储桶。|
| ``destBucketName``  | _String_  | 目的存储桶的名称。 |
| ``copyConditions`` | _CopyConditions_ | 对复制操作应用限制有效的的条件映射。|


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |


__示例__

```java
minioClient.copyObject("my-bucketname", "my-objectname", "my-destbucketname", copyConditions);
```

<a name="copyObject"></a>
### copyObject(String bucketName, String objectName, String destBucketName, String destObjectName)

*`public void copyObject(String bucketName, String objectName, String destBucketName, String destObjectName)`*

将原对象复制到新的目的对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#copyObject-java.lang.String-java.lang.String-java.lang.String-java.lang.String-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 源存储桶的名称。  |
| ``objectName``  | _String_  | 在源存储桶中被复制的对象名称。 |
| ``destBucketName``  | _String_  | 目的存储桶的名称。 |
| ``destObjectName`` | _String_ |创建的目的对象名称，如果没有为源对象命称提供默认值。|


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``No| ``copyConditions`` | _CopyConditions_ | 有效对复制操作应用限制的条件映射。|ResponseException`` : 服务器无响应。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |


__示例__

```java
minioClient.copyObject("my-bucketname", "my-objectname", "my-destbucketname", "my-destobjname");
```

<a name="copyObject"></a>
### copyObject(String bucketName, String objectName, String destBucketName, String destObjectName, CopyConditions copyConditions)

*`public void copyObject(String bucketName, String objectName, String destBucketName, String destObjectName, CopyConditions copyConditions)`*

复制一个原对象到所提供存储桶中具有所提供名字的新对象中。可以随意地选择一个键值CopyConditions并有条件地尝试copyObject。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#copyObject-java.lang.String-java.lang.String-java.lang.String-java.lang.String-io.minio.CopyConditions-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 源存储桶的名称。  |
| ``objectName``  | _String_  | 源存储桶中要复制的对象名称。 |
| ``destBucketName``  | _String_  | 目的存储桶名称。 |
| ``destObjectName`` | _String_ | 创建的目的对象名称，如果没有为源对象名称提供默认值。|
| ``copyConditions`` | _CopyConditions_ | 有效对复制操作应用限制的条件映射。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |


__示例__

```java
minioClient.copyObject("my-bucketname", "my-objectname", "my-destbucketname", "my-destobjname", copyConditions);
```

<a name="copyObject"></a>
### copyObject(String bucketName, String objectName, ServerSideEncryption sseSource, String destBucketName, String destObjectName, CopyConditions copyConditions, ServerSideEncryption sseTarget)

*`public void copyObject(String bucketName, String objectName, ServerSideEncryption sseSource, String destBucketName, String destObjectName, CopyConditions copyConditions, ServerSideEncryption sseTarget)`*

复制一个原对象到所提供存储桶中具有所提供名字的新对象中。可以随意地选择一个键值CopyConditions并有条件地尝试copyObject。


[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#copyObject-java.lang.String-java.lang.String-io.minio.ServerSideEncryption-java.lang.String-java.lang.String-io.minio.CopyConditions-io.minio.ServerSideEncryption-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 源存储桶的名称。  |
| ``objectName``  | _String_  | 源存储桶中要复制的对象名称。 |
| ``sseSource``  | _ServerSideEncryption_  | 源加密元数据 [服务端加密](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |
| ``destBucketName``  | _String_  | 目的存储桶名称。 |
| ``destObjectName`` | _String_ | 创建的目的对象，如果没有为源对象名称提供默认值。|
| ``copyConditions`` | _CopyConditions_ | 有效对复制操作应用限制的条件映射。|
| ``sseTarget``  | _ServerSideEncryption_  | Target Encryption metadata [ServerSideEncryption](http://minio.github.io/minio-java/io/minio/ServerSideEncryption.html). |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |


__示例__

```java
 minioClient.copyObject("my-bucketname", "my-objectname", sseSource, "my-destbucketname", "my-destobjname", copyConditions, sseTarget);
```

<a name="copyObject"></a>
### copyObject(String bucketName, String objectName, String destBucketName, String destObjectName, CopyConditions copyConditions, Map<String, String> metadata)

*`public void copyObject(String bucketName, String objectName, String destBucketName, String destObjectName, CopyConditions copyConditions, Map<String, String> metadata)`*

将objectName复制到destObjectName中。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#copyObject-java.lang.String-java.lang.String-java.lang.String-java.lang.String-io.minio.CopyConditions-)

__参数__

|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 源存储桶的名称。  |
| ``objectName``  | _String_  | 源存储桶中要复制的对象名称。 |
| ``destBucketName``  | _String_  | 目的存储桶名称。 |
| ``destObjectName`` | _String_ | 创建的目的对象，如果没有为源对象名称提供默认值。|
| ``copyConditions`` | _CopyConditions_ | 有效对复制操作应用限制的条件映射。|
| ``metadata``  | _Map_ | 对象元数据到目的对象的映射。|


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |

__示例__


这个API执行一个从给定源对象到目的对象的服务端复制操作。

```java
try {
  CopyConditions copyConditions = new CopyConditions();
  copyConditions.setMatchETagNone("TestETag");

  minioClient.copyObject("mybucket",  "island.jpg", "mydestbucket", "processed.png", copyConditions);
  System.out.println("island.jpg is uploaded successfully");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="removeObject"></a>
### removeObject(String bucketName, String objectName)

`public void removeObject(String bucketName, String objectName)`

删除一个对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#removeObject-java.lang.String-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |

|返回值类型	  | 异常   |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``IOException`` : 连接异常。           |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |



__示例__


```java
try {
      // Remove my-objectname from the bucket my-bucketname.
      minioClient.removeObject("mybucket", "myobject");
      System.out.println("successfully removed mybucket/myobject");
} catch (MinioException e) {
      System.out.println("Error: " + e);
}
```

<a name="removeObjects"></a>
### removeObjects(String bucketName, Iterable<String> objectNames)

`public Iterable<Result<DeleteError>> removeObjects(String bucketName, Iterable<String> objectNames)`

删除多个对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#removeObjects-java.lang.String-java.lang.String-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectNames`` | _Iterable<String>_  | 迭代对象包含着删除的对象名称。|

|Return Type	  | 异常	  |
|:--- |:--- |
| ``Iterable<Result<DeleteError>>``:DeleteError结果的迭代器。 | _None_  |



__示例__


```java
List<String> objectNames = new LinkedList<String>();
objectNames.add("my-objectname1");
objectNames.add("my-objectname2");
objectNames.add("my-objectname3");
try {
      // Remove object all objects in objectNames list from the bucket my-bucketname.
      for (Result<DeleteError> errorResult: minioClient.removeObjects("my-bucketname", objectNames)) {
        DeleteError error = errorResult.get();
        System.out.println("Failed to remove '" + error.objectName() + "'. Error:" + error.message());
      }
} catch (MinioException e) {
      System.out.println("Error: " + e);
}
```



<a name="removeIncompleteUpload"></a>
### removeIncompleteUpload(String bucketName, String objectName)

`public void removeIncompleteUpload(String bucketName, String objectName)`

删除一个未完整上传的对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#removeIncompleteUpload-java.lang.String-java.lang.String-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  None  | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |


__示例__


```java
try {
    // 从存储桶中删除名为myobject的未完整上传的对象。
	minioClient.removeIncompleteUpload("mybucket", "myobject");
	System.out.println("successfully removed all incomplete upload session of my-bucketname/my-objectname");
} catch(MinioException e) {
	System.out.println("Error occurred: " + e);
}
```

## 4. Presigned操作
<a name="presignedGetObject"></a>

### presignedGetObject(String bucketName, String objectName)
`public String presignedGetObject(String bucketName, String objectName)`

返回预先指定的URL，以使用默认的到期时间下载存储桶中的对象。默认到期事件是7天（以秒为单位）。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#presignedGetObject-java.lang.String-java.lang.String-)



__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_ | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |



| 返回类型   | 异常	  |
|:--- |:--- |
|  ``String`` : string包含着下载对象的URL。 | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidExpiresRangeException`` : 输入期限超出范围。     |


__示例__


```java
try {
	 String url = minioClient.presignedGetObject("my-bucketname", "my-objectname");
     System.out.println(url);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="presignedGetObject"></a>

### presignedGetObject(String bucketName, String objectName, Integer expires)
`public String presignedGetObject(String bucketName, String objectName, Integer expires)`

为HTTP GET操作生成预签名的URL。浏览器/移动客户端可能会指向URL去直接下载对象，即使存储桶是私有的。这个预签名的URL可以具有一个以秒为单位的限期，之后它将不再运行。默认的期限是7天。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#presignedGetObject-java.lang.String-java.lang.String-java.lang.Integer-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_ | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``expiry``  | _Integer_  | 期限以秒为单位。默认的期限为7天。  |


| 返回类型   | 异常	  |
|:--- |:--- |
|  ``String`` : string包含着下载对象的URL。 | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidExpiresRangeException`` : 输入的期限超出范围。              |

__示例__


```java
try {
	String url = minioClient.presignedGetObject("mybucket", "myobject", 60 * 60 * 24);
	System.out.println(url);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="presignedGetObject"></a>

### presignedGetObject(String bucketName, String objectName, Integer expires, Map<String,String> reqParams)
`public String presignedGetObject(String bucketName, String objectName, Integer expires, Map<String,String> reqParams)`

返回一个预签名的URL来使用在给定的的到期时间和自定义请求参数下载存储桶中的对象。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#presignedGetObject-java.lang.String-java.lang.String-java.lang.Integer-java.util.Map-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_ | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``expiry``  | _Integer_  | 以秒为单位的期限。默认的期限是7天。 |
| ``reqParams``  | _Map<String,String>_  | 覆盖响应头的值。当前支持的请求参数有[response-expires, response-content-type, response-cache-control, response-content-disposition]。 |


| 返回类型   | 异常	  |
|:--- |:--- |
|  ``String`` : string包含着下载对象的URL。 | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidExpiresRangeException`` : 输入输入期限超出范围。.            |

__示例__


```java
try {
	String url = minioClient.presignedGetObject("my-bucketname", "my-objectname", 60 * 60 * 24, reqParams);
	System.out.println(url);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```




<a name="presignedPutObject"></a>

### presignedPutObject(String bucketName, String objectName)

`public String presignedPutObject(String bucketName, String objectName)`

返回预先指定的URL，以使用默认的到期时间下载存储桶中的对象。默认到期事件是7天（以秒为单位）。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#presignedPutObject-java.lang.String-java.lang.String-)


__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶里的对象名称。 |

| 返回类型   | 异常	  |
|:--- |:--- |
|  ``String`` : string包含着下载对象的URL。 | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InvalidExpiresRangeException`` : 输入期限超出范围。.            |
|        | ``InternalException`` : 内部异常。        |


__示例__

```java
try {
	String url = minioClient.presignedPutObject("my-bucketname", "my-objectname");
    System.out.println(url);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```

<a name="presignedPutObject"></a>
### presignedPutObject(String bucketName, String objectName, Integer expires)

`public String presignedPutObject(String bucketName, String objectName, Integer expires)`

为HTTP PUT操作生成预签名的URL。浏览器/移动客户端可能会指向URL去直接下载对象，即使存储桶是私有的。这个预签名的URL可以具有一个以秒为单位的限期，之后它将不再运行。默认的期限是7天。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#presignedPutObject-java.lang.String-java.lang.String-java.lang.Integer-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``bucketName``  | _String_  | 存储桶名称。  |
| ``objectName``  | _String_  | 存储桶中的对象名称。 |
| ``expiry``  | _Integer_  | 期限以秒为单位。默认的期限为7天。 |

| 返回类型   | 异常	  |
|:--- |:--- |
|  ``String`` : string包含着下载对象的URL。 | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidExpiresRangeException`` : 输入期限超出范围。.            |


__示例__

```java
try {
	String url = minioClient.presignedPutObject("mybucket", "myobject", 60 * 60 * 24);
	System.out.println(url);
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
}
```


<a name="presignedPostPolicy"></a>
### presignedPostPolicy(PostPolicy policy)

`public Map<String,String> presignedPostPolicy(PostPolicy policy)`

允许给POST请求的presigned URL设置策略，比如接收对象上传的存储桶名称的策略，key名称前缀，过期策略。

[查看Javadoc](http://minio.github.io/minio-java/io/minio/MinioClient.html#presignedPostPolicy-io.minio.PostPolicy-)

__参数__


|参数   | 类型	  | 描述  |
|:--- |:--- |:--- |
| ``policy``  | _PostPolicy_  | 对象的post策略 |


| 返回值类型	  | 异常   |
|:--- |:--- |
| ``Map``: 由于构造表单数据的字符串映射。 | 异常列表: |
|        |  ``InvalidBucketNameException`` : 存储桶名字非法。 |
|        | ``NoSuchAlgorithmException`` : 计算签名期间没有找到相应的算法。           |
|        | ``InsufficientDataException`` : 给定InputStream的读取在读取到给定长度之前就得到一个EOFException。 |
|        | ``IOException`` : 连接异常。           |
|        | ``InvalidKeyException`` : 访问密钥（access key）和密钥（secret key）非法。           |
|        | ``NoResponseException`` : 服务器无响应。            |
|        | ``org.xmlpull.v1.XmlPullParserException`` : 解析返回的XML异常。            |
|        | ``ErrorResponseException`` : 运行失败。            |
|        | ``InternalException`` : 内部异常。        |
|        | ``InvalidArgumentException`` : 方法传递值非法。        |



__示例__

```java
try {
	PostPolicy policy = new PostPolicy("mybucket", "myobject",
  DateTime.now().plusDays(7));
	policy.setContentType("image/png");
	Map<String,String> formData = minioClient.presignedPostPolicy(policy);
	System.out.print("curl -X POST ");
	for (Map.Entry<String,String> entry : formData.entrySet()) {
    System.out.print(" -F " + entry.getKey() + "=" + entry.getValue());
	}
	System.out.println(" -F file=@/tmp/userpic.png  https://play.min.io:9000/mybucket");
} catch(MinioException e) {
  System.out.println("Error occurred: " + e);
```

## 5. 了解更多

- [创建属于你的照片API服务示例](https://github.com/minio/minio-java-rest-example)
- [完整的JavaDoc](http://minio.github.io/minio-java/)
