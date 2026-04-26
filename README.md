# The Niche Connectivity Paradox

## Multichrome Contagions Overcome Vaccine Hesitancy more effectively than Monochromacy

Ho-Chun Herbert Chang and Feng Fu

Dartmouth College

## Overview

This repository contains the code and intermediate data for reproducing the analyses in "The Niche Connectivity Paradox: Multichrome Contagions Overcome Vaccine Hesitancy more effectively than Monochromacy." The paper analyzes vaccine hesitancy through a network diffusion framework, distinguishing between monochrome contagions (vaccine-focused messaging alone) and multichrome contagions (vaccine messages spreading alongside thematically distant topics). Using 3.5 billion tweets from a COVID-19 dataset and 250 million tweets from a pro/anti-vax dataset, we demonstrate that fragmented, multi-topic networks generate higher pro-vaccine diffusion than dense, homogeneous ones, a finding we term the niche connectivity paradox.

## Repository Structure

**Notebooks**

- `Ideological_Diversity-NCOMMS.ipynb`
  Computes ideology scores and source diversity (Shannon entropy) for pro-vax, anti-vax, and wavering individuals. Produces Figure 5 (ideology distributions and cumulative source diversity).

- `Individual_Regressions-NCOMMS.ipynb`
  Individual-level analyses of switcher characteristics, including centrality comparisons (betweenness, core number, in-degree, out-degree) across the three user groups. Produces Figure 6 with pairwise permutation tests and Cohen's d effect sizes.

- `Pro-Hashnet-EXP-NCOMMS.ipynb`
  Constructs the multiplex hashtag co-occurrence networks. Identifies top co-spreading hashtags with pro-vax tweets, builds the frontier networks for AI/data science, Tokyo Olympics, climate change, and disease categories. Produces Figure 1 and Table 1.

- `Simulation_Explore-NCOMMS.ipynb`
  Exploratory analysis of network diffusion simulations. Examines diffusion dynamics across different co-contagion networks with and without dormancy. Produces Figures 2 and 3.

- `Simulations_Only_NCOMMS.ipynb`
  Runs the full Monte Carlo simulation suite (Algorithm 1) across 101 randomly sampled hashtag networks. Produces Figure 4 (conversion yield vs. network properties) and the sensitivity analysis across dormancy rates reported in Appendix E.

**Data Files**

- `indv_hashtag_simulations.pkl`
  Simulation results for the 101-hashtag validation (100 runs per hashtag). Contains conversion yield, speed, and gain for each simulation.

- `network_measures.pkl`
  Precomputed network statistics (density, connected components, overlap metrics) for each hashtag network.

- `simulations_group.pkl`
  Simulation results for the four main co-contagion networks (AI, Tokyo Olympics, Climate Change, Disease).

## Data Requirements

The raw Twitter data is not included in this repository due to Twitter's Terms of Service. The analyses depend on two public datasets.

**Dataset 1 (COVID-19 tweets).** Chen, E., Lerman, K., Ferrara, E. (2020). "Tracking social media discourse about the COVID-19 pandemic." JMIR Public Health and Surveillance, 6(2), e19273. Available at https://github.com/echen102/COVID-19-TweetIDs

**Dataset 2 (Pro/anti-vax tweets).** Muric, G., Wu, Y., Ferrara, E. (2021). "COVID-19 vaccine hesitancy on social media." JMIR Public Health and Surveillance, 7(11), e30642. Available at https://github.com/gmuric/avax-tweets-dataset

To reproduce the full pipeline from raw data, hydrate the tweet IDs from both datasets using the Twitter/X API, then follow the notebook order described below.

## Dependencies

- Python 3.8+
- numpy
- pandas
- scipy (sparse matrix operations for simulations)
- networkx
- matplotlib
- seaborn
- Botometer (v4, for bot detection; requires a RapidAPI key)
- pandarallel (for parallel processing)

Install with

```
pip install numpy pandas scipy networkx matplotlib seaborn botometer pandarallel
```

## Reproduction Steps

1. **Data preparation.** Hydrate tweet IDs from both datasets. Run Botometer v4 on user accounts and filter at the 0.5 threshold. Compute ideology scores from URL-sharing patterns using AllSides domain ratings.

2. **Network construction.** Run `Pro-Hashnet-EXP-NCOMMS.ipynb` to build the multiplex hashtag co-occurrence networks and identify the frontier between pro-vax and co-contagion communities.

3. **Simulations.** Run `Simulations_Only_NCOMMS.ipynb` to execute the Monte Carlo diffusion simulations (Algorithm 1). The notebook uses scipy.sparse CSR matrices for the adjacency operations. Run `Simulation_Explore-NCOMMS.ipynb` for the exploratory diffusion analyses.

4. **Individual analyses.** Run `Ideological_Diversity-NCOMMS.ipynb` for ideology and source diversity, then `Individual_Regressions-NCOMMS.ipynb` for centrality comparisons and permutation tests.

The `.pkl` files in the repository contain precomputed intermediate results so that downstream notebooks can be run without re-executing the full simulation suite.

## Citation

If you use this code or data, please cite

```
Chang, H.-C. H. & Fu, F. (2026). The Niche Connectivity Paradox: Multichrome
Contagions Overcome Vaccine Hesitancy more effectively than Monochromacy.
```

## License

MIT

## Contact

Herbert Chang
  herbert.chang@dartmouth.edu
