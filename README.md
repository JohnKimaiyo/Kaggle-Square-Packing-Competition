# Packing Unit Squares into a Square: Kaggle Solution

My entry for the Kaggle competition on packing n unit squares (side length 1)
into the smallest possible axis-aligned square container, for n = 1 to 1,000.

**Author:** John Kimaiyo
**Competition:** [competition name and link]
**Status:** Work in progress

## Problem

For each puzzle n, place n non-overlapping unit squares inside a square
container and make the container's side length as small as possible.
Squares may be rotated [confirm on the Data tab]. The score is
[total / average container side across all 1,000 puzzles; lower is better;
confirm on the Evaluation tab].

## Approach

1. **Baseline:** grid packing with side = ceil(sqrt(n)) and no rotation.
2. **Known packings:** best-known tilted packings for small n, taken from
   Erich Friedman's "Squares in Squares" collection.
3. **Optimization:** a shrink-and-repair loop. Reduce the container slightly,
   then resolve overlaps by moving and rotating squares (simulated annealing
   or gradient descent on an overlap penalty). Keep the result if overlap
   reaches zero.
4. **Validation:** every packing is checked before submission to confirm all
   squares are inside the container, none overlap, and each puzzle has
   exactly n squares.

## Requirements

- Python 3.10+
- numpy, pandas, scipy, shapely
- numba (optional)

```bash
pip install numpy pandas scipy shapely numba
```

## Project structure

```
.
├── data/                  # competition files (not committed)
├── baseline.py            # grid packing baseline
├── validate.py            # overlap and boundary checker
├── optimize.py            # shrink-and-repair search
├── submission.csv         # file uploaded to Kaggle
└── README.md
```

## How to run

```bash
python baseline.py         # writes submission.csv
python validate.py         # must pass before every submission
```

Then upload `submission.csv` on the competition's Submit Predictions page.

## Submission log

| Version | Description | Validated | Score |
|---|---|---|---|
| v1 | Plain grid, side = ceil(sqrt(n)), no rotation | Yes | [score] |
| v2 | Grid + best-known packings for small n | | |
| v3 | Optimization for n just below perfect squares | | |

## Notes

- Gains are largest for n just below a perfect square (5, 10, 17, 26, ...).
- Use a small numerical tolerance in the validator, since the official
  scorer may reject overlaps caused by rounding.

## References

- Erich Friedman, "Squares in Squares", Packing Center.
- Kaggle competition page: [link]

## License

[MIT or your choice]
