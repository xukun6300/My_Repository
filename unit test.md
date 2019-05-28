## Given-When-Then
All test methods should follow Given-When-Then style of representing test steps. This makes each individual test a logical, easy-to-understand, consistent sequence of steps.

Let’s describe each of the Given-When-Then steps in more detail:

**Given** — sets up a certain condition or creates the object(s) required to perform the test prior to executing the core test logic. This is effectively a pre-condition for your test.
Note that Given is not always necessary — sometimes there is no setup is needed for a particular test or common setup is performed before each test inside method annotated with @Before.


**When** — this is where the action we are testing is triggered.
```
// WHEN
String actualName = testSubject.getName();
```
**Then** — this is where we assert that once the test action took place, the state of the application is as expected (our code under test behaves the way we expect).
```
// THEN
assertTrue(expectedName.equals(actualName));
```
There are cases when explicit Then is not necessary. For instance, if When step is expected to throw an exception (as shown in the example above).


https://martinfowler.com/bliki/GivenWhenThen.html


## Test method names
The recommended test method naming convention is methodNameUnderTest_givenCondition_expectedBehavior where givenCondition is optional. Let’s see how it applies to CustomerTest.

ctor_givenNameIsNull_throwsException() consists of:

ctor indicates that we are testing constructor behavior
givenNameIsNull specifies condition when a null name is passed in to the constructor
throwsException indicates that when the condition is met (name is null), we will throw an exception. Note that @Test(expected = IllegalArgumentException.class) defines concrete exception we expect.

ctor_givenNameIsValid_setsName() consists of:

ctr indicates that we are testing constructor behavior
givenNameIsValid specifies condition when a non-null name is passed in to the constructor
setsName indicates that when the condition is met (name is non-null), class member name of our testCustomer should be set.

getName_returnsName() consists of:

getName indicates we are testing behavior of the getName() method
returnsName indicates that a valid non-null name should be returned.


Let’s test a simple Customer class that performs its own validation at construction time:

```
public class Customer {

    private final String name;

    public Customer(String name) {
        if (name == null) {
            throw new IllegalArgumentException("valid customer name is required");
        }
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

I see 3 potential candidates for testing:

Testing constructor if null parameter is passed in.
Testing constructor if non-null parameter is passed in.
Testing getName() method.
Once we test all of the above, the class will be fully tested (100% code coverage). Let’s implement those tests:
```
import static org.junit.Assert.assertTrue;

public class CustomerTest {

    Customer testSubject;

    @Test(expected = IllegalArgumentException.class)
    public void ctor_givenNameIsNull_throwsException() {
        // GIVEN
        String name = null;

        // WHEN
        new Customer(name);
    }

    @Test
    public void ctor_givenNameIsValid_setsName() {
        // GIVEN
        String expectedName = "linda";

        // WHEN
        testSubject = new Customer(expectedName);

        // THEN
        assertTrue(testSubject.getName().equals(expectedName));
    }

    @Test
    public void getName_returnsName() {
        // GIVEN
        String expectedName = "linda";
        testSubject = new Customer(expectedName);

        // WHEN
        String actualName = testSubject.getName();

        // THEN
        assertTrue(expectedName.equals(actualName));
    }
}
```

