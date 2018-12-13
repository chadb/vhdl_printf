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




