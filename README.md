# homework3-2
import io.appium.java_client.AppiumDriver;
import io.appium.java_client.android.AndroidDriver;
import org.junit.After;
import org.junit.Assert;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.net.URL;

public class FirstTest {

    private AppiumDriver driver;

    @Before
    public void setUp() throws Exception {
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("deviceName", "AndroidTestDevice");
        capabilities.setCapability("platformVersion", "9");
        capabilities.setCapability("automationName", "Appium");
        capabilities.setCapability("appPackage", "org.wikipedia");
        capabilities.setCapability("appActivity", ".main.MainActivity");
        capabilities.setCapability("app", "C:/Users/aleksey/Desktop/JavaAppiumAutomation/apks/org.wikipedia_50370_apps.evozi.com.apk");

        driver = new AndroidDriver(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
    }

    @After
    public void tearDown() {
        driver.quit();
    }

@Test
    public void testСancellationSearchJava() {
        {
            waitForElementAndClick(By.xpath("//*[contains(@text,'SKIP')]"),
                    "Cannot find Search Skip input",
                    5
            );
            waitForElementAndClick(
                    By.xpath("//*[contains(@text,'Search Wikipedia')]"),
                    "Cannot find Search wiki input",
                    5
            );
            waitForElementAndSendKeys(By.id("org.wikipedia:id/search_src_text"),
                    "java",
                    "cannot find search input",
                    5);
            waitForElementPresent(By.xpath("//*[@resource-id='org.wikipedia:id/search_results_list']//*[@text='Indonesian island']"),
                    "Cannot find  Ii topic searching by java ",
                    15);

            waitForElementPresent(By.xpath("//*[@resource-id='org.wikipedia:id/search_results_list']//*[@text='High-level programming language']"),
                    "Cannot find  H-lpl topic searching by java ",
                    15);

            waitForElementPresent(By.xpath("//*[@resource-id='org.wikipedia:id/search_results_list']//*[@text='Object-oriented programming language']"),
                    "Cannot find  oopl topic searching by java ",
                    15);


            waitForElementAndClick(
                    By.id("org.wikipedia:id/search_close_btn"),
                    "Cannot find X input",
                    5
            );

            waitForElementNotPresent(By.id("org.wikipedia:id/search_results_list"),
                    "Cannot find  search_results_list topic searching by java ",
                    15);

        }
    }


    private WebElement waitForElementPresent(By by, String error_message, long timeoutInSeconds) {
        WebDriverWait wait = new WebDriverWait(driver, timeoutInSeconds);
        wait.withMessage(error_message + "\n");

        return wait.until(
                ExpectedConditions.presenceOfElementLocated(by)
        );
    }

    private WebElement waitForElementPresent(By by, String error_message) {

        return waitForElementPresent(by, error_message, 5
        );
    }

    private WebElement waitForElementAndClick(By by, String error_message, long timeoutInSeconds) {
        WebElement element = waitForElementPresent(by, error_message, timeoutInSeconds);
        element.click();

        return element;

    }

    private WebElement waitForElementAndSendKeys(By by, String value, String error_message, long timeoutInSeconds) {
        WebElement element = waitForElementPresent(by, error_message, timeoutInSeconds);
        element.sendKeys(value);

        return element;

    }

    private boolean waitForElementNotPresent(By by, String error_message, long timeoutInSeconds) {
        WebDriverWait wait = new WebDriverWait(driver, timeoutInSeconds);
        wait.withMessage(error_message + "\n");

        return wait.until(
                ExpectedConditions.invisibilityOfElementLocated(by)
        );
    }
 
}
 
