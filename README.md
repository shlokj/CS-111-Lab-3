# Hash Hash Hash
This lab aims to implement a thread-safe hash table, which uses mutexes to ensure that no elements go missing when multiple threads try to add elements at the same time.

## Building
To build, simply run `make` in the folder where the Makefile and all other files are present.

## Running
To run the tester to get values for how long the hash table took to complete generation and whether it was completed correctly (number of missing values), run the `hash-table-tester` executable. It takes two options: `-t` and `-s`. `-t` specifies the number of threads to use and `-s` specifies the number of hash table entries to add per thread.

For example,

<img width="700" alt="image" src="https://github.com/shlokj/cs111-lab3/assets/34567765/484a084b-c76a-429f-b4af-a076061e9715">

## First Implementation

In my v1 implementation, I created a single mutex (`pthread_mutex_t mutex`) in the `hash_table_v1` struct. This is used to lock the entire hash table whenever an element is being added to it.

In the `hash_table_v1_add_entry` function, I call `pthread_mutex_lock` at the very beginning to lock the hash table. All the work is then done, after which I call `pthread_mutex_unlock` to unlock it (also in the `if` statement for the case where it already exists). This is a slow but correct/safe implementation.

### Performance

As we can see in the Running section of this readme, the v1 hash table is slower than the base implementation - around twice as slow. This is expected since there is overhead due to the thread locking. Threads must wait for others to complete before accessing the hash table, resulting in longer wait times. Here's another example:

<img width="700" alt="image" src="https://github.com/shlokj/cs111-lab3/assets/34567765/86f8a364-9504-4468-b3ad-01039051a0d1">

Here too, v1 is slower than the base implementation.

## Second Implementation
In my v2 implementation, instead of having a single mutex for the entire hash table, I have one mutex for each `hash_table_entry` (bucket) in the hash table. This way, items that are to be put in different buckets by different threads can happen in parallel, allowing a speedup.

In the `hash_table_v2_add_entry` function, the individual entry is locked, allowing other threads to add items to other buckets as long as they are not already in use. Unlocking is done in a similar fashion as in v1. This is both thread-safe and fast.

### Performance

As we can see in the Running section of this readme, the v2 hash table is significantly faster than the base implementation. This is because it optimally handles multiple threads without losing items. This time the speed up is around 4 times because of how multithreading is handled.

Here's the same example from the previous section, continued:

<img width="700" alt="image" src="https://github.com/shlokj/cs111-lab3/assets/34567765/9a65421e-02fa-4c96-be94-5ad77682ad52">

As we can see, the speedup is approximately 5.6x. This is because although 8 threads are specified, there are only 6 performance cores on the M1 Pro chip, where I ran this test. This is expected since 5.6 is around 6.

## Cleaning up

To clean up all binary files, run `make clean`.


