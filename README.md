# Hash Hash Hash
This lab aims to implement a thread-safe hash table, which uses mutexes to ensure that no elements go missing when 2 threads try to add elements at the same time.

## Building
To build, simply run `make` in the folder where the Makefile and all other files are present.

## Running
To run the tester to get values for how long the hash table took to complete generation and whether it was completed correctly (number of missing values), run the `hash-table-tester` executable. It takes two options: `-t` and `-s`. `-t` specifies the number of threads to use and `-s` specifies the number of hash table entries to add per thread.

For example,

<img width="600" alt="image" src="https://github.com/shlokj/cs111-lab3/assets/34567765/70147940-a493-4185-86fc-71945eb2bc0e">

## First Implementation

In my v1 implementation, I created a single mutex (`pthread_mutex_t mutex`) in the `hash_table_v1` struct. This is used to lock the entire hash table whenever an element is being added to it.

In the `hash_table_v1_add_entry` function, I call `pthread_mutex_lock` at the very beginning to lock the hash table. All the work is then done, after which I call `pthread_mutex_unlock` to unlock it. This is a slow but correct/safe implementation.

### Performance

As we can see in the Running section of this readme, the v1 hash table is slower than the base implementation. This is expected since there is overhead due to the thread locking. Threads must wait for others to complete before accessing the hash table, resulting in longer wait times.

This time version 1 is xxx

## Second Implementation
In the `hash_table_v2_add_entry` function, xxx

### Performance
```shell

```

This time the speed up is xxx

## Cleaning up
```shell

```
