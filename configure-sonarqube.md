# Configuring SonarQube

## SonarQube Token : `fc2dc9876ba6abf9e64306cd720e71be29219bc5`

### Step 1 : Install SonarLint VSCode extension

### Step 2 : 
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


### Step 3 : Configure Workspace to use sonarqube

Next, we need to configure your project workspace to allow it to scan the appropriate SonarQube project.

You'll need the **Project key** , contact sonarqube server maintainer to get the project key.

Next, we need to configure your project workspace to allow it to scan the appropriate SonarQube project.

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

We now need to update the SonarLint bindings for the workspace to ensure the rules are in-sync locally and on the server.

Again, hit `Ctrl + Shift + P` to open the command palette. Then enter `SonarLint: Update all bindings to SonarQube/SonarCloud` and select. You should see the following message on the bottom right of VS Code once complete.


### Step 4 : Run sonar-scanner

If already not installed, install `sonar-scanner` locally.

```
sonar-scanner.bat -D"sonar.projectKey=<yourprojectkey>" -D"sonar.sources=." -D"sonar.host.url=http://13.126.86.18/sonarqube" -D"sonar.login=fc2dc9876ba6abf9e64306cd720e71be29219bc5
```
