# Programming concepts (mostly linear order)

- How C programs work. I'll assume you already know how to write basic C, but I want to teach how program memory space is laid out, how compiling and linking works, etc. I'll cover this mostly from a practical perspective, with a little bit of theory.
- How Python programs work. The VM-interpreted model is popular (Java, Python, Ruby). I want to go into this and highlight the differences from the C model. What is ref counting?
- How to write concurrent programs in C. Writing concurrent programs in C is hard, but understanding how to do this in C where the programmer explicitly manages memory is crucial to understanding the concepts. Threading, processes, software-transactional memory
- How to write concurrent programs in Python. Futures, async/await, threading, GIL, multiprocessing, RPC, distributed computing (Dask, Spark).
- Concurrency from a theoretical perspective. Dining philosophers, readers/writers, problem of smoking, etc.
- Basic networking. TCP addresses and ports. Application-level protocols like HTTP, FTP, and SSH (how they work and how to use).

# How to use a computer like a hacker (mostly linear order)

- How to write shell scripts (boring but useful). Posix shell and ZSH. Variables, quoting, subshells, conditionals, arithmetic. Conventions for commandline programs.
- How to use unix-like systems. Package managers, file systems (I'll assume you already know how to get around), file command, find command, daemons, etc.
- Productivity in the commandline. tmux, zsh, oh-my-zsh, rg, fd, fzf (ctrl+r, alt+c, ctrl+t, independent usage), setting $PATH for tools, making your own commands, configging your editor (ligatures and powerline (of course))
- Working remotely. SSH aliases, SSH keys instead of passwords, mosh, tmux, rsync, scp, sshfs, tramp mode (if you use emacs)
- Version control done right. You probably know git commands already, but I want to present some workflows. Don't forget about centralized version control either. Editorconfig, the importance of linting, commit hooks, CI/CD pipelines.
- Tools to be aware of: meld, irc, pandoc, markdown, restructured text, imagemagick, awk, sed
- Unix theory? file-descriptors, processes, threads, containers, pipes, reaping zombie children in Docker (case study), syscalls

# Things we could go more into
- Binary exploits (security). Buffer overflow (logjam case study), ROP coding. How do BSD devs write secure code? How do other languages write secure code?
- Evolution of C to C++. How inheritance and polymorphism would work in C.
- How to use a computer securly. Disk encryption, GPG (maybe jump into public key crypto?), shred
- Containers, kubernetes
- Concurrency in programming language design. This might be my passion and might be my PhD area. Concurrency in imperative vs functional languages. Paradigms (future/promises, actors, shared-mem). Actor vs shared mem vs SIMD models.
