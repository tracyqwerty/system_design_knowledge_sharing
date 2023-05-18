# iterator

The Iterator pattern is a design pattern that provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation. It involves two key types: the `Iterator` and the `Iterable` (or `Aggregate`).

Here's a simple example in C++:

First, we define the `Iterator` and `Iterable` interfaces.

```cpp
template<typename T>
class Iterator {
public:
    virtual bool hasNext() = 0;
    virtual T& next() = 0;
};

template<typename T>
class Iterable {
public:
    virtual Iterator<T>* createIterator() = 0;
};
```

Then, we define a concrete `Iterable` class, `ConcreteIterable`.

```cpp
template<typename T>
class ConcreteIterable : public Iterable<T> {
public:
    class ConcreteIterator : public Iterator<T> {
    public:
        ConcreteIterator(std::vector<T>& items) : items(items), position(0) {}

        bool hasNext() override {
            return position < items.size();
        }

        T& next() override {
            return items[position++];
        }

    private:
        std::vector<T>& items;
        int position;
    };

    void addItem(const T& item) {
        items.push_back(item);
    }

    Iterator<T>* createIterator() override {
        return new ConcreteIterator(items);
    }

private:
    std::vector<T> items;
};
```

Finally, we can use these classes like this:

```cpp
int main() {
    ConcreteIterable<int> iterable;
    iterable.addItem(1);
    iterable.addItem(2);
    iterable.addItem(3);

    Iterator<int>* iterator = iterable.createIterator();
    while (iterator->hasNext()) {
        std::cout << iterator->next() << std::endl;
    }

    delete iterator;

    return 0;
}
```

In this example, `ConcreteIterable` is an iterable object that can create `ConcreteIterator` objects. `ConcreteIterator` is an iterator that can iterate over the items in a `ConcreteIterable`.

When `createIterator` is called on `ConcreteIterable`, it returns a new `ConcreteIterator` for its items. The `hasNext` method of `ConcreteIterator` checks if there are more items to iterate over, and the `next` method returns the next item and advances the iterator.

Please note that in a real-world application, you would want to handle potential memory leaks and exceptions more carefully. For example, you might want to use smart pointers instead of raw pointers.