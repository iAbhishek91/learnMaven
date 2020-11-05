# Maven

Maven is a project management tool for java projects

**Convenstion over configuration**

## Structure of Maven

This is one of the convension

src/main/java
src/test/java
pom.xml

## Build lifecycle of Maven

They are sequence of steps that is defined by maven. *When we execute any one of the steps the previous steps are executed in sequence*

The below is the default one.

Validate >> compile >> test >> package >> integration test >> verify >> install

## Terminologies associated with maven

### Plugin

Plugins extends the functionality of maven.

### Repositories

It saves all the dependencies and all the versions.

There are two repository one is **remote** and **local**

- all the downloaded dependencies are store in local dependencies.
- 

### Super POM, Parent POM, Effective POM

pom.xml can also inherit from other pom. Parent or Super pom are pom from which another pom inherits.

effective pom is the combination of pom and the properties inherited from super or parent pom.

### Transitive dependencies managements

jar files used in your project are dependencies. Transitive dependencies are jar which are required by other dependencies and maven automagically downloads everything.

### Range in dependencies

<version>[,4.1]</version> : any version less than or equal to 4.1
<version>[4.1,]</version> : any version more than or equal to 4.1
<version>[4.1,4.4]</version> : any version more than or equal to 4.1 and less than or equal to 4.4

### Scope of a dependencies

under dependencies we can mention the <scope> tag to mention where the dependencies are required.

Few valid values are: compile; import, system, test, runtime, provided (this dependencies are not managed by maven and will not be part of the package, instead it will be available in the deployment server or environment)

### Plugin configuration

an plugin can have configuration, they act as inputs.

for example: the "maven-compile-plugin" take verbose, source and target. *Soruce and target are important as this changes the version of the java version of the project*

```xml
<plugin>
	<groupId></groupId>
	<artifactId></artifactId>
	<version></version>
	<configuration>
		<verbose>true</verbose>
		<source>1.8</source>
		<target>1.8</target>
	</configuration>
</plugin>
```

### Multi-project Maven project

- package of parent pom of multi-project is **pom**
- mudules tag mention which all modules are build as part of this pom.
- build the parent pom, all the child projects are build automatically.

### Modules

- This is a concept available in multi project, where parent pom mentions these module's properties and dependencies etc are modified by this pom.
- Each modules will have their own pom.
- Folder name should be same as the module name.

> BEST PRACTICES: version of clild POM are managed by parent if they are shared. Hence no need to define the <version> under dependencies of child pom.

### Variables

we have different types of variables:

- properties: ${properties}
- project: ${project.version}

> BEST PRACTICES: use of same project.version are recommended in multi project.

## Maven commands:

```sh
# purpose: compiles all the src java files and place it under target/classes
# plugins used : maven-resource-plugin; maven-compile-plugin
mvn compile


# purpose: same as before, but compiles src/test folder as well and placed under target/test-classes
# plugins used : same as above
mvn test-compile


# purpose: delete the targt directory
# plugin used: maven-clean-plugin
mvn clean


# purpose: to test
# plugin used: maven-surefire-plugin
mvn test


# purpose: to create a jar of the project and place it in local folder target will now have classes; test-classes; surefire-results; maven-status; maven-archiver and the jar
# plugin used: maven-install-plugin
mvn package


# purpose: run any maven command with -x option
mvn -X clean install


# purpose: to view the effective pom from command line instead of IDE
mvn effective:pom
mvn help:effective-pom


# purpose: to print the dependency tree, it also includes the memory consumed
mvn dependency:tree


# purpose: to see the maven settigs
mvn help:effective-settings


# purpose: generate a project of specific architype, after going through a quentionnaire
mvn archeype:generate
```

### Tags

- **project**: root of all pom.xml, this is encloses everything
- **groupId**: **artifactId**: **version**
- **properties**: properties are parametes that can be used in the pom or child pom. Use case: similar version of multiple plugins or dependencies.
- **properties.abc-foo-bar**: use it as ${abc-foo-bar} in the pom.
- **packageing**: tell what package is required, jar, war or ear, or pom (for multi project, or act as a parent pom)
- **dependencies**: project dependencies
- **dependencies.dependency.exclusions**: exclude any transitive dependencies if not required.
- **plugins**: gives us more commads
- **plugins.plugin.configuration**: to input some configurations to the plugins
- **build.sourceDirectory**: default is ~/src/main/java/. mostly they are inherited from super or parent pom.
- **build.scriptDirectory**: default is ~/src/main/scripts.
- **build.testSourceDirectory**: default is ~/src/test/java.
- **build.outputDirectory**: default is ~/src/target/classes.
- **build.testOutputDirectory**: default is ~/src/target/test-classes.
- **build.scriptDirectory**: default is ~/src/main/scripts.
- **modules**: define the modules that has-dependencies on this pom.
