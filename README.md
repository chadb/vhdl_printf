# vhdl_printf

This vhdl package implements printf for vhdl.  It allows you to do formatted printing to a LINE type.

## Installation

To install PCK_FIO, define a VHDL library called EASICS_PACKAGES, and
analyze the VHDL file PCK_FIO_1993.vhd and PCK_FIO_1993_BODY.vhd into this library.

### Modelsim

1. vlib easics_packages
1. vcom -work easics_packages PCK_FIO_1993.vhd PCK_FIO_1993_BODY.vhd TB_PCK_FIO_1993.vhd
1. vsim -do "run -all" TBE_PCK_FIO 
1. diff PCK_FIO.out.gold PCK_FIO.out

### ghdl

1. mkdir easics_packages
1. ghdl -a --std=93 -Peasics_packages --work=easics_packages --workdir=easics_packages PCK_FIO_1993.vhd PCK_FIO_1993_BODY.vhd TB_PCK_FIO_1993.vhd
1. ghdl -e -Peasics_packages --work=easics_packages --workdir=easics_packages TBE_PCK_FIO
1. ./tbe_pck_fio 
1. diff PCK_FIO.out.gold PCK_FIO.out

## [Usage](https://cdn.jsdelivr.net/gh/chadb/vhdl_printf@blob/master/PCK_FIO.html)

PCK_FIO is a VHDL package that defines  fprint, a function for formatted file output.

After installing the package you can call fprint as follows:

```vhdl
  fprint(F, L, Format, fo(Expr_1), fo(Expr_2), ... fo(Expr_n));
```

where F is the filehandle and L is the line variable.

The argument Format is the format string, which consists of ``normal'' substrings which are copied verbatim, and format specifiers, starting with '%'. A typical format string looks as follows:

```vhdl
   "Arg1 = %6r, Arg2 = %10d, Arg3 = %-5r\n"
```

The remaining arguments are the expressions whose results you want to write to the file, embedded in fo function calls. There can be 0 to 32 of such arguments. The expressions can be of any type for which an fo function exists. String expressions can also be called directly.

The file output function 'fo'

The fo (file output) functions do the trick. They return a tagged string representation that is meaningful to format specifiers. Here are some examples:

```vhdl
  fo (signed'("1100"))   returns "S:1100" 
  fo (unsigned'("1100")) returns "U:1100" 
  fo (TRUE)              returns "L:T"
  fo (127)               returns "I:127"
```

The internal behavior of fo is irrelevant to the typical user. 
 
The fo function is currently overloaded as follows:

```vhdl
  function fo (Arg: unsigned)          return string;
  function fo (Arg: signed)            return string;
  function fo (Arg: std_logic_vector)  return string;
  function fo (Arg: std_ulogic_vector) return string;
  function fo (Arg: bit_vector)        return string;
  function fo (Arg: integer)           return string;
  function fo (Arg: std_ulogic)        return string;
  function fo (Arg: bit)               return string;
  function fo (Arg: boolean)           return string; 
  function fo (Arg: character)         return string;
  function fo (Arg: string)            return string;
  function fo (Arg: time)              return string;
```

To support null-terminated strings, the function fo(Arg: string) processes Arg up to the first NUL character, if any. If you want the whole string to be outputted you can just enter the string as a direct argument in fprint.  See also the examples in the testbench.

###Format specifiers

The general format of a format specifier is:

```
   %[-][n]c
```

The optional - sign specifies left justified output; default is right justified.
The optional number n specifies a field-width. If it is not specified, fprint does something reasonable.

| c | is the conversion specifier. Currently the following conversion specifiers are supported |
|---|-----|
| r | reasonable output format (inspired by Synopsys VSS) Prints the ``most reasonable'' representation e.g. hex for unsigned, signed and other bit-like vectors (not preferred for integers) |
| b | bit-oriented output |
| d | decimal output |
| s | string output (e.g. in combination with 'IMAGE for enum types) |
| q | ``qualified'' string output (shows internal representation from fo) |
| {} | Iteration operator, used as follows: %n{<format-string>} In this case, n is the iteration count and is mandatory. Iteration can be nested. |

Special characters

To print a double quote,  use '""' in the format string (VHDL convention). To print the special characters, '\', and '%', escape them with '\'. To prevent '{' and '}' from being interpreted as opening and closing brackets in iteration strings, escape them with '\'.

A newline is specified in the format string by '\n'.



## History

This was an open source package developed by easics.com in 2001.  The only think I have done is created a repo on github and uploaded it.  I did reformat this README file and added a license file.  Below is the original readme file:




```
----  $Id: README,v 1.11 2002/07/15 13:09:34 jand Exp $
----
----  PCK_FIO: a VHDL package for C-style formatted file output
----  Copyright (C) 1995, 2001 Easics NV 
----
----  This library is free software; you can redistribute it and/or
----  modify it under the terms of the GNU Lesser General Public
----  License as published by the Free Software Foundation; either
----  version 2.1 of the License, or (at your option) any later version.
----
----  This library is distributed in the hope that it will be useful,
----  but WITHOUT ANY WARRANTY; without even the implied warranty of
----  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
----  Lesser General Public License for more details.
----
----  You should have received a copy of the GNU Lesser General Public
----  License along with this library; if not, write to the Free Software
----  Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA
---- 
----  For suggestions, bug reports, enhancement requests, and info about  
----  our design services, you can contact us at the following address: 
----     http://www.easics.com
----     Easics NV, Interleuvenlaan 86, B-3001 Leuven, Belgium
----     tel.: +32 16 395 600   fax : +32 16 395 619 
----     e-mail: jand@easics.be (Jan Decaluwe)
----

Version 2002.07
===============

Contents
========

This distribution contains the following files:

  PCK_FIO_1987.vhd:         VHDL-87 source of the header of the PCK_FIO package
  PCK_FIO_1987_BODY.vhd:    VHDL-87 source of the body of the PCK_FIO package 
  PCK_FIO_1993.vhd:         VHDL-93 source of the header of the PCK_FIO package
  PCK_FIO_1993_BODY.vhd:    VHDL-93 source of the body of the PCK_FIO package 
  TB_PCK_FIO_1987.vhd:      VHDL-87 source of the testbench for package PCK_FIO
  TB_PCK_FIO_1993.vhd:      VHDL-93 source of the testbench for package PCK_FIO
  PCK_FIO.out.gold:    	    Certified test bench output
  PCK_FIO.html:             Manual for PCK_FIO in html format
  README:                   This file


Installation
============

VHDL-1987
---------
To install PCK_FIO, define a VHDL library called EASICS_PACKAGES, and
analyze the VHDL file PCK_FIO_1987.vhd and PCK_FIO_1987_BODY.vhd into this library.

To install the test bench, analyze TB_PCK_FIO_1987.vhd into the same library.

VHDL-1993
---------
To install PCK_FIO, define a VHDL library called EASICS_PACKAGES, and
analyze the VHDL file PCK_FIO_1993.vhd and PCK_FIO_1993_BODY.vhd into this library.

To install the test bench, analyze TB_PCK_FIO_1993.vhd into the same library.

Numeric packages
----------------
If you want to use IEEE.std_logic_arith instead of IEEE.numeric_std, you need
to edit the source code of the package, both header and body, and the test bench
and replace the package use clause. PCK_FIO works with either of these packages.

Documentation
-------------
To install the documentation, put the file point PCK_FIO.html in a path of
your choosing, point your web browser to it, and bookmark it.


Installation check
==================

After installing the test bench, you should run it. The corresponding VHDL
design unit is EASICS_PACKAGES.TBE_PCK_FIO(TB).

Simulating the test bench should create a file called PCK_FIO.out. This file
should be identical to PCK_FIO.out.gold. Any difference indicates a portability
issue or a simulator non-compliance or bug.




```
