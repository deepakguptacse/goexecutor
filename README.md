# goexecutor

A golang library to help with concurrent programming.

## Example:
```$xslt
...

ctx := context.Background()

// Creates a new parallel group s.t. a maximum of 10
// goroutines will be spawned at any point of time.
parallelGroup := goexecutor.NewParallelGroup(ctx, 10)


// Add hundred tasks to the parallel group
for i := 0; i < 100; i++ {
    parallelGroup.add(
        func() error {
            doSomethingIOBlocking(i)
        },
    )
}

// Tasks will execute ensuring that not more than
// ten goroutines are spawned at any point of time.
// RequireAll makes sure that all of tasks pass, if 
// one of them fails then an error is returbed and
// the ongoing tasks are cancelled.
err := parallelGroup.start(goexecutor.RequireAll)

...
```
