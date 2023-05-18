# command

The Command pattern is a behavioral design pattern that turns a request into a stand-alone object that contains all information about the request. This transformation lets you pass requests as a method arguments, delay or queue a request's execution, and support undoable operations.

Here's a simple example in C++:

First, we define the `Command` interface.

```cpp
class Command {
public:
    virtual ~Command() {}
    virtual void execute() const = 0;
};
```

Then, we define a `Receiver` class, which performs some business logic.

```cpp
class Receiver {
public:
    void doSomething(const std::string& a) const {
        std::cout << "Receiver: Working on (" << a << ".)\n";
    }
};
```

Next, we define a `ConcreteCommand` class, which implements the `Command` interface and uses the `Receiver`.

```cpp
class ConcreteCommand : public Command {
public:
    ConcreteCommand(Receiver* receiver, std::string a) : receiver(receiver), a(a) {}

    void execute() const override {
        std::cout << "ConcreteCommand: Getting receiver to do something.\n";
        this->receiver->doSomething(this->a);
    }

private:
    Receiver* receiver;
    std::string a;
};
```

Finally, we define an `Invoker` class, which asks the command to carry out the request.

```cpp
class Invoker {
public:
    void setCommand(Command* command) {
        this->command = command;
    }

    void doSomething() {
        if (this->command) {
            this->command->execute();
        }
    }

private:
    Command* command;
};
```

We can use these classes like this:

```cpp
int main() {
    Invoker* invoker = new Invoker;
    Receiver* receiver = new Receiver;
    Command* command = new ConcreteCommand(receiver, "Hello");
    invoker->setCommand(command);
    invoker->doSomething();

    delete invoker;
    delete receiver;
    delete command;

    return 0;
}
```

In this example, `ConcreteCommand` is a command that performs some action in the `Receiver`. The `Invoker` sets the command it will execute with `setCommand`, and when `doSomething` is called on the `Invoker`, it calls `execute` on the command.

Please note that in a real-world application, you would want to handle potential memory leaks and exceptions more carefully. For example, you might want to use smart pointers instead of raw pointers.