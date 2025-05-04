# Computational Theory Assessment

[![Python 3.10](https://img.shields.io/badge/python-3.10+-blue)]()
[![Notebook Validation](https://img.shields.io/badge/nbval-passing-brightgreen)]()

This document presents the completed work for the Computational Theory module (January–May 2025). The project is structured around eight tasks, each exploring a foundational concept of computation. All work is presented in a Jupyter Notebook and is guided by the requirements set out in the official assessment instructions. Each task is implemented using Python, with detailed Markdown explanations, validation tests, and adherence to the FIPS 180-4 Secure Hash Standard where applicable.

---

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Features](#features)  
3. [Environment & Installation](#environment--installation)  
4. [Task History](#task-history)  
   - [Task 1: Binary Representations](#task-1-binary-representations)  
   - [Task 2: Hash Functions](#task-2-hash-functions)  
   - [Task 3: SHA256](#task-3-sha256)  
   - [Task 4: Prime Numbers](#task-4-prime-numbers)  
   - [Task 5: Roots](#task-5-roots)  
   - [Task 6: Proof of Work](#task-6-proof-of-work)  
   - [Task 7: Turing Machines](#task-7-turing-machines)  
   - [Task 8: Computational Complexity](#task-8-computational-complexity)  
5. [Outputs](#outputs)  
6. [Development Reflection](#development-reflection)  
7. [Testing Strategy](#testing-strategy)

---

## Project Overview

This project demonstrates a rigorous and practical understanding of computational theory through the completion of eight structured tasks. Topics include bitwise operations, hashing algorithms, cryptographic padding schemes, number theory, fractional binary constants, mining simulations, formal machine models, and algorithm complexity.

Each task has been carefully implemented to showcase both technical correctness and theoretical understanding. The work emphasizes clean code, academic formatting, unit test coverage, and step-by-step logical explanation.

---

## Features

This notebook serves as a comprehensive implementation of foundational topics in computational theory, structured around the eight official tasks provided in the assessment brief. The design prioritizes clarity, correctness, and alignment with academic expectations.

### Complete and Accurate Task Coverage

Each of the eight required tasks is fully implemented using the exact task structure and naming provided in the official brief. Implementation avoids scope creep and stays true to the original intent of the instructions. Each task is clearly separated with proper Markdown headings and structured logic blocks.

Key areas include:

- **Bitwise operations** using precise binary manipulations with correct masking and rotation logic.
- **Hash function conversion** from C to Python with analysis on numeric choices and modular constraints.
- **SHA256 padding** using manual binary formatting and length encoding.
- **Prime number generation** via two algorithmic approaches with correctness checks.
- **Fractional root bit extraction** with binary output and bit-level slicing.
- **Proof-of-work simulation** using wordlist iteration and SHA256 digest analysis.
- **Turing machine implementation** using symbolic state logic and tape simulation.
- **Bubble sort complexity analysis** across all permutations with recorded comparisons.

The focus is on correctness, transparency, and minimal deviation from task intent.

### Consistent, Clear, and Contextual Markdown Documentation

Each task is documented with:

- An academic introduction outlining its theoretical purpose.
- Clarification of how the implementation satisfies the task.
- Contextual relevance to computer science, such as cryptography or algorithmic analysis.

Markdown cells are consistently structured and avoid unnecessary personal commentary. All explanations are phrased to demonstrate understanding rather than just describing code.

### Well-Defined Testing Approach

Tests are designed to be visible, intentional, and functionally informative:

- Each key function is followed by test cells that evaluate correctness and edge case handling.
- Output from these tests is displayed immediately for manual review.
- Results are explained where necessary, improving traceability of function behavior.

This approach allows each task to be assessed independently and transparently.

### Emphasis on Structure, Academic Tone, and Reproducibility

This project emphasizes academic consistency and technical presentation through:

- **Reproducibility**: Running the notebook top-to-bottom produces all results without external input.
- **Code clarity**: Logic is separated into minimal units, and code is formatted and commented to be readable without additional guidance.
- **Academic tone**: All content avoids casual language, maintains consistent terminology, and frames each task as a study in computational theory.

Together, these ensure that the notebook serves not just as a working submission, but also as a clear, inspectable, and technically mature project.

---

## Environment & Installation

This project was developed and tested with:

- Platform: win32
- Python 3.12.2
- Testing tools:
  - pytest 8.3.5
  - pluggy 1.5.0
  - nbval 0.11.0

First, clone the repository and switch into its folder:

  - git clone https://github.com/Cpgeragh/computational_theory_assessment.git
  - cd computational_theory_assessment

To install the required packages:

  - pip install -r requirements.txt

Or manually:

  - pip install pytest nbval

### Running the Notebook

To execute the project correctly:

  1. Open `tasks.ipynb` in Jupyter Notebook or VS Code.
  2. Run **all cells in order** from top to bottom using "Run All".
  3. Ensure all output and test results are displayed without errors.

### Verifying with Automated Testing

To validate that all outputs match the expected results:

  - pytest --nbval-lax tasks.ipynb

This ensures all cells execute correctly and that all test logic passes. Minor differences in runtime output (e.g., timing or file paths) are tolerated under `--nbval-lax`, making it ideal for reproducibility checks without being blocked by non-deterministic output.

---

## Task History

### Task 1: Binary Representations

This task introduces bitwise manipulation within the 32-bit unsigned integer domain. It focuses on implementing fundamental operations used in cryptographic hash functions and hardware logic:

- **Left and right bit rotations**: Used for nonlinear transformations in hashing.
- **Conditional bit selection (`ch`)**: Chooses bits from inputs based on selector masks.
- **Majority voting (`maj`)**: Determines bit consensus across three inputs.

These operations are essential to secure hash design and underpin functions in standards such as SHA-256. The task includes both implementation and verification through test cases.

---

### Task 2: Hash Functions

This task focuses on rewriting a classic hash function from C into Python, originally described by Kernighan and Ritchie. The function performs character-by-character hashing using:

- A multiplier-based recurrence relation.
- Modulo arithmetic to constrain output size.

The rationale for using constants such as `31` and `101` is discussed in the context of prime number distribution, entropy preservation, and hash collision reduction. The task explores how basic hashing can provide insight into more advanced techniques.

---

### Task 3: SHA256

This task explores the SHA256 message padding process, following the Secure Hash Standard (FIPS 180-4). The padding operation ensures that any input message conforms to a 512-bit block structure before processing.

Steps include:

- Appending a `1` bit to signal message end.
- Padding with zeros until the total message length is congruent to 448 modulo 512.
- Adding the original message length as a 64-bit big-endian integer.

```
SHA-256 Padding Process for Input "abc":
Original Message (24 bits = 3 bytes)
┌─────────┬─────────┬─────────┐
│    a    │    b    │    c    │
│ 01100001│ 01100010│ 01100011│
└─────────┴─────────┴─────────┘
Step 1: Append '1' bit
┌─────────┬─────────┬─────────┬─────────┐
│    a    │    b    │    c    │10000000 │
│ 01100001│ 01100010│ 01100011│10000000 │
└─────────┴─────────┴─────────┴─────────┘
▲
'1' bit followed by
7 '0' bits (0x80)
Step 2: Pad with zeros until length ≡ 448 mod 512 (56 bytes)
┌─────────┬─────────┬─────────┬─────────┬─────────────────────────────┐
│    a    │    b    │    c    │ 0x80    │       52 bytes of 0x00      │
│ 01100001│ 01100010│ 01100011│10000000 │00000000 00000000 ... 00000000│
└─────────┴─────────┴─────────┴─────────┴─────────────────────────────┘
Step 3: Append 64-bit length (big-endian) = 24 bits = 0x18
┌─────────┬─────────┬─────────┬─────────┬─────────────────┬─────────────────┐
│    a    │    b    │    c    │ 0x80    │  52 bytes of 0  │   0x00000018    │
└─────────┴─────────┴─────────┴─────────┴─────────────────┴─────────────────┘
▲
64-bit length field
(24 in hexadecimal)
Final padded message (512 bits = 64 bytes):
┌───────────────────────┬────────────────────────────────┬────────────────┐
│ Original 3 bytes +    │                                │                │
│ 1 byte terminator     │        52 bytes of zeros       │  8 byte length │
└───────────────────────┴────────────────────────────────┴────────────────┘
Hex view of padding only (excluding original "abc"):
80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 18
```

The result is a hexadecimal representation of the padding bytes. This task verifies conformance to official SHA-2 behavior and supports cryptographic integrity.

---

### Task 4: Prime Numbers

This task implements two prime number generation algorithms to compute the first 100 primes:

- **Trial Division**: A brute-force technique that checks each number’s divisibility up to its square root.
- **Sieve of Atkin**: A more sophisticated, optimized sieve-based method that filters primes using modular properties.

Both approaches are analyzed for correctness and performance. This task highlights the importance of primes in number theory and cryptography, especially for key generation and hash constants.

---

### Task 5: Roots

This task computes the first 32 bits of the fractional part of the square roots of the first 100 prime numbers. These constants are used in cryptographic algorithm design, including SHA-2, to introduce non-repeating, deterministic values into hashing processes.

Each root is:

- Calculated with high precision.
- Converted into a binary fractional format.
- Truncated to extract exactly 32 bits.

The final binary outputs are validated and used to demonstrate how irrational mathematical constants can contribute to secure cryptographic systems.

---

### Task 6: Proof of Work

This task simulates a simplified proof-of-work system by identifying English words whose SHA-256 hashes begin with the largest number of leading zero bits.

Steps include:

- Loading a dictionary of valid English words.
- Computing SHA-256 hashes for each word.
- Counting leading zero bits in each hash output.
- Reporting the words with the most leading zeros.

The task demonstrates how hash difficulty is quantified in mining protocols, such as Bitcoin, and includes dictionary validation to verify linguistic legitimacy of results.

---

### Task 7: Turing Machines

This task implements a simulated Turing Machine that performs binary incrementation. Starting with a binary string on tape, the machine:

- Scans from left to right.
- Identifies the least significant bit.
- Applies rules to flip bits and carry logic.
- Produces the incremented result on the same tape.

```
Binary Increment Turing Machine State Diagram:

START STATE: Move to end of tape
┌─────────┐
│  START  │
└────┬────┘
     │ Move Right until end
     ▼
┌─────────┐
│   END   │──┐
└────┬────┘  │ Any: Move Left
     │       │
     │       │
     ▼       │
┌─────────┐  │
│ PROCESS │◄─┘
└────┬────┘
     │
     ├────────────┬─────────────┐
     │            │             │
     ▼            ▼             ▼
┌─────────┐  ┌─────────┐   ┌─────────┐
│ Read '0' │  │ Read '1' │   │ No more │
└────┬────┘  └────┬────┘   └────┬────┘
     │            │             │
     │            │             │
     ▼            ▼             ▼
┌─────────┐  ┌─────────┐   ┌─────────┐
│Write '1' │  │Write '0' │   │Prepend '1'│
└────┬────┘  └────┬────┘   └────┬────┘
     │            │             │
     ▼            ▼             ▼
┌─────────┐  ┌─────────┐   ┌─────────┐
│  HALT   │  │Move Left│   │  HALT   │
└─────────┘  └────┬────┘   └─────────┘
                  │
                  └─────────────────────►

Example execution for input "100111":
Tape:      1 0 0 1 1 1
           ▲ Head starts here
                      ▲ Moves to end
                    ▲ Reads 1, writes 0, moves left
                  ▲ Reads 1, writes 0, moves left
                ▲ Reads 1, writes 0, moves left
              ▲ Reads 0, writes 1, halts
Output:    1 0 1 0 0 0
```

This task illustrates the principles of computation theory and models how state machines perform computation over symbolic tapes, reinforcing the concepts of halting, determinism, and state transitions.

---

### Task 8: Computational Complexity

This task performs a complexity analysis of bubble sort by applying it to all permutations of a five-element list. Both standard and optimized versions of bubble sort are tested:

- The standard version makes a full pass through the list regardless of sorting state.
- The optimized version terminates early if no swaps are performed in a pass.

For each permutation, the number of comparisons required to sort the list is recorded. This task demonstrates worst-case and best-case behavior and visualizes the sensitivity of bubble sort to input ordering.

---

## Outputs

Each task produces specific, verifiable outputs that demonstrate the success of the implementation and testing:

- **Task 1: Binary Representations**  
  Binary outputs of bitwise operations are printed and validated against known values. Includes left and right rotations for different shift amounts, and logical results from `ch` and `maj` functions using binary patterns. Unittest outputs confirm edge case behavior and binary correctness.

- **Task 2: Hash Functions**  
  Two outputs are produced:  
    1. Regular hash values for a set of test strings using a K&R-style polynomial hash function.  
    2. An expanded hash version prints step-by-step accumulation for each character, including ASCII values, intermediate products, and the final modulo result.

- **Task 3: SHA256**  
  Padding is computed and printed in both binary and hexadecimal forms. Output includes:  
  - Binary view of the original file content (`abc`)  
  - Appended `0x80` bit and zero-padding to align to 448 bits  
  - Final length block appended in big-endian 64-bit format  
  - Full 64-byte message block  
  - Extracted padding segment displayed in hex (`80 ... 18`) for FIPS 180-4 compliance

**Task 4: Prime Numbers**  
  Outputs the first 100 primes using both Trial Division and Sieve of Atkin algorithms with performance comparison. Tests confirm correct primality detection and elimination of composite values like 49 or 9.

  | Algorithm       | Execution Time (seconds) | Performance                  |
  |:----------------|:------------------------:|:-----------------------------|
  | Trial Division  | 0.000205                 | Faster for small inputs      |
  | Sieve of Atkin  | 0.000255                 | 1.24x slower for 100 primes  |

  Both algorithms produce identical outputs, validating their correctness while demonstrating that algorithmic complexity doesn't always predict performance for small datasets.

- **Task 5: Roots**  
  Produces a list of 32-bit binary representations of the fractional part of square roots for the first 100 primes. Outputs include:  
  - Binary strings shown for selected primes (first and last 10)  
  - Deterministic extraction via repeated tests on known values (e.g., √2)  
  - Tests ensure all 100 outputs are valid, reproducible, and bit-accurate

- **Task 6: Proof of Work**  
  Prints the English words that produce the most leading zero bits in their SHA-256 hash. Outputs include:  
  - Total number of words processed  
  - Maximum number of leading zero bits found: **16**  
  - Top word(s) with the most leading zero bits:

    | Word         | Leading Zero Bits |
    |:------------:|:-----------------:|
    | guilefulness |        16         |
    | mismatchment |        16         |
 
  - Binary conversion and hash integrity verified through unit tests

- **Task 7: Turing Machines**  
  Output consists of before-and-after tape states for binary strings incremented by the simulated Turing Machine. Includes multiple test cases like `111 → 1000` and `100111 → 101000`. Tests confirm correctness of state transitions and carry propagation logic.

**Task 8: Computational Complexity**  
  Two sets of outputs:  
  - Standard bubble sort prints input permutation, number of comparisons (always 10), and final sorted list  
  - Optimised version shows reduced comparisons (e.g., 4 for already sorted input)  
  - First 10 and last 10 permutations printed for both implementations to illustrate comparison cost across the full permutation space

  | Comparison Metrics | Standard Bubble Sort | Optimized Bubble Sort |
  |:-------------------|:--------------------:|:---------------------:|
  | Minimum comparisons | 10 | 4 |
  | Maximum comparisons | 10 | 10 |
  | Average comparisons | 10.00 | 9.26 |

  | Timing Performance | Standard Bubble Sort | Optimized Bubble Sort | Improvement |
  |:-------------------|:--------------------:|:---------------------:|:----------:|
  | All 120 permutations | 0.000199s | 0.000180s | 9.45% |
  | Already sorted | 0.000004s | 0.000001s | 61.11% |
  | Reversed | 0.000003s | 0.000003s | 10.00% |
  | 10 random samples | 0.000019s | 0.000016s | 16.06% |

  Both comparison counts and timing measurements confirm that the optimization provides significant benefits for sorted inputs while offering modest improvements for average cases.

---

## Development Reflection

The most challenging aspects of development included:

- Ensuring complete fidelity to the FIPS 180-4 padding specification.
- Generating valid English word lists and handling case sensitivity.
- Implementing a flexible Turing machine logic system with symbolic states.
- Managing computational performance while testing all permutations in Task 8.

Each challenge was approached methodically, and every solution was reviewed through incremental testing and documented analysis.

---

## Testing Strategy

A test-driven development approach was followed for all tasks. The notebook includes:

- Manual test cases for bitwise and hashing functions.
- File-based tests for SHA-256 padding.
- Dictionary validation to confirm word legitimacy.
- Assertions and runtime logs for Turing machine transitions.
- Full permutation traversal and result tracking for sorting complexity.

This strategy ensures that each task’s logic holds up under edge conditions and produces correct outputs with confidence.

