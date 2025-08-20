
# LRS - Longest Run Subsequence Problem

This repository contains the implementation of a BRKGA guided by LLM to solve the Longest Run Subsequence (LRS) problem.

## Problem Description

The LRS problem consists of finding a subsequence of an input string that maximizes the sum of the lengths of consecutive runs of identical characters.

## Project Structure

```
├── bin/                   # Executables
├── Instances/             # Instances
├── CD/                    # Statistical analysis and results
├── tuning_instances/      # Randomly generated instances for dataset tuning
└── LLM_probabilities/     # LLM probabilities
```

## Running the Algorithms

### Instance Format

Instances are in plain text format, each file contains a string of characters. Example:
```
BAABAABABBAABAABBABBBABAABBBBAAAAAABBAAABBBAABABBABBABBBBABAAABBBAAABAABBAABBABBBABAABBBAAAABAABABAB
```

### Parameters

```bash
./brkgallm -i <instance_file> [-p <pop_size>] [-pe <elite_prop>] [-pm <mutant_prop>] [-rhoe <inherit_prob>] [-t <time>] [-tuning] [-stnweb]
```
- `-p`: Population size 
- `-pe`: Elite proportion 
- `-pm`: Mutant proportion 
- `-rhoe`: Elite inheritance probability 
- `-t`: Time limit 
- `-tuning`: Tuning mode
- `-stnweb`: stnweb mode

- `-model(LLM)`: name of the probabilities folder inside LLM_probabilities


### Execution Examples

./brkgallm -i Instances/len_100_sigma32_1.txt -p 18 -pe 0.23 -pm 0.2 -rhoe 0.69 -model Lama-4-Maverick


## Statistical Analysis

The `CD/` directory contains tools for statistical analysis:

1. Prepare a `results.dat` file with the results of all algorithms
2. Use R with the script `statistical_evaluation.R` to generate statistical analyses

See `CD/Readme` for detailed instructions on statistical analysis.

## Instances


The `Instances/` directory contains test instances with different characteristics:
- `len_{100,200,300,500,1000,2000}_sigma{2,4,6,8,16,32}_{1..30}.txt`: 30 strings for each length-sigma combination

## Tuning Instances

The `Tuning_instances/` directory contains a randomly generated dataset:
- `len_{100,200,300,500,1000,2000}_sigma{2,4,6,8,16,32}.txt`: 1 instance for each length-sigma combination (35)
- `len_{100,200,300,500,1000,2000}_sigma{random}_1.txt`: 1 instance for each length, choosing sigma randomly (7)
for a total of 42 instances.


## Requirements

- C++ compiler with support for C++11 or higher
- For statistical analysis: R with the 'scmamp' package

