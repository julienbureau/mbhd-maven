## MultiBit HD Maven FORKED for trezor-ssh-agent application

A Maven staging repository for use with automated build tools. This allows for faster releaes cycles
that do not depend on Maven Central.

### Configuring your downstream projects to use this repo

To allow Travis builds that use Maven artifacts that are not in Maven Central, provide the following
entry into your parent POM:

```xml
 <repositories>
        <!-- Define the MultiBit staging repository for releases and snapshots -->
        <!-- Use https://raw.github.com to provide a consistent result -->
        <repository>
            <id>mbhd-maven-release</id>
            <url>https://raw.github.com/martin-lizner/mbhd-maven/master/releases</url>
            <releases/>
        </repository>
        <repository>
            <id>mbhd-maven-snapshot</id>
            <url>https://raw.github.com/martin-lizner/mbhd-maven/master/snapshots</url>
            <!-- These artifacts change frequently during development iterations -->
            <snapshots>
                <updatePolicy>always</updatePolicy>
            </snapshots>
        </repository>

    </repositories>
```

### Internal instructions for creating maven repo
* too lazy to write it elsewhere :-)

1. Pull multibit-hardware project, do code changes specific to trezor-ssh-agent
2. Change version - e.g. ```<version>0.8.1</version>```
  * core\pom.xml
  * pom.xml - mbhd-maven-release repository should point to martin-lizner
  * trezor\pom.xml and keepkey\pom.xml - dont forget to change ref to core dependency as well
3. Do maven magic:
```
mvn -DaltDeploymentRepository=release-repo::default::file:../mbhd-maven/releases clean deploy
```

### Credits
* MultiBit




