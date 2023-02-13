## Test pyramid:

![[testing-pyramid.png]]

## Test doubles

- Dummy
- Stub
- Spy
- Fake
- Mock

==One of the most important aspect of the unit testing is to understand the above test doubles and learn which to use when==. 

### Dummy

- Objects are passed around but never actually used. Usually they are just used to fill parameter lists.
- Usually they have no behaviour, all their methods return null or nothing. We use them because we need to comply with some interface and we are not particulary interested in what they do.
- Sometimes we might even want dummy to throw an exception if they are used (why? see when do i use section below to understand).

#### when do i use it?
1. When we are not worried about implementation details of a method or interface like a logger. we may need to instantiate logger for unit test to pass but we are not intersted in how its used. This is the case for a dummy.
2. It can also be use to ensure that a particular piece of code is not executed under the condition of the test. You might use this to test some branching logic. (you might want to throw an exception when dummy is used). Example:

``` typescript
function someFunction() {
  if (someCondition) {
    this.dependencyA.methodA();
  } else {
    this.dependencyB.methodB();
  }
}
```
		if dependencyB is called it should thow an error failing the unit test.
_______________________________________________________________________________

### Fake

- Objects actually have some working implementations, but usually take some shortcut which makes them not suitable for production. Example: InMemoryTestDatabase (https://martinfowler.com/bliki/InMemoryTestDatabase.html)
- It has same business logic behaviour as the real component, but using a simplified implmentation, they take some shortcurt and have simplified version of production code.

#### When do i use it?
-  To fake a stateful component. Example: Database backed service.
	- In this case we can use in memory db, this fake implementation will not engage database, but will use a simple collection to store data.

### Stub

- Provides pre-defined/hard-coded answers/values to calls made during the test.
- It usually just returns a pre-defined, predictable data when its methods are called.w
- ==returns an data/value/object which can be controlled==.

#### When to use it?
- When we don't want objects to return real-time data or ==have undesired side effects==.
- To ensure that the code you are testing has known, predictable data on which to operate.

### Spy

-  These are stubs that also record some information based on how they are called. Example: Email service that records how many messages it was sent.
- ==Recording the calls mde to it so that you can check that it was called with correct parameters==.

#### When to use it?
- When the dependency in your test also has a dependency and you want to make sure that the inner dependency is resolved.
- You use a spy when you want to be sure that, under the conditions of your test, a certain dependency got called, and with certain parameters.
- Example: Suppose you’re writing a test for a user onboarding flow, and when the user successfully completes their onboarding, they should receive a welcome email. You have a separate dependency `EmailManager` that has a method `send()` on it, and you’ll use this to send the email.
	``` typescript 
describe("when the user completes onboarding", () => {
  it("sends a welcome email to their address", () => {
    const emailManagerSpy = new EmailManagerSpy();
    const onboardingFlow = new OnboardingFlow(emailManagerSpy);

    onboardingFlow.complete();

    expect(emailManagerSpy.send).toHaveBeenCalledWith("user@example.com", "Welcome!");
  });
})
```




## Questions:

1. How to decide the single unit for unit testing? sometimes testing a whole class is better and easier than testing a single method. Are there any strategies or techniques to decide a single unit?