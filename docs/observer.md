# Observer

The Observer pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods. It is mainly used for implementing distributed event handling systems.

Here's a simple example in C++:

First, we define the `Observer` class and the `Subject` class.

```cpp
#include <vector>
#include <algorithm>

class Observer {
public:
    virtual void update(int value) = 0;
};

class Subject {
public:
    void addObserver(Observer* observer) {
        observers.push_back(observer);
    }

    void removeObserver(Observer* observer) {
        observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
    }

    void notifyObservers() {
        for (Observer* observer : observers) {
            observer->update(value);
        }
    }

    void setValue(int value) {
        this->value = value;
        notifyObservers();
    }

private:
    std::vector<Observer*> observers;
    int value;
};
```

Then, we define some concrete `Observer` classes.

```cpp
class ConcreteObserverA : public Observer {
public:
    void update(int value) override {
        std::cout << "ConcreteObserverA: " << value << std::endl;
    }
};

class ConcreteObserverB : public Observer {
public:
    void update(int value) override {
        std::cout << "ConcreteObserverB: " << value << std::endl;
    }
};
```

Finally, we can use these classes like this:

```cpp
int main() {
    Subject subject;
    ConcreteObserverA observerA;
    ConcreteObserverB observerB;

    subject.addObserver(&observerA);
    subject.addObserver(&observerB);

    subject.setValue(123);  // Both observers will receive this update

    subject.removeObserver(&observerA);

    subject.setValue(456);  // Only observerB will receive this update

    return 0;
}
```

In this example, `ConcreteObserverA` and `ConcreteObserverB` are observers of `Subject`. When `setValue` is called on `Subject`, it notifies all of its observers by calling their `update` method. If an observer is removed from the subject using `removeObserver`, it will no longer receive updates.