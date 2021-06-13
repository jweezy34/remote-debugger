# Learning Task 8

## Learning Objectives

* Use `ptrace` to set an initial breakpoint
* Use `ptrace` to continue program execution

## Issues

* In the `csdbg-client` repository, implement the command `set_breakpoint` that
    takes as argument an address. It should send a `SET BREAKPOINT` command
    message to the service with the address as an argument.
* In the `csdbg-client` repository, implement the command `continue` that takes
    no arguments and sends a `CONTINUE` command message to the service.
* In the `csdbg-service` repository, receive the `SET_BREAKPOINT` command and
    use `PTRACE_POKETEXT` to write an `INT 3` instruction (`0xcc`) at the
    address specified by the user. This is a breakpoint instruction, causing
    the program to stop when reached. Send the response message back to the
    client with a hardcoded breakpoint ID. The hardcoded breakpoint ID will be
    fixed in future tasks.
* In the `csdbg-service` repository, receive the `CONTINUE` command and call
    `ptrace` with the `PTRACE_CONTINUE` argument to continue program execution
    of the target program. The service should wait until the program either
    stops or exits and send a response message indicating the target program
    status.
* The client should receive the `SET BREAKPOINT RESPONSE` message and print the
    breakpoint ID.
* The client should receive the `CONTINUE RESPONSE` message and print the
    target program's status (e.g. "target has stopped with signal SIGTRAP" or
    "target has exited with exit code 1").

When a breakpoint is set at a valid address and then the `CONTINUE` command is
provided, the user should notice that the program stops at the breakpoint.
If the user inspects the registers at this point with a `READ REGISTERS`
command, the user should notice that the value of `RIP` is the breakpoint
address + 1.

**Note**: this current implementation will not work if we continue to set
breakpoints - there is some more cleaning up to do to get this to work. For
now, just ensure that you can set one breakpoint and send the `CONTINUE`
command to hit it once.
