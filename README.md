# Error-Tolerant HLL
Error-Tolerant against soft errors HLL

## Description
The Remove Minimum (RM) Scheme exploits the features of the HLL algorithm to provide effective protection against soft errors without
requiring additional memory. This code is used in the paper "Remove Minimum (RM): An Error-Tolerant Scheme for Cardinality Estimate by HyperLogLog" by Pedro Reviriego, Jorge Martinez, Ori Rottenstreich, Shanshan Liu and Fabrizio Lombardi.

The Error-Tolerant HyperLogLog code used Hideaki Ohno's HyperLogLog as a starting point https://github.com/hideo55/cpp-HyperLogLog

## Compilation
This Visual Studio C++ project consists of 3 files: hyperloglog.hpp, murmur3.h and main.cpp (test bench)

## Command line arguments
Command line arguments are:

- w: bit width, default value is w=10 and valid values are [4,30]
- k: random keys, default value is k=10000, valid values are {500, 1000, 5000, 10000, 50000, 100000, 500000, 1000000}
- e: errors, default value is e=1000
- r: runs, default value is 1000, it is used to run the test multiple times
- t: protect threshold, default value is t=2
- f: input keys, when not present the test is run with a set of random keys

**example: hll.exe w=10 k=100000 e=10000 t=0 r=1000**

The example above creates a HLL having 2^10 counters and inserts 100,000 random keys. Te test injects 10,000 errors in all the bit positions of the 1,024 counters, from bit 0 to bit 7. It compares the resulting estimate of the unprotected HLL vs. the protected HLL using the Remove Minimum (RM) Scheme.

In this example, the test is run 1,000 times and produces 8x2 output files, one for each bit for 2 scenarios, the unprotected HLL and the protected HLL using the RM Scheme. It injects 10,000 errors in all the bits of each HLL of the 1,024 counters. The output file with prefix "hll0_" contains the run, the HLL estimate, the minimum, average and the maximum estimate of the unprotected HLL. The output file with prefix "hll1_" contains the run, the HLL estimate, the minimum, average and the maximum estimate of the protected HLL using the RM Scheme. Fially, the test produces 2 global output files having prefix "hll0_" and "hll1_" and 1 additioal file with prefix "perf_" containing the results of the performance evaluation.

## License

MIT
