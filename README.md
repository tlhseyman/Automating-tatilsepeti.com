import org.openqa.selenium.By;
import org.openqa.selenium.Keys;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

import java.util.ArrayList;
import java.util.concurrent.TimeUnit;

public class TatilSepeti {

    public static void main(String[] args) throws InterruptedException {
        System.setProperty("webdriver.chrome.driver", "/Users/admin/Downloads/chromedriver");
        WebDriver driver = new ChromeDriver();
        driver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
        driver.get("https://www.tatilsepeti.com/"); //NAVIGATING TO TATILSEPETI.COM
        driver.findElement(By.id("bolge")).sendKeys("Ankara");  //ASSIGNING A VALUE FOR LOCATION
        driver.findElement(By.id("bolge")).sendKeys(Keys.ARROW_DOWN);  //1ST STEP OF CHOOSING LOCATION
        Thread.sleep(1000);
        driver.findElement(By.id("bolge")).sendKeys(Keys.ARROW_DOWN);  //2ND STEP OF CHOOSING LOCATION
        Thread.sleep(1000);
        driver.findElement(By.id("bolge")).sendKeys(Keys.ARROW_DOWN);
        driver.findElement(By.id("bolge")).sendKeys(Keys.ENTER);      //CHOOSING LOCATION
        driver.findElement(By.id("searchBtn")).click();              //COMMAND FOR CLICKING ON SEARCH BUTTON
        driver.findElement(By.xpath("//*[@class='col-lg-12']/div/div[4]")).click();  //COMMAND FOR CLICKING DESCENDING ORDER

        ArrayList<WebElement> priceList = (ArrayList<WebElement>) driver.findElements(By.xpath("//*[@class='discount-price']"));  //LISTING PRICE ELEMENTS
        WebElement selectedHotels = driver.findElement(By.id("totalHotelCount"));
        String numberOfSelectedHotels = selectedHotels.getText();
        System.out.println(numberOfSelectedHotels);
        int validationNumber = Integer.parseInt(numberOfSelectedHotels);
        for (int i = 0; i < priceList.size(); i++) {              //GETTING SELECTED PRICES ON CONSOLE FROM MAX PRICE TO MIN PRICE
            if(priceList.indexOf(i)>=priceList.indexOf(i+1)){
                System.out.println(priceList.get(i).getText());

            }
        }
        if(priceList.size()==validationNumber){         //IT IS AN IF CONDITION TO SEE IF IT IS VALID OR NOT
            System.out.println("These hotels listed as descending order correctly");
        }
        else{
            System.out.println("We have a problem for listing the hotels as descending order");
        }
    }
}
