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

Under your dependencies at the very end add:

```groovy
apply plugin: 'com.github.dcendents.android-maven'

group = publishedGroupId

install {
    repositories.mavenInstaller {
        // This generates POM.xml with proper parameters
        pom {
            project {
                packaging 'aar'
                groupId publishedGroupId
                artifactId artifact

                name libraryName
                description libraryDescription
                url siteUrl

                licenses {
                    license {
                        name licenseName
                        url licenseUrl
                    }
                }
                developers {
                    developer {
                        id developerId
                        name developerName
                        email developerEmail
                    }
                }
            }
        }
    }
}

apply plugin: 'com.jfrog.bintray'

version = libraryVersion

task sourcesJar(type: Jar) {
    from android.sourceSets.main.java.srcDirs
    classifier = 'sources'
}

task javadoc(type: Javadoc) {
    source = android.sourceSets.main.java.srcDirs
    classpath += project.files(android.getBootClasspath().join(File.pathSeparator))
}

task javadocJar(type: Jar, dependsOn: javadoc) {
    classifier = 'javadoc'
    from javadoc.destinationDir
}
artifacts {
    archives javadocJar
    archives sourcesJar
}

// Bintray
Properties properties = new Properties()
properties.load(project.rootProject.file('local.properties').newDataInputStream())

bintray {
    user = properties.getProperty("bintray.user")
    key = properties.getProperty("bintray.apikey")

    configurations = ['archives']
    pkg {
        repo = bintrayRepo
        name = bintrayName
        desc = libraryDescription
        websiteUrl = siteUrl
        vcsUrl = gitUrl
        licenses = allLicenses
        publish = true
        publicDownloadNumbers = false
        version {
            desc = libraryDescription
            gpg {
                sign = false //Determines whether to GPG sign the files. The default is false
                //passphrase = properties.getProperty("bintray.gpg.password")
                //Optional. The passphrase for GPG signing'
            }
        }
    }
}
```

Finally, in local.properties add the following:
(replace "yourbintrayusername" and "yourbintrayapikey" with your actual info)
```groovy
bintray.user=yourbintrayusername
bintray.apikey=yourbintrayapikey
```

To start the upload all you need to do is run ```./gradlew bintrayUpload``` in your projects terminal
