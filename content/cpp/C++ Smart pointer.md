We have 3 type smart pointer can be used in C++: unique_ptr, shared_ptr, weak_ptr

## `std::unique_ptr`

- Exclusive ownership: Only one `unique_ptr` can own an object at a time.
- Automatically deletes the object when it goes out of the scope.
- Supports move semantics (`std::move`), but not copy semantics

Example 1
```cpp
# main.cpp

#include <iostream>
#include <memory>

class Test {
public:
    Test() { std::cout << "Test created\n"; }
    ~Test() { std::cout << "Test destroyed\n"; }
    void show() { std::cout << "Test function\n"; }
};

int main() {
    std::unique_ptr<Test> ptr1 = std::make_unique<Test>(); // Preferred way to create unique_ptr
    ptr1->show();

    // Transfer ownership using std::move
    std::unique_ptr<Test> ptr2 = std::move(ptr1);
    if (!ptr1) {
        std::cout << "ptr1 is now null\n";
    }
    
    return 0;
}

```

Output
```text
Test created
Test function
ptr1 is now null
Test destroyed
```

Example 2
```cpp

#include <iostream>
#include <memory>

int main() {
    // Allocate an array of integers
    std::unique_ptr<int[]> arr = std::make_unique<int[]>(5);

    // Initialize array elements
    for (int i = 0; i < 5; ++i) {
        arr[i] = i * 10;
    }

    // Access elements
    for (int i = 0; i < 5; ++i) {
        std::cout << arr[i] << " ";
    }

    // No need to call delete[], unique_ptr will clean up automatically
    return 0;
}


```


## `std::shared_ptr`

- Shared ownership: Multiple `shared_ptr` instances can own the same object.
- Uses reference counting to manage object lifetime.
- The object is deleted when the last `shared_ptr` goes out of scope.

Example
```cpp
#include <iostream>
#include <memory>

class Test {
public:
    Test() { std::cout << "Test created\n"; }
    ~Test() { std::cout << "Test destroyed\n"; }
};

int main() {
    std::shared_ptr<Test> ptr1 = std::make_shared<Test>(); // Preferred way to create shared_ptr
    std::shared_ptr<Test> ptr2 = ptr1; // Shared ownership
    
    std::cout << "Reference count: " << ptr1.use_count() << "\n"; // 2

    return 0;
}

```

Output

```text
Test created
Reference count: 2
Test destroyed
```


>[!tip] Passing a `std::shared_ptr<T>` to a function
> We typically want to avoid unnecessary reference count increments when passing a `std::shared_ptr<T>` to a function parament. The best way to do this is by passing it as a `const std::shared_prt<T>&`


## `std::weak_ptr`

- Works with `std::shared_ptr` but does not contribute to reference count.
- Prevents circular reference issues.
- Used to check if an object still exists without owning it.

Example:
```cpp
#include <iostream>
#include <memory>

class Test {
public:
    Test() { std::cout << "Test created\n"; }
    ~Test() { std::cout << "Test destroyed\n"; }
};

int main() {
    std::shared_ptr<Test> sharedPtr = std::make_shared<Test>();
    std::weak_ptr<Test> weakPtr = sharedPtr; // Does not increase reference count

    std::cout << "Reference count: " << sharedPtr.use_count() << "\n"; // 1

    if (auto sp = weakPtr.lock()) { // Check if the object still exists
        std::cout << "Object is still alive\n";
    }

    return 0;
}

```

Output:
```text
Test created
Reference count: 1
Object is still alive
Test destroyed

```

## Summary

| Smart Pointer     | Ownership  | Copyable?     | Reference Counting | Best Used For                  |
| ----------------- | ---------- | ------------- | ------------------ | ------------------------------ |
| `std::unique_ptr` | Exclusive  | ❌ (move only) | ❌                  | Managing single objects        |
| `std::shared_ptr` | Shared     | ✅             | ✅                  | Shared ownership of objects    |
| `std::weak_ptr`   | Non-owning | ✅             | ❌                  | Avoiding circular dependencies |

