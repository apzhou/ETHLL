# Error-Tolerant HLL
Error-Tolerant HLL against soft errors on the HLL counters.

## Description
The Remove Minimum (RM) Scheme exploits the features of the HLL algorithm to provide effective protection against soft errors without
requiring additional memory. This code is used in the paper "Remove Minimum (RM): An Error-Tolerant Scheme for Cardinality Estimate by HyperLogLog" by Pedro Reviriego, Jorge Martinez, Ori Rottenstreich, Shanshan Liu and Fabrizio Lombardi, that has been accepted for publication in IEEE Transactions on Dependable and Secure Computing.

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

**example: hll.exe w=10 k=100000 e=10 t=0 r=1000**

The example above creates a HLL having 2^10 counters and inserts 100,000 random keys. Te test injects 10 errors in all the bit positions of the 1,024 counters, from bit 0 to bit 7. It compares the resulting estimate of the unprotected HLL vs. the protected HLL using the Remove Minimum (RM) Scheme.

In this example, the test is run 1,000 times and produces 16 output files, one for each bit for 2 scenarios, the unprotected HLL and the protected HLL using the RM Scheme. It injects 10 errors in all the bits of each HLL of the 1,024 counters. 

The test produces the output files "hll0_b0_w10_k100000_e10_t0_r1000.txt" to "hll0_b7_w10_k100000_e10_t0_r1000.txt" for the estimates of bits 0 to 7. These files contain contain the run, the HLL estimate, the minimum, average and the maximum estimate of the unprotected HLL. Files "hll1_b0_w10_k100000_e10_t0_r1000.txt" to "hll1_b7_w10_k100000_e10_t0_r1000.txt" contain the run, the HLL estimate, the minimum, average and the maximum estimate of the protected HLL using the RM Scheme.

In addition, the test produces 2 global output files, "hll0_w10_k100000_e10_t0_r1000.txt" and "hll1_w10_k100000_e10_t0_r1000.txt" for the unprotected HLL and the protected HLL, respectively. Finaly, the file "perf_w10_k100000_e10_t0_r1000.txt" contains the results of the performance evaluation in terms of execution time.

When an input file is given using the f parameter, the test is run with the keys of the input file instead of using random keys. The test hll.exe w=10 f=1000_ips.txt e=10000 r =1000 creates a HLL having 2^10 counters with the keys in the input file "1000_ips.txt".

## License

MIT
