# HugeSlackBuilds 

Like SlacBuild Script. (https://slackwiki.com/Writing_A_SlackBuild_Script) HugeSlackBuild Script wants to be another option to have build process automated, but all in one file. With automated md5 chain check, similar to a blockchain. From Slackware, Slackbuilds or official website sources.

## The concept

Provide all sources in one file. Sources include the SlackBuild Scripts without modifications. We achieve this by encoding all the sources in base64.

Make it easier to verify sources checksums by providing the md5 or sha of sources within the file itself and not in a separate file. Auto check it. And adding an md5 to the name of the HugeSlackBuild Script to check it whitout need of other files.

This adds an abstraction layer to the Slackbuild build process, to apply additional functions if needed like environment check ...

## The Plan

Make a repository for some HugeSlackBuilds on github, due to file limitations not all HugeSlackBuilds will be pushed.

Ask the comunity for contributions, help, and feedback.

Later play with custom environments and repetitivebuilds.

Maybe think about adding some warnings for required or automate of these.

Maybe make the HugeSlackBuild less huge, deleting the base64 blocks but adding flavors to the build process.

## Use HugeSlackBuild




## Run create.HugeSlackBuilds

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

