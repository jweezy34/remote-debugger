# Learning Task 7

## Learning Objectives

* Send data about the debug target back to the client.
* Learn to build interactive command line sessions in python using the `cmd`
  package.
* Implement more of the CSDBG network protocol.

## Issues

* In the `csdbg-client` repository, create a new module called `csdbgcmd` with
  a class `CsdbgCmd` that inherits from the `cmd.Cmd` class. Use the `CsdbgCmd`
  class in your main module such that once connected to the service, the user
  is prompted with additional commands. For now, just implement a
  `read_registers` command.
* Implement a function in `csdbg-client` that sends a Command Request Message
  to the service that requests the register state of a stopped process. Have
  this function be called when the user executes the `read_registers` command
  from the command line.
* Implement a function in `csdbg-service` that receives this message, and leads
  to the service executing the functionality to read registers (as
  implemented in [Learning Task 6](task6.md)).
* Create a function that sends a Command Response Message back to the client
  that contains all of the register values.
* Create a function in the client that receives the response message and prints
  the register values to the screen.

An example of what the user would see from the client:
```
$ python3 csdbg.py --ip <target IP> --target <executable>
[+] Connected to target service
(csdbg) > read_registers
rax:    <value>
rbx:    <value>
rcx:    <value>
rdx:    <value>
rdi:    <value>
rsi:    <value>
r8:     <value>
r9:     <value>
r10:    <value>
r11:    <value>
r12:    <value>
r13:    <value>
r14:    <value>
r15:    <value>
rbp:    <value>
rsp:    <value>
rip:    <value>
eflags: <value>
(csdbg) >
```
