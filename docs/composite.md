# composite

The Composite pattern is a structural design pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly.

Here's a simple example in C++:

First, we define the `Component` class.

```cpp
class Component {
public:
    virtual void operation() const = 0;
    virtual ~Component() {}
};
```

Then, we define the `Leaf` class, which represents end objects of a composition.

```cpp
class Leaf : public Component {
public:
    void operation() const override {
        std::cout << "Leaf operation.\n";
    }
};
```

Next, we define the `Composite` class, which can store child components.

```cpp
class Composite : public Component {
public:
    void add(Component* component) {
        children.push_back(component);
    }

    void remove(Component* component) {
        children.erase(std::remove(children.begin(), children.end(), component), children.end());
    }

    void operation() const override {
        std::cout << "Composite operation. Components: \n";
        for (const Component* child : children) {
            child->operation();
        }
    }

private:
    std::vector<Component*> children;
};
```

Finally, we can use these classes like this:

```cpp
int main() {
    Composite composite;
    Leaf leaf1, leaf2;

    composite.add(&leaf1);
    composite.add(&leaf2);

    composite.operation();  // Outputs: "Composite operation. Components: Leaf operation. Leaf operation."

    return 0;
}
```

In this example, `Composite` and `Leaf` are subclasses of `Component`. `Composite` can store child `Component` objects, which can be either `Leaf` objects or other `Composite` objects. When `operation` is called on a `Composite`, it calls `operation` on each of its child components. This allows you to treat individual `Leaf` objects and compositions of objects (i.e., `Composite` objects) uniformly.