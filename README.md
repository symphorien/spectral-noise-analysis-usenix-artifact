# Layout

Description of the folders:
* `./results`: Tamarin theories, corresponding proofs and resulting table strongest threat models + automatic analysis.
* `./vacarme`: The source of our tool
* `./tamarin`: The various versions of tamarin we used to run the proofs.

# Quickstart

We use the Nix package manager to ensure our results are reproducible. The following instructions show how to reproduce our results for the NN handshake, assuming only that the Nix package manager is installed. 

If you do not use the Nix package manager, the official NixOS VirtualBox VM Image available for download [here](https://releases.nixos.org/nixos/19.09/nixos-19.09.2008.ea553d8c67c/nixos-19.09.2008.ea553d8c67c-x86_64-linux.ova) has been tested with these instructions. You need only start the VM and download this Git repository. 

Example walkthrough to reproduce results for the pattern `NN`:
At the root of  the repository:

```
tar xvf vacarme/source.tar.bz2
cd thesis
nix-shell
```
and inside the shell that opens:
```
make compile
make report SAMPLE=specs/NN
```
and inspect the `out/report` folder. The format is explained in `results/README.md`.

Alternatives are presented in the README of each folder.
