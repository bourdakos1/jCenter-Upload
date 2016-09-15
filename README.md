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

In your Library's Module build.gradle add the following code at the top under ``apply plugin: 'com.android.library'``:
(Fill in required information in quotes)

```groovy
ext {
    bintrayRepo = 'maven'
    bintrayName = ''

    publishedGroupId = ''
    libraryName = ''
    artifact = ''

    libraryDescription = ''

    siteUrl = ''
    gitUrl = ''

    libraryVersion = ''

    developerId = ''
    developerName = ''
    developerEmail = ''

    licenseName = 'The Apache Software License, Version 2.0'
    licenseUrl = 'http://www.apache.org/licenses/LICENSE-2.0.txt'
    allLicenses = ["Apache-2.0"]
}
```
