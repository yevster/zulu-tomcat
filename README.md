# Instructions

To build the app image:

```bash
sudo docker build . --build-arg APP_FILE=myApp.war -t myApp:1
```

To run the app image:

```bash
sudo docker run -d -p 8080:8080 myApp:1
```

# Keeping dependencies up to date

Be sure to use the latest appropriate versions of Zulu and Tomcat after fully testing them with your application. Specific versions can be incorporated through build arguments without modifying the Dockerfile, for instance:


```bash
sudo docker build . --build-arg APP_FILE=myApp.war \
    --build-arg TOMCAT_VERSION=9.0.30 --build-arg TOMCAT_MAJOR=9 \
    --build-arg JDK_VERSION=8u222 -t myapp:1
```
