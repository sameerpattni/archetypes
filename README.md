# Using ArcheTypes

This tutorial is based on http://www.luckyryan.com/2013/02/15/create-maven-archetype-from-existing-project/ and creates an archetypes from an existing Mule project. 

## Step 1 - Create your Mule Project
Create your standard Mule project as you would normally do. Ensure you are using properties as opposed to hard coding configuration within you application.

## Step 2 - Creating the Archetype
Go to your Mule Project root folder and run the mvn create archetype command

````
cd $workspace/<muleproject>
mvn archetype:create-from-project
````
This will generate the archetype in `target/generated-sources/archetype` 

## Step 3 - Configure Archetype

Copy the generated archetype source to a new dir and add the relevant configuration properties.

#### Add properties
Edit `src/test/resources/projects/basic/archetype.properties` and add your own properties. 
e.g.
````
source-path=/path/
target-path=/path/
xslt-path=/path/myxslt.xslt
````

#### Prompt for required properties
Edit `src/main/resources/META-INF/maven/archetype-metadata.xml` and add the properties you want to prompt for entry
e.g.
````
<repositoryProperties>
  <repositoryProperty key=“source-path”/>
  <repositoryProperty key=“target-path”/>
  <repositoryProperty key=“xslt-path”/>
</repositoryProperties>
````
