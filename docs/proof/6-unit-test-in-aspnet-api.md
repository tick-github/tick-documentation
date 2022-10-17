# Unit Testing in a backend ASP.NET API

- [Unit Testing in a backend ASP.NET API](#unit-testing-in-a-backend-aspnet-api)
- [Intro](#intro)
  - [Unit Testing a Repository](#unit-testing-a-repository)
  - [Unit Testing a Controller](#unit-testing-a-controller)

# Intro

Unit testing is an important tool to verify a customer's needs on a technical level. Once you have your criteria set up, each time you make a change to your code, you can use the unit test to verify if your code still does what you intended it to do. Of course, this assumes the unit test you made is a valid unit test.

Unit testing the controllers and repositories inside an ASP.NET Core API is a straightforward job. In these tests I make use of the `xUnit` .NET testing framework, along with `FluentAssertions` for general test code readability.

You can read more about xUnit and FluentAssertions here:

- [xUnit](https://xunit.net/)
- [FluentAssertions](https://fluentassertions.com/about/)

## Unit Testing a Repository

Imagine you have implemented the repository pattern inside your API, to act as a gateway between your data store and your controller. Great thinking! The repository could look a bit like this:

```cs
public class OrderRepository {

    public List<Order> Orders { get; set; }

    public OrderManager() {
        Orders = new List<Order>();
    }

    public Response AddOrder(Order order) {  ...  }

    public Response<Order> GetOrder(string guid) {  ...  }
}
```

Assuming you have some conditions inside your `AddOrder` and `GetOrder` methods, you would want to test those conditions to assure they return the appropriate response when supplied with certain input. This is where Unit Testing comes in handy.

(the data store in this case is an in-memory list. If you have an EF data store, you would have to find a way to mock it.)

A pretty straightforward test for `AddOrder` would be:

```cs
[Fact]
public void AddOrder_WithNormalOrder_ShouldPopulateOrderList() {

    // Arrange
    var input = new Order();
    var response = new Response();
    
    // Act
    var action = () => response = _orderRepository.AddOrder(input);

    // Assert
    action.Should().NotThrow();
    response.Successful.Should().BeTrue();
    _orderManager.Orders.Should().NotBeEmpty()
        .And.HaveCount(1)
        .And.Contain(input);
}
```

Using the [Arrange-Act-Assert pattern](https://automationpanda.com/2020/07/07/arrange-act-assert-a-pattern-for-writing-good-tests/), we first define our set up variables, in this case a valid input (**Arrange**).

We then "do the thing" we are testing (**Act**), and assert the outcomes (**Assert**).

FluentAssertions makes this as readable as possible. We want the action to not throw an exception, the response should be successful and the data store should now contain one entry, which is `input`.

If, for instance, you have a condition that checks if the input has a `TableId` value of 0 or greater, you write a test for that:

```cs
public void AddOrder_WithNegativeTableId_ShouldReturnANegativeResponse() {

    // Arrange
    var input = new Order {TableId = -1};
    var response = new Response();

    // Act
    var action = () => response = _orderRepository.AddOrder(input);

    // Assert
    action.Should().NotThrow();
    response.Successful.Should().BeFalse();
}
```

## Unit Testing a Controller

Unit Testing a controller is a bit trickier. A requirement of a unit test is that the test should not have any dependencies. It should be as isolated as possible.

Our controller looks something like this:

```cs
public class OrderController : ControllerBase {

    private readonly IOrderRepository _orderRepository;

    public OrderController( IOrderManager orderManager) {
        _orderManager = orderManager;
    }

    // some controller endpoints
}
```

Oh no... it has a dependency. But we still want to unit test it. In this case, it is best to try and mock the dependency. There are a lot of frameworks and packages that can help you with that. A popular C# framework is `Moq`. 

The `CreateOrder` endpoint (which calls the repository's `AddOrder`) will have a test like this:

```cs
/* setup */
private readonly Mock<IOrderRepository> _mockOrderRepository;
private readonly OrderController _orderController;

public OrderControllerTests() {
    _mockOrderRepository = new Mock<IOrderRepository>();
    _orderController = new OrderController(_mockOrderRepository.Object);
}
/* setup end */

[Fact]
public void CreateOrder_WithCorrectOrderParameters_ShouldReturnOK() {

    // Arrange
    _mockOrderRepository
        .Setup(repository => repository.AddOrder(It.IsAny<Order>()))
        .Returns(new Response
        {
            Message = "Mock Success",
            Successful = true
        });

    /* some actions and asserts */
}
```

I will focus on the mocking part, as the act and arrange are self-explanatory. 

With `Moq`, you can make a 'pretend' class. In this case, a 'pretend' OrderRepository. Since we are only testing the controller, we pretend that the repository dependency returns a value. In the unit test of the controller, we simply do not care about what is going on in the repository, we just want to know how the controller will react to the value.

With each test, we arrange the mock repository, and make it return a predetermined value that will be passed on to the controller. In the above code snippet, the repository will return a successful response every time its `AddOrder` method will be called, within the scope of this fact.

This way we can focus on the controller, without wasting time, energy and error handling of the repository.

For more information on `Moq`, see: https://github.com/Moq
