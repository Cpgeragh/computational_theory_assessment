# **Computational Theory Assessment**

## **Table of Contents**
1. [Project Overview](#project-overview)  
2. [History](#history)  
   - [Binary Representations](#binary-representations)  
   - [Hash Functions](#hash-functions)  
   - [SHA256 Padding (FIPS 180-4 Standard)](#sha256-padding-fips-180-4-standard)  
   - [Prime Number Computation](#prime-number-computation)  
3. [Features](#features)  
4. [Installation](#installation)  
5. [Deployment](#deployment)  
6. [Expected Outputs and Demonstration](#expected-outputs-and-demonstration)  
7. [Development Difficulties](#development-difficulties)  
8. [Testing](#testing)  
9. [Bibliography](#bibliography)  

---

## **Project Overview**  
This project explores various **computational theory concepts**, including:  
- **Bitwise operations** for efficient data processing.  
- **Hash functions** for data integrity and security.  
- **SHA256 padding** as per cryptographic standards.  
- **Prime number calculations** used in encryption.  

All tasks are implemented in a **Jupyter Notebook (`tasks.ipynb`)**, with explanations and test cases for verification.

---

## **History**  

### **Binary Representations**  
Bitwise operations are essential for low-level computing, cryptography, and data processing. This project implements:  
- **Bit Rotation (ROTL/ROTR)** – Used in hashing and encryption for non-linear transformations.  
- **Conditional Bit Selection (ch(x, y, z))** – Used in cryptographic functions like SHA256.  
- **Majority Function (maj(x, y, z))** – Determines dominant bit values in hashing and voting mechanisms.  

These operations play a critical role in cryptographic algorithms, optimization techniques, and hardware-level processing.

### **Hash Functions**  
Hash functions convert input data into a fixed-length hash value used for:  
- Data integrity verification (e.g., detecting file corruption).  
- Fast lookups (e.g., indexing in databases).  
- Minimizing hash collisions (ensuring different inputs produce different outputs).  

This project implements a hashing function originally written in C, rewritten in Python:
- Uses a multiplicative hash technique (31 * hashval + char).
- Applies modular arithmetic (% 101) to constrain hash values to a defined range.
- Demonstrates the importance of prime numbers in reducing hash collisions.  

This type of hashing is used in string-based hashing algorithms for fast searching and indexing.

### **SHA256 Padding**  
SHA256 is a widely used cryptographic hash function that converts input data into a 256-bit hash value, designed for secure hashing in encryption and authentication:
- Used in digital signatures, secure password hashing, and blockchain technology.  
- **One-way function** – It is computationally infeasible to reverse the hash back to the original message.  
- **Collision-resistant** – No two different inputs should produce the same hash.  

SHA256 processes data in 512-bit message blocks, meaning padding is required** when a message does not fit this size. This is done according to FIPS 180-4 (Secure Hash Standard):
- A 1 bit (0x80) is appended to indicate the message's end.
- Zeros are added until the message length is 448 bits mod 512.
- The original message length is encoded as a 64-bit big-endian integer.  

This ensures SHA256 maintains block integrity and functions securely.

### **Prime Number Computation**  
Prime numbers are critical for encryption algorithms and number theory. This project implements two methods:  
- **Trial Division:** Checks divisibility up to √n, effective but slow.  
- **Sieve of Atkin:** Uses mathematical properties to generate primes efficiently.  

This comparison allows for analyzing performance trade-offs in number theory and cryptographic applications.

---

## **Features**  
This project includes the following completed tasks:  

### **Binary Representations**  
- Implements bitwise operations for 32-bit unsigned integers.  
- Includes bit rotation, bitwise selection (`ch`), and majority voting (`maj`).  
- Used in cryptographic algorithms for secure hashing.  

### **Hash Functions**  
- Converts a C-based hash function into Python.  
- Uses multiplication & modular arithmetic for hashing.  
- Explores why 31 and 101 are chosen for efficiency.  

### **SHA256 Padding**  
- Implements SHA256 message padding according to FIPS 180-4.  
- Appends a 1-bit (`0x80`), zero padding, and message length.  
- Required for secure hashing and cryptographic security.  

### **Prime Number Computation**  
- Computes the first 1,000 prime numbers.  
- Uses Trial Division and Sieve of Atkin for comparison.  
- Essential for cryptographic key generation and secure communications.  

---

## **Installation** 

**Prerequisites**
Ensure the following software is installed:

Python 3.x
Jupyter Notebook

1. **Clone the repository:**  
    - git clone https://github.com/Cpgeragh/computational_theory_assessment.git

2. **Navigate to the project directory:**
    - cd computational_theory_assessment
 
---

## **Deployment**

This project is executed entirely in a Jupyter Notebook.  

**Running the Notebook**

1. **Run all cells in order using Shift + Enter.**

2. **Alternatively execute the notebook via terminal:**
    - jupyter nbconvert --to notebook --execute tasks.ipynb

3. **Each task produces direct output in the notebook.**

---

## **Expected Outputs and Demonstration**

---

## **Development Difficulties**

---

## **Testing**

---

## **Bibliography**

---