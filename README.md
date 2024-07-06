Guided LAB 309.3.1- SP2-Demonstration of Spring Boot with Thymeleaf  

Introduction
Thymeleaf is a server-side template engine for Java. It has built-in support for the Spring framework and is widely used in Spring-based projects.

This lab will demonstrate two examples of how to use Thymeleaf with a Spring Boot web application:

Rendering a Single Model Attribute.
Rendering a Collection.

Learning Objective: 
By the end of this lab, learners will be able to use Thymeleaf library in the Spring boot application.

Instructions
Create a Spring Boot Application
We will use the Spring Initializr web tool to create our project. Head over to http://start.spring.io and generate a project with the following details:
Group: com.example
Artifact: thymeleaf-tour
Dependencies: Web, Thymeleaf, Spring DevTools, lombok


After generating the project, you must have your project’s zip file. Unzip the file and import it into your favorite IDE. Once you load the project, you can see the below dependencies for Thymleaf in the Porm.xml file.

<dependencies>
  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-thymeleaf</artifactId>
  </dependency>
  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
  </dependency>

  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-devtools</artifactId>
     <scope>runtime</scope>
     <optional>true</optional>
  </dependency>

  <dependency>
     <groupId>org.projectlombok</groupId>
     <artifactId>lombok</artifactId>
     <optional>true</optional>
  </dependency>

  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-test</artifactId>
     <scope>test</scope>
  </dependency>
</dependencies>

<build>
  <plugins>
     <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <configuration>
           <excludes>
              <exclude>
                 <groupId>org.projectlombok</groupId>
                 <artifactId>lombok</artifactId>
              </exclude>
           </excludes>
        </configuration>
     </plugin>
  </plugins>
</build>


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <parent>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-parent</artifactId>
       <version>3.3.1</version>
       <relativePath/> <!-- lookup parent from repository -->
   </parent>
   <groupId>com.sam</groupId>
   <artifactId>ThymeLeaf_Tour</artifactId>
   <version>0.0.1-SNAPSHOT</version>
   <name>ThymeLeaf_Tour</name>
   <description>ThymeLeaf_Tour</description>
   <url/>
   <licenses>
       <license/>
   </licenses>
   <developers>
       <developer/>
   </developers>
   <scm>
       <connection/>
       <developerConnection/>
       <tag/>
       <url/>
   </scm>
   <properties>
       <java.version>17</java.version>
   </properties>
   <dependencies>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-thymeleaf</artifactId>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-web</artifactId>
       </dependency>


       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-devtools</artifactId>
           <scope>runtime</scope>
           <optional>true</optional>
       </dependency>
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
           <optional>true</optional>
       </dependency>
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
   </dependencies>


   <build>
       <plugins>
           <plugin>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-maven-plugin</artifactId>
               <configuration>
                   <excludes>
                       <exclude>
                           <groupId>org.projectlombok</groupId>
                           <artifactId>lombok</artifactId>
                       </exclude>
                   </excludes>
               </configuration>
           </plugin>
       </plugins>
   </build>


</project>

Example One: Rendering a Single Model Attribute.
To render an attribute, use ‘th:text’ attribute in Thymeleaf Template
Syntax → <p th:text="${attributeKey}"> 
Step 1: Defining a Controller
First, create a new package named “mycontroller,” and then create a new class named HomeController.java with the following code.

@Controller
public class HomeController{
   @GetMapping("/showflowerList")
   public String sendDataToHtml(Model model) {
   String[] flowers = new String[] { "Rose", "Lily", "Tulip", "Carnation", "Hyacinth" };

   String[] City = new String[] { "nyc", "nj", "dallas", "chicago", "philadelphia" };
    model.addAttribute("flowersVariable", flowers);
    model.addAttribute("CityVariable", City);
    return "viewFlowers";
   }
}


The above method will be invoked when http://localhost:8080/showflowerList is accessed.

Step 2: Creating a Thymeleaf Template
All server-side templates go into the src/main/resources/templates directory. Create a new HTML file called viewFlowers.html inside the template’s directory with the following code.

viewFlowers.html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
   <meta charset="UTF-8">
   <title>Title</title>
</head>
<body>
<table style="border: 1px solid black">
<tr th:each="showflowers: ${flowersVariable}">
   <td th:text="${showflowers}" />
</tr>
</table>

<table style="border: 1px solid black">
<tr th:each="showCity: ${CityVariable}">
   <td th:text="${showCity}" />
</tr>
</table>
</body>
</html>





<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
   <meta charset="UTF-8">
   <title>Title</title>
</head>
<body>
<table style="border: 1px solid black">
   <tr th:each="showflowers: ${flowersVariable}">
       <td th:text="${showflowers}" />
   </tr>
</table>


<table style="border: 1px solid black">
   <tr th:each="showCity: ${CityVariable}">
       <td th:text="${showCity}" />
   </tr>
</table>
</body>
</html>



Notice the use of the th:text directive in the template above. It is a thyme leaf attribute, and the value for a key sent from the controller is accessed using "${}" syntax.

Thymeleaf comes with a special attribute th:each, which is used to iterate over collections of different object types.


Step 3: Run and Test
 Type the following URLs in your browser to access inboxpage.html 
http://localhost:8080/showflowerList





Example Two: Rendering a Collection
To render a collection, use ‘th:each’ attributes in the Thymeleaf template.
Syntax
<p th:each="variable:${collectionName}"> 
   <span th:text=${variable}> items iterated will be placed here </span>
</p>

Note: <span> tag will be iterated as much as the number of collection items.

Step 1: Defining a Controller
Create a new class named TemplateController.java under the mycontroller package with the following code.

import java.util.ArrayList;
import java.util.List;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/")
public class TemplateController{

   @GetMapping("/ExampleTwo")
   public String template(Model model) {
       String message = "Top 5 Cloud Service Providers";
       // creating a collection
       List<String> list = new ArrayList<>();
       list.add("Amazon Web Services");
       list.add("Microsoft Azure");
       list.add("Google Cloud");
       list.add("Alibaba Cloud");
       list.add("IBM Cloud");
       model.addAttribute("message", message);
       // adding the collection attribute
       model.addAttribute("cloudProvider", list);
       return "DemoPage";
   }
}




Step 2: Creating a Thymeleaf Template
All server-side templates go into the src/main/resources/templates directory. Create a new HTML file called DemoPage.html inside the templates folder with the following code.

<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
   <meta charset="UTF-8">
   <title>Title</title>
</head>
<body>
<div id="one">
 <h2 th:text="${message}">
   <span>message will print here</span>
 </h2>
</div >


<div id="two" th:each="List:${cloudProvider}">
 <ul>
   <li>
     <span th:text=${List}>items will print here</span>
   </li>
 </ul>
</div>
</body>
</html>



HTML
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
   <meta charset="UTF-8">
   <title>Title</title>
</head>
<body>
<div id="one">
   <h2 th:text="${message}">
       <span>message will print here</span>
   </h2>
</div >




<div id="two" th:each="List:${cloudProvider}">
   <ul>
       <li>
           <span th:text=${List}>items will print here</span>
       </li>
   </ul>
</div>
</body>
</html>









Step 3: Run and Test
Type the following URLs in your browser to access DemoPage.html 
http://localhost:8080/ExampleTwo






