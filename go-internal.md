1. Statically Typed Languages

- Type checking before program runs.
- You must declare the data types of variables.
- Type errors are caught before prog executes.
- eg. Java, C, C++, GO

**Example**

- int age = 25; // OK
- age = "Ryan"; // ❌ Compile-time error

**Compiler enforces types early - the code won't run even if types don't match**

2. Strongly Typed Languages

- Types are strictly enforced - you cannot perform ops on mismatched types without explicit conversion.

**Example**

- age = 25
- name = "Ryan"
- print(age + name) # ❌ TypeError

- print(str(age) + name) # ✅ Works

**Strong typing prevents implicit or unsafe type conversions**

**Go Core Philosophy**

1. Fast compile times
2. Simple syntax
3. Concurrency

# How Go operates under the hood

1. Compiled Language

- Go compiles directly to machine code using the gc **Go Compiler** targeting fast startup and runtime performance.

2. Go Runtime

- The Go routine handles:

1. Goroutine scheduling
2. Garbage collection
3. Stack management
4. Channels & select logic
5. timers

# What are Goroutines & concurrency

- They are lightweight threads managed by the Go runtime.

- Each goroutine starts with 2kb of stack
- Cheap as compared to OS threads

**Mutual Exclusion**

- var mu sync.Mutex
- **(Mutex)** Short for mutual exclusion. It prevents simultaneous access to a resource, used for locking shared data.

- mu.Lock()
- counter++
- mu.Unlock()

**Locks in Go**

1. sync.Mutex

- Basic mutual exclusion

2. sync.RWMutex

- Allow multiple readers, but only one writer.

3. sync.Once

- Run a function once (singleton hit)

4. sync.WaitGroup

- Wait for a group of goroutines to finish

**Defer**

- Runs functions at the end of the current scope
