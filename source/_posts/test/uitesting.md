---
title: cucumber
date: 2021-04-14 13:55:31
tags: cucumber
---

## What is BDD?
- TLD: Test Last Development (Coding -> Tests Creation)
- TDD: Test Driven Develoment (Tests Creation -> Coding)
- BDD: Behavior Driven Development 
  - BDD is an extension of TDD
  - a bahavior of the application
  - more user-focused
  - use human-readable description of user requirements
  - written in a shared language(tech non-tech stakeholders)
  - e.g. Gherkin(Cucumber provided)

- Gherkin will look like
```
Feature：
Scenario:
    Given 
    When
    And
    Then
```
- Tools for BDD: helps in Creating & Automating BDD user stories
 - Cucumber
 - JBehave
 - Behat

## Set a Cucumber Java Project
1. create a new maven project
2. add maven dependencies
  - Cucumber Java
  - Cucumber JUnit
  - JUnit
  - Selenium Java
3. create a folder features under /test/resources
4. create login feature under features
5. download plugins to Idea Plugins
  - Cucumber for Java
  - Gherkin
6. add content to feature
7. try to run feature file
8. add step definition / glue code under test/java package
9. create a runner class

## First Selenium Test
1. add maven dependiency
  - Selenium Java
2. create feature and add content
3. glue code
4. download browser driver
5. add selenium webdriver code
6. run feature and check execution

## Page Object Model
1. Designe pattern to create Object Repository
2. a class which created for each page to indentify web elements of that pag 
3. also contains methods to do action on the objects
4. seperate test objects and test scripts

### advantages
1. maintainability
2. usability
3. readability
4. easier faster reliable

## Page Factory [here](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/support/PageFactory.html)
1. a simple and easier implemtnation of POM in selenium
2. selenium's inbuild and optimize POM concept
3. as POM,has seperation of objects and test
4. use annotation @FindBy to find WebElements
 - @FindBy can use id,name,css,xpath,tagName,linkText,partialLinkText
 - @FindBy also can get element list
5. use method initElements to initialize web elements
 - on calling initElements method all objects in that page gets initialized
 - PageFactoy.initElements(driver,HomePage_PF.class) get `OutOfMemoryException`
 ```
 public HomePage_PF(WebDriver driver) {
     this.driver = driver;
     PageFactory.initElements(driver, this); //right use
 }
 ```
6. use @CacheLookup to instruct the initElements() method to cache element once its located and do that it will not be searched over and over again whenever calling it from any method
  - this works well with a basic web application
  - not recommended if you have Ajax applicaiton where DOM changes on user actions
  - in case ,you will get StaleElementExceptions,avoid using this
  - for Ajax application:
    - to handle loading time for element and to avoid '`NoSuchElementException`'
    - use AjaxElementLocatorFactory Class
    - timeout for a WebElement can be assigned to the Object page class with the help of this class
    ```
    PageFactory.initElements(new AjaxElementLocatorFactory(driver,30),this);
    ```

## Tags
1. Features and Scenarios can be marked by tags
2. in test runner we canrun specific tags
  - can run with single OR mutiples tags
  - can run with combination of tags or using AND OR NOT conditions
    - `"@smoke"`
    - `"@smoke or @regression"` 
    - `"@smoke and @regression"`
    - `"@smoke","@regression"`
    - `"@smoke and not @regression"`
  - can skip scnarios having specific tags
3. a feature or scenarios can have mutiples tags
4. tags can be placed above the following Gherkin elements:
  - Feature
  - Scenario
  - Scenario Outline
  - Examples
  - not possible to place tags above Background or steps(Given,When,Then,And,But)
5. create commands with tags combination as required to be run from command line
  - `mvn test -Dcucumber.filter.tags="@smoke and @regression"`

## Hooks
1. Blocks of code that runs before OR after each scenarios
2. Hooks in Cucumber are like Listeners in TestNG
3. can define hook by using annotations @Before @After
- Scenario Hooks - run before and after each scenarios
- Step Hook - run before and after each step
- Condition Hooks - hook asscociated with tags for condition execution
4. Why to use Hooks
 - to manage the setup and teardown
 - to avoid rewriting the common setup or teardown actions
 - allow better management of code workflow
5. `@Before @After @BeforeSteps @AfterSteps @After(value="@smoke",order=2)`

## Backfround
1. a step or a grounp of steps that are common to all the scenaiors in a feature
2. is defined once in the feature
3. runs before every scenario of the feature
4. why use?
  - to avoid repeating the common steps
  - for better readability & maintainance
  - unlike hoooks , background is vixible to the readers of the feature

## Run form commoand line
 1. What 
 - run your test or features from command line or terminal without using IDE or GUI
   - Command
   - Terminal
   - Console
2. Why use
  - no dependency on IDE or GUI
  - useful in integration with other processes
    - Continuous  Integration
    - Delivery and Deployment
  - Easier & Faster
  - consumes less memory
3. When
  - whenever fast run
  - whenever need to integration with other processes CI CD DevOps
  - whenever using CI tools like Jenkins
  - whenever you need any batch or scheduled execution
  - whenever you are done with your test creation and setup
4. How
  - `mvn test` 
  - `mvn test -Dcucumber.options --help` use help of cucumber
    - `mvn test -Dcucumber.options="feature file path"`
    - `mvn test -Dcucumber.options="feature file path:7"`
    - `mvn test -Dcucumber.options="--tags @smoke"`
    - `mvn test -Dcucumber.options="--plugin html:target/HtmlReports"`
  - `mvn test -Dcucumber.options="" -Dcucumber.options=""`

## HTML Report
1. How - maven cucumber reporting
 - add maven cuucmber reporting dependency
 - add the build plugins in pom.xml
 - [`mvn clean test` + `mvn verify -DskipTests` = `mvn clean verify`](https://stackoverflow.com/questions/51257224/maven-cucumber-reporting-plugin-is-not-generating-the-report-nothing-happens)
