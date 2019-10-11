# Minecraft Mod - Hello World

A quick run through of setting up vscode on windows to develop a new minecraft mod.

## Setup Environment
1) install\update `vscode` 1.39.1 was latest for me.
1) install these plugins: [vscode-java-pack](vscode:extension/vscjava.vscode-java-pack) (which includes `Debugger for Java`, `Java Dependency Viewer`, `Java Extension Pack`, `Java Test Runner`,  `Language Support for Java(TM) by Red Hat`), `Markdown Preview Gitgub Styling`, `Visual Studio Intellicode`, `Gradle Language Support`, `Better TOML`.  [See here for recommended plugins](https://code.visualstudio.com/docs/languages/java)
1) install this plugin `Minecraft JSON Schemas`
1) Install chocolatey
1) `choco install gradle -g` 5.6.2 was latest for me.  It takes a long time to install, just wait for it to say _Chocolatey installed 1/1 packages._
1) `choco install openjdk13 -g` 13.0.33 was latest for me.

## Setup New Minecraft Mod Project
Firstly, take a look at the [docs](https://mcforge.readthedocs.io/en/1.13.x/gettingstarted/)

### Downloading Minecraft Assets
1) [Download v1.14.4](https://files.minecraftforge.net/), unzip the files and copy `build.gradle` and `\src\` to the root directory of your repo. 
1) Open vscode to the root of your repo
1) Open a vscode terminal window and run `gradle build`

### Code and That
1) In `build.gradle` find the line that starts `group = `, and replace it with a domain you own in reverse, followed by package identifier e.g. `dev.mikemcmillan.modid`
1) Comment out the line `apply plugin: 'eclipse'`

### Build it
Clean and build: `gradle clean build`

### Run it
Tip: You can run `gradle tasks` to output all tasks available.  Such as `runserver`:

1) `gradle runserver`  This will download a whole bunch of minecraft assets. ... this failed for me at the :runserver step.  This may or may not be needed.
1) `gradle runclient` This appears to launch minecraft.  Swish.

### Change the Mod Name
Note that the ModId doesn't allow symbols!

In `\build.gradle`
1) change `args '--mod', 'examplemod'` to `args '--mod', 'mikesmod'`
1) change `Specification-Title` to `"mikesmod"`
1) change `group` to `group = 'dev.mikemcmillan.mikesmod'`
1) change `archivesBaseName` to `archivesBaseName = 'mikesmod'`

In `\src\main\resources\META-INF\mods.toml` 
1) change `displayName=` to `displayName="Mikes Mod"`
1) change `modId=` to `modId="mikesmod"`
1) change `[[dependencies.examplemod]]` to `[[dependencies.mikesmod]]`.  This is in 2 places.
1) change the multiline `description=` to `description="Mikes Hello World Mod"`
1) change `displayURL=` to `displayURL="http://mikemcmillan.dev"`

In `\src\main\java\com\example\examplemod\ExampleMod.java` 
1) change the @Mod annotation from `@Mod("examplemod")` to `@Mod("mikesmod")` 

In `\src\main\resources\pack.mcmeta`
1) change `description` to `"mikesmod resources"`

Open a terminal and run
1) `gradle clean build runclient`

### Commit to git
1) Sign the `\run\eula.txt`
1) Setup .gitignore to ignore build\run assets, and ensure we're not distributing mojang intellectual property!