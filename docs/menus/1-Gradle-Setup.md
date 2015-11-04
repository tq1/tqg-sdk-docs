## Gradle Setup

If you don't have already jcenter as a repository, add on the project's top-level 'build.gradle' file as in the following example:

 ```
 allprojects {
    repositories {
        jcenter()
    }
}
 ```

To use TQG just add the SDK as a gradle dependency directly replacing <version> with the desire version number (e.g, 0.3.0):

```java
compile 'com.taqtile:tqg-android-sdk:<version>'
```