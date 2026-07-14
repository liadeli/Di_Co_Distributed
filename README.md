# Simulation Parameters for SMILE

This repository contains the MATLAB parameter files used for the numerical experiments associated with the paper:

> **Distributed Learning in Markovian Restless Bandits over Interference Graphs for Stable Spectrum Sharing**  
> Liad Lea Didi and Kobi Cohen

The files specify the simulation horizons, network sizes, interference neighborhood sets, Markov transition matrices, reward parameters, and additional experiment-specific settings used to evaluate the proposed **SMILE** algorithm.

## About SMILE

SMILE, short for **Stable Multi-matching with Interference-aware LEarning**, is a distributed learning algorithm for stable spectrum sharing over interference graphs under unknown restless Markovian channel dynamics.

The simulations examine convergence, sensitivity to the exploration parameter, scalability, adaptation to topology changes, comparisons with benchmark learning algorithms, spatial interference, and dynamic traffic conditions.

## Repository Contents

| Figure | Simulation scenario | Main configuration | Parameter file |
|---|---|---|---|
| Fig. 5 | Small-network convergence and per-cell rates | \(L=3,\ S=5\) | [`Fig05.m`](Fig05.m) |
| Fig. 6 | Convergence to the stable allocation | \(L=5,\ S=3\) | [`Fig06.m`](Fig06.m) |
| Fig. 7 | Sensitivity to the exploration parameter \(\epsilon\) | \(L=7,\ S=4\) | [`Fig07.m`](Fig07.m) |
| Fig. 8 | Large-scale scalability | [`Fig08.m`](Fig08.m) |
| Fig. 9 | Adaptation to a dynamic interference topology | \(L=5,\ S=3\) | [`Fig09.m`](Fig09.m) |
| Fig. 10 | Comparison with RMAB-based benchmarks | \(L=3,\ S=6\) | [`Fig10.m`](Fig10.m) |
| Fig. 11 | Benchmark comparison under i.i.d. channels | \(L=6,\ S=6\) | [`Fig11.m`](Fig11.m) |
| Fig. 12 | Heterogeneous i.i.d. Gaussian rewards | \(L=4,\ S=4\) | [`Fig12.m`](Fig12.m) |
| Fig. 13 | Geometry-based spatial interference | \(L=10,\ S=5\) | [`Fig13.m`](Fig13.m) |
| Fig. 14 | Dynamic traffic and queueing buffers | \(L=10,\ S=5\) | [`Fig14.m`](Fig14.m) |

## Parameter-File Structure

The files use a common notation whenever applicable:

- `max_T`: simulation horizon.
- `t_grid`: interval between recorded performance samples.
- `t_vec`: vector of recorded time indices.
- `L`: number of cells.
- `S`: number of channels.
- `epsilon`: exploration parameter used by SMILE.
- `N_l_mat{l}`: interference-neighborhood set of cell \(l\).
- `N`: number of Markov states.
- `P` or `P_s`: Markov transition probability matrix.
- `P_matrices`: collection of transition matrices.
- `markov_states`: state-dependent transmission rewards.
- `mu_mat`: expected cell-channel reward matrix.

Rows of `mu_mat` correspond to cells and columns correspond to channels. Unless stated otherwise, the entries of `markov_states` are ordered by cell-channel pairs:

```text
(1,1), ..., (1,S), (2,1), ..., (2,S), ..., (L,1), ..., (L,S)
```
## License

Add a license file before publication. For research code and parameter files, commonly used options include the MIT License and the BSD 3-Clause License.
