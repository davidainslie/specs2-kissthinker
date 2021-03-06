Test Library for Scala
======================
Scala library to help with easier unit/integration testing.

Application built with the following (main) technologies:

- Scala

- SBT

- Specs2

Application
-----------
The application is configured as per a typical Scala application, where the default configuration file is "application.conf" (or reference.conf).
This default file can be overridden with other "conf" files and then given to the application upon boot with the following example Java option:
```bash
-Dconfig.file=test-classes/application.test.conf
```

Individual configuration properties can be overridden again by Java options e.g. to override which Mongodb to connect:
```bash
-Dmongo.db=some-other-mongo
```

where this overrides the default in application.conf.

Build and Deploy
----------------
The project is built with SBT. On a Mac (sorry everyone else) do:
```bash
brew install sbt
```

It is also a good idea to install Typesafe Activator (which sits on top of SBT) for when you need to create new projects - it also has some SBT extras, so running an application with Activator instead of SBT can be useful. On Mac do:
```bash
brew install typesafe-activator
```

Install Kafka and its dependency Zookeeper:
```bash
brew install zookeeper
brew install kafka
```

To compile:
```bash
sbt compile
```

or
```bash
activator compile
```

To run the specs:
```bash
sbt test
```

To actually run the application, you can simply:
```bash
sbt run
```

or first "assemble" it:
```bash
sbt assembly
```

This packages up an executable JAR - Note that "assembly" will first compile and test.

Then just run as any executable JAR, with any extra Java options for overriding configurations.

For example, to use a config file (other than the default application.conf) which is located on the file system (in this case in the boot directory)
```bash
java -Dconfig.file=test-classes/my-application.conf -jar <jar name>.jar
```

Note that the log configuration file could also be included e.g.
```bash
-Dlogback.configurationFile=path/to/my-logback.xml
```

So a more indepth startup with sbt itself could be:
```bash
sbt run -Dconfig.file=target/scala-2.11/test-classes/application.test.conf -Dlogback.configurationFile=target/scala-2.11/test-classes/logback.test.xml
```

And another example:

running from directory of the executable JAR using a config that is within said JAR:
```bash
java -Dconfig.resource=application.uat.conf -jar <jar name>.jar
```

SBT - Revolver
--------------
sbt-revolver is a plugin for SBT enabling a super-fast development turnaround for your Scala applications:

See https://github.com/spray/sbt-revolver

For development, you can use ~re-start to go into "triggered restart" mode.
Your application starts up and SBT watches for changes in your source (or resource) files.
If a change is detected SBT recompiles the required classes and sbt-revolver automatically restarts your application. 
When you press &lt;ENTER&gt; SBT leaves "triggered restart" and returns to the normal prompt keeping your application running.

Gatling - Performance (Integration) Testing
-------------------------------------------
Performance tests are under src/it, and test reports are written to the "target" directory.

To execute Gatling performance integration tests from withing SBT:
```bash
gatling-it:test
```

Example Usage
-------------
TODO