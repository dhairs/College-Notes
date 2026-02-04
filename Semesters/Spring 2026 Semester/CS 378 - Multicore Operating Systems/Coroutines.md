## Stack-less Coroutines

Every time the function is called, local state is stored in some struct. This serves as the stack frame for that call to the function. The compiler can still do all the optimizations it wants to.

In addition, the struct stores the resume point of the function if it exited early.

The function can return to its caller, but the struct with the state can still be long-living and contain the state of the function. This means that the function is able to continued later. 

There must be a `lazy::promise_type` that is the implementation of what the compiler calls for suspending execution.

There must also be a `handle` that holds pointers to both of them. This handle gives each invocation a unique identity.

### Example

Lets say we call a recursive function `f`:

```cpp
lazy<int> f(long n) {
  printf("f(%ld) %lx\n", n, get_sp());
  if (n == 0) {
    co_return 1;
  } else {
    co_return n * co_await f(n-1);
  }
}
```

After reaching the await, the function will still return but store the state in the struct. Then, the calling function (the first one to have called `f`) needs to make sure that `f` continues running. 

So, there needs to be a `while not done` to ensure execution of the `f` coroutines.
