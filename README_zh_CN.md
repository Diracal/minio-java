# 适用于与Amazon S3兼容的云存储的MinIO Java SDK [![Slack](https://slack.min.io/slack?type=svg)](https://slack.min.io)

MinIO Java Client SDK提供简单的API来访问任何与Amazon S3兼容的对象存储服务。

本快速入门指南将向你展示如何安装客户端SDK并执行示例java程序。有关API和示例的完整列表，请查看[Java Client API Reference](http://docs.min.io/docs/java-client-api-reference)文档。

## 最低需求
Java 1.8或更高版本，并且有以下的环境之一:

* [OracleJDK 8.0](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [OpenJDK8.0](http://openjdk.java.net/install/)

## 使用maven
```xml
<dependency>
    <groupId>io.minio</groupId>
    <artifactId>minio</artifactId>
    <version>6.0.7</version>
</dependency>
```

## 使用gradle
```xml
dependencies {
    compile 'io.minio:minio:6.0.7'
}
```

## 直接下载JAR
你可以到maven仓库直接下载最新版的[JAR](http://repo1.maven.org/maven2/io/minio/minio/6.0.7/)。

## 快速入门示例—文件上传
本示例程序连接到一个对象存储服务，创建一个存储桶并上传一个文件到该桶中。

你需要有存储服务的三个参数才能连接到该服务。

| 参数     | 说明 |
| :------- | :------------ |
| Endpoint | 对象存储服务的URL |
| Access Key    | Access key就像用户ID，可以唯一标识你的账户。  |
| Secret Key     | Secret key是你账户的密码。    |


在下面的例子的中，我们将使用一个运行在[https://play.min.io:9000](https://play.min.io:9000)的免费托管的MinIO服务。你可以随意使用此服务进行测试和开发。此示例中显示的访问凭据是公开的。

#### FileUploader.java

```java
import java.io.IOException;
import java.security.NoSuchAlgorithmException;
import java.security.InvalidKeyException;

import org.xmlpull.v1.XmlPullParserException;

import io.minio.MinioClient;
import io.minio.errors.MinioException;

public class FileUploader {
  public static void main(String[] args) throws NoSuchAlgorithmException, IOException, InvalidKeyException, XmlPullParserException {
    try {
      // 使用MinIO服务的URL，端口，Access key和Secret key创建一个MinioClient对象
      MinioClient minioClient = new MinioClient("https://play.min.io:9000", "Q3AM3UQ867SPQQA43P2F", "zuf+tfteSlswRu7BJ86wekitnifILbZam1KYY3TG");

      // 检查存储桶是否已经存在
      boolean isExist = minioClient.bucketExists("asiatrip");
      if(isExist) {
        System.out.println("Bucket already exists.");
      } else {
        // 创建一个名为asiatrip的存储桶，用于存储照片的zip文件。
        minioClient.makeBucket("asiatrip");
      }

      // 使用putObject上传一个文件到存储桶中。
      minioClient.putObject("asiatrip","asiaphotos.zip", "/home/user/Photos/asiaphotos.zip");
      System.out.println("/home/user/Photos/asiaphotos.zip is successfully uploaded as asiaphotos.zip to `asiatrip` bucket.");
    } catch(MinioException e) {
      System.out.println("Error occurred: " + e);
    }
  }
}
```

#### 编译FileUploader
```sh
javac -cp "minio-6.0.7-all.jar"  FileUploader.java
```

#### 运行FileUploader
```sh
java -cp "minio-6.0.7-all.jar:." FileUploader
/home/user/Photos/asiaphotos.zip is successfully uploaded as asiaphotos.zip to `asiatrip` bucket.

mc ls play/asiatrip/
[2016-06-02 18:10:29 PDT]  82KiB asiaphotos.zip
```

## API文档

下面链接是完整的API文档

* [API完整文档](https://docs.min.io/docs/java-client-api-reference)

### API文档: 存储桶操作
* [`makeBucket`](https://docs.min.io/docs/java-client-api-reference#makeBucket)
* [`listBuckets`](https://docs.min.io/docs/java-client-api-reference#listBuckets)
* [`bucketExists`](https://docs.min.io/docs/java-client-api-reference#bucketExists)
* [`removeBucket`](https://docs.min.io/docs/java-client-api-reference#removeBucket)
* [`listObjects`](https://docs.min.io/docs/java-client-api-reference#listObjects)
* [`listIncompleteUploads`](https://docs.min.io/docs/java-client-api-reference#listIncompleteUploads)

### API文档: 对象操作
* [`getObject`](https://docs.min.io/docs/java-client-api-reference#getObject)
* [`putObject`](https://docs.min.io/docs/java-client-api-reference#putObject)
* [`copyObject`](https://docs.min.io/docs/java-client-api-reference#copyObject)
* [`statObject`](https://docs.min.io/docs/java-client-api-reference#statObject)
* [`removeObject`](https://docs.min.io/docs/java-client-api-reference#removeObject)
* [`removeIncompleteUpload`](https://docs.min.io/docs/java-client-api-reference#removeIncompleteUpload)

### API文档: Presigned操作
* [`presignedGetObject`](https://docs.min.io/docs/java-client-api-reference#presignedGetObject)
* [`presignedPutObject`](https://docs.min.io/docs/java-client-api-reference#presignedPutObject)
* [`presignedPostPolicy`](https://docs.min.io/docs/java-client-api-reference#presignedPostPolicy)

### API文档: 存储桶策略操作
* [`getBucketPolicy`](https://docs.min.io/docs/java-client-api-reference#getBucketPolicy)
* [`setBucketPolicy`](https://docs.min.io/docs/java-client-api-reference#setBucketPolicy)

## 完整示例

#### 完整示例: 存储桶操作
* [ListBuckets.java](https://github.com/minio/minio-java/tree/master/examples/ListBuckets.java)
* [ListObjects.java](https://github.com/minio/minio-java/tree/master/examples/ListObjects.java)
* [BucketExists.java](https://github.com/minio/minio-java/tree/master/examples/BucketExists.java)
* [MakeBucket.java](https://github.com/minio/minio-java/tree/master/examples/MakeBucket.java)
* [RemoveBucket.java](https://github.com/minio/minio-java/tree/master/examples/RemoveBucket.java)
* [ListIncompleteUploads.java](https://github.com/minio/minio-java/tree/master/examples/ListIncompleteUploads.java)

#### 完整示例: 对象操作
* [PutObject.java](https://github.com/minio/minio-java/tree/master/examples/PutObject.java)
* [PutObjectEncrypted.java](https://github.com/minio/minio-java/tree/master/examples/PutObjectEncrypted.java)
* [GetObject.Java](https://github.com/minio/minio-java/tree/master/examples/GetObject.java)
* [GetObjectEncrypted.Java](https://github.com/minio/minio-java/tree/master/examples/GetObjectEncrypted.java)
* [GetPartialObject.java](https://github.com/minio/minio-java/tree/master/examples/GetPartialObject.java)
* [RemoveObject.java](https://github.com/minio/minio-java/tree/master/examples/RemoveObject.java)
* [RemoveObjects.java](https://github.com/minio/minio-java/tree/master/examples/RemoveObjects.java)
* [StatObject.java](https://github.com/minio/minio-java/tree/master/examples/StatObject.java)

#### 完整示例: Presigned操作
* [PresignedGetObject.java](https://github.com/minio/minio-java/tree/master/examples/PresignedGetObject.java)
* [PresignedPutObject.java](https://github.com/minio/minio-java/tree/master/examples/PresignedPutObject.java)
* [PresignedPostPolicy.java](https://github.com/minio/minio-java/tree/master/examples/PresignedPostPolicy.java)

#### 完整示例: 存储桶策略操作
* [SetBucketPolicy.java](https://github.com/minio/minio-java/tree/master/examples/SetBucketPolicy.java)
* [GetBucketPolicy.Java](https://github.com/minio/minio-java/tree/master/examples/GetBucketPolicy.java)

#### 完整示例： 服务端加密
* [CopyObjectEncrypted.java](https://github.com/minio/minio-java/tree/master/examples/CopyObjectEncrypted.java)
* [CopyObjectEncryptedKms.java](https://github.com/minio/minio-java/tree/master/examples/CopyObjectEncryptedKms.java)
* [CopyObjectEncryptedS3.java](https://github.com/minio/minio-java/tree/master/examples/CopyObjectEncryptedS3.java)
* [PutGetObjectEncrypted.java](https://github.com/minio/minio-java/tree/master/examples/PutGetObjectEncrypted.java)
* [PutObjectEncryptedKms.java](https://github.com/minio/minio-java/tree/master/examples/PutObjectEncryptedKms.java)
* [PutObjectEncryptedS3.java](https://github.com/minio/minio-java/tree/master/examples/PutObjectEncryptedS3.java)

## 了解更多
* [MinIO完整文档](https://docs.min.io)
* [MinIO Java Client SDK API文档](https://docs.min.io/docs/java-client-api-reference)
* [创建属于你的照片API服务-完整示例](https://github.com/minio/minio-java-rest-example)

## 贡献
[贡献者指南](https://github.com/minio/minio-java/blob/master/docs/zh_CN/CONTRIBUTING.md)

[![Build Status](https://travis-ci.org/minio/minio-java.svg)](https://travis-ci.org/minio/minio-java)
[![Build status](https://ci.appveyor.com/api/projects/status/1d05e6nvxcelmrak?svg=true)](https://ci.appveyor.com/project/harshavardhana/minio-java)
