---
layout: post
title: Testing with XUnit and Moq
date:   2021-05-17 16:40:40
categories: 
- csharp
- test
---

## Testing with XUnit

In this article we will learn how to test your Web API with [XUnit](https://xunit.net/).

### What is XUnit

Is an open source tool for testing C# applications.

### How to configure

1. First you need to initilize your project:

    ```bash
    dotnet new webapi -n MoqXUnit
    ```

1. Then you need to initialize a XUnit project for testing

    ```bash
    dotnet new xunit -n MoqXUnit.Test
    ```

    This command will create a Test Project on your root folder.

1. Now you need to add MoqXUnit [project reference](https://docs.microsoft.com/pt-br/dotnet/core/tools/dotnet-add-reference) to MoqXUnit.Test

    ```bash
    dotnet add MoqXUnit.Test reference MoqXUnit
    ```

    Having the reference you can access classes from the other project. In another words, now you can test them.

Now we conclude the configuration part. Let's make some tests.


### Testing

Let's add some features to ours MoqXUnit Web API.

Create another controller calling CalculatorController inside MoqXUnit/Controller folder and add this code.

```csharp
using Microsoft.AspNetCore.Mvc;

namespace MoqXunit.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class CalculatorController : ControllerBase
    {
        [HttpGet]
        public ActionResult SumTwoNumbers([FromQuery] int num1, 
                                          [FromQuery] int num2)
        {            
            return Ok(num1 + num2);
        }
    }
}
```

SumTwoNumbers endpoint will only sum two numbers. Now let's add some tests.

Inside MoqXunit.Test add a .cs file and add a code more like:

```csharp
using System;
using Microsoft.AspNetCore.Mvc;
using MoqXunit.Controllers;
using Xunit;

namespace MoqXunit.Teste
{
    public class CalculatorControllerTest
    {
        [Theory]
        [InlineData(1, 2)]
        [InlineData(1, 5)]
        [InlineData(1, 6)]
        [InlineData(10, 2)]
        [InlineData(1999, 2)]
        public void Sum_Two_Numbers_using_theory(int num1, int num2)
        {
            //arrange
            CalculatorController controller = new CalculatorController();
            int expected = num1 + num2;

            //act
            var response = controller.SumTwoNumbers(num1, num2).Result as OkObjectResult;
            
            //assert
            Assert.NotNull(response);
            Assert.Equal(response.Value, expected);
        }

        [Fact]
        public void Sum_two_numbers_using_fact()
        {
            //arrange
            CalculatorController controller = new CalculatorController();
            int num1 = 1;
            int num2 = 2;
            int expected = num1 + num2;            

            //act
            var response = controller.SumTwoNumbers(num1, num2).Result as OkObjectResult;
            
            //assert
            Assert.NotNull(response);
            Assert.Equal(response.Value, expected);
        }
    }
}

```

XUnit has two types of anottations to say that this method is a Test Method: [Fact and Theroy](https://xunit.net/docs/getting-started/netfx/visual-studio).

- **Fact** for methods with invariant data.
- **Theory** with variant data and those data is set by using InlineData anottations.

Using Asset Methods you can validade the results from your test. Go check the available ones.


## Using Moq

[Moq](https://github.com/moq/moq4) is a library to Mock some interfaces to make testing easier.

### How to add to your test project

you can just execute the following command:

```bash
dotnet add .\MoqXunit.Teste\ package Moq
```

Change .\MoqXunit.Teste\ to the name of your project.

Now you have it installed.


### How to use Moq

You gonna use to mock some integrations that you don't want to execute in your test, like, databases.

Let's create a folder inside MoqXunit project called Interfaces and add a interface for a ICalculatorRepository.cs We are not implementing calculator repository, it's just an example.

```csharp
using System.Collections.Generic;
using MoqXunit.Models;

namespace MoqXunit.Interfaces 
{
    public interface ICalculatorRepository
    {
        IEnumerable<Calculation> GetAllCalculations();
        void SaveCalculation(Calculation calc);
    }
}
```

And let's create this Calculation class:

```csharp
namespace MoqXunit.Models
{
    public record Calculation
    {
        public int Value1 { get; init; }
        public int Value2 { get; init; }
        public int Result { get; init; }
        
    }
}
```

Now let's make some changes in our code to use this interface and calculation class.

```csharp
using System.Linq;
using Microsoft.AspNetCore.Mvc;
using MoqXunit.Interfaces;
using MoqXunit.Models;

namespace MoqXunit.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class CalculatorController : ControllerBase
    {
        private ICalculatorRepository _repository;

        public CalculatorController(ICalculatorRepository repository)
        {
            _repository = repository;
        }

        [HttpGet]
        public ActionResult SumTwoNumbers([FromQuery] int num1,
                                          [FromQuery] int num2)
        {

            var allCalculations = _repository.GetAllCalculations();
            if (allCalculations.Any(e => e.Value1 == num1 && e.Value2 == num2))
            {
                return Ok(allCalculations.First(e => e.Value1 == num1 && e.Value2 == num2));
            }
            else
            {
                var calculation = new Calculation
                {
                    Value1 = num1,
                    Value2 = num2,
                    Result = num1 + num2
                };
                
                _repository.SaveCalculation(calculation);

                return Ok(calculation);
            }
        }
    }
}
```

We add ICalculatorRepository as a dependency to our controller, and add a few changes on SumTwoNumbers to use GetAllCalculations and SaveCalculation method. Now we have this endpoint that if calculation exist in the database, it will return the result from it. Else it will create a instance of Calculation and save it with the result. The two paths will return Calculation object as response.

To test this controller we need to make some changes and configurate the responses from GetAllCalculation and SaveCalculation methods. We do not want to execute the implementation of this interface.

Moq solve this issue by using a class called Mock. With Mock you can create a setup to the interface by setting it's methods income and output when it will be called inside the method that we are testing. 

```csharp
[Fact]
        public void Sum_two_numbers_using_fact()
        {
            //arrange
            var mock = new Mock<ICalculatorRepository>();

            var controller = new CalculatorController(mock.Object);

            //... all the other operations above
        }
```
Instantiate a Mock object by setting ICalculatorRepository as the type and pass mock.Object as parameter to CalculatorController and now you have mocked ICalculatorRepository.

Inside SumTwoNumber method from CalculatorController we have a call to GetAllCalculations that will return all calculation in a IEnumerable. How to set that? By calling Setup and Return in mock instance.

Example:

```csharp
mock.Setup(e => e.GetAllCalculations()).Returns(Enumerable.Empty<Calculation>());
```

Our full method test will be something like this:

```csharp
        [Fact]
        public void Sum_two_numbers_using_fact()
        {
            //arrange
            var mock = new Mock<ICalculatorRepository>();
            mock.Setup(e => e.GetAllCalculations()).Returns(Enumerable.Empty<Calculation>());
            mock.Setup(e => e.SaveCalculation(It.IsAny<Calculation>()));
            var controller = new CalculatorController(mock.Object);

            int num1 = 1;
            int num2 = 2;
            int expected = num1 + num2;            

            //act
            var response = controller.SumTwoNumbers(num1, num2) as OkObjectResult;
            
            //assert
            Assert.NotNull(response);
            Assert.Equal(response.Value, expected);
        }
```

You can also mock a method from a class that does not have a interface by setting virtual in the method declaration.
