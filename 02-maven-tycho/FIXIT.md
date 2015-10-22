## Maven Tycho based build

Investigating a Tycho based build process.

### First deploy

 * Create a channel `tycho1`
 * Add deploy keys
 * Run `mvn deploy`
 * Check
 * Add "P2 repository" aspect -> content -> provided by Tycho
 
In this example the repository zip is not being deployed to the channel.

### Make an OSGi R5/OBR repository in addition

In addition to the P2 repository we extract OSGi meta data from the uploaded
bundles and render an OSGi R5/OBR repository.

 * Add the "OSGi" aspect
 * Add the "OBR repository" aspect
 * Check
 
### Use Package Drone for P2 meta data

Instead of using the P2 meta data from Tycho, we use the
OSGi extracted meta data and let Package Drone create the P2
meta data.

 * Add the "Tycho cleaner" aspect
 * Add the "P2 meta data" aspect
 * Clear channel -> deploy -> check

### Use the P2 repo ZIP instead of single artifacts

Instead of uploading single artifacts we change the process to
upload the P2 repository and create the repositories based on
its content.

 * Change the launch configuration to include the profile `onlyRepo`
 * clear channel -> deploy -> check

No luck .. content is not expanded:

 * Add the "P2 unzip" aspect
 * Check -> content (both P2 and OSGi R5/OBR)

### Don't trust Package Drone ... unzip!

 * Check: <http://localhost:8080/unzip/maven/latest-SNAPSHOT/tycho1/org.eclipse.packagedrone.ece2015/repo/content.jar>
 
This shows the file content of the "latest SNAPSHOT" with the
group id "org.eclipse.packagedrone.ece2015" and the artifact id "repo".
 
Also check <http://doc.packagedrone.org/book/unzip_adapter.xhtml> and
<https://github.com/ctron/package-drone/wiki/Unzip-Adapter>
for more information on the "Unzip Adapter".
 