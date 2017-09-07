# airprobe, September 2017,
@PCabreraCamara

This is airprobe already patched to GnuRadio 3.7 and some adaptations to be used with cellanalysis using USRP and RTLSDR out-of-the-box.

Instructions to install (asuming you already have GNURadio and libosmocore installed, as well as hardware drivers):

1) git clone git://github.com/pcabreracamara/airprobe
2) cd airprobe/gsmdecode
3) ./bootstrap
4) ./configure
5) ./make
6) ./make install
7) ldconfig
8) cd ..
9) cd gsm-receiver
10) repeat from 3 to 7

Sometimes, on step "./make" on gsm-receiver folder, an error exit the compilation process:

"make[4]: Entering directory '/opt/airprobe/gsm-receiver/src/lib'
/bin/bash ../../libtool  --tag=CXX   --mode=compile g++ -DHAVE_CONFIG_H
-I. -I../..  -I -I -I/usr/local/include/  -I -I/usr/include/python2.7   
-g -O1 -Wno-strict-aliasing -Wno-parentheses  -g -O2 -Wall
-Woverloaded-virtual -MT _gsm_la-gsm.lo -MD -MP -MF
.deps/_gsm_la-gsm.Tpo -c -o _gsm_la-gsm.lo `test -f 'gsm.cc' || echo
'./'`gsm.cc
libtool: compile:  g++ -DHAVE_CONFIG_H -I. -I../.. -I -I
-I/usr/local/include/ -I -I/usr/include/python2.7 -g -O1
-Wno-strict-aliasing -Wno-parentheses -g -O2 -Wall -Woverloaded-virtual
-MT _gsm_la-gsm.lo -MD -MP -MF .deps/_gsm_la-gsm.Tpo -c gsm.cc  -fPIC
-DPIC -o .libs/_gsm_la-gsm.o
gsm.cc:154:21: fatal error: Python.h: No such file or directory
 # include <Python.h>
                     ^
compilation terminated.
Makefile:739: recipe for target '_gsm_la-gsm.lo' failed
make[4]: *** [_gsm_la-gsm.lo] Error 1
make[4]: Leaving directory '/opt/airprobe/gsm-receiver/src/lib'
Makefile:869: recipe for target 'all-recursive' failed
make[3]: *** [all-recursive] Error 1
make[3]: Leaving directory '/opt/airprobe/gsm-receiver/src/lib'
Makefile:414: recipe for target 'all-recursive' failed
make[2]: *** [all-recursive] Error 1
make[2]: Leaving directory '/opt/airprobe/gsm-receiver/src'
Makefile:564: recipe for target 'all-recursive' failed
make[1]: *** [all-recursive] Error 1
make[1]: Leaving directory '/opt/airprobe/gsm-receiver'
Makefile:471: recipe for target 'all' failed
make: *** [all] Error 2"

To solve this problem, use CPATH and LD_LIBRARYY_PATH variables as follows (check /usr/include/python2.7/ exists on your Linux!):

export CPATH="/usr/include/python2.7/:/usr/include/gnuradio/swig/:/opt/airprobe/gsm-receiver/src/lib/decoder/openbtsstuff/"
export LD_LIBRARY_PATH="/usr/include/python2.7/:/usr/include/gnuradio/swig/:/opt/airprobe/gsm-receiver/src/lib/decoder/openbtsstuff/"
