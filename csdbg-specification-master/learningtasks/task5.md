# Learning Task 5

## Learning Objectives

* Learn about the `ptrace` syscall
* Implement first steps of debugger functionality

## Issues

* Read about the Linux ptrace syscall (`man ptrace`). Specifically focus on
  learning how to attach to another process and understand what that means.
  Feel free to use additional internet resources outside of just the man page.
* Implement functionality in the `csdbgd` service that:
  * Receives the `session initiate request` message from the client and parses
    it (you already have this done)
  * If the request is to attach to a running process (indicated if the 
    `session initiate request` message is of type `attach` and has a pid 
    field), attempt to attach to that process.
  * If the request is to start a process and attach to it (indicated if the
    `session initiate request` message is of type `start` and has a target name
    field), start the process indicated and attach to it at its entry point.
  * If the above actions are successful, send the 
    `session initiate acknowledge` message that you implemented in task 4. If 
    not, send an error message (documented vaguely in the 
    [protocol specification](../protocol.md)).
* Implement functionality in the `csdbg-client` that receives the 
  `session initiate acknowledge` message or the error message and print the 
  result to the screen.

This is a bigger learning task that is going to require some independent 
research and thinking, but it's okay. Don't be afraid to ask for pointers or
more specific guidance. I'm here to mentor, not just to dump tasks on you.
