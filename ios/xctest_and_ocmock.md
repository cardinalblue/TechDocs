# Unit Test with XCTest and OCMock

## XCTest

### Divide the test method into three parts: `given`, `when`, `then`

- `given`: set up the environment and input variables.
- `when`: contain the code we want to test.
- `then`: check the result of our action.   

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

Add the prefix `DISABLED_` to the test method you want to disable, so the XCTest will skip the method since the method name no longer starts with the keyword `test`.

```
- (void)DISABLED_testSomthing
```

## OCMock

### Import

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

The problem with OCMClassMock is that the entire object is mocked, but sometimes we only want to mock some
parts of the object. `OCMockObject partialMock:` lets us use `OCMStub` object to replace the value we want to test, 
but the other behaviors of the object remain the same.

```
SomeClass *obj = [SomeClass new];
obj.somePublicProperty = someValue;

id mockObj = [OCMockObject partialMockForObject:obj];
OCMStub([mockObj someMethod]).andReturn(anotherValue);
```

## References

- [objc.io - XCTest](https://www.objc.io/issues/15-testing/xctest/)
