# jCenter-Upload
Step-by-step instructions for uploading to jCenter

## Create a jCenter account
https://bintray.com/bintray/jcenter

## Gradle
In your Project's build.gradle make sure you have the following dependencies:
```groovy
dependencies {
        classpath 'com.android.tools.build:gradle:2.1.2'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.4'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
}
```
