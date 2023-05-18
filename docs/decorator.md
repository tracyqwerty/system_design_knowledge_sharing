# decorator

The Decorator pattern is a structural design pattern that allows you to add new behaviors to objects dynamically by placing these objects inside special wrapper objects. Using decorators, you can stack behaviors dynamically at runtime.

Here's a simple example in C++:

First, we define the `Component` interface.

```cpp
class Component {
public:
    virtual ~Component() {}
    virtual std::string operation() const = 0;
};
```

Then, we define a `ConcreteComponent` class, which provides default behavior.

```cpp
class ConcreteComponent : public Component {
public:
    std::string operation() const override {
        return "ConcreteComponent";
    }
};
```

Next, we define the `Decorator` base class, which follows the same interface as the other components and keeps a reference to a decorated component.

```cpp
class Decorator : public Component {
protected:
    Component* component;

public:
    Decorator(Component* component) : component(component) {}

    std::string operation() const override {
        return this->component->operation();
    }
};
```

Finally, we define some `ConcreteDecorator` classes, which add new behaviors.

```cpp
class ConcreteDecoratorA : public Decorator {
public:
    ConcreteDecoratorA(Component* component) : Decorator(component) {}

    std::string operation() const override {
        return "ConcreteDecoratorA(" + Decorator::operation() + ")";
    }
};

class ConcreteDecoratorB : public Decorator {
public:
    ConcreteDecoratorB(Component* component) : Decorator(component) {}

    std::string operation() const override {
        return "ConcreteDecoratorB(" + Decorator::operation() + ")";
    }
};
```

We can use these classes like this:

```cpp
void clientCode(const Component* component) {
    std::cout << "RESULT: " << component->operation() << "\n";
}

int main() {
    Component* simple = new ConcreteComponent;
    clientCode(simple);  // Outputs: RESULT: ConcreteComponent
    std::cout << "\n";

    Component* decorator1 = new ConcreteDecoratorA(simple);
    Component* decorator2 = new ConcreteDecoratorB(decorator1);
    clientCode(decorator2);  // Outputs: RESULT: ConcreteDecoratorB(ConcreteDecoratorA(ConcreteComponent))

    delete simple;
    delete decorator1;
    delete decorator2;

    return 0;
}
```

In this example, `ConcreteDecoratorA` and `ConcreteDecoratorB` are decorators that add new behaviors to the `Component` they decorate. When `operation` is called on a decorator, it delegates the call to the decorated component and then adds its own behavior to the result.

Please note that in a real-world application, you would want to handle potential memory leaks and exceptions more carefully. For example, you might want to use smart pointers instead of raw pointers.