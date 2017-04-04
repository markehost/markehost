---
layout: post
title: Updating Java on Mac OS X and IntelliJ 12
date: '2013-02-02 17:00:00'
---

Many blog and Stack Overflow posts are instructing users to set their <code>$JAVA_HOME</code> path within Terminal or by directly adding it to their <code>~/.bash_profile</code> file.  The highly esteemed [OJDX](http://ojdx.com) (author of [robe-and-wizard-hat](link:https://npmjs.org/package/robe-and-wizard-hat)) has informed me this is not the correct solution.  

The reason being, you may need to use multiple versions of Java on your machine for different projects.  Setting the <code>$JAVA_HOME</code> path will cause issues for projects using different versions of Java.  There is a reason in Mac OS X 10.7+ this path variable is not set and will show empty resuts when checking within Terminal.


### Upgrading Java on a Mac

If you're developing on your Mac you need to install the JDK, download the version you need directly from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).  In my case, I was upgrading from Java 6 to 7, and JDK 1.6 to 1.7.

Running the DMG file quickly installs everything you need Java Development.


### Updating Java Version within IntelliJ 12

You will only need to do this if your current project needs a different language and JDK version.

If you're using IntelliJ for a Java project you likely need to modify your Maven Runner settings.  Within the Maven Settings project settings, you will want to change the JRE used with the <code>Maven > Runner</code>. It will give you a list of options (Internal JDK, Use JAVA_HOME, Use Project JDK, etc) but the new JDK version you just installed is not available.

To add the new version of the JDK in IntelliJ go to <code>File > Project Structure > Platform Settings > SDKs</code>.  Click the <code>+</code> icon in the middle pane and navigate to the <code>Home</code> folder of the new JDK you installed.  Likely, it's in <code>/Library/Java/JavaVirtualMachines</code> which is where it was for me, but it could also be in your <code>System</code> directory.

##### Project SDK

This will now give us a new option in our Maven Runner JRE settings, but I wanted to change the default Project JDK within the Runner settings to 1.7 and also *needed* to upgrade the Language Level to 7.  

To do this add the new JDK within the <code>Project SDK</code>.  Again located in <code>File > Project Structure</code> but in <code>Project Settings > Project</code>. Change the Project SDK to 1.7 within the dropdown.  I also changed the language level to 7.0, in the dropdown below. 

Click OK.  Go back to your <code>Maven > Runner</code> settings.  The JRE dropdown should now include the option <code>Use Project SDK( version you added)</code>.  Click OK.  Build your project and you should be all set.  You should now see the new Java version path displayed immediately on top of the <code>Run</code> console whenever you run Maven.


### Extra

##### Check to See if You Have JDK

In Terminal type:

<code>/usr/bin/java</code>

Expect to see something like this:

	/usr/bin/java

##### Checking Your Version of Java

In Terminal type:

<code>java -version</code>

Expect to see something like this:

	java version "1.7.0_11"
	Java(TM) SE Runtime Environment (build 1.7.0_11-b21)
	Java HotSpot(TM) 64-Bit Server VM (build 23.6-b04, mixed mode)

##### Print the $JAVA_HOME Path

In Terminal type:

<code>echo $JAVA_HOME</code>

Expect to see something like this:

	<!-- In Mac OS X 10.7+ you should see a blank line -->


##### Set Your $JAVA_HOME Path in Terminal

In Terminal type:

<code>export JAVA_HOME=/Library/Java/Home</code>

This sets the path only for the session and could be set to a directoy other than that listed above.  Open or create a <code>~./.bash_profile</code>  file and enter the path into the file.  Then restart your machine for it to take affect.

	<!-- within .bash_profile -->
	JAVA_HOME=/Library/Java/Home


### Feedback

Let me know if you have trouble setting your Java or JDK version for IntelliJ.  It may be of help in the future to myself and others.