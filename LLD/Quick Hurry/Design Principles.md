 - Two types of principles  -  **General software design principles** and **object-oriented design principles**

## General Software Design Principles

KISS - Keep It Simple, Stupid
- always try to keep it simple and don't over engineer 

DRY - Don't Repeat Yourself
- dont repeat the same code 
- logic should be conceptually same 
- "I expect this validation logic to appear in multiple places, but I'm going to start by keeping it in the User class to avoid adding unnecessary complexity early. If we see it duplicated three or four times, we can pull it into a shared validator."

YAGNI - You Aren't Gonna Need It
- This principle doesn't mean "never think ahead" - it means don't build ahead. Design with extension in mind, but only implement what's needed now.
- "how would you extend this?" That's your cue to talk about how you'd modify the design if new requirements appeared. But in your initial design, stick to what's actually needed.

Separation of Concerns
- Different parts of your code should handle different responsibilities, and they shouldn't know about each other's internals.
- UI shouldn't know business logic, business logic shouldn't how data is stored  and data access layer should not format etc 

Bad Scenario (DSA code)
```java
import java.util.Scanner;
class TicTacToe {
  char[][] board = new char[3][3];
  void play() {
    Scanner scanner = new Scanner(System.in);
    while (true) {
      // Display mixed with game logic
      for (int i = 0; i < 3; i++) {
        System.out.println(board[i]);
      }
      // Input handling mixed in
      int row = scanner.nextInt();
      int col = scanner.nextInt();
      board[row][col] = 'X';
      // Win checking mixed in
      if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) {
        System.out.println("Winner!");
        break;
      }
    }
    scanner.close();
  }
}
```


Good Scenario
```java
class TicTacToe {
  Board board;
  Display display;
  InputHandler input;
  
  void play() {
    while (!board.hasWinner()) {
      display.render(board);
      Move move = input.getNextMove();
      board.makeMove(move);
    }
    display.showWinner(board.getWinner());
  }
}
```


Law of Demeter
- A method should only talk to its immediate friends, not reach through objects to access distant parts of the system.
- actually very cool and never thought of law (I should have known this law brother)
- method chaining is not the problem

bad practise 
```
order.getCustomer().getAddress().getZipCode()
```
Because you are going deeper and deeper into how the object and its internal 

good practise 
```
Order called getCustomerZipCode()
```
above is good because there is one function which works on going into internals 


## Object-Oriented Design Principles (SOLID)

Single Responsibility Principle 
- A class having one role only - create more class for different work

Open Closed Principle
- open for extension, closed for modifications

Bad 
```java
class PaymentProcessor {
  void process(String type, double amount) {
    if (type.equals("credit")) {
      // credit card logic
    } else if (type.equals("paypal")) {
      // paypal logic
    }
    // Adding crypto means modifying this method
  }
}
```

Good 
```java
interface PaymentMethod {
  void process(double amount);
}

class CreditCardPayment implements PaymentMethod {
  public void process(double amount) { /* credit card logic */ }
}

class PayPalPayment implements PaymentMethod {
  public void process(double amount) { /* paypal logic */ }
}

class CryptoPayment implements PaymentMethod {
  public void process(double amount) { /* crypto logic */ }
}

class PaymentProcessor {
  void process(PaymentMethod method, double amount) {
    method.process(amount);
  }
}
```


LSP - Liskov Substitution Principle
- _“Can I replace parent with child safely?”
- 




ISP
- _“Am I forcing clients to implement unused methods?”_ 


