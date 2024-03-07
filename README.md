# HugeSlackBuilds 

Like SlacBuild Script. (https://slackwiki.com/Writing_A_SlackBuild_Script) HugeSlackBuild Script wants to be another option to have build process automated, but all in one file. With automated md5 chain check, similar to a blockchain. From Slackware, Slackbuilds or official website sources.

## The concept

Provide all sources in one file. Sources include the SlackBuild Scripts without modifications. We achieve this by encoding all the sources in base64.

Make it easier to verify sources checksums by providing the md5 or sha of sources within the file itself and not in a separate file. Auto check it. And adding an md5 to the name of the HugeSlackBuild Script to check it whitout need of other files.

This adds an abstraction layer to the Slackbuild build process, to apply additional functions if needed like environment check ...

## The Plan

Make a repository for some HugeSlackBuilds on github, due to file limitations not all HugeSlackBuilds will be pushed.

Ask the comunity for contributions, help, and feedback.

Later play with custom environments and reproduciblebuilds.

Maybe think about adding some warnings for required or automate of these.

Maybe make the HugeSlackBuild less huge, deleting the base64 blocks but adding flavors to the build process.

## Use HugeSlackBuild

From now there are some files that I will try to explain.

+ make.HugeSlackBuild.
+ create.HugeSlackBuilds.
+ chroot.HugeSlackBuild.
+ HugeSlackBuild scripts like ./ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild.

HugeSlackBuild scripts like ./ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild can be used to make a reporducible package for Slackware in this case with ncdu aplication.



### make.HugeSlackBuild

This file will made HugeSlackBuild script like ./ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild under the default directory /tmp/HugeSlackBuils/.
Normaly executed in the source directory that have a SlackBuild script and sources that compile correctly, make.HugeSlackBuild will catch the date (SOURCE_DATE_EPOCH) the environment, and the sources files in base64 in one only file per packages source. That help us to only download one file that can be used to reproduce the sources, the environment, the date, and finaly reproduce the Slackware package byte by byte in others systems with only one file and getting the same md5, sha checksum result. See [https://reproducible-builds.org/](https://reproducible-builds.org/) for more info.
To thust the sources when HugeSlackBuilds scripts are made, make.HugeslackBuild add some md5 sources that can be checked. And stops the execution if some file not match it md5.

To make a reproducible HugeSlackBuild script for example for ncdu, copy the Slackbuild tarball and sources of ncdu to a temp directory (recomended) or go on the directory with the Slackware or Slackbuilds sources u want to crate. You know.
Then check the sources and make the HugeSlackbuild script running make.HugeSlackBuild. Easy.
```
[root@arcadia ncdu]# grep ncdu /opt/slackware-repositories/slackbuilds/15.0/CHECKSUMS.md5
120fbf59e2743bda19a8d9a85175fe3c  ./system/ncdu.tar.gz
a5687c5f3e458caa245cf7d301db7929  ./system/ncdu.tar.gz.asc
b76268fc5f4a6152ed1f388e325ecfa8  ./system/ncdu/README
b08f96e3e648ad0713dc2e3a4245c128  ./system/ncdu/ncdu.SlackBuild
1697e61a13fcf25a6fcabc774038203a  ./system/ncdu/ncdu.info
67c100dc3b10f5f103dde073b89e21d7  ./system/ncdu/slack-desc
[root@arcadia ncdu]# curl https://slackbuilds.org/repository/15.0/system/ncdu/ | grep ncdu-1
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  7777  100  7777    0     0   6053      0  0:00:01  0:00:01 --:--:--  6066
<b>Source Downloads:</b><br />  <a href="https://dev.yorhel.nl/download/ncdu-1.17.tar.gz">ncdu-1.17.tar.gz</a> (0a872dbda2d79e45937e22d5c97c01d4)<br />
[root@arcadia ncdu]# ls -la
total 188
drwxr-xr-x  2 root root    160 Mar  7 14:27 .
drwxrwxrwt 16 root root    500 Mar  7 13:24 ..
-rw-r--r--  1 root root    311 Mar  6 18:44 README
-rwxr-xr-x  1 root root  13148 Mar  7 13:56 make.HugeSlackBuild
-rw-r--r--  1 root root 157187 Mar  6 18:44 ncdu-1.17.tar.gz
-rwxr-xr-x  1 root root   3081 Mar  6 18:44 ncdu.SlackBuild
-rw-r--r--  1 root root    271 Mar  6 18:44 ncdu.info
-rw-r--r--  1 root root    896 Mar  6 18:44 slack-desc
[root@arcadia ncdu]# md5sum *
b76268fc5f4a6152ed1f388e325ecfa8  README
8f799567ef6460dcfd8da13b44554994  make.HugeSlackBuild
0a872dbda2d79e45937e22d5c97c01d4  ncdu-1.17.tar.gz
b08f96e3e648ad0713dc2e3a4245c128  ncdu.SlackBuild
1697e61a13fcf25a6fcabc774038203a  ncdu.info
67c100dc3b10f5f103dde073b89e21d7  slack-desc
[root@arcadia ncdu]# ./make.HugeSlackBuild
[+] Working on dir: /tmp/ncdu
Excluding ./make.HugeSlackBuild
Huge file: ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild
Output compressed file: /tmp/HugeSlackBuilds/ncdu.HugeSlackBuild.tar.zst
Congrats you have created your firts HugeSlackBuild script.

For now I leaved the HugeSlackBuild script output ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild on /tmp/HugeSlackBuilds to can chech it whitout extract it from the compressed file. In late versions i will remove and leave only the compressed file with the HugeSlackBuild script inside.

So now /tmp/HugeslackBuilds/ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild have all it need to make a ncdu Slackware package that othes can reproduce.

You can see the SOURCE_DATE_EPOCH date. The date when that HugeSlackBuild script was created.
```
[root@arcadia ncdu]# grep "^SOURCE_DATE_EPOCH" /tmp/HugeSlackBuilds/ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild | head -1
SOURCE_DATE_EPOCH=${SOURCE_DATE_EPOCH:-1709819289}
```
The md5sum of the files inside.
```
[root@arcadia ncdu]# cat /tmp/HugeSlackBuilds/ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild | grep echo | grep md5sum
echo "b76268fc5f4a6152ed1f388e325ecfa8  ./README" | md5sum -c || exit 1
echo "0a872dbda2d79e45937e22d5c97c01d4  ./ncdu-1.17.tar.gz" | md5sum -c || exit 1
echo "b08f96e3e648ad0713dc2e3a4245c128  ./ncdu.SlackBuild" | md5sum -c || exit 1
echo "6f98514252b417842314981cd73b6c11  ./ncdu.SlackBuild.reproduciblebuilds.patch" | md5sum -c || exit 1
echo "1697e61a13fcf25a6fcabc774038203a  ./ncdu.info" | md5sum -c || exit 1
echo "67c100dc3b10f5f103dde073b89e21d7  ./slack-desc" | md5sum -c || exit 1
[root@arcadia ncdu]#
```
Too deep. To reproduce that HugeSlackbuild script use the same SOURCE_DATE_EPOCH.
```
[root@arcadia ncdu]# SOURCE_DATE_EPOCH=1709819289 ./make.HugeSlackBuild
[+] Working on dir: /tmp/ncdu
Excluding ./make.HugeSlackBuild
Huge file: ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild
Output compressed file: /tmp/HugeSlackBuilds/ncdu.HugeSlackBuild.tar.zst
```
If you run it whitout SOURCE_DATE_EPOCH you made a new HugeSlackBuild script with a new SOURCE_DATE_EPOCH timestamp and a new md5sum.
```
[root@arcadia ncdu]# ./make.HugeSlackBuild
[+] Working on dir: /tmp/ncdu
Thu Mar  7 14:28:21 CET 2024
Excluding ./make.HugeSlackBuild
Huge file: ncdu.34259572e376bccdde3b0eb9ac1403fc.HugeSlackBuild
Output compressed file: /tmp/HugeSlackBuilds/ncdu.HugeSlackBuild.tar.zst
[root@arcadia ncdu]#
```

### HugeSlackBuild scripts

HugeSlackBuild scripts are files that can be reproduced. See point above.

The HugeSlackBuild script have all you need to compile the sources and made a Slackare package that can be reproduced for other people with other systems, environment, time zones, etc. Whit the same architecture or cross-compiling it.

WARNING: Runing HugeSlackBuild scripts will change your system date. The use of a virtual machine or containers are hight recomended, or REMEMBER update your system date after run HugeSlackBuild scripts.

When you run for the firt time a HugeSlackBuild script like ncdu.4cba24a92fee3614203e0590a51e2de9.HugeSlackBuild it will compile the sources like a Slackbuild script and create a Slackware package that u can install in Slackware systems. Like a SlackBuild script do but with an extra layer that made the resulting package to be reproducible.

That pàckage reproduction are made storing and reproducing some timestamps, environment variables, and patching some Slackbuild scripts as needed. Each package can need different treatment. You can play with and help to made reproducibles all packages.

So it is recomended run it on a temporal empty directory.

After nuning for the first time u can notice that a Slackware package are made, and the name of the HugeSlackBuild have changed. 

```
[root@arcadia ncdu]# mkdir  /tmp/build.ncdu
[root@arcadia ncdu]# cd /tmp/build.ncdu/
[root@arcadia build.ncdu]# cp /tmp/HugeSlackBuilds/ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild .
[root@arcadia build.ncdu]# chmod +x ncdu.694781a44d61ee0e813d719f4598f909.HugeSlackBuild
Seting SOURCE_DATE_EPOCH
Thu Mar  7 14:48:09 CET 2024

Creating dirs if needed.

Extracting needed files.
./README: OK
./ncdu-1.17.tar.gz: OK
./ncdu.SlackBuild: OK
./ncdu.SlackBuild.reproduciblebuilds.patch: OK
./ncdu.info: OK
./slack-desc: OK

Printing environment.
SHELL=/bin/bash
WINDOWID=20971525
XDG_CONFIG_DIRS=/etc/xdg:/etc/kde/xdg
TERM_PROGRAM_VERSION=3.2a
TMUX=/tmp/tmux-0/default,5906,0

--squipped--

Patching ncdu.SlackBuild to be reproducible.
patching file ncdu.SlackBuild

Runing ncdu.SlackBuild patched for reproduciblebuilds with Epoch date: 1709818088
ncdu-1.17/
ncdu-1.17/install-sh
ncdu-1.17/Makefile.am
ncdu-1.17/deps/
ncdu-1.17/deps/strnatcmp.c
ncdu-1.17/deps/khashl.h
ncdu-1.17/deps/yopt.h
ncdu-1.17/deps/strnatcmp.h
ncdu-1.17/aclocal.m4
ncdu-1.17/Makefile.in

--squipped--

gcc  -O2 -fPIC   -o ncdu src/browser.o src/delete.o src/dirlist.o src/dir_common.o src/dir_export.o src/dir_import.o src/dir_mem.o src/d
ir_scan.o src/exclude.o src/help.o src/shell.o src/quit.o src/main.o src/path.o src/util.o deps/strnatcmp.o  -lncursesw -ltinfo
make[1]: Leaving directory '/tmp/SBo/ncdu-1.17'
make[1]: Entering directory '/tmp/SBo/ncdu-1.17'
 /bin/mkdir -p '/tmp/SBo/package-ncdu/usr/bin'
  /bin/ginstall -c ncdu '/tmp/SBo/package-ncdu/usr/bin'
 /bin/mkdir -p '/tmp/SBo/package-ncdu/usr/man/man1'
 /bin/ginstall -c -m 644 ncdu.1 '/tmp/SBo/package-ncdu/usr/man/man1'
make[1]: Leaving directory '/tmp/SBo/ncdu-1.17'

Slackware package maker, version 3.14159265.

Searching for symbolic links:

No symbolic links were found, so we won't make an installation script.
You can make your own later in ./install/doinst.sh and rebuild the
package if you like.

This next step is optional - you can set the directories in your package
to some sane permissions. If any of the directories in your package have
special permissions, then DO NOT reset them here!

Would you like to reset all directory permissions to 755 (drwxr-xr-x) and
directory ownerships to root.root ([y]es, [n]o)? n

Creating Slackware package:  /tmp/ncdu-1.17-x86_64-1_SBo.tgz

tar: Option --mtime: Treating date '@1709819289' as 2024-03-07 14:48:09
./
install/
install/slack-desc
usr/
usr/bin/
usr/bin/ncdu
usr/doc/
usr/doc/ncdu-1.17/
usr/doc/ncdu-1.17/COPYING
usr/doc/ncdu-1.17/ChangeLog
usr/doc/ncdu-1.17/README
usr/doc/ncdu-1.17/ncdu.SlackBuild
usr/man/
usr/man/man1/
usr/man/man1/ncdu.1.gz

Slackware package /tmp/ncdu-1.17-x86_64-1_SBo.tgz created.

Unpatch ncdu.SlackBuild.
patching file ncdu.SlackBuild

Added md5 to HugeSlackBuild script.
New file: ./ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild
```
Notice that the md5sum of the resulting Slackware package are added to the HugeSlackBuild script.

So if you or some that wnat to reproduce the Slackware package ncdu-1.17-x86_64-1_SBo.tgz run again the HugeSlackBuild script, that  will made the same /tmp/ncdu-1.17-x86_64-1_SBo.tgz with the same md5sum 3b1561b4530078e7fdbbec2b35c39df3.

So copy to a virtual machine an test.

```
[root@arcadia build.ncdu]# scp ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild live@10.10.10.22:/tmp/live/
(live@10.10.10.22) Password:
ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild                 100%  218KB  32.1MB/s   00:00
[root@arcadia build.ncdu]#
[root@arcadia build.ncdu]# ssh live@10.10.10.22
(live@10.10.10.22) Password:
Linux 5.15.145.

Keep women you cannot.  Marry them and they come to hate the way
you walk across the room; remain their lover, and they jilt you
at the end of six months.
                -- Moore

live@darkstar:~$ su
Password:
root@darkstar:/home/live#
root@darkstar:/home/live# cd /tmp/live
root@darkstar:/tmp/live# ls -la
total 220
drwxr-xr-x  2 live root      60 Mar  7 14:20 .
drwxrwxrwt 10 root root     340 Mar  7 14:19 ..
-rwxr-xr-x  1 live users 222815 Mar  7 14:20 ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild
root@darkstar:/tmp/live#
root@darkstar:/tmp/live# md5sum ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild
694781a44d61ee0e813d719f4598f909  ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild
root@darkstar:/tmp/live# ./ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild
Seting SOURCE_DATE_EPOCH
Thu Mar  7 13:48:09 UTC 2024

Creating dirs if needed.

Extracting needed files.
./README: OK
./ncdu-1.17.tar.gz: OK
./ncdu.SlackBuild: OK
./ncdu.SlackBuild.reproduciblebuilds.patch: OK
./ncdu.info: OK
./slack-desc: OK

Printing environment.
SHELL=/bin/bash

--skipped--

Creating Slackware package:  /tmp/ncdu-1.17-x86_64-1_SBo.tgz

tar: Option --mtime: Treating date '@1709819289' as 2024-03-07 13:48:09
./
install/
install/slack-desc
usr/
usr/bin/
usr/bin/ncdu
usr/doc/
usr/doc/ncdu-1.17/
usr/doc/ncdu-1.17/COPYING
usr/doc/ncdu-1.17/ChangeLog
usr/doc/ncdu-1.17/README
usr/doc/ncdu-1.17/ncdu.SlackBuild
usr/man/
usr/man/man1/
usr/man/man1/ncdu.1.gz

Slackware package /tmp/ncdu-1.17-x86_64-1_SBo.tgz created.

Unpatch ncdu.SlackBuild.
patching file ncdu.SlackBuild

Reproduciblebuild  md5 will match.
Check output of: ./ncdu.694781a44d61ee0e813d719f4598f909.3b1561b4530078e7fdbbec2b35c39df3.HugeSlackBuild
3b1561b4530078e7fdbbec2b35c39df3  /tmp/ncdu-1.17-x86_64-1_SBo.tgz
If not match please report it at mantainer.

root@darkstar:/tmp/live#
```
Have a reproducible Slackware package ncdu-1.17-x86_64-1_SBo.tgz that you can sign and share and othes can reproduce and check 3b1561b4530078e7fdbbec2b35c39df3 if u share your HugeSlackBuild too. 

Provide the sources. In base64 within HugeSlackBuild script. 
Respect the licences. Don't modify it or patch and unpatch. Can be valided with checksum.
Minimal patch to be reproducible.
So now sign your ncdu source HugeSlackBuild script share and enjoy.

Hope users can integrate some similar process in their SlackBuild scripts to have less layers and made it kiss. Then HugeSlackBuilds will be no necessary.

## create.HugeSlackBuilds

From now this file will made from my up to date Slackware 15.0 and Slackbuilds local repositorys on sources with single Slackbuild script the corresponding HugeSlackBuild script. 

I will share it on the HugeSlackBuild directory on this. 

Be care if u run it on yours repositories some packages are too big and you need lot of space.

To minimize disk I/O I run it on /tmp mounted on a tmpfs.

Due to github file restrictions I will upload only some little packages that I use, and all others that I can do due to size.

## 

## Contributing
All contributions are welcome.

## Author

* **Viel Losero** - *Initial work* - [Viel Losero](https://github.com/VielLosero)

## Copyrights

Slackware® is a Registered Trademark of Patrick Volkerding. 

Linux® is a Registered Trademark of Linus Torvalds.

## License
This project is licensed under the BSD 1-Clause License - see the [LICENSE.md](LICENSE.md) file for details

