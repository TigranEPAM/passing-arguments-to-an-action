# Passing arguments to an action

In this lesson, arguments are passed to the following actions:

- [actions/checkout](https://github.com/actions/checkout)
- [actions/setup-java](https://github.com/actions/setup-java)

```
name: Build Tomcat

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Check out tomcat-users.xml
      uses: actions/checkout@v2

    - name: List project files and java version
      run: |
          ls -ltr
          java -version

    - name: Check out Apache Tomcat
      uses: actions/checkout@v2
      with:
        repository: apache/tomcat # Repository name with owner
        ref: master               # The branch, tag or SHA to checkout
        path: ./tomcat            # Relative path under $GITHUB_WORKSPACE

    - name: Setup Java 9
      uses: actions/setup-java@v1
      with:
        java-version: '9.0.4'     # The JDK version to make available on the path
        java-package: jdk         # (jre, jdk, or jdk+fx) - defaults to jdk
        architecture: x64         # (x64 or x86) - defaults to x64

    - name: List project files and java version
      run: |
          ls -ltr
          java -version

    - name: Copy tomcat-users.xml into Tomcat configuration directory
      run: cp -v tomcat-users.xml ./tomcat/conf/tomcat-users.xml

    - name: Compile Tomcat
      run: |
        cd ./tomcat
        ant
```
#   p a s s i n g - a r g u m e n t s - t o - a n - a c t i o n  
 