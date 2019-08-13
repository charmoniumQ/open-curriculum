# Programming concepts (mostly linear order)

- How C programs work. I'll assume you already know how to write basic C, but I want to teach how program memory space is laid out, how compiling and linking works, etc. I'll cover this mostly from a practical perspective, with a little bit of theory.
- How Python programs work. The VM-interpreted model is popular (Java, Python, Ruby). I want to go into this and highlight the differences from the C model. What is ref counting?
- How to write concurrent programs in C. Writing concurrent programs in C is hard, but understanding how to do this in C where the programmer explicitly manages memory is crucial to understanding the concepts.
- How to write concurrent programs in Python. Futures, async/await, threading, GIL, multiprocessing, RPC, distributed (Dask, Spark).
- Concurrency from a theoretical perspective. Dining philosophers, readers/writers, problem of smoking, etc.
- Basic networking. TCP addresses and ports. Application-level protocols like HTTP, FTP, and SSH (how they work and how to use).
- Distributed computing.

# How to use a computer like a hacker (mostly linear order)

- How to write shell scripts (boring but useful). Posix shell and ZSH. Variables, quoting, subshells, conditionals, arithmetic. Conventions for commandline programs.
- How to use unix-like systems. Package managers, file systems (I'll assume you already know how to get around), file command, find command, daemons, etc.
- Productivity in the commandline. tmux, zsh, oh-my-zsh, rg, fd, fzf (ctrl+r, alt+c, ctrl+t, independent usage), setting $PATH for tools, making your own commands, configging your editor (ligatures (of course))
- Working remotely. SSH aliases, SSH keys instead of passwords, mosh, tmux, rsync, scp, sshfs, tramp mode (if you use emacs), irc (if you want to)
- Version control done right. You probably know git commands already, but I want to present some workflows. Don't forget about centralized version control either.
- Unix theory? file-descriptors, processes, threads, containers, pipes, reaping zombie children in Docker (case study), syscalls

# Things we could go more into
- Binary exploits (security). Stack overflow, ROP coding
- Evolution of C to C++. How inheritance and polymorphism would work in C.
- How to use a computer securly. Disk encryption, GPG
