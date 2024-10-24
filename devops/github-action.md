# Set up new GitHub Actions workflow

## Created in branch main

    1. Action tab
    2. New workflow
    3. Choose the template
    4. Adjust then commit

## Created in branch feature

    1. mkdir .github/workflows
    2. Create .yml workflow file. Ex: maven.yml
    3. Adjust then commit

## .yml file examples

    Remember to add application.properties to test folder if not public it file, then use github secrets to store the serects varibles
    Setting -> Secrets and Varibles -> Action ->

```yml
name: Java CI with Maven

on:
  push:
    branches: ["*"]
  pull_request:
    branches: ["*"]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout the repository
      - uses: actions/checkout@v4

      # Step 2: Set up JDK 17
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: "17"
          distribution: "temurin"
          cache: maven

      - name: Set environment variables
        run: |
          echo "EMAIL_USERNAME=${{ secrets.EMAIL_USERNAME }}" >> $GITHUB_ENV
          echo "EMAIL_PASSWORD=${{ secrets.EMAIL_PASSWORD }}" >> $GITHUB_ENV

      # Step 3: Build and run tests with Maven
      - name: Build and Test with Maven
        run: mvn -B clean install --file pom.xml # This ensures the tests are run
```
