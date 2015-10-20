## Plain Maven Build

This project is a plain maven project. We will:

 * Deploy it to Package Drone
 * Convert it into an OSGi bundle
 * Create a P2 and OSGi R5/OBR repository
 
### Deploy to Package Drone

* Create new channel in Package Drone called "mvn1"
* Add the following snippet to the `pom.xml`

	<distributionManagement>
		<repository>
			<id>drone</id>
			<url>http://localhost:8080/maven/mvn1</url>
		</repository>
	</distributionManagement>

* Run `mvn deploy`
* Check the logs!
* Add deploy key to channel
* Add the deploy key to `~/.m2/settings.xml`
* Run `mvn deploy` again

### Make a Maven repository

 * Add the maven repository aspect
 * Check maven repository content

### Make P2 repository

 * Add P2 repository aspect -> no content
 * Add OSGi aspect -> still no content
 * Add the following snippet to the `pom.xml`
 
	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.felix</groupId>
				<artifactId>maven-bundle-plugin</artifactId>
				<version>2.5.3</version>
				<extensions>true</extensions>
				<configuration>
					<instructions>
						<Export-Package>org.eclipse.packagedrone.ece.sample01.plain.maven</Export-Package>
					</instructions>
				</configuration>
			</plugin>
	
			<plugin>
				<artifactId>maven-source-plugin</artifactId>
				<version>2.4</version>
				<executions>
					<execution>
						<id>attach-sources</id>
						<phase>package</phase>
						<goals>
							<goal>jar-no-fork</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
 * Add `<packaging>bundle</packaging>` to the `pom.xml`
 * Run `mvn deploy` again
 * Check output -> still no content
 * Add P2 Metadata aspect -> content!
 * Add Eclipse Source bundle aspect -> check again
 
### Make it OSGi R5 / OBR

 * Add the OSGi R5 repository aspect -> content!