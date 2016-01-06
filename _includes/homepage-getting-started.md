## Built for the Enterprise

Nebula is a collection of Gradle plugins built for Netflix engineers to eliminate boilerplate build logic and provide sane conventions. We chose Gradle for our underlying build system because we feel Gradle is the best build tool for Java applications.

In order to understand the value that Nebula provides, let's look at a Gradle build file for a typical Java web project.

~~~output
apply plugin: 'java'
apply plugin: 'war'
apply plugin: 'application'

mainClassName = 'com.netflix.sampleApp.Application'
~~~

Gradle provides a lot of functionality out of the box. For instance, the above build.gradle file allows you to:

- compile Java source files located in a Maven standard layout
- compile and execute unit tests
- produce javadocs from source
- package the compile source into a Java web application (`.war`)
- bundle the app as a `.zip` or `.tar` file with OS specific start scripts

Now, let's sprinkle in some Nebula plugin goodness and see what additional benefits we achieve.

~~~output
apply plugin: 'java'
apply plugin: 'war'
apply plugin: 'application'
apply plugin: 'nebula.project-plugin'
apply plugin: 'nebula.dependency-lock'
apply plugin: 'nebula.ospackage-application-daemon'
apply plugin: 'nebula.maven-publish'
apply plugin: 'nebula.javadoc-jar'
apply plugin: 'nebula.sources-jar'
apply plugin: 'nebula.release'
apply plugin: 'nebula.bintray'

mainClassName = 'com.netflix.sampleApp.Application'

contacts {
    'bob@foobar.com' {
        moniker 'Bob Smith'
        github 'bobsmith'
    }
}
~~~

In addition to previous mentioned features provided by Gradle, the Nebula plugins we added allow this project to:

- define contact information for the project
- metadata about the project is now captured and written into the .war's manifest
- produce `.jar` files for Javadocs as well as Java source files
- produce and commit to version control a `dependency.lock` file containing the complete transitive dependency graph as resolved by Gradle
- produce a `.deb` (or `.rpm`) file configured to use [daemontools](https://cr.yp.to/daemontools.html) for starting and stopping the application.
- publish the `.war` (or `.jar`) to a maven repository
- publish a `*-javadoc.jar` and a `*-sources.jar` to a maven repository
- add tasks to bump the major, minor or patch version based on [Semantic Versioning](http://semver.org/)
- the major/minor/patch release can be published to Bintray

You can start by checking out our [Introduction to Nebula]({{ site.baseurl }}/documentation/introduction_to_nebula.html).

