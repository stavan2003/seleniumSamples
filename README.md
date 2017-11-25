# seleniumSamples

##   Execute Multiple TestNG file : 

java -cp "./bin;./lib/*" org.testng.TestNG testng1.xml testng2.xml testng3.xml

##   Execute a particular test : 
java -cp "./bin;./lib/*" org.testng.TestNG -testnames "SampleTest1" testng1.xml 

####   Running TestNG from Command Prompt. 
"cp" above is setting classpath


##   Basic Authentication
		driver.get("http://the-internet.herokuapp.com/basic_auth");
		Thread.sleep(3000);
		driver.switchTo().alert().sendKeys("admin" + Keys.TAB + "admin");
		Thread.sleep(3000);
		driver.switchTo().alert().accept();
	
##   Execute AutoIT Scripts
		Runtime.getRuntime().exec("Path to EXE File");
		
##   Gmail Login Test
		System.setProperty("webdriver.gecko.driver","C:\\Users\\Admin\\Documents\\Software\\geckodriver-v0.16.0-win64\\geckodriver.exe");
		WebDriver driver = new FirefoxDriver();
		driver.manage().window().maximize();
		driver.get("https:##   mail.google.com/mail/");
		WebElement element = driver.findElement(By.id("identifierId"));
		element.sendKeys("stavan2003");
	    driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
		
		element = driver.findElement(By.id("identifierNext"));
		element.click();
		Thread.sleep(5000);
	
		WebElement myDynamicElement = (new WebDriverWait(driver, 150)).until(ExpectedConditions.presenceOfElementLocated(By.name("password")));
		element = driver.findElement(By.xpath(".##   *[@id='password']/div[1]/div/div[1]/input"));
		element.sendKeys("****");
				
		element = driver.findElement(By.id("passwordNext"));
		element.click();

		driver.quit();

##   Form Authentication
		driver.get("http://the-internet.herokuapp.com/login");
		driver.findElement(By.id("username")).sendKeys("tomsmith");
		driver.findElement(By.id("password")).sendKeys("SuperSecretPassword!");
		driver.findElement(By.xpath(".##   *[@id='login']/button")).submit();
		WebElement myDy = (new WebDriverWait(driver, 10)).until(ExpectedConditions.presenceOfElementLocated(By.cssSelector(".button.secondary.radius")));
		System.out.println("Logout Located");
		driver.findElement(By.cssSelector(".button.secondary.radius")).click(); 
		
##   Link Navigation
		driver.get("http://the-internet.herokuapp.com");
		driver.findElement(By.linkText("Form Authentication")).click();

##   Check if Element Exists
		public static boolean isElementExisting(WebDriver driver, By by) {
		boolean isExists = true;
		try {
			driver.findElement(by);
			
		} catch (Exception e) {
			isExists =  false;
		}
		return isExists;
		 
	}

##   Find all <a> elements on the page
		driver.get("http://the-internet.herokuapp.com");
		List<WebElement> listofLinks = driver.findElements(By.tagName("a"));
		for (WebElement link : listofLinks ){
			System.out.println(link + " " + link.getAttribute("href") + " " + link.getText());
		}
		
##   Check if all Links on page are working
	public static boolean isLinkWorking(WebDriver driver, String hrefString) throws Exception{
		boolean isWorking = true;
		URL url = new URL(hrefString);
		HttpURLConnection connection = (HttpURLConnection) url.openConnection();
		String response = "";
		try {
			connection.connect();
			response = connection.getResponseMessage();
			System.out.println(response);
			connection.disconnect();
		} catch (Exception e){
			isWorking = false;
		}
		return isWorking;
	}
	
##   Handling Alerts
		driver.get("http://the-internet.herokuapp.com/javascript_alerts");
		driver.findElement(By.xpath("##   button[@onclick='jsConfirm()']")).click();
		driver.switchTo().alert().accept();
		driver.switchTo().alert().dismiss();
		
##   Handling Elements inside Alerts
		driver.get("http://the-internet.herokuapp.com/javascript_alerts");
		driver.findElement(By.xpath("##   button[@onclick='jsPrompt()']")).click();
		Alert prompt = driver.switchTo().alert();
		prompt.sendKeys("This is Stavan");
		prompt.accept();

	
##   Opening multiple windows, switching to parent window, print handle id of all child windows
		driver.get("http://the-internet.herokuapp.com/windows");
		String parentWindowHandler = driver.getWindowHandle();
		
		driver.findElement(By.linkText("Click Here")).click();
		driver.switchTo().window(parentWindowHandler).findElement(By.linkText("Click Here")).click();		
		driver.switchTo().window(parentWindowHandler).findElement(By.linkText("Click Here")).click();
		
		System.out.println("No. of handles :"+ driver.getWindowHandles().size());

		for(String handle : driver.getWindowHandles()){
			System.out.println(handle);
			driver.switchTo().window(handle);
			driver.close();
		}

##   handling Drag and Drop
		driver.get("http://jqueryui.com/resources/demos/droppable/default.html");
		WebElement drag = driver.findElement(By.id("draggable"));
		WebElement drop = driver.findElement(By.id("droppable"));
		Actions worker = new Actions(driver);
		worker.dragAndDrop(drag, drop);
		worker.perform();	
		
##   CheckBox and Radio Button
		driver.get("http://toolsqa.com/automation-practice-form/");
		List<WebElement> checkboxes = driver.findElements(By.name("profession"));
		for (WebElement checkbox : checkboxes) {
			System.out.println("CheckBox :" + checkbox.getAttribute("value"));
			System.out.println("Original State isSelected :" + checkbox.isSelected());
			checkbox.click();
			System.out.println("After click State isSelected :" + checkbox.isSelected());
		}		

		
##   Menu Items - Single and Multiple Select Type Drop Downs
		driver.get("http://toolsqa.com/automation-practice-form/");
		WebElement mySelectElement = driver.findElement(By.id("continents"));
		Select dropdown = new Select(mySelectElement);
		System.out.println("Is multiple Select Allowed : " + dropdown.isMultiple());
		System.out.println("No. of elements in Drop Down :" + dropdown.getOptions().size());
##   Select a particular option
		dropdown.selectByVisibleText("South America");
##   Scan throgh all the elements
		for (WebElement menuItem : dropdown.getOptions()) {
			System.out.println("Menu Item :" + menuItem.getText());
			menuItem.click();
			System.out.println("------------");
		}
		
##   Get all options for a particular select box using CSS		
		driver.get("http://toolsqa.com/automation-practice-form/");
		List<WebElement> selectOptions = driver.findElements(By.cssSelector("#selenium_commands > option"));
		for (WebElement ele : selectOptions){
			System.out.println(ele.getText());
		}
		driver.quit();
		
##   Navigation
		driver.get("http://toolsqa.com/automation-practice-form/");
		driver.findElement(By.linkText("Link Test")).click();
		driver.navigate().back();
		driver.navigate().forward();
		
##   External Java Script - Scroll on page
		driver.get("http://the-internet.herokuapp.com/infinite_scroll");
		JavascriptExecutor jsx = (JavascriptExecutor)driver;
		jsx.executeScript("window.scrollBy(0, 100)", "");
		jsx.executeScript("alert('Hiiii')", "");

		
##   Wait for a Condition - Title to change for e.g.
		driver.get("http://toolsqa.com/automation-practice-form/");
		driver.findElement(By.linkText("Link Test")).click();
		WebDriverWait waiter = new WebDriverWait(driver, 10);
		waiter.until(ExpectedConditions.titleContains("Demo Table for practicing"));
		System.out.println(driver.getCurrentUrl());
		
##   Screenshot
		driver.get("http://toolsqa.com/automation-practice-form/");
		TakesScreenshot shot = (TakesScreenshot) driver;
		byte[] output = shot.getScreenshotAs(OutputType.BYTES);
		BufferedOutputStream out = new BufferedOutputStream(new FileOutputStream("error.jpg"));
		out.write(output);
		out.close();
