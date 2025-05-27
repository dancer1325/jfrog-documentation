https://jfrog.com/help/r/get-started-with-the-jfrog-platform/quickstart-guide-maven-and-gradle

* [quick start guide](get-started-with-the-jfrog-platform.quickstart-guide.md) -- via -- Maven & Gradle

* requirements
  * install [Maven](https://maven.apache.org/install.html) or [Gradle](https://gradle.org/install/)
  * [install JFrog CLI](https://docs.jfrog-applications.jfrog.io/jfrog-applications/jfrog-cli)
  * [JFrog self-hosted subscription](https://jfrog.com/start-free/#hosted) OR [JFrog Cloud subscription](https://jfrog.com/start-free/)

# Step1: Build & run your Maven / Gradle project
* fork [this git repo](https://github.com/dancer1325/jfrog-getstarted)

# Step2: log in | your environment

# Step3: add Maven repositories & artifacts
* goal
  * create a Maven/Gradle repository type
    * virtual
    * remote
    * local
  * upload your project

* steps
  * to create repositories
    * log in | JFrog Platform UI
    * | Administration's repositories
    * create repositories
  * `jf c add`
  * `jf mvn-config` OR `jf gradle-config`


* Artifactory -- as -- your artifact repository