# TestNG
---------
# Interview Questions and Answers on TestNG Framework
-----------------------------------------------------

## 1. What is TestNG (or) What do you mean by TestNG
TestNG is an automation testing framework in which NG stands for “Next Generation”. TestNG is inspired by JUnit which uses the annotations (@). TestNG overcomes the disadvantages of JUnit and it is designed to make end-to-end testing easy.

Using TestNG, you can generate a proper report, and you can easily come to know how many test cases are passed, failed, and skipped. You can execute the failed test cases separately.

## 2. Advantages of TestNG

- TestNG provides **parallel execution** of test methods
- It allows to define **dependency** of one test method over other method
- It allows to assign **priority** to test methods
- It allows **grouping** of test methods into test groups
- It has support for **parameterizing** test cases using @Parameters annotation
- It allows **data driven testing** using @DataProvider annotation
- It has different **assertions** that helps in checking the expected and actual results
- Detailed (HTML) **reports**

### Advantages of TestNG over JUnit
There are three major advantages of TestNG over JUnit:

- **Annotations are easier** to understand
- Test cases can be **grouped** more easily
- **Parallel testing** is possible

## 3. What are the Annotations in TestNG

### 1. BeforeSuite
The annotated method will be run **before all tests in this suite have run**.
### 2. BeforeGroups
The list of groups that this configuration method will run before. This method is guaranteed to run shortly before the first test method that belongs to any of these groups is invoked.
### 3. BeforeTest
methods under @BeforeTest annotation will be executed prior to **the first test case in the TestNG file**.
### 4. BeforeClass
The annotated method will be run **before the first test method in the current class is invoked**.
### 5. BeforeMethod
methods under @BeforeMethod annotation will be executed prior to **each method in each test case**.
### 6. Test
The annotated method is a **part of a test case**. By default, methods annotated by @Test are executed **alphabetically**. 
### 7. AfterMethod
methods under @AfterMethod annotation will be executed **after each method in each test case**.
### 8. AfterClass
The annotated method will be run **after all the test methods in the current class have been run**.
### 9. AfterTest
methods under @AfterTest annotation will be executed **after all test cases in the TestNG file are executed**.
### 10. AfterGroups
The list of groups that this configuration method will run after. This method is guaranteed to run shortly after the last test method that belongs to any of these groups is invoked.
### 11. AfterSuite
The annotated method will be run **after all tests in this suite have run**.
### 12. DataProvider



## 4. Order of testng.xml file tags from Parent to Child and Structure of testing.xml file
	<?xml version="1.0" encoding="UTF-8"?>
	<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
	<suite name="TestNG Sample Test Suite">
	  <test name="TestNG Sample Test">
	    <groups>
	      <define name="include-groups">
	        <include name="sanity" />
	        <include name="integration" />
	      </define>
	      <define name="exclude-groups">
	        <include name="pass" />
	        <include name="fail" />
	      </define>
	      <run>
	        <include name="include-groups" />
	        <exclude name="exclude-groups" />
	      </run>
	    </groups>
	    <classes>
	      <class name="com.groups.TestNGGroupsExample" />
	    </classes>
	  </test>
	</suite>

## 5. How to Create testng.xml file and How to run
- Right-click on the project folder → go to New and then select 'File'.
- In the New file wizard, add the filename as 'testing XML' and click on the Finish button.
- After this, it will add an XML file below the project folder.
- Write the below code: <suite name="Testing">


## 6. What is the importance of testng.xml


## 7. How to pass parameters through testng.xml file to test case


## 8. What is TestNG Assert and list out common TestNG Assertions (Usefull Methods in Assert Class)
Asserts helps us to verify the conditions of the test and **decide whether test has failed or passed**. Some of the common assertions are:
– Assert.**assertEqual**(String actual,String expected)
– Assert.**assertTrue**(condition)
– Assert.**assertFalse**(condition)

## 9. What is Soft Assertion in TestNG
Soft Assert collects errors during @Test is running. They **don't throw an exception when an assert fails**. The **execution will continue** with the next step after the assert statement.

If you need/want to throw an exception (if such occurs) then you need to use **assertAll**() method as a last statement in the @Test and test suite again continue with next @Test as it is.

Unlike Hard Results, for Soft Asserts we need to **create an object in order to use** them.

	SoftAssert softassert = new SoftAssert();
	softassert.assertEquals("actual","expected","message");
	softassert.assertEquals("actual","expected","message");
	softassert.assertEquals("actual","expected","message");
	softassert.assertAll();

## 10. What is Hard Assertion in TestNG
Hard Assert is used when you want to halt the execution of the test script (or test method) when the assert condition does not match with the expected result.

	Assert.assertEqual(String actual,String expected, String message);
	Assert.assertTrue(condition);
	Assert.assertFalse(condition);


## 11. What is Exception Test in TestNG


## 12. How to set Testcase priority in TestNG

We can prioritise the Testcases by giving the attribute priority with a value in the Test annotation.
the lesser the priority value the higher the priority.

## 13. What is Perameterized testing in TestNG


## 14. How can we create Data driven framework using TestNG


## 15. How to run Group of testcases using TestNG


## 16. How to create Group of groups in TestNG


## 17. How to run testcases in parallel using TestNG


## 18. How to exclude a particular test method from test execution


## 19. How to exclude a particular test group from a testcase exection


## 20. How to Disable a testcase in TestNG


## 21. How to skip @Test method from execution in TestNG

We can skip Test methods in 3 ways:

- we can write an attribute in @Test annotation to skip that particular method: **enabled = false**
- we can write hard skip by using SkipException class with message
	**throw new SkipException("customMessage");**
- we can write conditional skip by using SkipException class
	**if(true){
		// execute the test
	}
	else{
		// don't execute
		throw new SkipException("customMessage");
	}**

## 22. How to ignore a testcase in TestNG


## 23. How TestNG allows to state dependancies


## 24. What are the different ways to produce the reports for TestNG Results


## 25. What is the use of @Listener annotation in TestNG

### 1. ITestListener

### 2. IReporter

## 26. How to write regular expressions in testng.xml for search @Test methods containing "smoke" keyword


## 27. What is the time unit that we specify in the test suits and testcases


## 28. Ways to invok the TestNG


## 29. How to run TestNG with Command Line


## 30. What is the use of invocationCount in TestNG


## 31. What is the use of threadPoolSize in TestNG


## 32. What is the use of timeOut in TestNG


## 33. What are @Factory and @DataProvider annotations


