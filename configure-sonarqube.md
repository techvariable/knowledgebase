# Configuring SonarQube

> SonarQube Token : `fc2dc9876ba6abf9e64306cd720e71be29219bc5`

> SonarQube Server URL : http://13.126.86.18/sonarqube

### Step 1 : Install SonarLint VSCode extension

### Step 2 : Install Sonar-scanner and add the path to the environment variable

### Step 3 : 
Once installed, restart or reload VS Code to ensure it's taken effect.

If SonarLint can't detect a JAVA JRE on your system, it will prompt you to download one. Let it download if required.

Once VS Code is up and running again, hit `Ctrl + Shift + P` to open the command palette. Then enter `Preferences: Open Settings (JSON)` and select to open up your settings.

To get SonarLint working, you need to specify the following settings.

```
"sonarlint.connectedMode.connections.sonarqube": [
    { 
        "connectionId": "sonar", // id of your sonarqube server
        "serverUrl": "http://13.126.86.18/sonarqube", // url of your sonarqube server
        "token": "XXXX" // token to authenticate with sonarqube
    }

],
"sonarlint.pathToNodeExecutable": "C:\\\\Program Files\\\\nodejs\\\\node.exe", // path to your node.js installation if analyzing Javascript/Typescript
```


### Step 4 : Configure Workspace to use sonarqube

Next, you need to configure your project workspace to allow it to scan the appropriate SonarQube project.

You'll need the **Project key** , contact sonarqube server maintainer to get the project key.

Next, you need to configure your project workspace to allow it to scan the appropriate SonarQube project.

In VSCode hit `Ctrl + Shift + P` to open the command palette. Then enter `Preferences: Open Workspace Settings (JSON)` and select to open up your workspace settings.

To get SonarLint working, you need to specify the following settings.

```
{
  "sonarlint.connectedMode.project": {
    "connectionId": "sonar", // should be same connectionId you defined above
    "projectKey": "XXXX" // Replace with project key you grabbed from SonarQube server
  }
}
```

You now need to update the SonarLint bindings for the workspace to ensure the rules are in-sync locally and on the server.

Again, hit `Ctrl + Shift + P` to open the command palette. Then enter `SonarLint: Update all bindings to SonarQube/SonarCloud` and select. If binding fails, proceed to the next step.


### Step 5 : Configure your project
Create a configuration file in your project's root directory called `sonar-project.properties`
> Note : The configuration file will differ from project to project. This is a example file. Please configure it based on your project
```
sonar.projectKey=<projectKey>

sonar.host.url=http://13.126.86.18/sonarqube

sonar.login=fc2dc9876ba6abf9e64306cd720e71be29219bc5
# defaults to project key
sonar.projectName=<ProjectName>
# defaults to 'not provided'
#sonar.projectVersion=1.0
 
# Path is relative to the sonar-project.properties file. Defaults to .
# For all sources
#sonar.sources=.
# For /src
sonar.sources= src/
# To exclude files
sonar.exclusions = node_modules/
 
# Encoding of the source code. Default is default system encoding
#sonar.sourceEncoding=UTF-8
```

### Step 5 : Run sonar-scanner

If already not installed, install `sonar-scanner` locally.

```
sonar-scanner
```
