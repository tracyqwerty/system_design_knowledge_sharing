# adapter

## introduction

The Adapter pattern is a structural design pattern that allows objects with incompatible interfaces to work together. It wraps an existing class with a new interface so that it becomes compatible with the client's interface.

Here's a simple example in C++:

First, we define the `Target` interface, which is the interface the client expects to work with.

```cpp
class Target {
public:
    virtual void request() const {
        std::cout << "Target: The default target's behavior.\n";
    }
    virtual ~Target() {}
};
```

Then, we define an `Adaptee` class, which has a different interface.

```cpp
class Adaptee {
public:
    void specificRequest() const {
        std::cout << "Adaptee: The adaptee's behavior.\n";
    }
};
```

Next, we define the `Adapter` class, which makes `Adaptee` compatible with the `Target` interface.

```cpp
class Adapter : public Target {
public:
    Adapter(Adaptee* adaptee) : adaptee(adaptee) {}

    void request() const override {
        adaptee->specificRequest();
    }

private:
    Adaptee* adaptee;
};
```

Finally, we can use these classes like this:

```cpp
void clientCode(const Target* target) {
    target->request();
}

int main() {
    Adaptee* adaptee = new Adaptee;
    Target* adapter = new Adapter(adaptee);
    clientCode(adapter);

    delete adaptee;
    delete adapter;

    return 0;
}
```

In this example, `clientCode` is a function that works with objects of type `Target`. `Adaptee` is a class that has a `specificRequest` method, which is not compatible with the `request` method expected by `clientCode`. `Adapter` is a class that inherits from `Target` and contains an `Adaptee`. It overrides the `request` method and calls `specificRequest` on the `Adaptee`, making `Adaptee`'s interface compatible with `Target`'s interface.

Please note that in a real-world application, you would want to handle potential memory leaks and exceptions more carefully. For example, you might want to use smart pointers instead of raw pointers.

## adapter in c++ stl

In the C++ Standard Template Library (STL), an adapter is a container that adapts or modifies the interface of another container. The STL provides several container adapters, including `stack`, `queue`, and `priority_queue`.

A `queue` is a container adapter that provides a first-in, first-out (FIFO) data structure. It adapts a container to provide a specific set of member functions, allowing it to be used as a queue. The underlying container can be any of the standard sequence containers (`deque`, `list`, or `vector`), but by default, if no container is specified, `deque` is used.

Here's a simple example of how to use a `queue`:

```cpp
#include <queue>
#include <iostream>

int main() {
    std::queue<int> q;

    // Add elements to the queue
    q.push(1);
    q.push(2);
    q.push(3);

    // Access the first element
    std::cout << "Front of the queue: " << q.front() << "\n";  // Outputs: 1

    // Remove the first element
    q.pop();

    // Access the first element again
    std::cout << "Front of the queue after pop: " << q.front() << "\n";  // Outputs: 2

    return 0;
}
```

In this example, `push` is used to add elements to the end of the queue, `front` is used to access the first element, and `pop` is used to remove the first element. Note that `pop` does not return the removed element; to access the first element before removing it, you need to use `front`.

The `queue` adapter provides a restricted interface to the underlying container, ensuring that elements are only added at one end and removed from the other, maintaining the FIFO order.