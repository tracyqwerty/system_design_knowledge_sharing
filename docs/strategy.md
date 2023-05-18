# strategy

The Strategy pattern is a behavioral design pattern that turns a set of behaviors into objects and makes them interchangeable inside the original context object. The original object, called context, holds a reference to a strategy object and delegates it executing the behavior. In order to change the way the context performs its work, other objects may replace the currently linked strategy object with another one.

Here's a simple example in C++:

First, we define the `Strategy` interface.

```cpp
class Strategy {
public:
    virtual ~Strategy() {}
    virtual std::string execute() const = 0;
};
```

Then, we define some `ConcreteStrategy` classes.

```cpp
class ConcreteStrategyA : public Strategy {
public:
    std::string execute() const override {
        return "ConcreteStrategyA: Execute strategy A.";
    }
};

class ConcreteStrategyB : public Strategy {
public:
    std::string execute() const override {
        return "ConcreteStrategyB: Execute strategy B.";
    }
};
```

Next, we define the `Context` class, which uses a `Strategy`.

```cpp
class Context {
private:
    Strategy* strategy;

public:
    Context(Strategy* strategy) : strategy(strategy) {}

    ~Context() {
        delete this->strategy;
    }

    void setStrategy(Strategy* strategy) {
        delete this->strategy;
        this->strategy = strategy;
    }

    void executeStrategy() const {
        std::cout << this->strategy->execute() << "\n";
    }
};
```

Finally, we can use these classes like this:

```cpp
int main() {
    Context* context = new Context(new ConcreteStrategyA);
    context->executeStrategy();  // Outputs: ConcreteStrategyA: Execute strategy A.

    context->setStrategy(new ConcreteStrategyB);
    context->executeStrategy();  // Outputs: ConcreteStrategyB: Execute strategy B.

    delete context;

    return 0;
}
```

In this example, `ConcreteStrategyA` and `ConcreteStrategyB` are strategies that implement a specific behavior. The `Context` class uses a `Strategy` to execute a behavior. By changing the `Strategy` it uses with `setStrategy`, the `Context` can change its behavior at runtime.

Please note that in a real-world application, you would want to handle potential memory leaks and exceptions more carefully. For example, you might want to use smart pointers instead of raw pointers.