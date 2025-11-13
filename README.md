# Ultimate Cheat Sheet: Numerical Methods (Lectures 1–3)

> **Includes: NumPy Guide, IEEE754, Big-O, Python Labs**

---

## What Are Numerical Methods?

| Question | Answer |
|----------|--------|
| **Definition** | Algorithms to **approximate** solutions when **exact (analytical) solutions** are impossible. |
| **Why Needed?** | Engineering/science: PDEs, nonlinear systems, large-scale simulations (FEA, CFD). |
| **Purpose** | Simulate, optimize, predict real-world behavior on computers. |
| **Examples** | Root finding, integration, solving `Ax=b`, optimization. |

---

## What is NumPy? How It Works

| Feature | Explanation |
|---------|-------------|
| **NumPy** | **Numerical Python** — fast arrays, math, linear algebra |
| **Core** | `np.array` — N-D array (vector, matrix, tensor) |
| **Speed** | 10–100x faster than lists (C/Fortran backend) |
| **Vectorized** | `a + b` → element-wise, no loops |
| **linalg** | `solve`, `inv`, `det`, `norm`, `eig`, etc. |

---

## Summary Table of NumPy Functions Used

| Function | Purpose |
|----------|---------|
| `np.array()` | Create array |
| `np.dot(a,b)` | Dot product / matrix mult |
| `np.cross(a,b)` | 3D cross product |
| `np.linalg.norm(v, ord=2)` | L2 norm (L1, L∞) |
| `np.max(arr)` | Max value |
| `np.abs(arr)` | Absolute value |
| `np.append(arr, values)` | Append |
| `np.allclose(a,b)` | Approximate equality |
| `np.eye(n)` | Identity matrix |
| `np.linalg.det(A)` | Determinant |
| `np.linalg.inv(A)` | Inverse |
| `np.linalg.pinv(A)` | Pseudoinverse |
| `np.linalg.cond(A)` | Condition number |
| `np.linalg.matrix_rank(A)` | Rank |
| `np.concatenate()` | Join arrays |
| `np.zeros()` | Zeros array |
| `np.copy()` | Deep copy |
| `np.arccos(x)` | Inverse cosine |
| `np.linalg` | Linear algebra module |

---

# LECTURE 1 — Complexity and Big-O Notation

## A. Concept & Definition Questions

1. **What are Numerical Methods, and why are they needed?**  
   → Algorithms to approximate solutions when exact ones are impossible. Needed in engineering (FEA, CFD) and science (simulations, optimization).

2. **Distinguish between analytical and numerical solutions, with example.**  
   - **Analytical**: Exact, closed-form.  
     `x² = 4 → x = ±2`  
   - **Numerical**: Approximate, iterative.  
     Newton-Raphson for `x³ - x - 1 = 0`

3. **What is meant by a numerical algorithm?**  
   → Step-by-step procedure to compute an approximate solution.

4. **Why are results approximate?**  
   → Finite precision, round-off, truncation, convergence tolerance.

5. **What is meant by computational complexity?**  
   → Resources (time/space) required as input size `n → ∞`.

---

## B. Big-O Notation & Computation

6. **Define Big-O and its importance.**  
   → `f(n) = O(g(n))` if `f(n) ≤ c·g(n)` for large `n`.  
   → Predicts scalability, compares algorithms.

7. **How does Big-O relate to execution time?**  
   → Estimates operations as function of input size `n`.

8. **If 3n² + 4n + 2 operations → Big-O?**  
   → **O(n²)** (dominant term).

9. **State Big-O for each:**  
   a) Loop `n` times → **O(n)**  
   b) Nested loops → **O(n²)**  
   c) Binary search → **O(log n)**  
   d) Matrix multiplication → **O(n³)**

10. **Why only highest order term?**  
    → Lower terms negligible as `n → ∞`.

---

## C. Application & Analysis

11. **Count operations in nested loop → Big-O?**  
    ```python
    for i in range(n):
        for j in range(n):
            sum += 1  # n² ops → O(n²)
    ```

12. **Compare O(n log n) vs O(n²). Which is better for large n?**  
    → **O(n log n)** is better (e.g., `n=10⁶`: 20M vs 1T ops).

13. **Why does efficiency matter in numerical methods?**  
    → Large systems (`n = 10⁶+`) → poor complexity = infeasible.

14. **Real-world example?**  
    → FEA in structural engineering: `O(n³)` solve on 3D mesh → supercomputers.

15. **n doubles in O(n³) → performance?**  
    → Time ×8 (`(2n)³ = 8n³`).

---

## D. Conceptual/Reasoning

16. **How does Big-O compare algorithms?**  
    → Growth rate determines which scales better.

17. **Why prefer O(n log n) sorting?**  
    → Faster for large data (quicksort vs bubble sort).

18. **Trade-off: accuracy vs time?**  
    → More iterations → better accuracy, higher cost.

19. **Why different times for same problem?**  
    → Different `O()`, constants, or hardware use.

20. **Link between optimization and numerical methods?**  
    → Gradient descent, least squares → numerical solvers.

---

# LECTURE 2 — Representation of Numbers

## A. Base Systems & Conversion

1. **Define decimal and binary systems.**  
   - **Decimal**: Base-10, digits 0–9  
   - **Binary**: Base-2, digits 0–1

2. **Digits in base-3?**  
   → 0, 1, 2

3. **Convert:**  
   a) `11₁₀ → 1011₂`  
   b) `37₁₀ → 100101₂`  
   c) `121₃ → 1×9 + 2×3 + 1 = 16₁₀`

4. **49.84₁₀ in expanded form?**  
   → `4×10¹ + 9×10⁰ + 8×10⁻¹ + 4×10⁻²`

5. **Why binary in computers?**  
   → Two states (on/off) → reliable hardware.

---

## B. Binary Operations & Bit Concepts

6. **Basic logical operations in binary?**  
   → AND, OR, NOT, XOR

7. **What is a 32-bit computer?**  
   → Processes 32-bit integers/addresses.

8. **How many numbers in 32-bit?**  
   → `2³² = 4,294,967,296` (0 to 2³²−1 unsigned)

9. **Number exceeds max?**  
   → **Overflow** → wraps or error.

10. **One advantage and limitation of binary?**  
    → **Adv**: Fast logic. **Lim**: Can't represent all decimals exactly.

---

## C. Floating Point Numbers (IEEE754)

11. **Why binary insufficient for engineering?**  
    → Can't represent `0.1`, `π` exactly.

12. **What is a floating-point number? Why useful?**  
    → `± mantissa × base^exponent`. Handles huge/small numbers.

13. **Three components in IEEE754?**  
    → **Sign**, **Exponent (biased)**, **Mantissa**

14. **64-bit (double) bits?**  
    → Sign: 1, Exponent: 11, Mantissa: 52

15. **General formula?**  
    → `(-1)^s × (1 + m/2⁵²) × 2^(e − 1023)`

16. **Single vs double precision?**  
    → Single: 32-bit (~7 digits). Double: 64-bit (~15 digits)

17. **15.0 in IEEE754 double (conceptual)?**  
    - Sign: `0`  
    - Exponent: `1026` (3 + 1023) → `10000000010₂`  
    - Mantissa: `111000...` (1.111 × 2³ = 15)

18. **Define "gap" in floating-point?**  
    → Smallest difference between representable numbers.

19. **Why gap increases for larger numbers?**  
    → Fixed mantissa bits → larger steps at higher exponents.

20. **Add 2 to max float in Python?**  
    → `inf` (overflow)

---

## D. Round-off Errors

21. **Define round-off error.**  
    → Difference between exact and stored value.

22. **Two examples?**  
    → `0.1`, `1/3` (infinite binary)

23. **Accumulation of round-off error? Why?**  
    → Errors build up in loops/summations.

24. **Why (1/3 + 1/3 + 1/3) ≠ 1?**  
    → `1/3 ≈ 0.333...` (truncated) → sum ≈ `0.999...`

25. **Python code to show accumulation?**  
    ```python
    s = 0.0
    for _ in range(1000000): s += 0.1
    print(s)  # 100000.00000135526 ≠ 100000.0
    ```

26. **How to minimize round-off?**  
    → Higher precision, Kahan summation, avoid close subtraction.

27. **Truncation vs round-off?**  
    → **Truncation**: Cut series (Taylor). **Round-off**: Finite representation.

28. **Why critical in simulations?**  
    → Small errors → instability (chaos, divergence).

---

## E. Summary/Reasoning

29. **Compare binary, decimal, floating-point:**  
    | Type | Exact? | Range | Precision |
    |------|--------|-------|-----------|
    | Binary | Yes (int) | Limited | Full |
    | Decimal | Human | — | — |
    | Float | No | Huge | Limited |

30. **How IEEE754 balances range/precision?**  
    → More bits to exponent → range; to mantissa → precision.

31. **Significance of "MIND THE GAP"?**  
    → Gaps cause `0.1 + 0.2 ≠ 0.3` → use tolerances.

32. **Why Python float fails simple decimals?**  
    → `0.1 = 0.0001100110...₂` → infinite → approximated.

---

# LECTURE 3 — Linear Algebra & Systems

## A. Vector Concepts

1. **Define vector + example in ℝ³.**  
   → Ordered tuple. e.g., `<1, 2, 3> ∈ ℝ³`

2. **Dot product? What does it represent?**  
   → `a·b = Σ aᵢbᵢ` → projection, angle (cos θ)

3. **Cross product? When computable?**  
   → 3D only, perpendicular, `|a×b| = area`

4. **L₂ norm of (3,4)?**  
   → `√(9+16) = 5`

5. **Dot product = 0?**  
   → **Orthogonal** (90°)

6. **Define L₁, L₂, L∞ norms + significance.**  
   - L₁: `|x|+|y|` (Manhattan)  
   - L₂: Euclidean  
   - L∞: `max(|x|,|y|)` (Chebyshev)

---

## B. Linear Independence & Combination

7. **Define linear combination.**  
   → `x = αv + βw`

8. **Linearly independent?**  
   → Only trivial combo gives zero.

9. **Test using determinant?**  
   → `det([v w]) ≠ 0`

10. **If det(A) = 0?**  
    → Columns **dependent** → singular

11. **Example: x = αv + βw**  
    → `x = 2<1,0> + 3<0,1> = <2,3>`

12. **How is Ax=b a linear combo?**  
    → `b` = linear combo of columns of `A` with weights `x`.

---

## C. Matrices & Determinants

13. **Define matrix. Row vs column vector?**  
    → 2D array. Row: 1×n, Column: n×1

14. **Square matrix?**  
    → `n×n`

15. **Determinant? Use?**  
    → Scalar. `det ≠ 0 → invertible`

16. **Identity matrix? Property?**  
    → `I`, diagonal 1s. `A·I = A`

17. **Matrix inverse? A·A⁻¹ = I means?**  
    → `A⁻¹` "undoes" `A`

18. **Singular vs nonsingular?**  
    → Singular: no inverse. Nonsingular: has inverse.

19. **Condition number? Large value?**  
    → `κ(A) = ‖A‖·‖A⁻¹‖`. Large → **ill-conditioned**

20. **Rank of matrix?**  
    → Max number of independent rows/columns.

---

## D. Solving Systems of Linear Equations

21. **Three outcomes of Ax=b?**  
    → Unique, infinite, none.

22. **Gauss Elimination?**  
    → Row reduce to upper triangular → back-substitution.

23. **Gauss vs Gauss-Jordan?**  
    → Gauss: Upper triangular. G-J: Reduced row echelon.

24. **LU decomposition? Advantages?**  
    → `A = L·U`. Reuse for multiple `b`.

25. **LU process?**  
    → `Ly = b` (forward), `Ux = y` (back).

26. **Iterative vs direct methods?**  
    → Iterative: guess + refine. Direct: exact in finite steps.

27. **Gauss-Seidel method?**  
    → Update immediately:  
    `xᵢ⁽ᵏ⁺¹⁾ = (bᵢ - Σ_{j<i} aᵢⱼxⱼ⁽ᵏ⁺¹⁾ - Σ_{j>i} aᵢⱼxⱼ⁽ᵏ⁾)/aᵢᵢ`

28. **Convergence condition?**  
    → Spectral radius <1 or **diagonally dominant**

29. **Diagonally dominant?**  
    → `|aᵢᵢ| ≥ Σ_{j≠i} |aᵢⱼ|` per row.

30. **If not dominant?**  
    → May **diverge**

---

## E. Higher Thinking / Application

31. **Given 3×3 matrix → singular? Inverse?**  
    → Compute `det`. If ≠0 → inverse via `np.linalg.inv()`.

32. **det([[1,2],[3,4]])? Implication?**  
    → `1·4 - 2·3 = -2 ≠ 0 → invertible`

33. **Gauss vs LU efficiency?**  
    → Gauss: O(n³). LU: O(n³) factor + O(n²) per `b` → better for multiple.

34. **Round-off in Ax=b?**  
    → Amplified in ill-conditioned systems.

35. **Why ill-conditioned problematic?**  
    → Tiny input change → huge output error.

36. **Benefits of NumPy linalg?**  
    → Optimized, stable, pivoting, fast BLAS.

37. **Moore–Penrose pseudo-inverse? When?**  
    → `A⁺` for non-square/singular → least squares.

38. **Why avoid matrix inversion?**  
    → O(n³) + unstable. Use `solve()`.

39. **Rank of [A\|b] → solutions?**  
    - `rank(A) = rank([A\|b])` → consistent  
    - `rank < n` → infinite

40. **How iterative methods improve accuracy?**  
    → Refine via residual: `r = b - Ax`, update `x`.

---

## Python Labs (NumPy)

### 1. Decimal to Binary

```python
def dec_to_bin(n):
    return bin(n)[2:] if n >= 0 else '-' + bin(-n)[2:]

print(dec_to_bin(11))  # '1011'
```

### 2. IEEE754 Gap

```python
import numpy as np
print(np.spacing(1.0))  # ~2.22e-16
```

### 3. Solve Ax=b

```python
A = np.array([[3, 1], [1, 2]])
b = np.array([9, 8])
x = np.linalg.solve(A, b)
print(x)
```

### 4. LU Decomposition

```python
from scipy.linalg import lu

P, L, U = lu(A)
print(np.allclose(P @ L @ U, A))  # True
```

### 5. Gauss-Seidel

```python
def gauss_seidel(A, b, tol=1e-6, max_iter=100):
    x = np.zeros_like(b, dtype=float)
    for _ in range(max_iter):
        x_new = x.copy()
        for i in range(len(b)):
            s1 = sum(A[i][j] * x_new[j] for j in range(i))
            s2 = sum(A[i][j] * x[j] for j in range(i+1, len(b)))
            x_new[i] = (b[i] - s1 - s2) / A[i][i]
        if np.allclose(x, x_new, atol=tol):
            return x_new
        x = x_new
    return x
```

### 6. Det & Inverse

```python
A = np.random.rand(3, 3)
det = np.linalg.det(A)
if abs(det) > 1e-10:
    inv = np.linalg.inv(A)
```

---

