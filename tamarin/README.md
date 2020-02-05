# Compiling tamarin
Our work uses a slightly modified version of Tamarin.
* Anonymity proofs can be run with vanilla Tamarin v1.5
* Secrecy and agreement need Tamarin v1.5 patched with
  `tamarin/sources/oracle_information.patch`
* Curve 22519 proofs need a fork of tamarin called tamarin-prover-subgroup

You will find the sources of all these versions in this folder, as well as
binaries.

## Compiling from source

Tamarin is most easily built with stack. Install it first.

For vanilla tamarin v1.5 we used revision 05b5a935b4ea889705b5a935b4ea8897
whose source is available in `tamarin/sources/tamarin-vanilla-rev-05b5a935b4ea88973.tar.gz`.
For tamarin-prover-subgroup the source is available at `tamarin/sources/tamarin-prover-subgroup.tar.bz2`.

* unpack the sources, `cd` to the source root.
* if building a tamarin for Secrecy and agreement proofs, apply the patch:
```
patch -p1 < /path/to/oracle_information.patch
```
* usual `make; make install`

## Installing the binaries
The binaries are compiled for `x86_64-linux` and need a recent enough kernel to run
`glibc-2.27`. Unfortunately, the installation procedure requires root access.
```
sudo tar xvf tamarin/binaries_x86_64-linux.tar.bz2
```

Vanilla Tamarin v1.5 is then available as
`/nix/store/h7hysgm66rkm2q47l60cqh080rxm4qwg-tamarin-prover-1.5.1b/bin/tamarin-prover`
The patched Tamarin v1.5 for secrecy and agreement proofs is available as
`/nix/store/yrmgr7qra289d4zhab6jjrxg23p300i1-tamarin-prover-1.5.1b-oracle/bin/tamarin-prover`
tamarin-prover-subgroup is available as
`/nix/store/mipfkfq7b2xg2zcjlz3c79nm749w868l-tamarin-prover-1.5/bin/tamarin-prover`.

Note that the binaries are not relocatable; you may however create a symbolic
link to them in a more convenient location.

#### Uninstalling
```
sudo rm -rf /nix
```
