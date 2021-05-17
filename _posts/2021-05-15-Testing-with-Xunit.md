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
