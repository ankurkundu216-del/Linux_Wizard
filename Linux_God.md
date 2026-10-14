# 🧙‍♂️ Linux Wizard Dojo: Complete Field Guide

Welcome to my **Linux Wizard** repository! This repository documents my hands-on journey toward mastering system-level debugging, performance profiling, log triage, and process lifecycle management in Linux.

---

## 📂 Repository Structure

- [`README.md`](README.md) - Project overview and documentation landing page.
- [`linux_wizard_field_guide.md`](linux_wizard_field_guide.md) - Comprehensive cheat sheets covering text-processing pipelines, system tracing (`strace`), CPU profiling (`perf`), and process/memory management.

---

## 🚀 1. Stream & Text-Processing Toolchain (Log Triage)

You mastered building multi-stage data pipelines to filter, parse, and rank log files like a veteran incident response engineer.

*   **`grep -E "pattern1|pattern2"`**: Extended regex pattern matching to filter lines containing multiple search criteria (e.g., catching error codes `403` or `500`).
*   **`awk '{print $N}'`**: Column extraction wizardry, splitting rows by whitespace and pulling specific fields (like IP addresses or status codes).
*   **`sort`**: Alphabetical sorting by default; combine with **`-nr`** for numeric reverse sorting (largest numbers at the top).
*   **`uniq -c`**: Counts adjacent duplicate lines, prefixing them with their total occurrence count.
*   **`tr -d 'CHAR'`**: Deletes specific characters from a stream (e.g., stripping unwanted quotation marks).
*   **The Ultimate Pipeline Formula**:
    ```bash
    grep -E "ERROR" server.log | awk '{print $1}' | sort | uniq -c | sort -nr
    ```

---

## 🔍 2. System Tracing & Debugging (`strace`)

`strace` acts as an X-ray lens into how user-space programs communicate with the Linux kernel via **system calls (syscalls)**.

*   **Core Concept**: Every time a program opens a file, allocates memory, or writes to a terminal, it must ask the kernel via a syscall.
*   **Key Syscalls Encountered**:
    *   `execve`: Launches/executes a new binary program.
    *   `openat`: Opens or creates file descriptors on disk.
    *   `mmap`: Maps files or anonymous memory into process address space.
    *   `exit_group`: Terminates all threads of a process group cleanly.
*   **Forensic Value**: Traces can leak internal architecture details—such as discovering whether a command uses standard C GNU Coreutils or a Rust-based rewrite (`uucore`) by spotting localization configuration files (`.ftl`).

---

## ⚡ 3. CPU Performance Profiling (`perf`) & Hardware Boundaries

When code runs hot or lags, `perf` measures execution efficiency at the hardware level.

*   **`perf stat <command>`**: Summarizes execution time, CPU cycles, instruction counts, and branch behavior.
*   **Virtualization Quirks**: VirtualBox and standard hypervisors isolate guest VMs from physical CPU Performance Monitoring Units (PMUs) for security and portability. This is why raw hardware metrics like `cpu-cycles` show up as `<not supported>` inside VMs, while software timers and user/sys time remain fully active.
*   **Compiler Smarts (`-O2`)**: Modern compilers like GCC can analyze deterministic loops at compile time and optimize them out entirely using mathematical formulas, executing billions of iterations in microseconds.

---

## 🧠 4. Process & Memory Management

An operating system is a dynamic ecosystem of competing processes. You learned how to inspect, track, and control them.

*   **Process Snapshots (`ps aux`)**:
    *   `a`: Show processes for all users.
    *   `u`: Display user-oriented format (CPU/Memory usage, owners).
    *   `x`: Include background daemons without controlling terminals.
*   **The Signal Hierarchy**:
    *   **`SIGINT` (Signal 2 / Ctrl+C)**: Graceful interrupt request.
    *   **`SIGTERM` (Signal 15 / Default `kill`)**: Polite termination request allowing cleanup.
    *   **`SIGKILL` (Signal 9 / `kill -9`)**: The nuclear option handled instantly by the kernel; cannot be caught or ignored.
*   **Live Interactive Dashboards (`top` & `htop`)**:
    *   Real-time monitoring of `%CPU` and `%MEM`.
    *   Distinguishing between **Virtual Memory (`VIRT`)** and **Resident Set Size (`RES` / actual physical RAM)**.
    *   Recognizing multi-process architectures (like modern browsers splitting tasks into isolated subprocesses).

---
*Built with hands-on labs and command-line mastery.*
