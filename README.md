# Using ArcheTypes

This tutorial is based on http://www.luckyryan.com/2013/02/15/create-maven-archetype-from-existing-project/ and creates an archetypes from an existing Mule project. 

## Step 1 - Create your Mule Project
Create your standard Mule project as you would normally do. Ensure you are using properties as opposed to hard coding configuration within you application.

## Step 2 - Create the Archetype (from Mule Project)
Go to your Mule Project root folder and run the mvn create archetype command.

````
cd $workspace/<muleproject>
mvn archetype:create-from-project
````
This will generate the archetype in `target/generated-sources/archetype` 

## Step 3 - Configure Archetype

Copy the generated archetype source to a new dir and add the relevant configuration properties.
e.g.

````
mkdir -p $workspace/my-archetypes/<mule-project>-archetype
cd $workspace/my-archetypes/<mule-project>-archetype
cp -r $workspace/<muleproject>/target/generated-sources/archetype .
````

#### Add archetypes properties
Edit `src/test/resources/projects/basic/archetype.properties` and add archetype properties. 

e.g.
````
source-path=/path/
target-path=/path/
xslt-path=/path/myxslt.xslt
````

#### Update app.properties
Open the application properties file and replace the property values with archetype properties that mvn will substitute when your archetype instance is generated.

Edit `src/main/resources/archetype-resources/src/main/app/mule-app.properties` or all property files.
e.g.
````
source-path=${source-path}
target-path=${target-path}
xslt-path=${xslt-path}
````

#### Prompt for these required properties 
Edit `src/main/resources/META-INF/maven/archetype-metadata.xml` and add the properties you want to prompt for entry
e.g.
````
<requiredProperties>
  <requiredProperty key=“source-path”/>
  <requiredProperty key=“target-path”/>
  <requiredProperty key=“xslt-path”/>
</requiredProperties>
````

## Step 4 Install archetype into repository
This assumes a local install to your .m2 repo. In the root directory for your archetype run mvn install
````
mvn install
````

## Step 5 Generate archetype instance (project)
You can now create an instance of that archetype in a working folder.

e.g.
````
cd <your-workspace>
mvn archetype:generate -DarchetypeGroupId=com.mands -DarchetypeArtifactId=ms-simplefile-archetype -DarchetypeVersion=1.0.0-SNAPSHOT -DarchetypeCatalog=local -DgroupId=com.mands -DartifactId=filetransfer -Dversion=1.0.0-SNAPSHOT -Dpackage=com.mands -Dsource-path=/Users/sameerpattni/Mule/MandS/source -Dtarget-path=/Users/sameerpattni/Mule/MandS/target -Dxslt-path=/Users/sameerpattni/Mule/MandS/xslt/myxslt.xslt
````

