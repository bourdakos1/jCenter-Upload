# jCenter-Upload
Step-by-step instructions for uploading to jCenter

## Create a jCenter account
https://bintray.com

## Gradle
In your Project's build.gradle make sure you have the following dependencies:
```groovy
dependencies {
        classpath 'com.android.tools.build:gradle:2.1.2'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.4'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
}
```

In your Project's gradle.properties add the following:

```
bintray.bintrayRepo=maven
bintray.bintrayName=android-text-manager

bintray.publishedGroupId=com.xlythe
bintray.libraryName=AndroidTextManager
bintray.artifact=android-text-manager

bintray.libraryDescription=''

bintray.siteUrl=https://github.com/Xlythe/AndroidTextManager
bintray.gitUrl=https://github.com/Xlythe/AndroidTextManager.git

bintray.libraryVersion=1.0.1

bintray.developerId=bourdakos1
bintray.developerName=Nicholas Bourdakos
bintray.developerEmail=bourdakos1@gmail.com

bintray.licenseName=The Apache Software License, Version 2.0
bintray.licenseUrl=http://www.apache.org/licenses/LICENSE-2.0.txt
bintray.allLicenses=Apache-2.0
```

At the very end of your library module's build.gradle add:

```groovy
apply from: 'https://raw.githubusercontent.com/bourdakos1/jCenter-Upload/master/upload.gradle'
```

Finally, in local.properties add the following:

```groovy
bintray.user=yourbintrayusername
bintray.apikey=yourbintrayapikey
```

To start the upload do a gradle synce and run ```./gradlew bintrayUpload``` in your projects terminal
