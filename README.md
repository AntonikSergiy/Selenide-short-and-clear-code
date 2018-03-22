***Three simple steps***
```sh open(page)
$(element) doAction
$(element) check(condition)
```

```sh
open("http://website.com/index.php");
$("#contact-link").click();
$(".navigation_page").should(appear);
```

***Browsers***
	Chrome
	IE
	Edge
	Firefox (geckodriver)
	PhantomJS
	Safari

***Navigating***
```sh
baseUrl = "http://website.com";
open("/login");
```
       
```sh    
open("http://google.com");
switchTo().frame($("#myFrame").toWebElement());
```

***WebDriver***
```sh
getWebDriver().findElement(By.id("username"));     // import static com.codeborne.selenide.WebDriverRunner.getWebDriver;
WebDriverRunner.setWebDriver(myWebDriver);
```

***Page and Browser***
```sh
startMaximized = true;
holdBrowserOpen = true;
getWebDriver().manage().window().maximize();
getWebDriver().manage().window().setSize(new Dimension(0,0));   // to minimize
sleep(5000);
refresh();
url();
source();
getWebDriver().getTitle();
confirm();
confirm("expectedDialogText");
dismiss();
writeToFile("content", targetFile);
takeScreenShot("fileName");
clearBrowserCache();
addListener(listener);

ie();       //is selenide configured to use IE
phantomjs();
htmlUnit();
```

***Selectors***
$(element).doAction;

__Find__
$ for element
$$ for elements

**Css**
```sh
$("#element");
$$("#elements");
```
___By___
```sh
$("element", 1);	          // index starts with 0, the second element will be selected
$("#elementid");	          // By id (same as $(byId("elementid");)
$(".classname"); 	          //By class (same as $(byClassName("classname");)
$(By.xpath(""));    
$(By.className(""));
$(By.name(""))
$(By.tagName(""));
$(By.linkText(""));
$(By.partialLinkText(""));
```    
```sh    
$(byText("cheezburger"));	  // Searches exact text
$(withText("ezburger")); 	  //Search based on partial text
$(byTitle("title")); 		    // By title (same as $("[title=tytul]");)
$(by("md-svg-src","img/icons/android.svg")); 	//Search based on attribute (same as $(byAttribute("class", "g"));)
$(byValue("value"));		    // By value (same as $("[value=wartosc]");)
```
***Chainable Selectors:***
___Multiple selectors can be used in one statement:___
```sh
$("div.container").$("button.buycheesburger");
$(".container").$(".subarea").$(withText("ezburger"));
```
___Parent and closest(tag) helps navigation in DOM:___
```sh
$(byText("Cheezburger")).parent().closest("ul").shouldBe(visible);
```
***Using and/or with selectors:***
___Only one of the requirements has to be met:___
```sh
$("h1").shouldBe(or(".class", visible, hidden));
```
___All of the requirements have to be met:___
```sh
$("h1").shouldBe(and("hamburger", visible, not(disabled)));
```
***Mouse and keyboard actions***
	$(element).doAction();

___Mouse actions:___
```sh
$(".class").click();
$("#id").contextClick(); 	   //right click on element
$("h1").doubleClick(); 		   //double click on element
$(".class").hover(); 		    //mouse over element
$("#id").scrollTo(); 		    //scrolling to element
actions().keyDown(Keys.ALT)
	.sendKeys("a")
	.keyUp(Keys.ALT);
```
	
***Clicking links and buttons***
```sh    
$("#submit").click();
$("#agreement").submit();
$(".g").doubleClick();
$(".g").contextClick();    // context menu
$("q").pressEnter();
$("q").pressTab();
$("#lst-ib").sendKeys(Keys.chord(Keys.CONTROL, "a"));   // select all
actions().click($("#rememberMe")).build().perform();
actions().click($("#lst-ib").val("selenide")).build().perform();
```
```sh
    executeJavaScript("console.log('Hello')");
```

***Interacting with forms=***
```sh
$("#login").setValue("John Doe");
$("#login").val("John Doe");
$(".menu").selectOption(String text);
$(By.name("menu")).selectOptionByValue(String value);
$(By.name("menu")).getSelectedOption();
$(By.name("menu")).getSelectedText();
$(By.name("menu")).getSelectedValue();
selectRadio(By.name("user.gender"), "male");
$("#element")).hover();
```
***Upload/Download files***
```sh
$("#upload").uploadFromClasspath("c:/files/my-file.txt");
$("#upload").uploadFile("c:/files/my-file.txt");
File file = $("#download_button").download();
$("#cv").uploadFile(
	new File("cv1.doc"),
        new File("cv2.doc"),
        new File("cv3.doc"),
        new File("cv4.doc"));
```
***Scoping***
```sh
$("#mainElement").$("#subElement");
$("#customerContainer").find(".user_name");
$$("li").get(5); 
$("li", 5);               // looking for Nth element 
```
***Visibility and existence assertions:***
___Text assertions:___
```sh
$(element).check(condition);
$("#element").shouldHave(text("CHEEZBURGER"));				                  //case insensitive, partial match
$("selector").shouldHave(exactText("DOUble CHeezBurGer")); 		          //case insensitive, exact match
$("selector").shouldHave(textCaseSensitive("Cheezburger")); 		        //case sensitive, partial match
$("selector").shouldHave(exactTextCaseSensitive("Double Cheezburger")); //case sensitive, exact match
$("#input").shouldHave(exactValue("John"));
$("selector").should(matchText("[A..Z]eezburger"));  			              //regexp
Html.text.containsCaseSensitive(source(), "Text pattern From Page Source");
```    
___Other assertions:___
```sh
$("h1").shouldHave(css("font-size", "16px"));
$$("#mytable tbody tr").shouldHave(size(2));
$("#input").shouldHave(name("fname"));
$("#input").shouldHave(value("John"));
$("#input").shouldHave(type("checkbox"));
$("#input").shouldHave(id("myForm"));
$("#input").shouldNotHave(text("Hello"), text("World"));
$("selector").shouldHave(attribute("layout","row"));                      //with value
$("selector").shouldNotHave(attribute("href"));                           //any value
$("selector").shouldHave(cssClass(".class"));
$("[type=button]").shouldHave(type("button"));
$("[type=button]").shouldNotHave(id("idselector"));
```
```sh
$$(".errors").shouldHave(size(2));
$$(".errors").shouldHave(exactTexts("text 1", "text 2"));
$$(".errors").shouldHave(texts("text 1", "text 2"));
```    
___Positive assertions:___
```sh
$("input").shouldBe(visible, enabled);                    //visible | appear 	// Same as $("selector").shouldBe(visible);
$("input").shouldBe(exist);                               //present | exist  
```
```sh
$("input").shouldBe(readonly); 
$("input").shouldBe(focused);
$(".errors").shouldBe(empty);
$$(".errors").shouldBe(empty);
$("#element").should(exist);
```
___Negative assertions:___
```sh
$("input").shouldBe(hidden);			            //hidden | disappear | not(visible) // Same as $("selector").should(disappear);
$("input").shouldNotBe(visible, enabled);
$("selector").shouldNot(exist); 	            //element should not exist in DOM
```

***Querying***
```sh
$("#element").isDisplayed();
$("#element").exists(); 
```
```sh
$$("#multirowTable tr").findBy(text("Norris"));
$$("#multirowTable tr").filterBy(text("Norris"));
$$("#multirowTable tr").excludeWith(text("Chack"));    
    
$$(“#employees tbody tr”)
	.filter(visible)
	.shouldHave(size(4));
```
___Search for parents/children___
```sh
$(“td”).parent()
$(“td”).closest(“tr”)
$(“.btn”).closest(“.modal”)
$(“div”).find(By.name(“q”))
```

***Wait***

___with text/value/attribute___
```sh
$("#welcome").waitUntil(hasText("Hello, Johny!"), 2000);
$("#username").waitUntil(hasAttribute("name", "user.name"), 2000);
$("#username").waitUntil(hasClass("green-button"), 2000);
$("#username").waitUntil(hasValue("123"), 2000);
$("#username").waitUntil(matchesText("Johny"), 2000);
$("#username").waitUntil(not(matchesText("Noname")), 2000);
$("#username").waitUntil(matchText("^Johny$"), 2000);
```

***with Conditions***
```sh
$("#username").waitUntil(present, 5000); //enabled, disabled, visible appears, disappears;
```

***Collections***
	$$(selector)

  ***Collections basics:***
***Collections are iterable SelenideElements:***
```sh
ElementsCollection collection = $$("div");
$$("selector"); 					                // doesn't search anything!
```
***They use the same Selectors as in $:***
```sh
$$(withText(„eezburger"));
```
***Operations on Collections:***
___Choosing an element:___
```sh
$$("div").first();
$$("div").last();
$$("div").get(2);			                  // get third element, index from 0
$$("div").findBy(text("123")); 		      // finds the first element
```

___Filtering:___
```sh
$$("div").filterBy(text("123"));	      //only with text 123
$$("div").excludeWith(text("123"));	    // all except with text 123
```
***Collection assertions:***
___Size assertion:___
```sh
$$("div").shouldBe(CollectionCondition.empty);
$$("div").shouldHave(size(5)); / or $$("div").shouldHaveSize(5);
$$("div").shouldHave(sizeGreaterThan(1));
$$("div").shouldHave(sizeGreaterThanOrEqual(1));
$$("div").shouldHave(sizeLessThan(100));
$$("div").shouldHave(sizeLessThanOrEqual(100));
$$("div").shouldHave(sizeNotEqual(1984));
```
___Text assertions (case sensitive):___
```sh
$$("div").shouldHave(texts(”kjlj", ”TTHT")); 			                    //partial matches of every single text
$$("div").shouldHave(exactTexts(”Here is your", ”Hamburger"));
```
___Operations returns:___
```sh
ElementsCollection collection = $$("div").filterBy(text("123")); 	    // even when filters to a single element
ElementsCollection collection2 = $$("div").filterBy(text("xyz")); 	  // empty collection
SelenideElement element = $$("div").get(2);
SelenideElement element2 = $$("div").find(text("xyz"));               // null
```

***Inputs, dropdowns and checkboxes***
___Inputs:___
```sh
$("#name").setValue(„Aleks");
$("#name").shouldHave(value(„Aleks"));
$("input[ng-model='user.company']").shouldBe(disabled);
$("input[ng-model='user.firstName']").shouldBe(enabled);
$("input[ng-model='user.firstName']").shouldBe(empty);
$("input[ng-model='user.company']").shouldHave(value("Goo"));         //partial match
$("input[ng-model='user.company']").shouldHave(exactValue("Google"));
```
___Checkboxes:___
```sh
$("input[type=checkbox]").click();
$("input[type=checkbox]").shouldBe(checked);
```
or
```sh
$("input[type=checkbox]").setSelected(true);
$("input[type=checkbox]").shouldBe(checked);
$("input[type=checkbox]", 1).setSelected(false);
$("input[type=checkbox]", 1).shouldNotBe(checked);
```
***Dropdown menu:***
___Only standard HTML selects___
```sh
$("#dropdown").selectOption("Option 2"); 		            //exact text match
$("#dropdown").selectOptionContainingText("ption 1"); 	//partial match
$("#dropdown").selectOption(3); 			                  //starting from 0, fourth option
$("#dropdown").selectOptionByValue("1");
$("#dropdown").getSelectedOption().shouldBe(disabled);
$("#dropdown").getSelectedOption().shouldHave(text("Option 1"), value("1"));
```
	
