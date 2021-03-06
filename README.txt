Shared memory arrays for NumPy and Multiprocessing

To build .pyd files:

> python setup.py build_ext

Usage:

> import sharedmem as shm
> array = sm.zeros((m,n), dtype=float)

These arrays can be passed to multiprocessing.Queue and are pickled
by the name of the segment rather than the contents of the buffer.
As pickle is slow, the intention is to save memory, not provide faster 
IPC than making a copy of the NumPy array would do. If memory is not 
an issue, just use normal NumPy arrays instead.



Warning about shared memory:

As always when using shared memory, beware of 'false sharing'. If you
don't know what that is, chances are that NOT USING SHARED MEMORY will
give you better performance. It is also for this reason that C programs
using multiple processes (e.g. MPI or fork) tend to perform better than 
programs using multithreading (e.g. OpenMP or pthreads).

http://en.wikipedia.org/wiki/False_sharing

Shared memory segments are also readable files in the file system 
(under /tmp on Linux). This might be a security issue on some systems.



Copyright (c) 2009, 2011, 2012, Sturla Molden
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, 
are permitted provided that the following conditions are met:

  o Redistributions of source code must retain the above copyright notice, this 
    list of conditions and the following disclaimer.
    
  o Redistributions in binary form must reproduce the above copyright notice, 
    this list of conditions and the following disclaimer in the documentation 
    and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND 
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED 
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. 
IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, 
INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, 
BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY 
OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE 
OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED 
OF THE POSSIBILITY OF SUCH DAMAGE.



