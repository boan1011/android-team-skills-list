# Appium

#### Development Environment

- Ubuntu 15.04
- Android Studio 1.3.2
- nodejs (版本 >10)
- maven

#### Built Environment
- 安裝node js，並以node js 安裝appium
- $ apt-get install nodejs
- $ apt-get install npm
- $ npm install appium


- 以nvm切換版本
- $ nvm install stable
- $ nvm alias stable
- 執行 appium 
- $ appium

- (可以用appium-doctor指令查看環境是否安裝完整)
![](./picture/Demo_1.png)

- $ sudo apt-get install maven

- 開新專案
- $ mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -   DinteractiveMode=false
- 將pom.xml 內容改為
``` xml
<project xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://maven.apache.org/POM/4.0.0"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.mycompany.app</groupId>
    <artifactId>my-app</artifactId>
    <packaging>jar</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>my-app</name>
    <url>http://maven.apache.org</url>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>3.8.1</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.appium</groupId>
            <artifactId>java-client</artifactId>
            <version>3.2.0</version>
        </dependency>
    </dependencies>
</project>
```

- 將import資料夾中import AppTest 中
- 在pom.xml目錄下，執行測試
- $ mvn test


#### The Simplest Sample
```java

	public class AppTest
	    extends TestCase
	{
	    private AppiumDriver<AndroidElement> driver;
	    public AppTest( String testName )
	    {
		super( testName );
	    }
	    @override
	    public void setUp() throws Exception {
		// set up appium
		DesiredCapabilities capabilities = new DesiredCapabilities();
	//        capabilities.setCapability(CapabilityType.BROWSER_NAME, "");//这句不是必须的
		capabilities.setCapability("deviceName","Android Emulator");//設定android 模擬器
		capabilities.setCapability("platformVersion", "4.4");//android 版本
		capabilities.setCapability("platformName","Android");//運行平台
		//以下以開啟計算機為例
		capabilities.setCapability("appPackage", "com.android.calculator2");//開啟的package name
		capabilities.setCapability("appActivity", ".Calculator");// 開啟的Activity
		driver = new AndroidDriver<AndroidElement>(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);

	    }

	    public void testaction (){
		//數字0-9
		for (int i=0 ;i<10 ;i++) {
		    WebElement act = driver.findElement(By.name(Integer.toString(i)));
		    act.click();
		}
	    }

	    @Override
	    protected void tearDown() throws Exception {
		super.tearDown();
	    }
	}

```

![](./picture/Demo_2.png)
