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

+ make.HugeSlackBuild
+ create.HugeSlackBuilds
+ chroot.HugeSlackBuild
+ HugeSlackBuild scripts.

### make.HugeSlackBuild

This file will made HugeSlackBuild script like ncdu.fd7914ff97104524913501f503e21ce5.7902274c83259a4bb12a4a8117de865a.HugeSlackBuild under /tmp/HugeSlackBuils/ dirrectory by default.
Normaly executed in the source directory that have the SlackBuild script and the sources files needed to build the Slackware package. make.HugeSlackBuild will catch the date (SOURCE_DATE_EPOCH) the environment, and the sources files in base64 in one only file per packages source. That help us to only download one file that can be used to reproduce the sources, the environment, the date, and finaly the Slackware package in others systems with only one file.
To thust the sources when make.HugeSlackBuild does HugeSlackBuilds scripts add some md5 sources checks that can be checked. And stop the execution if some file not match it md5.

To show md5sums inside HugeSlackBuilds scripts.

```
[root@arcadia ncdu]# cat ncdu.fd7914ff97104524913501f503e21ce5.7902274c83259a4bb12a4a8117de865a.HugeSlackBuild | grep echo | grep md5sum
echo "b08f96e3e648ad0713dc2e3a4245c128  ./ncdu.SlackBuild" | md5sum -c || exit 1
echo "348c3ced11475b292b0a73576935f68a  ./ncdu.SlackBuild.reproduciblebuilds.patch" | md5sum -c || exit 1
echo "0a872dbda2d79e45937e22d5c97c01d4  ./ncdu-1.17.tar.gz" | md5sum -c || exit 1
echo "b76268fc5f4a6152ed1f388e325ecfa8  ./README" | md5sum -c || exit 1
echo "67c100dc3b10f5f103dde073b89e21d7  ./slack-desc" | md5sum -c || exit 1
echo "1697e61a13fcf25a6fcabc774038203a  ./ncdu.info" | md5sum -c || exit 1
```
To check sources on your repo or in the web. 

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
```
To repoduce a HugeSlackBuild script the SOURCE_DATE_EPOCH var will be set with the same value the HugeSlackBuild script have at the time it are made.

```
[root@arcadia ncdu]# grep ^SOURCE_DATE_EPOCH ncdu.fd7914ff97104524913501f503e21ce5.7902274c83259a4bb12a4a8117de865a.HugeSlackBuild | head -1
SOURCE_DATE_EPOCH=${SOURCE_DATE_EPOCH:-1709747077}
[root@arcadia ncdu]#
[root@arcadia ncdu]# SOURCE_DATE_EPOCH=1709747077 bash make.HugeSlackBuild
```
That will 


## HugeSlackBuild scripts.

HugeSlackBuild scripts are files that are made to be reproduciblebuild for the packages it made for Slackware.

Like the example ncdu.fd7914ff97104524913501f503e21ce5.7902274c83259a4bb12a4a8117de865a.HugeSlackBuild script




## Runing create.HugeSlackBuilds

I run it on /tmp mounted on tmpfs. So no disk I/O wear.


 


## Contributing
All contributions are welcome.

## Author

* **Viel Losero** - *Initial work* - [Viel Losero](https://github.com/VielLosero)

## Copyrights

Slackware® is a Registered Trademark of Patrick Volkerding. 

Linux® is a Registered Trademark of Linus Torvalds.

## License
This project is licensed under the BSD 1-Clause License - see the [LICENSE.md](LICENSE.md) file for details

