# Learning Task 9

## Learning Objectives

* Implement linked list and associated functions
* Iteratively enable or disable all breakpoints contained in a list

## Issues

* Create a header file `breakpoint.h` to contain all definitions of breakpoint
    related structs, defines, and functions.
* In `breakpoint.h`, implement a `Breakpoint` struct that will represent a
    node in a linked list of breakpoints for the current debug session with the
    following fields:
    * `id` (int) - unique identifier of the breakpoint
    * `address` (long) - address of the breakpoint
    * `original_contents` (long) - contents of the program instructions when
        a breakpoint is not set
    * `breakpoint_contents` (long) - contents of the program instructions when
        a breakpoint is set (should be the same as the `original_contents` but
        overwritten with a breakpoint instruction)
    * `enabled` (int) - a value representing whether or not the breakpoint is
        currently enabled or disabled
    * any other fields that are necessary to implement a node in a linked list
* Copy the definitions of the following functions into `breakpoint.h`:

```c
/**
 * @brief   create new breakpoint and append to list of breakpoints. If a
 *          breakpoint already exists at the provided address, do not create
 *          a new breakpoint
 *
 * @param   pointer to list of breakpoints starting with head node
 * @param   address of breakpoint
 * @param   original_contents of the program text at the breakpoint location
 * @param   breakpoint_contents of the program text when the breakpoint is set
 *
 * @return  breakpoint ID (0 or greater) on success, -1 on failure
 */
int Breakpoint_create(Breakpoint **list, long address, long original_contents,
        long breakpoint_contents);

/**
 * @brief   remove breakpoint from list of breakpoints
 *
 * @param   pointer to list of breakpoints starting with head node
 * @param   id of node to remove
 *
 * @return  0 on success, -1 on failure, -2 if breakpoint ID does not exist
 *          in list
 */
int Breakpoint_destroy(Breakpoint **list, int breakpoint_id);

/**
 * @brief   get pointer to next breakpoint in list
 *
 * @param   node pointer to breakpoint
 *
 * @return  pointer to next breakpoint on success, NULL if last item in list
 */
Breakpoint *Breakpoint_get_next(Breakpoint *node);

/**
 * @brief   get breakpoint node in list referenced by a breakpoint ID
 *
 * @param   pointer to list of breakpoints starting with head node
 * @param   id of breakpoint referenced
 *
 * @return  pointer to breakpoint node if found in list, NULL if no breakpoint
 *          allocated with given breakpoint ID
 */
Breakpoint *Breakpoint_get_by_id(Breakpoint **list, int id);

/**
 * @brief   get breakpoint node in list referenced by address
 *
 * @param   pointer to list of breakpoints starting with head node
 * @param   address of breakpoint references
 *
 * @return  pointer to breakpoint node if found in list, NULL if no breakpoint
 *          allocated at given address
 */
Breakpoint *Breakpoint_get_by_address(Breakpoint **list, long address);
```

* Create an implementation file `breakpoint.c` and implement the defined
    functions.
* In the file where you implemented your `ptrace` functionality, write a
    function `enable_all_breakpoints(Breakpoint **list)` that iterates over
    a list of breakpoints and checks if they are enabled. If not, the function
    should enable the breakpoint by writing a breakpoint to the address of
    the breakpoint.
* In the same file, implement a `disable_all_breakpoints(Breakpoint **list)`
    that similarly iterates over a list of breakpoints and checks if they are
    enabled. If a breakpoint is enabled, it should disable the breakpoint by
    setting the instruction contents back to what they were without the
    breakpoint being set.
* Unit test the implementation of functions in `breakpoint.c`.
