pipeline {
    agent any


    tools {
        maven 'Maven'
    }


    stages {
        stage('Create Maven Project') {
            steps {
                echo 'Creating Java Maven project...'


                bat 'if not exist src\\main\\java mkdir src\\main\\java'


                writeFile file: 'pom.xml', text: '''<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>myapp</artifactId>
    <version>1.0</version>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
</project>
'''


                writeFile file: 'src/main/java/App.java', text: '''public class App {
    public static void main(String[] args) {
        System.out.println("Hello from Maven and Jenkins!");
    }
}
'''
            }
        }


        stage('Build') {
            steps {
                echo 'Building Java application using Maven...'
                bat 'mvn -version'
                bat 'mvn clean package'
            }
        }


        stage('Test') {
            steps {
                echo 'Checking generated JAR file...'
                bat 'dir target'
            }
        }


        stage('Deploy') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar',
                                 allowEmptyArchive: false


                echo ' application built and archived successfully!'
            }
        }
    }
}
