# Automate UI Testing in iOS

## Intro to Automating UI tests
In iOS7, Apple introduced automating UI testing which helps developers to significantly reduce the amount of time in testing their apps.
The recording function records user's actions and automatically writes down the code in test methods so that later on when you want to test the same feature, UI test can run the whole process automatically.

## XCUI API - Accessibility
In order for the UITest to recognize the elements and interact with it, we need to make our elements **accessible**.

Add the below code in your object class
```objective-c
- (BOOL)isAccessibilityElement
{
    return YES;
}
```

Usually, we'll set the **accessibility identifier** in order for the UITest to recognize what the element is and perform the action.

```objective-c
- (NSString *)accessibilityIdentifier
{
    return @"image scrap view";
}
```

Some useful hint:

When you're setting the accessibility identifier, it's better to also set the **_accessibility label_** to be the same as the identifier.
The reason behinds thats is it will be easy for your to debug your code. 

When you use the simulator, once you enable the accessibility inspector, you can click the element to check it's label (aka. identifier) in this case. However, make sure you set the label back to what it was after you're done testing because you do not want the people who actually use VoiceOver clicks on the view and hear something random.

Go to **Settings -> General -> Accessibility -> turn on VoiceOver**,

[Link to see what UIAccessibilityElement is about](https://developer.apple.com/library/tvos/documentation/UIKit/Reference/UIAccessibilityElement_Class/index.html)

## XCTest

Once you open the UITest class, you will see three functions **setUp()**, **tearDown()** and **testExample()**.
Everything in the **setUp()** will be run **_EVERY TIME_** when it's running a new test function.
And once a test function is done, it will run **tearDown()**.

---------------------------------------------------------------------
Click the red button to record certain actions, you will see the codes written in _testExample()_.
Most of time, you will have to rewrite the code, but the recording function gives you a good start.


Recording:
```swift
    func testExample() {
        // Use recording to get started writing UI tests.
        // Use XCTAssert and related functions to verify your tests produce the correct results.
        let app = XCUIApplication()
        app.navigationBars["Sent Memes"].buttons["Add"].tap()
        
        let toolbarsQuery = app.toolbars
        toolbarsQuery.buttons["Pick an Image"].tap()
        app.tables.buttons["Camera Roll"].tap()
        app.collectionViews["PhotosGridView"].cells["Photo, Landscape, March 13, 2011, 8:17 AM"].tap()
        
        // Below is the code that's being written when you click on the textfield
        let element = app.childrenMatchingType(.Window).elementBoundByIndex(0).childrenMatchingType(.Other).element.childrenMatchingType(.Other).element
        element.childrenMatchingType(.TextField).elementBoundByIndex(0).tap()
        app.buttons["Done"].tap()
    }
```

Modified:
```swift
    func testExample() {
        // Use recording to get started writing UI tests.
        // Use XCTAssert and related functions to verify your tests produce the correct results.
        
        let app = XCUIApplication()
        app.navigationBars["Sent Memes"].buttons["Add"].tap()
        
        // choose an image from camera roll
        app.toolbars.buttons["Pick an Image"].tap()
        app.tables.buttons["Camera Roll"].tap()
        app.collectionViews["PhotosGridView"].cells["Photo, Landscape, March 13, 2011, 8:17 AM"].tap()
        
        // tap on the textfield to edit
        app.textFields["TopTextfield"].tap()
        
        // manually type the text in textfield
        app.typeText("PicCollage")
        
        app.buttons["Done"].tap()
        
        let currentImage = app.images["MemeImage"]
  
        // Check if the image exists on the view
        XCTAssert(currentImage.exists)
    }
```

When you click on the textfield, UITest does not know what you are typing.
Therefore, you will have to manually add `app.typeText("PicCollage")` to enter text.

