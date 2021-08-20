# Bukkit-Plugin-Tutorial
This is my tutorial for creating Minecraft Bukkit plugins using Eclipse IDE

# Don't worry, I'm still in progress!


# 1. Install and prepare your IDE.

I'll use Eclipse for this tutorial. You can install it here: https://www.eclipse.org/downloads/

Once you've your Java IDE installed, make sure you have the m2e plugin (https://github.com/eclipse-m2e/m2e-core/blob/master/README.md#-installation)

# 2. Creating the project.

Now we need a project to work with. To create one, you need to go to File > New > Project...

![image](https://user-images.githubusercontent.com/47731321/130196077-b61b2064-34d0-498d-8bc3-151651e53919.png)

Select *Maven Project* option:

![image](https://user-images.githubusercontent.com/47731321/130196660-ecee9cc7-9005-4d50-ac71-2f496d102ba1.png)

Put a tick into the "Create a simple project" box and click next:

![image](https://user-images.githubusercontent.com/47731321/130196909-09e97946-28ad-4636-89ef-4e9c3eb22f48.png)

Now, we need to fill in some information about our project.

Let's start with Group Id, there are a few options:
1. Use your domain name. For domain example.com, your Group Id will be _com.example_. If you don't have one, use GitHub Pages (https://pages.github.com/). For GitHub Pages it will be _io.github.username_.
2. If you are lazy, you can use your email. For email _example@mail.com_ it looks like _com.mail.example_.
3. Don't like those two options? Just use _me.<some_name>_
By the way, your Group Id must _not_ begin with:
- org.bukkit
- net.bukkit
- com.bukkit
- com.mojang
- net.minecraft

Once we are done with it, we need to specify the Artifact Id. It's simple, just use your plugin's name.

So, you will have something like that:

![image](https://user-images.githubusercontent.com/47731321/130200193-9734da44-736a-4aaf-8bc1-a795aa4a5d87.png)

Click the "Finish" button to create the project!

![image](https://user-images.githubusercontent.com/47731321/130201324-36cbce71-089a-451d-b05b-1e60065d1cf9.png)

# 3. Bukkit API

Open pom.xml by double-clicking on it. 

![image](https://user-images.githubusercontent.com/47731321/130202246-2ed67ead-b95b-456d-9160-44edbe30e2f2.png)

If you are using Java 6+, you need to specify it here. Just paste this code before </project> line:
~~~
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>2.3.2</version>
          <configuration>
            <source>1.16</source>
            <target>1.16</target>
          </configuration>
      </plugin>
    </plugins>
  </build>
~~~

I am using Java 16, so just replace 16 with your version.

Now we need to specify the Bukkit repository. As we can see, it's down (http://repo.bukkit.org/content/groups/public/), so we'll use the Spigot repository instead. Don't worry, we'll be able to use it as the former of Bukkit repo. Again, paste this code before </project> line:
~~~
  <repositories>
    <repository>
      <id>spigot-repo</id>
      <url>https://hub.spigotmc.org/nexus/content/repositories/public/</url>
    </repository>
  </repositories>
~~~

And, finally, let's paste some dependencies before </project> line:
~~~
  <dependencies>
    <dependency>
      <groupId>org.spigotmc</groupId>
      <artifactId>spigot-api</artifactId>
      <version>1.12.2-R0.1-SNAPSHOT</version>
      <type>jar</type>
      <scope>provided</scope>
    </dependency>
  </dependencies>
~~~
Change the 1.12.2-R0.1-SNAPSHOT to the version you want. The list of versions is here: https://hub.spigotmc.org/nexus/#nexus-search;gav~org.spigotmc~spigot-api~~jar~~kw,versionexpand

As a result, you should see something similar:

![image](https://user-images.githubusercontent.com/47731321/130212944-2331a2d4-c2e9-46e9-bc1b-c11b0214088b.png)

Now, press Ctrl + S to save the file and give it a few minutes to download and install all dependencies.

# 4. Enable Javadoc

Javadoc helps you while you are coding, and it will be better to enable it for the Spigot repo. To do so, right-click your project in package explorer > Properties > Javadoc Location and copy the link https://hub.spigotmc.org/javadocs/spigot/, then press Apply and Close.

![image](https://user-images.githubusercontent.com/47731321/130214014-3f62d709-219d-47c3-a005-66c3cff76a8f.png)

# 5. Creating plugin's package and class

Right-click src/main/java > New > Package

![image](https://user-images.githubusercontent.com/47731321/130216274-0983dfe3-8082-431b-9dae-786e93738c63.png)

Put <GroupId>.<ArtifactId> into "Name" field.

![image](https://user-images.githubusercontent.com/47731321/130216792-30de5509-5eb6-4dcf-b249-d9acf3dc3f23.png)

Now, let's create a class inside of a package. Right-click the package you've created before and click New > Class

![image](https://user-images.githubusercontent.com/47731321/130217903-1c8d3e8d-21c5-4e75-9d3c-ff0f857fa1db.png)

Put your Artifact Id as a name of a class. Make sure your class looks like this:

![image](https://user-images.githubusercontent.com/47731321/130227288-79769ed0-495f-4a61-8a3e-d8d00b3f527c.png)

# 6. Create plugin.yml

Create plugin.yml by right-clicking on project > New > File and specify plugin.yml as the name.

Now, open it and write this:
~~~
name: <PluginName> 
main: <PackageName>.<MainClass>
version: 0.0.1
~~~
Where <MainClass> is the name of the class we've created.

Example:
![image](https://user-images.githubusercontent.com/47731321/130227477-3ebaaa63-1230-4362-a7d1-145d04df8120.png)

#7. Build

To make a .jar file from plugin source code, you need to right-click projet > Export > JAR File and enter the name of a plugin JAR file.
  
![image](https://user-images.githubusercontent.com/47731321/130228197-30c9b35d-ff3b-4a22-835e-2132dbc19300.png)

### _*From here, your plugin can be loaded by the server. To check if you've done everything properly, simply start a Spigot/Bukkit server with a plugin's JAR file in the "plugins" directory and check the logs. You should see something like this:*_

![image](https://user-images.githubusercontent.com/47731321/130228733-f1500ebd-7293-42a4-8699-a7c8d37aca5a.png)

### Congratulations, you've created your own Spigot/Bukkit Minecraft plugin!
