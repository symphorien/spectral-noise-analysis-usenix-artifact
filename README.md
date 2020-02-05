Description of the folders:
* `./results`: Tamarin theories, corresponding proofs and resulting table strongest threat models + automatic analysis.
* `./vacarme`: The source of our tool
* `./tamarin`: The various versions of tamarin we used to run the proofs.

Quick way to reproduce our results for the sole NN handshake, assuming only that the Nix package manager is installed.
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

More details and alternatives, are given in the README of each folder.
