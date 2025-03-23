
`std::move` is a utility function in the `<utility>` header that converts an object to an rvalue reference, allowing move semantics to take place. It does not actually move anything - it simply enables moving.

## Moving `std::unique_ptr`

`std::unique_ptr` cannot be copied, but it can be move

### Example 1: Transferring ownership

```cpp
#include <iostream>
#include <memory>

class Test {
public:
    Test() { std::cout << "Test created\n"; }
    ~Test() { std::cout << "Test destroyed\n"; }
};

int main() {
    std::unique_ptr<Test> uptr1 = std::make_unique<Test>();
    std::unique_ptr<Test> uptr2 = std::move(uptr1); // Ownership transferred

    if (!uptr1) {
        std::cout << "uptr1 is now null\n";
    }

    return 0;
}

```

Output:

```text
Test created
uptr1 is now null
Test destroyed

```

## Moving Return Values

Returning large objects efficiently by moving instead of copying.

```cpp
#include <iostream>
#include <vector>

std::vector<int> createVector() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    return std::move(vec); // Moves instead of copying
}

int main() {
    std::vector<int> myVec = createVector();
}

```

## Summary

| Scenario                            | Use `std::move` ? | Why?                          |
| ----------------------------------- | ----------------- | ----------------------------- |
| Moving `std::unique_ptr`            | ✅ Yes             | Transfers ownership           |
| Moving `std::vector`, `std::string` | ✅ Yes             | Avoids deep copy              |
| Returning large objects             | ✅ Yes             | Moves instead of copying      |
| Moving `std::shared_ptr`            | ❌ No              | `shared_ptr` supports copying |
