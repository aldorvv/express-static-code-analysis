# Express static code analysis

A super simple, easy-to-mount, self-hosted static code analyzer.

**Prerequisites**

- [Docker](https://docs.docker.com/get-docker/)
- [docker-compose](https://docs.docker.com/compose/install/)


## Setup

This project consists of two parts, a [SonarQube server](https://docs.sonarqube.org/latest/setup/install-server/)
and a [SonarScanner](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)

In order to get the Scanner running, you will need to setup te server first.


## Server

After clonning this repository, open a new terminal and run:
```bash
$ cd ./server/
$ docker-compose up -d
```

Then, open a new browser and navigate to `http://localhost:8888` you should see a login page like this
![sonarserver login page](https://github.com/aldorvv/static-assets-bucket/raw/main/express-static-code-analyzer/login.png)

SonarServer default credentials are
 - User: admin
 - Password: admin

Don't worry, the nex step is to change the password.

Once you created a new, super-safe password, let´s go to create a new project, select "Manually" option.

![sonarserver create project](https://github.com/aldorvv/static-assets-bucket/raw/main/express-static-code-analyzer/manage-project.png)


Now, choose a new name for your project, after naming your project, select "Locally" in the next screen.

![sonarserver repo management](https://github.com/aldorvv/static-assets-bucket/raw/main/express-static-code-analyzer/manage-repo.png)

We are almost there! Create a new login token, keep it safe, we will use it later.

![sonarserver token admin](https://github.com/aldorvv/static-assets-bucket/raw/main/express-static-code-analyzer/create-token.png)


That's it! Now, lets setup the SonarScanner

## Scanner

On this project, open a new terminal, and copy all the project files you want to analyze within `scanner/src` using:

```bash
$ cp -r /path/to/your/project/* scanner/src/
```


Now, create a file within the `scanner/src/` folder named `sonar-project.properties` you can use the `sonar-project.properties.template` file as an example.


Setup a name for your code analysis, please be descriptive, I highly recommend to use the reporsitory's name and the tag that you are using.


After that, create a `.env` file within `scanner/` you can use the `.env.template` file as an example
Fill the environment variables on your all new `.env` file.


And that's it!

## Running Scan

Open a new terminal and run:

```bash
$ cd ./scanner/
$ docker-compose run --build
```