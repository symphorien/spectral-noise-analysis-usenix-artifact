# Vacarme

### Flavors
Vacarme is able to convert a handshake pattern into tamarin theories, and once
tamarin has run enough of these theories, parse and analyse the results.
For this reason, it contains the noise specification encoded into its logic.
`vacarme/source.tar` contains a version of Vacarme encoding the vanilla Noise
specification.
`vacarme/psk-no-early-encryption.tar` contains a version of vacarme relating to
the following modification of the Noise specification:
"The function encryptAndHash returns the clear text before the first `psk` or DH
token".


### Using Vacarme
#### Dependencies
* rustc and cargo 1.30
* A suitable version of tamarin (see `tamarin/README.md`)
* python3.6 at least to run the oracle

Optional:
* to visualize the results, graphviz
* for runtime minimization of proof goals, python3 with tqdm, pydot, matplotlib, and networkx.

Quick way to get up and running:

* with Nix (recommended):
```
tar xvf vacarme/source.tar.bz2
cd thesis
nix-shell
```
* without Nix (not recommended):
```
curl https://sh.rustup.rs -sSf | sh
rustup install 1.30.0
rustup default 1.30.0
pushd /
sudo tar xvf tamarin/binaries_x86_64-linux.tar.bz2
popd
export PATH=/nix/store/yrmgr7qra289d4zhab6jjrxg23p300i1-tamarin-prover-1.5.1b-oracle/bin:$PATH

```
Dependencies will be compiled and made available inside the shell (and only inside this one).


#### Using vacarme
To run the tool on NN (a simple handshake which should take less than a CPU hour):
```
cd thesis
make compile
```
At this point the yet unproven tamarin theories are in `out/instrument_NN`
```
make LOCAL=1 SAMPLE=specs/NN report
```
This proves the theories, saves the proof files in `out/instrument_NN/proofs` and creates
some human readable reports in `out/report`.

More details on the format of reports in the `results` folder.
More details on vacarme in the README in the `thesis` folder of the tarball.

###

##### Runtime proof optimisation
To benefit of the associated speed bump, you need the Nix package manager.
```
make LOCAL=0 SAMPLE=specs/NN report
```
If possible, this is recommended.

#### Alternative Versions

##### Noise without early encryption

To generate case studies corresponding to the alternative version of Noise without early encryption, use the `vacarme/psk-no-early-encryption.tar` archive instead of the `vacarme/source.tar.bz2`mentioned above. 

##### Noise with Curve25519

1. Unpack the source archive as normal. 
2. Edit `thesis/nix/shell.nix`:
 * Delete the line `tamarin-prover-oracle`
 * Replace it with `tamarin-prover-subgroup`
3. Run `nix-shell` in `thesis/`
4. Copy `thesis/helpers/oracle_C25519_K1X1.py` over `thesis/helpers/oracle.py`
5. Run `make compile` in `thesis/` 
6. Run `python3 subgroupify.py` in `framework`
7. Copy `thesis/out_C25519/` over `thesis/out`
8. Run `make report` as you would have done normally (see above).

TODO: CHECK these instructions are correct.

