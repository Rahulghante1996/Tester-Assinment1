
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;

public class UpdateBillingInformation {
    @Test
    public void updateBillingInfo() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver");

        // 1. Configure the Web browser
        WebDriver driver = new ChromeDriver();
        driver.manage().window().maximize();

        // 2. Navigate to the website
        driver.get("https://minimals.cc/");

        // 3. Login to the website
        WebElement emailField = driver.findElement(By.id("email"));
        WebElement passwordField = driver.findElement(By.id("password"));
        emailField.sendKeys("demo@minimals.cc");
        passwordField.sendKeys("demo1234");
        driver.findElement(By.xpath("//button[@type='submit']")).click();

        // 4. Navigate to the Account page
        driver.findElement(By.xpath("//a[@href='#user']")).click();
        driver.findElement(By.xpath("//a[@href='#account']")).click();

        // 5. Open the Billing tab
        driver.findElement(By.xpath("//a[@href='#billing']")).click();

        // 6. Update billing information
        WebElement billlingNameField = driver.findElement(By.id("billing_name"));
        billlingNameField.clear();
        billlingNameField.sendKeys("Deja Brady");

        WebElement paymentMethodDropdown = driver.findElement(By.id("payment_method"));
        paymentMethodDropdown.click();
        driver.findElement(By.xpath("//option[@value='card_1234']")).click();

        // 7. Save changes
        driver.findElement(By.xpath("//button[@type='submit']")).click();

        // 8. Validate changes
        WebElement updatedBillingName = driver.findElement(By.id("billing_name"));
        Assert.assertEquals(updatedBillingName.getAttribute("value"), "Deja Brady");

        WebElement updatedPaymentMethod = driver.findElement(By.id("payment_method"));
        Assert.assertEquals(updatedPaymentMethod.getAttribute("value"), "card_1234");
    }
}
    }
}

