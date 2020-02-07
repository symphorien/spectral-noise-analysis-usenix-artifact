# Results

These tarballs are a recording of the proofs we ran and what we can deduce from them.

The tarballs cover slightly different protocols:
* `results/vanilla_noise.tar.bz2` is vanilla Noise with a prime order field. It is the most complete one.
* `results/curve.tar.bz2` is Noise with curve 22519. No anonymity proofs are included. Results are identical
to Noise on a prime order field.
* `results/psk_no_early_encryption.tar.bz2` is Noise with the following
  modification: the function `encryptAndHash` returns the plain text before the
  first DH or psk token. Only KXpsk2 has anonymity proofs.

We discuss how these results were generated in the vacarme [folder](https://github.com/symphorien/spectral-noise-analysis-usenix-artifact/tree/master/vacarme). 

# Interpreting the Results

Each folder has the same structure:
* for each pattern x, a folder `instrument_$x` containing:
  1. Tamarin theories `name.spthy`
  2. a proof folder with proofs, under one of two forms.
     * either as a triplet `name.spthy`,
     `name.out`, `name.time` where the sphty can be fed to Tamarin to inspect the
     proof, `name.out` contains the summary and `name.time` gives the run time,
     * or as a set of files in the form `some hash.out.spthy.out` which contain,
     concatenated: the proved Tamarin theory, the summary, and timing
     information. In this case, to open the proof with Tamarin, you need to
     remove the lines before `theory XXX begin` and after `end`. Some empty `spthy`  
     files may exist in the same folder. You can safely ignore them.
* a folder `report` containing some automated analysis
  1. `table` contains the table of the strongest threat model for secrecy and
     agreement claims
  2. `anon` contains the table of the strongest threat model for anonymity
     claims, along with a completion status: `full` if all proofs completed, `no
     self reveal` if only proofs where reveals of self are allowed did not
     complete, and `bound` otherwise.
  3. `levels` contains a table of the correspondance between strongest threat
     model and Noise specification levels, along with information about
     monotonicity of these levels
  4. `classes` is the list of strongest equivalence classes we encountered (you can
  cross reference it with the tables in `table` and `anon`.
  5. `levels.dot` and `classes.dot` represents (parts of) the set ordered by
     subsumption of strongest threat models. The color represents which levels
     correspond: blue for agreement (0 light to 2 dark) and red to green for
     secrecy 0 to 5.
  6. `*handshake_order.dot` represents the "cryptographically better" partial order
  on patterns. The `no_anon` version ignores anonymity results, the `imprecise_anon`
  only includes patterns where we have anonymity results up to the `no self reveal` levels,
  and the `precise_anon` up to the `full` level.

Dot format graphs are expect to be viewed after transitive reduction:
```
tred imprecise_anon_handshake_order.dot | dot -Txlib
```

Each spthy file can be loaded into the tamarin prover and its correctness verified. If an attack is found, it can be inspected in the prover's graphical interface. Further information on using Tamarin can be found at its [website](https://tamarin-prover.github.io/) or in its [manual](https://tamarin-prover.github.io/manual/tex/tamarin-manual.pdf).

