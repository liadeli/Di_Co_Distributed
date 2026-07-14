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
| Fig. 5 | Small-network convergence and per-cell rates | \(L=3,\ S=5\) | [`Fig05_Small_Network_Convergence_Parameters.m`](Fig05_Small_Network_Convergence_Parameters.m) |
| Fig. 6 | Convergence to the stable allocation | \(L=5,\ S=3\) | [`Fig06_Stable_Allocation_Convergence_Parameters.m`](Fig06_Stable_Allocation_Convergence_Parameters.m) |
| Fig. 7 | Sensitivity to the exploration parameter \(\epsilon\) | \(L=7,\ S=4\) | [`Fig07_Epsilon_Sensitivity_Parameters.m`](Fig07_Epsilon_Sensitivity_Parameters.m) |
| Fig. 8(a) | Large-scale scalability | \(L=50,\ S=50\) | [`Fig08a_Large_Scale_L50_S50_Parameters.m`](Fig08a_Large_Scale_L50_S50_Parameters.m) |
| Fig. 9 | Adaptation to a dynamic interference topology | \(L=5,\ S=3\) | [`Fig09_Dynamic_Interference_Topology_Parameters.m`](Fig09_Dynamic_Interference_Topology_Parameters.m) |
| Fig. 10 | Comparison with RMAB-based benchmarks | \(L=3,\ S=6\) | [`Fig10_RMAB_Benchmark_Comparison_Parameters.m`](Fig10_RMAB_Benchmark_Comparison_Parameters.m) |
| Fig. 11 | Benchmark comparison under i.i.d. channels | \(L=6,\ S=6\) | [`Fig11_IID_Channel_Benchmark_Comparison_Parameters.m`](Fig11_IID_Channel_Benchmark_Comparison_Parameters.m) |
| Fig. 12 | Heterogeneous i.i.d. Gaussian rewards | \(L=4,\ S=4\) | [`Fig12_Heterogeneous_IID_Channel_Comparison_Parameters.m`](Fig12_Heterogeneous_IID_Channel_Comparison_Parameters.m) |
| Fig. 13 | Geometry-based spatial interference | \(L=10,\ S=5\) | [`Fig13_SINR_Based_Spatial_Interference_Parameters.m`](Fig13_SINR_Based_Spatial_Interference_Parameters.m) |
| Fig. 14 | Dynamic traffic and queueing buffers | \(L=10,\ S=5\) | [`Fig14_Dynamic_Traffic_Queueing_Parameters.m`](Fig14_Dynamic_Traffic_Queueing_Parameters.m) |

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
- `sim_size`: number of independent Monte Carlo realizations.

Rows of `mu_mat` correspond to cells and columns correspond to channels. Unless stated otherwise, the entries of `markov_states` are ordered by cell-channel pairs:

```text
(1,1), ..., (1,S), (2,1), ..., (2,S), ..., (L,1), ..., (L,S)
```

## Simulation Summary

### Figure 5: Small-Network Convergence

This experiment uses three cells and five channels. Cells 1 and 2 interfere with each other, while cell 3 is isolated. The wireless channels are represented by a six-state finite-state Markov channel model.

The parameter file includes:

- the common \(6 \times 6\) transition matrix;
- the \(3 \times 5\) expected transmission-rate matrix;
- the interference graph;
- the simulation horizon and sampling grid.

### Figure 6: Stable-Allocation Convergence

This experiment uses five cells and three channels under a five-state restless Markov model. The file includes the interference topology, transition matrix, and expected rate matrix used to evaluate convergence to the optimal stable allocation.

### Figure 7: Sensitivity to \(\epsilon\)

This experiment evaluates:

```matlab
epsilon_values = [0, 0.05, 0.5];
```

Each channel follows a two-state restless Markov process. The state rewards are drawn from the interval \([0,10]\). A fixed MATLAB random seed is included in the parameter file to make the generated reward matrix reproducible.

### Figure 8(a): Large-Scale Scalability

This file contains the parameters for the \(L=50,\ S=50\) experiment. The cells form a line interference graph, and all channels use a common two-state transition matrix.

Only the parameters for Fig. 8(a) are currently included. Separate files should be added for Fig. 8(b), with \(L=100,\ S=100\), and Fig. 8(c), with \(L=100,\ S=50\), if those configurations are to be reproduced independently.

### Figure 9: Dynamic Interference Topology

This experiment studies adaptation to a topology change at:

```matlab
topology_change_time = 200000;
```

The file contains separate pre-change and post-change neighborhood sets:

```matlab
N_l_mat_pre
N_l_mat_post
```

It also contains the two-state Markov transition matrices and the state-dependent transmission rates.

### Figure 10: RMAB Benchmark Comparison

This experiment compares SMILE with RCA, DSEE, and DSSL. It uses three cells, six channels, and heterogeneous two-state Markov transition matrices.

The second Markov state has zero reward, consistent with a good/bad channel model in which the bad state yields no transmission rate.

### Figure 11: i.i.d. Channel Comparison

This experiment uses temporally independent channel realizations rather than Markov transitions. The channel success probabilities are:

```matlab
p_iid = [1.0, 0.9, 0.8, 0.7, 0.6, 0.5];
```

The good-state and bad-state rewards are:

```matlab
reward_states = [1.0; 0.1];
```

The parameter file also computes the expected reward of each channel.

### Figure 12: Heterogeneous i.i.d. Gaussian Rewards

The instantaneous reward is generated according to:

\[
r_{\ell,s}(t)=\mu_{\ell,s}+z_{\ell,s}(t),
\]

where \(z_{\ell,s}(t)\) is zero-mean Gaussian noise. The file contains the \(4 \times 4\) expected reward matrix, the interference topology, the Gaussian parameter, and the number of Monte Carlo runs.

This experiment compares SMILE with dE3 and GoT.

### Figure 13: Spatial Interference

This experiment uses ten cells and five channels. The file contains the binary interference graph used by the learning and allocation algorithm, together with the Markov transition and reward parameters.

The experiment is intended to evaluate performance when the actual achieved rates are affected by continuous spatial interference, while the distributed allocation mechanism operates using a binary graph abstraction.

### Figure 14: Dynamic Traffic and Queueing

This experiment evaluates SMILE in a non-saturated network with time-varying packet arrivals and dynamic transmission queues.

The file includes:

```matlab
traffic_load = 0.90;
packet_size_bytes = 1500;
packet_size_bits = 12000;
```

Packet arrivals are modeled by a Poisson process. The traffic load is set to \(90\%\) of the corresponding stable-allocation service rate.

## Using the Parameter Files

Each file is a MATLAB script. To load a parameter set, place the file in the MATLAB working directory and run it. For example:

```matlab
run('Fig05_Small_Network_Convergence_Parameters.m');
```

The parameters will then be available in the MATLAB workspace.

The files include basic consistency checks for matrix dimensions, transition-probability rows, stationary distributions, and interference-neighborhood definitions.

## Software

The parameter files are written for MATLAB.

Please record the exact MATLAB release used for the published experiments here:

```text
MATLAB version: [TO BE ADDED]
Operating system: [TO BE ADDED]
```

## Reproducibility Notes

These files contain the experiment parameters. The full simulation implementation, plotting scripts, benchmark implementations, and random-number-generation procedures should also be included in the repository if complete end-to-end reproduction of the published figures is required.

Before making the repository public, verify the following items:

1. **Figure 7 topology:** the neighborhood sets in the current parameter file should be checked against the topology described in the final manuscript.
2. **Figure 9 post-change topology:** the post-change neighborhood sets should be checked against the final version of the paper.
3. **Figure 12 Gaussian parameter:** confirm whether `sigma = 0.05` denotes the standard deviation or whether the intended condition is \(\sigma^2=0.05\).
4. **Figure 13 transition matrices:** six transition matrices are currently stored although the experiment uses five channels. The file assigns the first five matrices to the channels.
5. **Figure 14 reward matrix:** the supplied `markov_states` matrix currently contains 43 cell-channel columns, while \(L \times S=50\) columns are required.
6. **Figure 14 topology:** the neighborhood sets should be checked against the topology reported in the final manuscript.
7. **Figure 8:** parameter files for Fig. 8(b) and Fig. 8(c) have not yet been added.

This verification section can be removed once the final repository and manuscript are fully synchronized.

## Citation

When using these parameter files, please cite the associated paper:

```bibtex
@article{didi_smile,
  author  = {Didi, Liad Lea and Cohen, Kobi},
  title   = {Distributed Learning in Markovian Restless Bandits over
             Interference Graphs for Stable Spectrum Sharing},
  journal = {[Journal name]},
  year    = {[Year]},
  doi     = {[DOI]}
}
```

## Contact

For questions regarding the simulation parameters, please contact:

**Liad Lea Didi**  
School of Electrical and Computer Engineering  
Ben-Gurion University of the Negev  
Email: liadeli@post.bgu.ac.il

## License

Add a license file before publication. For research code and parameter files, commonly used options include the MIT License and the BSD 3-Clause License.
