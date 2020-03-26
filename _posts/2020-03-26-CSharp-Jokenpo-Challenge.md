---
layout: post
title: CSharp - Jokenpo Challenge
date:   2020-03-26 11:37:40
categories: 
- csharp
---
_You can check the [repository right here](https://github.com/luturol/jokenpo)._
## Jokenpo Challenge

I like to solve problems and challenges, they make me feel excited about coding because I have to be on my best game and try to solve the problem is exciting . It gives that feel of accomplishment and victory when you finished.

The challenge consist of making a Jokenpo game logic, by all means, you must implement the rules of the game. Rock wins against Scissor and lose against Paper, Paper wins against Rock and lose against Scissor, Scissor wins against Paper and lose against Rock. How can we implement that in C#?

For this I thought that I must have some way of validation. The validation I wanted was to make it more "generic" and easy to create. Each validation only works for that one had form. To do it, I made an Enum for Hand forms:

```csharp
public enum HandForm
{
    Rock,
    Paper,
    Scissor
}
```

Now the problem is: _How to validate the Enum? How the Enum will have it's own Rule?_

The way I thought of solving was: create an extension for this enum that will return the **Rule Class**.

```csharp
public static class HandFormExtensions
{
    public static AbstractRules ToRule(this HandForm handForm)
    {
        if (handForm == HandForm.Rock)
            return new RockRules();
        else if (handForm == HandForm.Paper)
            return new PaperRules();
        else if (handForm == HandForm.Scissor)
            return new ScissorRules();
        else
            throw new ArgumentException("There is no hand form rule for this option");
    }
}   
```

Rule class will implement the AbstractRule class that will contain an abstract method that returns the result of that play, this means that the Rule class will have the checks for that hand form against the opponent hand form.

```csharp
public abstract class AbstractRules
{
    public abstract GameResult WinAgainst(HandForm opponent);
}
```

Now the Judge of the Jokenpo will have only one line of code:

```csharp
public GameResult ValidateGame(Player player1, Player player2)
{
    return player1.HandForm.ToRule().WinAgainst(player2.HandForm);             
}
```

So, whenever someone call the Judge class to validate the game, it will only return the result of the game based on the first Player passed as Parameter.


That's it folks. Don't forget to eat clean and drink water.

Peace.
