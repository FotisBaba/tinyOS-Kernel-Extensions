# tinyOS Kernel Extensions

My kernel work for the Operating Systems course (COMP301) at the Technical University of Crete, Fall 2019. It's built on **tinyos3**, a small teaching OS by the course staff that runs on a simulated multicore machine on Linux.

## What I implemented

| Feature | File | System calls |
|---|---|---|
| Multithreaded processes | `kernel_threads.c` | `CreateThread`, `ThreadSelf`, `ThreadJoin`, `ThreadDetach`, `ThreadExit` |
| Pipes | `kernel_pipe.c` | `Pipe`, using a ring buffer with a blocking reader and writer |
| Stream sockets (built on pipes) | `kernel_socket.c` | `Socket`, `Listen`, `Accept`, `Connect`, `ShutDown` |
| Process info stream | `kernel_proc.c` | `OpenInfo`, which reads one record per process |

Threads use reference-counted thread control blocks and condition variables, so a thread can be joined or detached safely and is cleaned up when its process exits. Every other file, including the scheduler, comes from the original tinyos3 code.

## Build and run

You need Linux, GCC with C11 support, and make.

```bash
make
./validate_api            # run the course's API test suite
./validate_api thread_tests   # threads only
./mtask 1 0 5 5           # dining philosophers demo
```

To use the interactive shell with two terminals:

```bash
./terminal 0 &   # run each terminal in its own window
./terminal 1 &
./tinyos_shell 1 2
```

## Credits

The tinyos3 base system is by the course instructors at the Technical University of Crete. The extensions listed above are mine.
