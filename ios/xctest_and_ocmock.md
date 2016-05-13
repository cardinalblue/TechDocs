# Unit Test with XCTest and OCMock

## XCTest

### Split the test method with `Given`, `When`, `Then` 

The `given` section sets up the environments and input variables.
The `when` section contains the code we want test.
The `then` section checks the result of our action.

```
- (void)testThatItDoesURLEncoding
{
    // given
    NSString *searchQuery = @"$&?@";
    HTTPRequest *request = [HTTPRequest requestWithURL:@"/search?q=%@", searchQuery];

    // when
    NSString *encodedURL = request.URL;

    // then
    XCTAssertEqualObjects(encodedURL, @"/search?q=%24%26%3F%40");
}
```

### Disable a Test

Add a prefix `DISABLED_` to the test method you want to disabled, and the XCTest will skip the method since the method name no longer starts with `test`.

```
- (void)DISABLED_testSomthing
```

## OCMock

### First Import

```
#import <OCMock.h>
```

### Mock Object with `OCMClassMock`

```
id mockObj = OCMClassMock([TheClassYouWantToMock class]);
```

### Set the Mock Object Value with `OCMStub`

```
OCMStub([mockObj someMethodOrProperty]).andReturn(someValue);
```

### Partial Mock Object with `OCMockObject partialMock:`


## References

[objc.io - XCTest](https://www.objc.io/issues/15-testing/xctest/)
