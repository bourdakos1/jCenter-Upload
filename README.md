# jCenter-Upload
Step-by-step instructions for uploading to jCenter

## Create a Bintray account
https://bintray.com

## Gradle
![](help_gradle.png)

In your Project's build.gradle make sure you have the following dependencies:
```groovy
dependencies {
        classpath 'com.android.tools.build:gradle:2.1.2'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.4'
        classpath 'com.github.dcendents:android-maven-gradle-plugin:1.3'
}
```

In the next step you will need to provide some information about your library. Some of this information includes your ``GroupId`` your ``artifact`` and your ``libraryVersion`` they can be whatever you like, but normally look something like this:
```groovy
dependencies {
        compile 'com.xlythe:android-text-manager:1.0.0'
                (GroupId:artifact:libraryVersion)
}
```

In your Project's gradle.properties add the following:
```properties
bintray.bintrayRepo=maven
bintray.bintrayName=your librarys bintray name

bintray.publishedGroupId=your group id
bintray.libraryName=library name
bintray.artifact=artifact name *This must match your module's name*

bintray.libraryDescription=your library description

bintray.siteUrl=your website url
bintray.gitUrl=your git url

bintray.libraryVersion=your librarys version

bintray.developerId=your id
bintray.developerName=your name
bintray.developerEmail=your email address

bintray.licenseName=The Apache Software License, Version 2.0
bintray.licenseUrl=http://www.apache.org/licenses/LICENSE-2.0.txt
bintray.allLicenses=Apache-2.0
```

At the very end of your library module's build.gradle add:
```groovy
apply from: 'https://raw.githubusercontent.com/bourdakos1/jCenter-Upload/master/upload.gradle'
```

Finally, in local.properties add the following:
```properties
bintray.user=your bintray username
bintray.apikey=your bintray apikey
```

## Upload
Run ```./gradlew bintrayUpload``` in your projects terminal
