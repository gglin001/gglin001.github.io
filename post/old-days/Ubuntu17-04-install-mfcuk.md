## 0x01 Download
Download source code 
https://github.com/nfc-tools/mfcuk
```
allen@allen_ubuntu:~/Git$ git clone https://github.com/nfc-tools/mfcuk
Cloning into 'mfcuk'...
remote: Counting objects: 334, done.
remote: Total 334 (delta 0), reused 0 (delta 0), pack-reused 334
Receiving objects: 100% (334/334), 179.09 KiB | 223.00 KiB/s, done.
Resolving deltas: 100% (220/220), done.

allen@allen_ubuntu:~/Git$ cd mfcuk/
allen@allen_ubuntu:~/Git/mfcuk$ ls
AUTHORS  ChangeLog  configure.ac  COPYING  INSTALL  LICENSE  Makefile.am  NEWS  README  src  TODO  tools
```
## 0x02 Install
```
allen@allen_ubuntu:~/Git/mfcuk$ cat README 
README
======

Compiling:
    automake
    autoconf
    ./configure
    make
...
```
But I got error:
```
allen@allen_ubuntu:~/Git/mfcuk$ automake
configure.ac: error: no proper invocation of AM_INIT_AUTOMAKE was found.
configure.ac: You should verify that configure.ac invokes AM_INIT_AUTOMAKE,
configure.ac: that aclocal.m4 is present in the top-level directory,
configure.ac: and that aclocal.m4 was recently regenerated (using aclocal)
configure.ac:7: error: required file 'config.h.in' not found
src/Makefile.am: error: required file './depcomp' not found
src/Makefile.am:   'automake --add-missing' can install 'depcomp'
/usr/share/automake-1.15/am/depend2.am: error: am__fastdepCC does not appear in AM_CONDITIONAL
/usr/share/automake-1.15/am/depend2.am:   The usual way to define 'am__fastdepCC' is to add 'AC_PROG_CC'
/usr/share/automake-1.15/am/depend2.am:   to 'configure.ac' and run 'aclocal' and 'autoconf' again
/usr/share/automake-1.15/am/depend2.am: error: AMDEP does not appear in AM_CONDITIONAL
/usr/share/automake-1.15/am/depend2.am:   The usual way to define 'AMDEP' is to add one of the compiler tests
/usr/share/automake-1.15/am/depend2.am:     AC_PROG_CC, AC_PROG_CXX, AC_PROG_OBJC, AC_PROG_OBJCXX,
/usr/share/automake-1.15/am/depend2.am:     AM_PROG_AS, AM_PROG_GCJ, AM_PROG_UPC
/usr/share/automake-1.15/am/depend2.am:   to 'configure.ac' and run 'aclocal' and 'autoconf' again
```
and
```
allen@allen_ubuntu:~/Git/mfcuk$ autoconf
configure.ac:9: error: possibly undefined macro: AM_INIT_AUTOMAKE
      If this token and others are legitimate, please use m4_pattern_allow.
      See the Autoconf documentation.
configure.ac:15: error: possibly undefined macro: AC_MSG_ERROR
```
and
```
allen@allen_ubuntu:~/Git/mfcuk$ ./configure 
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables... 
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
./configure: line 3002: AM_INIT_AUTOMAKE: command not found
./configure: line 3008: syntax error near unexpected token `libnfc,'
./configure: line 3008: `PKG_CHECK_MODULES(libnfc, libnfc >= $LIBNFC_REQUIRED_VERSION, , AC_MSG_ERROR([libnfc >= $LIBNFC_REQUIRED_VERSION is mandatory.]))'
```
and
```
allen@allen_ubuntu:~/Git/mfcuk$ make
make: *** No targets specified and no makefile found.  Stop.
```
Wrong!!
## 0x03 Right way to build
```
allen@allen_ubuntu:~/Git/mfcuk$ ls
AUTHORS  ChangeLog  configure.ac  COPYING  INSTALL  LICENSE  Makefile.am  NEWS  README  src  TODO  tools

allen@allen_ubuntu:~/Git/mfcuk$ autoheader 
allen@allen_ubuntu:~/Git/mfcuk$ aclocal
aclocal: warning: couldn't open directory 'm4': No such file or directory

allen@allen_ubuntu:~/Git/mfcuk$ autoconf 
allen@allen_ubuntu:~/Git/mfcuk$ automake
configure.ac:5: error: required file './compile' not found
configure.ac:5:   'automake --add-missing' can install 'compile'
configure.ac:9: error: required file './install-sh' not found
configure.ac:9:   'automake --add-missing' can install 'install-sh'
configure.ac:9: error: required file './missing' not found
configure.ac:9:   'automake --add-missing' can install 'missing'
src/Makefile.am: error: required file './depcomp' not found
src/Makefile.am:   'automake --add-missing' can install 'depcomp'

allen@allen_ubuntu:~/Git/mfcuk$ automake --add-missing 
configure.ac:5: installing './compile'
configure.ac:9: installing './install-sh'
configure.ac:9: installing './missing'
src/Makefile.am: installing './depcomp'

allen@allen_ubuntu:~/Git/mfcuk$ ls
aclocal.m4  autom4te.cache  compile      configure     COPYING  INSTALL     LICENSE      Makefile.in  NEWS    src   tools
AUTHORS     ChangeLog       config.h.in  configure.ac  depcomp  install-sh  Makefile.am  missing      README  TODO
```
Then I can run 
```
allen@allen_ubuntu:~/Git/mfcuk$ ./configure 
...
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: creating config.h
config.status: executing depfiles commands
```
OK
## 0x04 Install
```
allen@allen_ubuntu:~/Git/mfcuk$ make
...
allen@allen_ubuntu:~/Git/mfcuk$ ls ./src/
build_cygwin.sh  crypto1.o    mfcuk           mfcuk.h         mfcuk_utils.c  mifare.o           trace1.txt
crapto1.c        data         mfcuk.c         mfcuk_mifare.c  mfcuk_utils.h  nfc-utils.c        xgetopt.c
crapto1.h        Makefile     mfcuk_finger.c  mfcuk_mifare.h  mfcuk_utils.o  nfc-utils.h        xgetopt.h
crapto1.o        Makefile.am  mfcuk_finger.h  mfcuk_mifare.o  mifare.c       nfc-utils.o        xgetopt.o
crypto1.c        Makefile.in  mfcuk_finger.o  mfcuk.o         mifare.h       pm3_mfc_parser.py
```
Executable file 'mfcuk' is what we want.
Install it to our system.
```
allen@allen_ubuntu:~/Git/mfcuk$ sudo make install
Making install in src
make[1]: Entering directory '/home/allen/Git/mfcuk/src'
make[2]: Entering directory '/home/allen/Git/mfcuk/src'
 /bin/mkdir -p '/usr/local/bin'
  /usr/bin/install -c mfcuk '/usr/local/bin'
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/allen/Git/mfcuk/src'
make[1]: Leaving directory '/home/allen/Git/mfcuk/src'
make[1]: Entering directory '/home/allen/Git/mfcuk'
make[2]: Entering directory '/home/allen/Git/mfcuk'
make[2]: Nothing to be done for 'install-exec-am'.
make[2]: Nothing to be done for 'install-data-am'.
make[2]: Leaving directory '/home/allen/Git/mfcuk'
make[1]: Leaving directory '/home/allen/Git/mfcuk'
```
```
allen@allen_ubuntu:~/Git/mfcuk$ mfcuk
mfcuk - 0.3.8
Mifare Classic DarkSide Key Recovery Tool - 0.3
by Andrei Costin, zveriu@gmail.com, http://andreicostin.com

Usage:
-C - require explicit connection to the reader. Without this option, the connection is not made and recovery will not occur
-i mifare.dmp - load input mifare_classic_tag type dump
-I mifare_ext.dmp - load input extended dump specific to this tool, has several more fields on top of mifare_classic_tag type dump
-o mifare.dmp - output the resulting mifare_classic_tag dump to a given file
-O mifare_ext.dmp - output the resulting extended dump to a given file
-V sector[:A/B/any_other_alphanum[:fullkey]] - verify key for specified sector, -1 means all sectors
	After first semicolon key-type can specified: A verifies only keyA, B verifies only keyB, anything else verifies both keys
	After second semicolon full 12 hex-digits key can specified - this key will override any loaded dump key for the given sector(s) and key-type(s)
-R sector[:A/B/any_other_alphanum] - recover key for sector, -1 means all sectors.
	After first semicolon key-type can specified: A recovers only keyA, B recovers only keyB, anything else recovers both keys
-U UID - force specific UID. If a dump was loaded with -i, -U will overwrite the in the memory where dump was loaded
-M tagtype - force specific tagtype. 8 is 1K, 24 is 4K, 32 is DESFire
-D - for sectors and key-types marked for verification, in first place use default keys to verify (maybe you are lucky)
-d key - specifies additional full 12 hex-digits default key to be checked. Multiple -d options can be used for more additional keys
-s - milliseconds to sleep for SLEEP_AT_FIELD_OFF (Default: 10 ms)
-S - milliseconds to sleep for SLEEP_AFTER_FIELD_ON (Default: 50 ms)
-P hex_literals_separated - try to recover the key from a conversation sniffed with Proxmark3 (mifarecrack.c based). Accepts several options:
	Concatenated string in hex literal format of form uid:tag_chal:nr_enc:reader_resp:tag_resp
	Example -P 0x5c72325e:0x50829cd6:0xb8671f76:0xe00eefc9:0x4888964f would find key FFFFFFFFFFFF
-p proxmark3_full.log - tries to parse the log file on it's own (mifarecrack.py based), get the values for option -P and invoke it
-F - tries to fingerprint the input dump (-i) against known cards' data format
-v verbose_level - verbose level (default is O)

Usage examples:
  Recove all keys from all sectors:
    mfcuk -C -R -1
  Recove the sector #0 key with 250 ms for all delays (delays could give more results): 
    mfcuk -C -R 0 -s 250 -S 250
```
OK!
## 0x05 Key
The use of 
```
autohead
aclocal
autoconf
automake
make && make install
```
Other program like libnfc,mfoc which contains 
```
 configure.ac
 Makefile.am
``` 
can be build as the same.
