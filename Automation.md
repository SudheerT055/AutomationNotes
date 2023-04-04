# Automation Selenium With JAVA

## Selenium Components:

1. Selenium IDE
2. Selenium Webdriver( Introduced in Selenium-2)
3. Selenium Grid
4. Selenium RC ( Deprecated after Release of Selenium-3)

## Selenium Webdriver Architecture:

in Selenium 3 (3.8)- Json Wire protocol is used between Client libraries and Browser specific drivers.
in Json Wire protocol, Encoding and Decoding is done.
1. ChromeDriver - Google Chrome
2. GekoDriver - Firefox
3. EdgeDriver - MS Edge

from Selenium 4 (3.11) - W3C (World Wide Web Consortium) protocol is used between Client libraries and Browser specific drivers. and no need of encoding and decoding required.

## Useful Methods in WebDriver class:

1. driver.get(link) - navigate to the link url
2. driver.getTitle() - returns (String) Title of the webpage.
3. driver.getCurrentUrl - returns (String) Current URL of the webpage.
4. driver.getPageSource - returns (String) current webpage html source.
5. driver.findElement(By.id('id') | By.xpath("xpath") | By.name("name") | By.tagName("tag")) - returns (WebElement) webelement of the given element id, xpath or name etc...

### Finding the element in WebDriver FindElement method:
1. By.id('id')
2. By.xpath("xpath")
3. By.name("name") 
4. By.tagName("tag")
5. By.linkText("exact_text"); 
6. By.partialLinkText("text");

### Navigation methods in WebDriver class:
1. driver.navigate().back(); - Navigates to the last visited page.
2. driver.navigate().forward(); - Navigates to the forward visited page.
3. driver.navigate().refresh(); - Refreshes the current webpage.
4. driver.navigate().to(URL | String(link)); - navigates to the given link. (URL type or String type)

### Window Handling methods in WebDriver class:
1. driver.getWindowHandle(); // returns (String) the windowID of the current active window.
2. driver.getWidnowHandles(); // returns (Set< String >) the  windowID's of all opened windows. ParentID and then ChildID respectively.
3. driver.switchTo().window(windowID); //  window control will be send to given windowID
4. driver.close(); // current active window will be terminated(closed).
5. driver.quit(); // all the windows will be closed.


## Useful Methods in WebElement class:

1. webelement.clear() - clears the text present in the element.
2. webelement.sendKeys(String(Email)) - enters the string value in the element.
3. webelement.getText() - returns(String) the inner text of the element(The visible text of this element.).
4. webelement.getAttribute(String(href)) - returns (String) The attribute/property's current value or null if the value is not set.

5. webelement.isDisplayed() - returns (Bool) value of the element displayed on the screen or not.
6. webelement.isEnabled() - returns (Bool) value of the element is Enabled or not on the screen.
7. webelement.isSelected() - returns (Bool) value of the element is selected or not on the screen. 
8. webelement.getLocation() - returns (Point obj) top left-hand corner co-ordintes of the specified WebElement.  
9. webelement.getSize() - returns (Dimension obj) the size of a web element.

10. webelement.getCssValue("backgroundColor") - returns (String) the css value of the backgroundcolor for the element 

## Differance Between navigate().to() and get() method:

Functionally, there is no differance between navigate().to() and get() methods. but,
the only difference is get() method accepts String as parameter. but, navigate().to() method accepts String and URL instance as perameter.
## Differance Between findElement() and findElements():

1. FindElement returns only sigle element but, FindElements returns multiple elements
2. FindElement returns only first occurance of the many elements but, FindElements returns all the occurances of the elements.
3. FindElement throws **NoSuchElementException**, FindElements does not throw any exception.
4. FindElement returns **WebElement** but, FindElements returns **List< WebElement >**


## Use of SELECT class:

this is mostly commanly used for dropdown elements.
SELECT dropdownselect = new SELECT(dropdownelement);

dropdownselect.selectByVisibleText(String(text)); // selects the dropdown option based on the visible text.
dropdownselect.selectByValue(String(text)); // selects the dropdown option based on the value attribute.
dropdownselect.selectByIndex(int(index)); // selects the dropdown option based on the index (starts from 0).
dropdownselect.getOptions(); // returns (List< WebElement >) list of all the options available in the dropdown.

## Usefull methods from Collections class:

Collections.sort(ArrayList(list)); // sort the collection in alphabetical order/ascending order and stored in the same variable(list).

## Usefull methods in Keys class:

1. Keys.ARROW_DOWN // down arrow button click will be sent to the browser.
2. Keys.ARROW_UP //   up arrow button click will be sent to the browser.
3. Keys.ARROW_LEFT // left arrow button click will be sent to the browser.
4. Keys.ARROW_RIGHT // right arrow button click will be sent to the browser.
5. Keys.chord(Keys.CONTROL,Keys.RETURN); // This is to send the multiple keys.
BACK_SPACE, ENTER, ALT, CONTROL, SHIFT , F1, F9 etc...

## Usefull methods in Actions class:

	Actions action = new Actions(driver);
	action.keyDown(Keys.CONTROL);
	action.sendKeys("a");
	action.keyUp(Keys.CONTROL);
	action.build().perform();

## Usefull methods in Interator class:

Interator class usually used in Collections in java. like, Set, ArrayList etc...

	Iterator<String> iter = windowsIDS.iterator();
	iter.next();   // this will return the datatype of the iterator.

## What is Broken link and how to find it:

A broken link, also often called a dead link, is one that does not work i.e. does not redirect to the webpage it is meant to. 
This usually occurs because the website or particular web page is down or does not exist.

	List<WebElement> links = driver.findElements(By.tagName("a"));
	for(WebElement linkElement: links){
		String url = linkElement.getAttribute("href");
		if(url == null || url.isEmpty()){
			// URL is empty. // not a broken link
			continue;
		}
		URL urlLink = new URL(url);
		try{
			HttpURLConnection httpconnection = urlLink.openConnection();
			httpconnection.connect();
			if(httpconnection.getResponseCode() >= 400){
				// **Broken Link**
			}
			else{
				// **Valid Link**
			}
		}
		catch(Exception e){
			e.printStackTrace();
		}
	}

## How to Handle Alerts:

### 1. The Java script alert with single button (OK):
	driver.switchTo().alert().accept(); // accepts the alert by clicking single button.

### 2. The Java script alert confirm with 2 buttons (Ok | Confirm) and (Cancel)
	driver.switchTo().alert().accept(); // OK | Confirm
	driver.switchTo().alert().dismiss(); // Cancel

### 3. The Java script alert prompt with text input box and 2 buttons (Ok) and (Cancel)
	Alert alertwindow = driver.switchTo().alert();
	alertwindow.getText(); - returns (String) the text displayed on the alert window.
	alertwindow.sendKeys("text input"); - enters the value in the text input box.
	alertwindow.accept();
	alertwindow.dismiss();

### 4. The Java script alert with Login Authentication request
We should pass the Username and password inside the URL

Sytax: https://**Username**:**Password**@**URL**

### 5. The notification alerts
	ChromeOptions options = new ChromeOptions();
	options.addArguments("--disable-notifications");
	WebDriver driver = new ChromeDriver(options);

## Differance Between Frame and iFrame:

- Frame is a HTML tag that is used for dividing the web page into various frames/windows. Used as < frame> tag, it specifies each frame within a frameset tag. 
- Iframe as < iframe> is also a tag used in HTML but it specifies an **inline frame**, that means it is used to embed some other document within the current HTML document.

## How to do action on Elements inside an iFrame:

1. driver.switchTo().frame(name or id of the frame); // we have to switch to specific iframe by giving name or id of the iframe.
2. driver.switchTo().frame(WebElement); // we have to get the entire iframe as webElement and switchTo the frame.
3. driver.switchTo().frame(index); // we have to send the index of the iframe. starts with 0.
4. driver.switchTo().**defaultContent()**; // we have to switch to main frame so that we can work on the other iframes. 
5. driver.switchTo().**parentFrame()**; // switch to parentFrame from childFrame 

		If the webpage have multiple iframe:
		driver.switchTo().frame(frame1);
		driver.findElement(By.id("frame1_elementId")).click();
		driver.switchTo().defaultContent(); // going to main frame.

		If the webpage have iframes inside an iframe
		driver.switchTo().frame(parentframeID);
		driver.switchTo().frame(ChildframeID);
		driver.findElement(By.id("Childframe_element")).click();
		driver.switchTo().parentFrame();
		driver.findElement(By.id("ParentFrame_element")).click();

## What is Synchronization problem in Selenium?

Synchronization issues occur when operations are performed on a web element that is not yet present in the DOM, or it is not a state to accept commands (e.g., not visible, not clickable, etc.)

## Different Types of Waits in Selenium:

1. Implicit wait
2. Explicit wait
3. Fluent wait

### 1. Implicit wait:
The Implicit Wait in Selenium is used to tell the web driver to wait for a certain amount of time before it throws a “No Such Element Exception”.

	driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
								or
	driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

### 2. Explicit wait:
The Explicit Wait in Selenium is used to tell the Web Driver to wait for certain conditions (Expected Conditions) or maximum time exceeded before throwing “ElementNotVisibleException” exception.

	WebDriverWait mywait = new WebDriverWait(driver, Duration.ofSeconds(10)); // need to give the driver and time as perameters to the WebDriverWait.
	WebElement element = mywait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("xpath")));
	element.click();

	Generic method to Explicit wait:
	public static WebElement waitForElementPresent(WebDriver driver, By locator, int timeout){
		WebDriverWait mywait = new WebDriverWait(driver, Duration.ofSeconds(timeout));
		WebElement element = mywait.until(ExpectedConditions.presenceOfElementLocated(locator));
		return driver.findElement(locator);
	}

### 3. Fluent Wait:
The Fluent Wait in Selenium is used to define maximum time for the web driver to wait for a condition, as well as the frequency with which we want to check the condition before throwing an “ElementNotVisibleException” exception. 
**It checks for the web element at regular intervals until the object is found or timeout happens.**

	<!-- Creating the Fluent wait. -->
	Wait<WebDriver> mywait = new FluentWait<WebDriver>(driver).withTimeout(Duration.ofSeconds(30)).pollingEvery(Duration.ofSeconds(5)).ignoring(NoSuchElementException.class);
	<!-- usage of the Fluent wait. -->
	WebElement myelement = mywait.until(driver -> {
	  return driver.findElement(By.xpath("xpath"));
	});
	myelement.click();

## How to handle Tables in webpage from selenium:

### 1. Static Table handling
- a. find the xpath of the table. xpath: //table[@class ='myTable']
- b. find the no of rows present in the table. xpath: //table[@class ='myTable']/tbody/tr
- c. find the no of columns present in the table. xpath: //table[@class='myTable']//thead/tr/th
- d. retrieve the values/data from the table. xpath: //table[@class='myTable']//tr[1]/td[1] 
**Note: table index starts with 1**

### 2. Dynamic Table with Pagination handling 
- a. find the difference and similarities between active and inactive pages and find the xpath for the similar properties.
- b. find the xpath for present active dynamic table.
- c. find the no of rows present in the table.
- d. retrieve the values/data from the table.
- e. find the next page xpath with generic approach and click on the element to go next page using pagination.
- f. repeate the steps
**Note: table index starts with 1**

## How to handle the Date Picker:

The handling of Datepickers are different from eachother....
- a. find the proper xpath of the Month & Year and select the desired month and year.
- b. find the xpath for date table and select the desired date.

## How to handle Mouse actions in Selenium:

to do Mouse actins we can make use of Actions class methods.
### 1. Mouse Right click 
	WebDriver driver = new ChromeDriver();
	WebElement ele= driver.findElement(By.id(elementID));
	Actions myAction = new Actions(driver);
	myAction.contextClick(ele).perform(); 
### 2. Double click
	WebDriver driver = new ChromeDriver();
	WebElement button= driver.findElement(By.id(buttonID));
	Actions myAction = new Actions(driver);
	myAction.doubleClick(button).perform(); 
### 3. Drag and Drop
	WebDriver driver = new ChromeDriver();
	WebElement box1= driver.findElement(By.id(box1ID)); // source element
	WebElement box2= driver.findElement(By.id(box2ID)); // target element
	Actions myAction = new Actions(driver);
	myAction.dragAndDrop(box1, box2).perform();
### 4. Mouse Hover and Click
	WebDriver driver = new ChromeDriver();
	WebElement element= driver.findElement(By.id(elementID));
	Actions myAction = new Actions(driver);
	myAction.moveToElement(element).perform();
	

## How to handle Range Slider element

	WebDriver driver = new ChromeDriver();
	WebElement element= driver.findElement(By.id(elementID));
	Actions myAction = new Actions(driver);
	myAction.dragAndDropBy(element, 100, 0).perform(); // Slider element will be move forward in the X-axis for 100px
	myAction.dragAndDropBy(element, -100, 0).perform(); // Slider element will be move backward in the X-axis for 100px
	myAction.dragAndDropBy(element, 0, 100).perform(); // Slider element will be move forward in the Y-axis for 100px
	
## Difference between Actions and Action

1. Actions is a class and Action is a interface
2. Actions class is based on builder design pattern which builds a composite actions with the aggregation of Selenium WebDriver, where webdriver is only used to identify the presence of web elements on web application
3. Action interface is only used to represent the single user interaction i.e to perform the series of action items build by Actions class.
	**Note: .build() will return the Action interface variable. so, that will can perform the action later on.**

## Difference between build() and perform()

build() will builds the action that we created. where as perform() will builds and performs(completes) the action.


## Handling the keyboard keys in selenium
	
	## this is for only single combination
	WebDriver driver = new ChromeDriver();
	Actions myAction = new Actions(driver);
	myAction.sendKeys(Keys.ENTER).perform();

	## this is for multiple combinations of the keys
	WebDriver driver = new ChromeDriver();
	Actions myAction = new Actions(driver);
	myAction.keyDown(Keys.CONTROL)
	myAction.sendKeys("c");
	myAction.keyUp(Keys.CONTROL);
	myAction.perform();


## Useful methods in Actions class:

Actions myAction = new Actions(driver);
1. myAction.contextClick(element);  // Mouse Right click on the element
2. myAction.perform();				// Build and Perform the action specified above
3. myAction.doubleClick(button); 	// double click on the button
4. myAction.dragAndDrop(source,target); // drag and drop from source to target
5. myAction.dragAndDropBy(element,xOffset,yOffset); // drag and drop will be done based on the X and Y axis Offsets.
6. myAction.moveToElement(element);	// MouseHover action will take place on the element
7. myAction.sendKeys(Keys.ENTER); 	// send the keys to the webpage.
8. myAction.keyDown(Keys.CONTROL);	// Control key will be down. this helps in the multiple key press like CNTL + C

## How to take screenshots of a webpage

### 1. get the screenshot for entire screen
	TakesScreenshot ts = (TakesScreenshot) driver; // WebDriver class is sibling of the TakesScreenshot class. it's parents class is RemoteWebDriver.
	File src = ts.getScreenshotAs(OutputType.FILE); // get the screenshot for entire screen.
	File trg = new File(".\\screenshots\\homepage.png");
	FileUtils.copyFile(src, trg);
### 2. get the screenshot for specific part of the screen
	WebElement section = driver.findElement(By.xpath("sectionXpath"));
	File src = section.getScreenshotAs(OutputType.FILE); // get the screenshot of the section given in as xpath.
	File trg = new File(".\\screenshots\\mysection.png");
	FileUtils.copyFile(src, trg);
### 3. get the screenshot for the specific webelement
	WebElement element = driver.findElement(By.xpath("elementXpath"));
	File src = element.getScreenshotAs(OutputType.FILE); // get the screenshot of the element given in as xpath.
	File trg = new File(".\\screenshots\\element.png");
	FileUtils.copyFile(src, trg);

## How to open a link in new tab

### The below code is to open a link in new tab from the webpage. 

	String newtab = Keys.chord(Keys.CONTROL,Keys.RETURN); 
	driver.findElement(By.xpath("xpath")).sendKeys(newtab); // new tab will be open but old tab will be active window

### The below code is to open a page in new tab in same browser window.
	
	driver.get("google.com");
	driver.switchTo().newWindow(WindowType.TAB);
	driver.get("yahooo.com");   // new tab will be open and active at the sametime.

### The below code is to open a page in new tab in another browser window.

	driver.get("google.com");
	driver.switchTo().newWindow(WindowType.WINDOW);
	driver.get("yahooo.com");   // new tab will be open in new window and active at the sametime.

## How to JavascriptExecutor Interface

1. Flash an element
2. Draw boarder and take screenshot
3. Get the title of the page with js
4. Click action
5. Generate an alert 
6. Refresh the page
7. Scroll Up and Down
8. Zoom in and Zoom out page

### 1. Flash an element

	JavascriptExecutor js = (JavascriptExecutor) driver;
	String bgcolor = element.getCssValue("backgroundColor");
	for(int i = 0; i< 100 ; i++){
		js.executeScript("arguments[0].style.backgroundColor = '+bgcolor+'", element);
		Thread.sleep(20);
		js.executeScript("arguments[0].style.backgroundColor = '#000000'", element);
	}
	

### 2. Draw boarder and take screenshot

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("arguments[0].style.border = '3px solid red'", element)
	WebElement element = driver.findElement(By.xpath("elementXpath"));
	File src = element.getScreenshotAs(OutputType.FILE);
	File trg = new File(".\\screenshots\\element.png");
	FileUtils.copyFile(src, trg);

### 3. Get the title of the page with js

	JavascriptExecutor js = (JavascriptExecutor) driver;
	String title = js.executeScript("return document.title;").toString();

### 4. Click action

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("arguments[0].click();",element);

### 5. Generate an alert

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("alert('welcome message')");

### 6. Refresh the page
History can be accessed by the javascript code by using the index. 

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("history.go(0)");  // run the latest history file i.e current page

### 7. Scroll Up and Down
#### Down

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("window.scrollTo(0,document.body.scrollHeight)");

#### Up

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("window.scrollTo(0,-document.body.scrollHeight)");

### 8. Zoom a page

	JavascriptExecutor js = (JavascriptExecutor) driver;
	js.executeScript("document.body.style.zoom='50%'");

## Methods to handle cookies

1. driver.manage().getCookies(); // Returns (Set< Cookie>) the list of all cookies
2. driver.manage().getCookieNamed();  // Returns the Cookie with name
2. driver.manage().addCookie(arg(0));  // Create and add the cookie
3. driver.manage().deleteCookie(arg(0)); // Delete a specific cookie
4. driver.manage().deleteCookieNamed(arg(0)); // Delete a cookie with name
5. driver.manage().deleteAllCookies();  // Delete all cookies

## Usefull methods in Cookie Class

Cookie cookie = new Cookie("name of the cookie", "value of the cookie");

1. cookie.getName(); // returns (String) the name of the cookie.
2. cookie.getValue(); // returns (String) the value of the cookie.

## How to manage and change the Location of the downloads

### 1. This works for Chrome and Edge browsers (.docx)	
	String location = System.getProperty("user.dir") + "\\Downloads\\"
	HashMap preferences = new HashMap();
	preferences.put("download.default_directory", location);
	ChromeOptions options = new ChromeOptions();
	options.setExperimentalOption("prefs", preferences);
	WebDriver driver = new ChromeDriver(options);

**.PDF**

	preferences.put("plugins.always_open_pdf_externally", true); // for pdf download

### 2. Firefox browser (.docx)
	String location = System.getProperty("user.dir") + "\\Downloads\\"
	FirefoxProfile profiles = new FirefoxProfile();
	profiles.setPreference("browser.helperApps.neverAsk.saveToDisk", "applicaton/msword"); // sending preference with MIME type of the file that we want to download.
	profiles.setPreference("browser.download.folderList",2); // 0 - Desktop, 1 - Downloads, 2 - Desired Location.
	profiles.setPreference("browser.download.dir", location);
	FirefoxOptions options = new FirefoxOptions();
	options.setProfile(profiles);
	WebDriver driver = new FirefoxDriver(options);

**.PDF**

	profiles.setPreference("pdfjs.disabled", true); // for pdf download
	profiles.setPreference("browser.helperApps.neverAsk.saveToDisk", "applicaton/pdf");


## Usefull methods in ChromOptions class

1. options.setExperimentalOption("prefs", preferences); // setting the preferences before creating driver instance.
2. options.addArguments("--remote-allow-origins= \*");

## How to upload a file in webpage

1. if the element is having attribute type = "file" then we can use sendKeys method with file path to upload a file.
	driver.findElement(By.xpath("xpath")).sendKeys("C:\\Sudheer\\file.pdf")
2. if the element is not having the type = "file" attribute, then we have to use the Robot class method approach. By using Robot class we can handle the Windows File Browser window. So, to open the file browser window, we have to click on the element. sometimes we can't click on the element directly so, we have to use JavascriptExecutor class for the click action on the upload button. 
		
		WebDriver driver = new ChromeDriver();
		WebElement upload = driver.findElement(By.xpath("xpath of upload button"));
		JavascriptExecutor js = (JavascriptExecutor) driver;
		js.executeScript("arguments[0].click();",upload); // click action on the upload button using js
		- 1. Copy the path
		- 2. CNTR + V
		- 3. ENTER 
		Robot rb = new Robot();   // import from java.awt and include AWTException
		rb.delay(3000); // giving the delay to open the file browser window.
		StringSelection ss = new StringSelection("C:\\Sudheer\\file.pdf");
		Toolkit.getDefualtToolkit().getSystemClipboard().setContents(ss,null); // copying path to the clipboard
		rb.keyPress(KeyEvent.VK_CONTROL); // these 2 lines will do the Control+V action.
		rb.keyPress(KeyEvent.VK_V); 
		rb.keyRelease(KeyEvent.VK_CONTROL); // these 2 lines will release the both keys
		rb.keyRelease(KeyEvent.VK_V);
		rb.keyPress(KeyEvent.VK_ENTER); // these 2 lines will click enter key and release 
		rb.keyRelease(KeyEvent.VK_ENTER);  


## How to do Database testing with Selenium

If the User Registration has been done, we can do testcase validation by observing the Customer registered text. But, we have to test whether it is updated in the database or not.

So, for that we have to add my-sql maven dependency in the pom.xml to do database operations to check the registered user data is present in the database or not.

After the Registration is done, we need to validate from the database. So, in this below example mySql database validation with JDBC(Java Database Connectivity).

	Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/databasename", "username", "password"); // import Connection class from java.sql package and add SQLException to the method
	Statement statement = connection.createStatement();
	String myQuery = "Select firstname,lastname,email,telephone from tablename";
	ResultSet resultset = statement.executeQuery(myQuery);
	while(resultset.next()){
		String firstname = resultset.getString("firstname");
		String lastname = resultset.getString("lastname");
		String email = resultset.getString("email");
		String telephone = resultset.getString("telephone");
		boolean status = false;
		if(firstname.equals("myName") && lastname.equals("myLast") && email.equals("n@gmail.com") && telephone.equals("525252522")){
			System.out.println("Record found in database");
			status = true;
			break;
		}
	}
	if(status == false){
		System.out.println("Record not found in database");
	}
