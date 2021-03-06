# gdb_systemc_trace
GDB Python scripts for SystemC design introspection and tracing

Automatically creates a trace of all signals and module member variables in design


### Limitations
Fixed-point datatypes are not supported yet


## Installation

### Prerequisites
* GDB 7.x configured with Python scripting support https://www.gnu.org/software/gdb/download/
* libstdc++ pretty printers initialized with .gdbinit https://sourceware.org/gdb/wiki/STLSupport
* Patched SystemC 2.3.1a built as .so library with debuginfo (see below)
* Python : to run top-level gdb_systemc_trace.py script

### Patching and Building SystemC 
1. Download SystemC 2.3.1.a http://accellera.org/downloads/standards/systemc
2. Replace sc_trace.cpp and sc_trace.h with files from systemc2.3.1.a_patch 
3. Configure build as shared library with debug information:
    (../configure --enable-debug --enable-shared)
4. Build your design with debug info (-g)

## Running simulation with full trace dump

* ./gdb_systemc_trace.py path/to/your/simulation_executable
* systemc_trace.vcd will be created
* Use vcd_hierarchy_manipulator to create hierarchical VCDs: https://github.com/yTakatsukasa/vcd_hierarchy_manipulator
* Use GtkWave to view vcd waveform : http://gtkwave.sourceforge.net/

## Tracing only required signals

* ./gdb_systemc_trace.py -l path/to/your/simulation_executable
* List of all detected signals in design will be printed to console
* Copy required signal names (full hierarchical names) into some file, say signals.txt
* ./gdb_systemc_trace.py -f signals.txt
* systemc_trace.vcd will be created

## Print design tree
* ./gdb_systemc_trace.py -p path/to/your/simulation_executable

## Passing arguments to simulation executable
* ./gdb_systemc_trace.py  path/to/your/simulation_executable argument_1 argument_2 ...
