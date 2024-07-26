package utils;

import java.io.File;
import java.io.IOException;
import java.time.Duration;

import org.apache.commons.io.FileUtils;
import org.json.simple.parser.ParseException;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.ITestResult;

import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;

public class SeleniumWrapper {

	protected WebDriver driver;
    private WebDriverWait wait;
    private Actions actions;

    public SeleniumWrapper(WebDriver driver) {
        this.driver = driver;
        this.wait = new WebDriverWait(this.driver,Duration.ofSeconds(10));
        this.actions = new Actions(driver);
     
    }

    public void clickElement(By locator) {
        WebElement element = wait.until(ExpectedConditions.elementToBeClickable(locator));
        element.click();
    }

    public void typeText(By locator, String text) {
        WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(locator));
        element.clear();
        element.sendKeys(text);
    }


    
    public void scrollToElement(By locator) {
        WebElement element = driver.findElement(locator);
        JavascriptExecutor jsExecutor = (JavascriptExecutor) driver;
        jsExecutor.executeScript("arguments[0].scrollIntoView(true);", element);
    }

    
    public void hoverOverElement(By locator) {
        WebElement element = driver.findElement(locator);
        JavascriptExecutor jsExecutor = (JavascriptExecutor) driver;
        String script = "arguments[0].scrollIntoView(true);";
        jsExecutor.executeScript(script, element);
    }
    
    //upload file
    public void uploadFile(By locator, String filePath) {
        WebElement fileInput = driver.findElement(locator);
        fileInput.sendKeys(filePath);
    }
    
    //verify text
    public boolean verifyText(By locator, String expectedText) {
        WebElement element = wait.until(ExpectedConditions.visibilityOfElementLocated(locator));
        String actualText = element.getText();
        return actualText.equals(expectedText);
    }
    
    
    //take screenshot
    
    public String getScreenshot(String testCaseName,WebDriver driver) throws IOException
    {
    	TakesScreenshot ts = (TakesScreenshot)driver;
    	File source =ts.getScreenshotAs(OutputType.FILE);
    	File file = new File(System.getProperty("user.dir")+"//reports//"+testCaseName+".png");
    	FileUtils.copyFile(source, file);
    	return System.getProperty("user.dir")+"//reports"+ testCaseName+ ".png";
    }

	public void OnFinish(ITestResult result) {
		// TODO Auto-generated method stub
		
	}
	
	
	//fetching test data
	
	   public String getJsonData(String filePath, String jsonPath) throws IOException, ParseException {
	        File file = new File(filePath);
	        ObjectMapper objectMapper = new ObjectMapper();
	        JsonNode jsonNode = objectMapper.readTree(file);

	        String[] pathSegments = jsonPath.split("\\.");
	        for (String segment : pathSegments) {
	            jsonNode = jsonNode.get(segment);
	            if (jsonNode == null) {
	                return null; // Handle the case where the path is invalid
	            }
	        }

	        return jsonNode.textValue();
	    }

	    public String getTestData(String jsonPath) throws IOException, ParseException {
	        String path = System.getProperty("user.dir") + "\\src\\test\\java\\data\\testData.json";
	        String result = getJsonData(path, jsonPath);
	        System.out.println(result);

	        return result;

	    }
    

   
    
    
    
}

