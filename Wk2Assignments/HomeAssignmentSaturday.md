Goal: Convert the Selenium Java Code to Playwright Typescript

Instructions:

- Use Playwright v1.56+ syntax and best practices for TypeScript.
- Preserve all original test steps exactly—do not add, remove, or modify any logical steps from the source.
- Use the same locators as defined in the Selenium Java code (e.g., if the Java code uses By.id("foo"), use '#foo' in Playwright)
- Do not hardcode sleep or waitForTimeout—use Playwright’s built-in auto-waiting mechanisms (e.g., await page.locator(...).click(), await page.waitForURL(), etc.).
- If a Selenium Java feature has no direct equivalent in Playwright TypeScript, insert a comment: // not implemented.
- Include clear comments in the TypeScript code to explain each step, mirroring the intent of the original Java code.
- The output must be valid Playwright TypeScript—not generic TypeScript or pseudocode.
- Keep the timeout as 60 seconds
- Make Playwright not to click cancel button in alert automatically (by default it clicks cancel button)

Context

- You are an AI assistant specialized in test automation migration. 
- Your task is to accurately translate legacy Selenium Java test scripts into modern, idiomatic Playwright TypeScript scripts while maintaining functional parity and leveraging Playwright’s native capabilities.

Example:

Selenium Java Code for example:

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.Assert;
import org.testng.annotations.AfterMethod;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.Test;

public class PlaywrightTitleTest {

    WebDriver driver;

    @BeforeMethod
    public void setUp() {
        // Set the path to your chromedriver executable if required
        // System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");
        driver = new ChromeDriver();
        driver.manage().window().maximize();
    }

    @Test
    public void verifyTitleContainsPlaywright() {
        driver.get("https://playwright.dev/");
        
        String pageTitle = driver.getTitle();
        // Assert that the title contains "Playwright"
        Assert.assertTrue(pageTitle.contains("Playwright"), "Title does not contain 'Playwright'");
    }

    @AfterMethod
    public void tearDown() {
        if (driver != null) {
            driver.quit();
        }
    }
}


Converted Playwright Code for example:

import { test, expect } from '@playwright/test';

test('has title', async ({ page }) => {
  await page.goto('https://playwright.dev/');

  // Expect a title "to contain" a substring.
  await expect(page).toHaveTitle(/Playwright/);
});






My Selenium Java Code (which need to be converted to playwright typescript):



import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.annotations.AfterTest;
import org.testng.annotations.BeforeTest;
import org.testng.annotations.Test;
import java.time.Duration;

public class AmazonLoginTest {
    
    private WebDriver driver;
    private WebDriverWait wait;
    
    @BeforeTest
    public void setUp() {
        // Set up Chrome driver
        driver = new ChromeDriver();
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        driver.manage().window().maximize();
    }
    
    @Test
    public void verifyAmazonInLoginFunctionality() {
        // Navigate to Amazon India homepage
        driver.get("https://www.amazon.in/");
        
        // Handle "Continue shopping" popup if present
        try {
            WebElement continueButton = driver.findElement(By.xpath("//button[text()='Continue shopping']"));
            if (continueButton.isDisplayed()) {
                continueButton.click();
            }
        } catch (Exception e) {
            System.out.println("Continue shopping popup not found");
        }
        
        // Click on "Hello, sign in" using XPath
        WebElement helloSignIn = wait.until(ExpectedConditions.elementToBeClickable(
            By.xpath("//a[.//span[text()='Hello, sign in']]")));
        helloSignIn.click();
        
        // Wait for email input field to be visible and fill email
        WebElement emailInput = wait.until(ExpectedConditions.visibilityOfElementLocated(
            By.xpath("//input[@type='email']")));
        emailInput.sendKeys("8109388923");
        
        // Click Continue button using XPath
        WebElement continueBtn = wait.until(ExpectedConditions.elementToBeClickable(
            By.xpath("//span[@id='continue']//input[@type='submit']")));
        continueBtn.click();
        
        // Wait for password input field to be visible and fill password
        WebElement passwordInput = wait.until(ExpectedConditions.visibilityOfElementLocated(
            By.xpath("//input[@type='password']")));
        passwordInput.sendKeys("Rudransh#3223");
        
        // Click Sign In button using XPath
        WebElement signInSubmit = wait.until(ExpectedConditions.elementToBeClickable(
            By.xpath("//input[@id='signInSubmit']")));
        signInSubmit.click();
        
        // Additional verification - check if user is redirected to homepage or account page
        wait.until(ExpectedConditions.urlContains("amazon.in"));
        String currentUrl = driver.getCurrentUrl();
        assert currentUrl.contains("amazon.in") : "Login failed - not redirected to Amazon page";
        System.out.println("Login successful! Redirected to: " + currentUrl);
    }
    
    @AfterTest
    public void tearDown() {
        // Close the browser
        if (driver != null) {
            driver.quit();
        }
    }
}




INPUT DOM:



INPUT DOM:

<div class="nav-div" id="nav-link-accountList">
  <a href="https://www.amazon.in/ap/signin?openid.pape.max_auth_age=0&amp;openid.return_to=https%3A%2F%2Fwww.amazon.in%2F%3Fref_%3Dnav_ya_signin&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=inflex&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0" class="nav-a nav-a-2   nav-progressive-attribute" data-nav-ref="nav_ya_signin" data-nav-role="signin" data-ux-jq-mouseenter="true" tabindex="0" data-csa-c-type="link" data-csa-c-slot-id="nav-link-accountList" data-csa-c-content-id="nav_ya_signin" aria-controls="nav-flyout-accountList" data-csa-c-id="2wr46g-b6d0p0-yg5lmj-vao0c8">
  <div class="nav-line-1-container"><span id="nav-link-accountList-nav-line-1" class="nav-line-1 nav-progressive-content">Hello, sign in</span></div>
  <span class="nav-line-2 ">Account &amp; Lists
  </span>
  </a>
  <button class="nav-flyout-button nav-icon nav-arrow" aria-label="Expand Account and Lists" tabindex="0" style="visibility: visible;" aria-expanded="false"></button>
  </div>


<input type="email" id="ap_email_login" autocomplete="username" name="email" class="a-input-text" data-tab-layout-weblab-treatment="" aria-label="Enter your mobile number or email" fdprocessedid="cw057l">

<span id="continue" class="a-button a-spacing-top-small a-button-span12 a-button-primary aok-relative"><span class="a-button-inner"><input class="a-button-input" type="submit" aria-labelledby="continue-announce" fdprocessedid="wodtg"><span id="continue-announce" class="a-button-text a-text-center" aria-hidden="true">
        <!-- Overlaid spinner -->
        <span id="claim-submit-spinner" class="a-spinner a-spinner-medium aok-hidden"></span>
        Continue
      </span></span></span>



<input type="password" maxlength="1024" id="ap_password" autocomplete="current-password" name="password" spellcheck="false" class="a-input-text a-span12 auth-autofocus auth-required-field" aria-required="true" fdprocessedid="ax65u6">


<input id="signInSubmit" class="a-button-input" type="submit" aria-labelledby="auth-signin-button-announce" fdprocessedid="zvgod">







Persona

- Act as Senior automation Tester to generate the code
- Act as senior tech architect to review the code

Output Format

- Follow the coding standards as per tech stack given

Tone

Script should be slightly informal, easier to read, approachable style.

