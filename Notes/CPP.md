# C++ 

A simple Hello World program written in c++

```cpp
#include<iostream>
using namespace std;

int main(){
    cout << "Hello Ubuntu from Yash";
    return 0;
}
```

Explanation

- `#include<iostream>`, we include the iostream file using the include directive
- `using namespace std` imports the std namespace, if we do not do this, we will need to do `std::cout` to use the cout function, we can also do, `using std::cout` to import just the cout function from the std namespace