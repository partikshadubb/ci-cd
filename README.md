CI/CD with GitHub Actions for React Native
This repository demonstrates how to set up CI/CD using GitHub Actions for a React Native project. The workflow is triggered on every push to the main branch.
Workflow YAML File
The following is the content of the YAML file (.github/workflows/build-android.yml) that defines the GitHub Actions workflow:


yaml

name: "Build Android app"

on:
  push:
    branches: [main]
    # can add push and pull_request here 

jobs:
  build-android:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Run Yarn Install
        run: |
             yarn install  

      - name: Build application
        run: |
             cd ./android &&
             ./gradlew assembleRelease  
             
      - name: Upload Release Build to Artifacts
        uses: actions/upload-artifact@v3
        with:
           name: release-artifacts.apk
           path: |
            android/app/build/outputs/apk/release/
            retention-days: 3

Explanation of YAML Keywords
* name: Specifies the name of the workflow.
* on: Defines the events that trigger the workflow. In this case, it is triggered on every push to the main branch.
* jobs: Contains the list of jobs to be executed as part of the workflow.
* build-android: The name of the job, which can be customized.
* runs-on: Specifies the operating system and version on which the job should run. In this case, it is set to ubuntu-latest.
* steps: Contains the list of steps to be executed as part of the job.
* Checkout repository: Uses the actions/checkout action to clone the repository into the runner environment.
* Run Yarn Install: Runs the command yarn install to install project dependencies.
* Build application: Changes the directory to ./android and executes the Gradle command ./gradlew assembleRelease to build the Android application.
* Upload Release Build to Artifacts: Uses the actions/upload-artifact action to upload the release APK file as an artifact.
    * name: Specifies the name of the artifact.
    * path: Specifies the path to the release APK file.
    * retention-days: Sets the number of days the artifact should be retained.
Setting Up CI/CD
To set up CI/CD using GitHub Actions for your React Native project, follow these steps:
1. Create a new repository or use an existing one on GitHub.
2. Initialize a basic React Native project in the repository.
3. Create a new file named .github/workflows/build-android.yml.
4. Copy the contents of the YAML file mentioned above into build-android.yml.
5. Commit and push the changes to the main branch.
6. GitHub Actions will automatically detect the workflow and start executing it whenever there is a push to the main branch.
7. The workflow will build the Android application, and the release APK file will be uploaded as an artifact.
You can customize the workflow file according to your project's specific requirements, such as adding additional steps, including tests, deploying to various platforms, etc.