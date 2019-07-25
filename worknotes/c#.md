# c# related knowledge 

### IServiceProvider (service allocator) 
https://stackify.com/service-locator-pattern/


## language

### class vs structs
class is reference type
structs is a value type 

## functional programming 
> http://hamidmosalla.com/2019/04/25/functional-programming-in-c-sharp-a-brief-guide/#Immutable_Types

why ? 
- concurrent programming 

### fundamental principles 
- Pure functions doesn’t cause any side effects
- Referential transparency,
```c#
// this is not referentially transparent. because of now 
public int CalculateElapsedDays(DateTime from)
{
     DateTime now = DateTime.Now;
     return (now - from).Days;
}

// this is 
public static int CalculateElapsedDays(DateTime from, DateTime now) => (now - from).Days;
```

- function honesty
```c#
// NOT honest because of 0 
public int Divide(int numerator, int denominator)
{
   return numerator / denominator;
}
```
### first-class citizens
which means they can be assigned to function 

### HOF 
like `where`



### pure function & impure function 
avoid state mutation, why ? because of the parallelization
`zip` function 



## Functional programming examples 
- Imuutable Types
- expression instead of statement 
- function composition 
    -  is the act of creating a new function by combining two functions together 
- method chaining 
- Not creating unnecessary types using `yield` keyword
- Declarative programming instead of imperative programming using LINQ
- Thread-Safe Collections
- command query separation 
- partial application 
- curried function 



## OOP 

### Interface 
why ? 
> Using interface-based design concepts provides loose coupling, 
> component-based programming, easier maintainability, makes your code base 
> more scalable and makes code reuse much more accessible because the  
> implementation is separated from the interface.


### dependency injection 
https://www.codementor.io/mrfojo/c-with-dependency-injection-k2qfxbb8q

This is also why DI is an implementation of the Inversion of control (IoC) principle.

The provided object will satisfy the dependency during program execution but would not be known at compile time.

- constructor injection 
```c#
public class UserLogic
{
    private GoogleOAuthService _authService;
    private IEmailService _emailService; // dependency 

    public UserLogic(IEmailSevice emailService)
    {
        _authService = new GoogleOAuthService();
        _emailService = emailService;
    }
    ...
}
```
- setter injection 
- method injection
```c#
OutlookEmailService outlookEmailService = new OutlookEmailService();
UserLogic userLogic = new UserLogic()
{
    EmailService = outlookEmailService
};
```

