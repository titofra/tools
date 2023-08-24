Below is a compilation of the profiling tools and Linux commands that I frequently use. It's important to note that for most of these tools, optimization flags should be removed, and the `-O0` compiler flag should be added for proper usage.

# Versatile Profiling

## Perf
The `perf` command is a versatile performance analysis tool that comes with the Linux kernel. It offers a wide array of profiling capabilities, including CPU performance monitoring, trace analysis, and more. You can employ it to profile both user-level and kernel-level events.
* Add the `-g` compiler flag.
* Run your program as usual.
* Use `sudo perf record <yourProgram.out> && sudo perf report` for event reports and more, or `sudo perf stat -d <yourProgram.out>` for CPU statistics.

# Execution Time Analysis

## GNU Profiler
The GNU Profiler is a command-line tool that provides insights into the time spent in various functions of your code. It generates a report displaying the execution time of each function.
* Add the `-pg` compiler and linker flags (*don't forget to include `target_link_libraries (${PROJECT_NAME} PRIVATE -pg)` in your CMakeLists.txt file*).
* Compile and **run** your program as usual.
* Execute `gprof <yourProgram.out> > analytics.txt` to generate the analysis report.

# Memory Management Profiling

## Valgrind
Valgrind is a robust tool for memory profiling, memory leak detection, and performance analysis. It aids in identifying memory-related issues and provides insights into your program's runtime behavior.
* Add the `-g` compiler flag.

### Memcheck
This tool detects memory leaks, invalid memory accesses, and other memory-related issues.
* Run `valgrind --tool=memcheck --leak-check=full <yourProgram.out>`.

### Callgrind
Valgrind's callgrind tool helps you analyze program execution and function call behavior.
* Execute `valgrind --tool=callgrind <yourProgram.out>`.
* Visualize the output using kCachegrind.

### Cachegrind
Use this tool to analyze cache behavior.
* Run `valgrind --tool=cachegrind <yourProgram.out>`.
* Visualize the output using kCachegrind.

### Helgrind
For programs involving threads, use helgrind to identify threading-related issues.
* Run `valgrind --tool=helgrind <yourProgram.out>`.

### Massif
A heap memory profiler.
* Run `valgrind --tool=massif <yourProgram.out>`.
* Visualize the output file using `ms_print`. Alternatively, use a GUI tool like [massif-visualizer](https://github.com/KDE/massif-visualizer) for easier interpretation.

# Debugger

## GNU Debugger
* Add the `-g` compiler flag.
* Launch the debugger with `gdb <yourProgram.out>`.
* Use `run` to execute the program.
* Employ `bt` for backtrace information.

# Miscellaneous

## dmesg
The `dmesg` command can be useful for retrieving information on program termination.
* Use `dmesg -T | grep -E -i -B100 'killed process'` to determine why your program was terminated. On Mac OS, omit the `-T` flag.
