# Learning Task 6

## Learning Objectives

* Interact with debugged process at breakpoints
* Learn to use `ptrace` to peek process state

## Issues

* Implement functionality in the `csdbg` such that when the debugged process
  (or the "tracee") is attached to by the `csdbg` service (the "tracer"), the
  tracee's registers are printed to the terminal.
* After printing the registers, have the `csdbg` service continue the tracee
  process.
