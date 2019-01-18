##Nexus 

###TL;DR

````
docker-compose up
````


Build the image

```
docker build .  --build-arg proxy=${proxy_http} -t <youruser>/mynexus:latest
```

Run the image locally:

```
docker run -p 8081:8081 <youruser>/mynexus:latest
```

Push it to a repository:

```
docker push <youruser>/mynexus:latest
```

###Know issues:

The build fail because the Java jre cannot be extracted. 

````
Recipe: java::oracle
  * yum_package[tar] action install (up to date)
  * java_ark[jdk] action install
    * yum_package[curl for download_direct_from_oracle] action install (up to date)
    - download oracle tarball straight from the server[2019-01-18T08:02:19+00:00] FATAL: Failed to extract file server-jre-8u192-linux-x64.tar.gz!
````

It is due to the fact that Oracle is constantly releasing new URL and removing previous ones.

Solving issue:

1 - Find a newer URL for downloading JRE

visit : https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html \

[It should look like this](JAVA_URL.png)

You want the **Linux x64 tar.gz**

2 - Replace the JAVA_URL arg into docker-compose file with the new URL