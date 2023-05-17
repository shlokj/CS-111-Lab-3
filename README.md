# Hash Hash Hash
This lab aims to implement a thread-safe hash table, which uses mutexes to ensure that no elements go missing when 2 threads try to add elements at the same time.

## Building
To build, simply run `make` in the folder where the Makefile and all other files are present.

## Running
To run the tester to get values for how long the hash table took to complete generation and whether it was completed correctly (number of missing values), run the `hash-table-tester` executable. It takes two options: `-t` and `-s`. `-t` specifies the number of threads to use and `-s` specifies the number of hash table entries to add per thread.

For example,

<img width="600" alt="image" src="https://github.com/shlokj/cs111-lab3/assets/34567765/70147940-a493-4185-86fc-71945eb2bc0e">

## First Implementation
In the `hash_table_v1_add_entry` function, xxx

### Performance
```shell

```

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
