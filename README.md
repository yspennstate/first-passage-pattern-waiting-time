# The waiting time for a first-passage pattern in simple random walk

Yitzchak Shmalo

Paper: [paper/main.pdf](paper/main.pdf) (source [paper/main.tex](paper/main.tex)).

Fix $\lambda<0$ and let $T_n$ be the first time at which the last $n$ steps of a simple symmetric random walk form a
first-passage path to the level nearest $\lambda\sqrt n$ (rounded down, then up by one if the parity is wrong).
Pitman and Tang (arXiv:1411.0041) showed that $E T_n$ lies between constant multiples of $n$ and $n^{5/4}$, and
Peres conjectured that its order is $n\log n$. The paper proves this: $c\,n\log n\le E T_n\le C\,n\log n$.

The key estimate is that a first-passage window starts in a given interval of length $n/2$ with probability of
order $1/\log n$. The upper bound comes from the range of the difference of two independent walks sampled at the
descending ladder times of one of them, which has expected size $O(\sqrt n/\log n)$.

## Code

No step of the proof uses computation. Run from the repository root:

```sh
clang++ -O3 -std=c++17 code/simulate.cpp -o code/simulate
code/simulate check 8 2            # compares the window detector with direct scanning
python3 code/exact.py --max-n 12   # exact E T_n by the matching matrix and by the prefix automaton
python3 code/run_numerics.py       # Monte Carlo estimates of E T_n and of the ladder-time range
python3 code/audit.py              # finite checks of the identities in the proof, and fit summaries
```

`code/simulate wait n a reps seed` prints the sample mean of $T_n$ for the endpoint $-a$. The outputs used in the
paper are in `data/`: `exact.csv` (Table 1), `monte_carlo.csv` (Table 2), `record_range.csv`, `audit.json` and
`fits.json`. The Python scripts need NumPy and SciPy.

## Funding

The research presented in this paper was supported by the European Research Council (ERC) under the European
Union's Horizon Europe research and innovation program (grant agreement No. 101041711), by the Simons Foundation
as part of the Collaboration on the Mathematical and Scientific Foundations of Deep Learning, by Heights Labs, by
Convex Nexus Capital, by the Israel Science Foundation (grant number 2258/19), and by the Israel Science Foundation
(ISF Grant 4101/25). Computational resources were provided in part by Google Cloud through its education credits
program (credit 530550103).
