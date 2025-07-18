# Asynchronous Code Tips

1. suffix methods with **Async**
2. Use Value, ValueResult<> for
3. Use **Task** for Compute bound tasks
4. Use **TaskCompletionSource** for I/O bound tasks
5. Use **ContinueWith** to start a task on another task completion

## Parallel Programming
1. Parcel out processing to multiple CPUS:
```
  Parallel.ForEach(sourceCollection, item => Process(item))
```


