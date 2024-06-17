PowerPack SLD 2.6
 +---------------------------------------------------------------------------+
 | Note: In the following text, "PowerPack" refers to the PowerPack emulator,|
 | "PowerScope" refers to the PowerScope debugger, and "SLD" refers to the   |
 | PowerPack SLD software.                                                   |
 +---------------------------------------------------------------------------+

________________________________________
Contents

Changes in 2.6
486 Configuration Guidelines
Windows/PowerPack SLD Configuration Guidelines
Notes
Diagnosing Fatal PowerPack SLD Errors


________________________________________
Changes in 2.6

* New features

Completes the software release for EA-486
 -Hardware timestamp
 -Qualified trace
 -Support for external trace and triggering
 -Improved counter/timer support

Support for 386EX C-step bondout is added

Support for long file names under Win95

Shell command Addressof can display address of local variable

________________________________________
486 Configuration Guidelines


* PowerPack EA-486 with revision 000 probe heads must have the following
  entry in the powerpak.ini file:

     [SystemInfo]
     LC486Rev000=1

  Without this entry, the state of the 16/32 bit configuration will be
  wrong.

  Refer to "Determining probe head revision" below.


* Determining probe head revision:

  A revision 000 probe head is marked with "14894-000" on the underside
  of the probe head between the SJ1 and SJ2 cable connectors. (The -001
  probe head, with EPLD version 2.2, is required for zero wait state
  overlay memory operation.)


* EA-486 jumper settings for supported Intel CPUs

Refer to "Determining probe head revision" above.

Revision 000 probe head:

emulator  chip                FPU   SLE   16B
--------- ---------------     ---   ---   ---
EA-486    486DX/DX2           ON    ON    OFF
          486SX/SX2           OFF   ON    OFF
          486DX/DX2, non-sle  ON    OFF   OFF
          486SX/SX2, non-sle  OFF   OFF   OFF
          ULP 486SX           OFF   ON    OFF

Revision 001 probe head:

emulator  chip                FPU   SLE   32B
--------- ---------------     ---   ---   ---
EA-486    486DX/DX2           ON    ON    ON
          486SX/SX2           OFF   ON    ON
          486DX/DX2, non-sle  ON    OFF   ON
          486SX/SX2, non-sle  OFF   OFF   ON
          ULP 486SX           OFF   ON    ON
          ULP 486GX           OFF   ON    OFF

________________________________________
Windows/PowerPack SLD Configuration Guidelines

* Reset PowerPack Base after Error

If an error occurs, forcing you to exit PowerPack SLD or restart Windows,
you should reset the PowerPack before restarting PowerPack SLD.


* Adobe Type Manager

If you use Adobe Type Manager, turn it off when running SLD.  The
proportional font in the SLD trigger window is displayed incorrectly when
ATM is running.


* Serial Communications with 16550

If you have a communications port with a 16550 FIFO enabled, rebooting
without properly closing Windows may result in an inability to
reestablish communications with the emulator.  You can avoid this
problem by including the default address of the COM port in your
system.ini file.  Edit the [386Enh] section of system.ini to include one
of the following addresses corresponding to the COM port used for
communication with the PowerPack or PowerScope:

        COM1Base=3f8h
        COM2Base=2f8h
        COM3Base=3e8h
        COM4Base=2e8h


________________________________________
Notes


* General

The Map command can time out (up to 90 seconds is required) when mapping
extremely large regions of target memory to TARGET NONE.  The workaround
is to perform the mapping in two or three commands instead of a single
command.

Enumerated types can not be edited by symbolic values.

Enums, structs and unions are limited to 256 elements.

The CPU window uses colors from the Windows color palette for text and
background.  Registers are either "normal", "highlighted" (to indicate
a value change), or "reverse video" to indicate the cursor position.
Occasionally, when a register is displayed with both a highlight and
reverse video, the register value is not visible.  Selecting a different
color combination for windows text, windows background, highlight text,
or highlight background will solve this problem.

The fatal error "Out of object pointers" indicates that PowerPack SLD
has exhausted system display resources.  If you frequently encounter
this error condition, try the following:
- close windows that are not in use.
- reduce the size of windows.
- decrease the number of saved transcript lines and history commands
  in the shell window.

The message "Out of memory" indicates that the PowerPack/SLD's internally
allocated memory is exhausted.  The default maximum amount of available
memory is 8M.  You can increase the amount of internally allocated memory
to anywhere between 9M and 16M.  Command "_maxmemsize" displays the
current maximum memory size; "_maxmemsize" followed by a number increases
the maximum memory size to that value, e.g. "_maxmemsize 10" sets the
maximum memory size to 10M.  Note that the memory size cannot be reduced
below the current setting.

If you add an event that has embedded spaces in the name, it can be saved
to a file, but when restored will result in the error "Cannot read file".
In general, spaces should not be used in event names.

During hardware initialization, the PowerPack may encounter a target 
condition that interferes with CPU operation.  In these cases, one or more
target signals may be disabled from reaching the CPU.  There is currently
no automatic notification that signals have been disabled.  Add the line
"signal;" to include.me to show a list of the gatable signals and their
states, or the line "signal all enable;" to be sure all signals are
enabled.

The memory window doesn't properly handle memory ranges that aren't on
16 byte boundaries.  Memory ranges are adjusted to the closest valid
16 byte boundary (lower boundaries are adjusted up, upper boundaries are
adjusted down).  Use the shell window to view and modify memory outside
of what is shown in the memory window.


* Toolchain Notes

PowerPack SLD supports OMF86 and OMF386 file formats.  Testing has
confirmed, however, that there are numerous interpretations of the OMF
file specifications.  PowerPack SLD has been tested with these
toolchains:

     OMF86:  Microsoft Visual C 1.5 & SSI Link&Locate-86, 7.2h
     OMF86:  Borland C 4.0, Paradigm Locate 4.0

     OMF386: Metaware High C 3.21 & SSI Xlink386 2.0
     OMF386: Borland 4.5, Phar Lap TNT LinkLoc 8.0
     OMF386: WATCOM 10.5, CSI 1.5
     OMF386: MRI 1.0, MRI 1.0

Using Metaware High C and Phar Lap LinkLoc, variable void * types are
displayed as signed short int *.  Phar Lap does not generate the void
types; these types default to signed short ints.

Using Metaware High C and Phar Lap LinkLoc, variable enumeration types
show as signed char.  Phar Lap does not generate the enumerated types.
These default to signed char.

Using Metaware High C and Phar Lap LinkLoc, when the linker generates the
warning "Cannot process all of the debug information in module",
PowerPack SLD might not have all the debug information for the module.

Using Metaware High C, type "unsigned int" is converted to "unsigned
long".

Borland floating point emulation is done by replacing the floating point
instruction with an INT instruction and some byte information that the
interrupt handler is going to read.  The interrupt handler reads this
information and then modifies the stack pointer to return to the next
executable instruction.  The SLD disassembler knows nothing of this
operation and hence when the source code is disassembled, it disassembles
the INT instruction and then tries to disassemble the bytes that follow
the INT instruction.  These bytes are not really opcodes (they are
special bytes that the INT routine knows about).  The disassembly is
incorrect until the next line number is reached.  At this point the
disassembly has synched up again and the disassembly is correct.  Trying
to step past this code will not work correctly either (suffers from the
same symptoms).  However, if the source is viewed in Source Only (not
mixed mode) then single stepping should work just fine since the
breakpoint will be placed on the line number.


* 386EX

The BUSY#, ERROR#, and PEREQ pins normally interface to a coprocessor.
The 386EX allows these pins to be redirected to one of the internal
timers instead.  Since the 386EX powers up with the pins programmed to
their FPU function, the PP firmware will detect if a coprocessor is
present.  However, if the pins are later redefined by user code or in the
peripheral window, SLD may crash since it can no longer access the
coprocessor.  This will only affect users who (1) have a target
coprocessor, and (2) reprogram the pins as above so it cannot be
accessed, and (3) try to access the coprocessor from SLD.

When the 386EX is reset internally, breakpoints and ICECFG0 contents are
lost.  Normally, emulation is briefly stopped when the CPU is reset in
order to restore the user's breakpoint and ICECFG0 register contents.
However, the user can also reset the CPU by writing to PORT92 at io
address 0xFF92.  In this case, the emulator cannot detect the reset, and
debug registers and ICECFG0 contents are not restored.  This could result
in a system hang if software breakpoints are installed since the op code
used for software breakpoints would be handled as an INT1 instead of
breaking emulation.

If BS8# is asserted from the target while emulation is stopped, control
of the bondout is lost.  BS8# assertion interferes with the fetching of
debug code.


________________________________________
Diagnosing Fatal PowerPack SLD Errors


* GP Faults

If you have received a GP fault, our ability to find and fix it is
increased if you run the Dr. Watson recorder, which captures
information at the point of the GP fault.  The Dr. Watson program is
shipped with Windows and is located in your windows directory.

To start Windows with Dr. Watson enabled, use the File Manager to drag
and drop the drwatson.exe icon (in your windows directory) into the
Windows StartUp Group.  Another way to do this is to add the path and
filename to the load= line of your win.ini file.  Example:

       load=c:\windows\drwatson.exe

After a GP fault, the drwatson.log file in your Windows directory holds
the information.  Fax or e-mail this file, along with any other
information that led up to the GP fault, to Microtek International.

      Fax: 1-503-629-8460.         E-mail: csupport@microtekintl.com


* POWERPAK.DMP
Under some conditions, an error can occur which produces a message box
indicating that information about a problem has been placed in the file
powerpak.dmp in your PowerPack SLD directory.  This file gets written
over each time an error occurs, so we recommend that you rename the file,
then fax or e-mail it to Microtek International.
