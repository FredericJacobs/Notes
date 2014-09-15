# Introduction to Lattices

## Formal definition 

A lattice is defined as a set of points L = {a_1 v_1 + … + a_n v_n | a_i integers | v_n linearly independent vectors}. Similar to span of vectors but with integers => Discrete structure. 

A lattice **basis is not unique**. L(B) is a lattice where B is an n*n matrix with columns v_1 … v_n. A lattice is a **discrete** structure.

Spoiler alert: In crypto, we try to hide the shortest vectors of a given lattice.

## Historically 

Interest from Gauss (1801), Hermite (1850) and Minkowski (1896) focused on the Number Theory aspect. 

The more recent/important results came with the publication of the LLL (Lenstra-Lenstra-Lovasz) algorithm in 1982.  

The algorithm has many applications:
- Approximating the shortest vector in a lattice
- Factoring rational polynomials
- Solving integer programs in a fixed dimension
- Finding integer relations

In 1996, Ajtai and Ajtai-Dwork showed the power of lattice-based cryptography BUT the resulting systems were extremely inefficient (slow and keys that were multiple gigabytes long).

It’s only in 2003 and 2005 that significant progress was made to have very efficient constructions that are way more versatile. [MicciancioR03,R05]
Those newer schemes are based on two key lattice problems called Short Integer Solution (SIS) and Learning With Error (LWE).

Another line of work gives extremely efficient contractions from ideal lattices (ring, cyclic, …) -> only kilobytes long keys. 

## Lattice-based cryptology. Why?

### Cryptanalysis 

The first relations between cryptography and lattices came shortly after the publication of the LLL algorithm. It was first used to do some cryptanalysis to break Knapsack-based crypto systems [LagariasOdylyzko85], RSA [Håstad85, Coppersmith01] …

### Cryptography

Lattices were then later considered to design cryptography primitives. The advantages of lattice-based schemes are:
- Thought to be resistant to Quantum Computers (still at least a decade away)
- Although we can not prove that P ≠ NP, we can prove that some lattice problems are at least as hard as NP-hard problems. ~ Provably secure (we don’t have that for RSA!)
- Homomorphic schemes —> Permute vectors of the lattice :o
- Security based on a worst-case problem.
- Based on lattice problems (been around for 2 centuries, established problem, hard to solve)
- Very simple computations (mostly additions) -> FAST and HARDER to screw up implementations 

## Lattices: Equivalent basis

The set of problems used in lattice cryptography rely on the fact that we have multiple bases for the same lattice.

## Provable Security

The security proof relies on showing that the security of lattice reduction problems is at least as hard as some well-known problems in mathematics that have gotten a lot of scrutiny from the math community.

The security proof gives a strong evidence that our cryptographic function has no fundamental flaws. The proof of security gives hints at the choice of parameters.

### Example of a security proof

If I have an algorithm that says

1) Pick p and q, two large primes and N = p*q
2) f(x) = x^2 mod N

If we can compute square roots then we can factor N. Therefore, we know that the factoring of N is only as hard as finding an inversion of that function.
—
This shows that this one way function, f(x) = x^2 mod N is as hard as factoring N. BUT, this security proof doesn’t say much about the security about the system because no constraints are clearly set on picking N.

How do we select eligible primes for p and q? Safe primes?

After RSA came out, people started researching what are good primes to be used.

In 1978, people realized that the largest prime factors of p-1 and q-1 should be large.
In 1981, p+1 and q+1 should have a large prime factor.
In 1982, if the largest prime factor of p-1 and q-1 is p’ and q’, then p’-1 and q’-1 should have large prime factors.
In 1984, if the largest prime factor of p+1 and q+1 is p’ and q’, then p’-1 and q’-1 should have large prime factors.
—> The bottom line, breaking RSA doesn’t mean you can factor means you can do something with a very specific N, but not able to factorize all numbers. This is known as **average-case hardness**. RSA security doesn’t rely on the fact that it is hard to factor all numbers but it’s hard to factor a small fraction of them.

Lattices DON’T SUFFER FROM that, we say that the lattice problem is hard in the **worst-case**. This is a much stronger security guarantee and makes it harder to screw up implementations.

# A Quick Look into Lattices

## When do two bases generate the same lattice?

- We can permute vectors v_i <-> v_j
- We can negate a vector v_i <- -v_i
- We can add an integer multiple of one vector to another, v_i <- v_i + k*v_j for some k ∈ Integers.
—
Succinctly, we can multiply B from the right by any unimodular matrix U (i.e. , an integer matrix of determinant +/- 1). 
**Two bases B1, B2 are equivalent iff B_2 = B_1 U for a unimodular U.**

(Note: the inverse of a unimodular matrix is also an unimodular integer matrix)

## Periodicity in higher dimensions

A **fundamental region** of a lattice, a parallelogram in 2D and parallelepiped in higher dimensions is defined as P(B) = {a_1 b_1 + a_n b_n | all a_i in [0,1)}

Why is this useful to find a find fundamental regions of lattices? If we want to compute the distance from a point to a lattice, we can compute that by calculating: if x=(a_1 b_1 + … + a_n b_n) then x mod P(B) := (a_1 mod 1)b_1 + … + (a_n mod 1)b_n
Conceptually, reducing a point to the modulo of any fundamental parallelepiped will give the distance to the lattice. 
`x mod P(B) = 0` <=>  x belongs to the lattice L(B).

Note: There are other fundamental regions than parallelepipeds that are valid but that are not as useful for crypto. Hexagons are another noticeable one that can have interesting applications.

# Good references


# Research ideas

Backdooring lattice cryptography
Homemorphic stuff


# WHY I’M EXCITED ABOUT LATTICES AS A DEVELOPER

- Safer 
- Probably Resistant to cryptosystems
- FAST 
- WORST-case —> Harder to screw up implementations