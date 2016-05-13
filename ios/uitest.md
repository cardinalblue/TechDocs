# Automate UI Testing in iOS

## Intro to Automating UI tests
In iOS7, Apple introduced automating UI testing which helps developers to significantly reduce the amount of time in testing their apps.
The recording function records user's actions and automatically writes down the code in test methods so that later on when you want to test the same feature, UI test can run the whole process automatically.

## XCUI API - Accessibility
In order for the UITest to recognize the elements and interact with it, we need to make our elements **accessible**.

Add the below code in your object class
```
- (BOOL)isAccessibilityElement
{
    return YES;
}
```

Usually, we'll set the **accessibility identifier** in order for the UITest to recognize what the element is and perform the action.

```
- (NSString *)accessibilityIdentifier
{
    return @"image scrap view";
}
```

[Link to see what UIAccessibilityElement is about](https://developer.apple.com/library/tvos/documentation/UIKit/Reference/UIAccessibilityElement_Class/index.html)

## XCTest
