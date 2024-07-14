### Iterative Approach with Button Save:

```a!localVariables(
  local!array: { 0, 1 },
  local!n: 10,
  a!buttonWidget(
    label: "Click",
    saveInto: a!forEach(
      enumerate(local!n - 2),
      a!save(
        local!array,
        append(
          local!array,
          sum(
            tointeger(
              index(local!array, length(local!array), null),
              index(local!array, length(local!array) - 1, null)
            )
          )
        )
      )
    )
  )
)```

#### Explanation:

- **Purpose:** This snippet demonstrates an iterative approach to generate a Fibonacci-like sequence using a button click in Appian.
- **Variables:**
  - `local!array`: Initial array containing `{ 0, 1 }`.
  - `local!n`: Number of iterations, set to `10`.
- **Functionality:** Upon clicking the button labeled "Click":
  - It iterates `local!n - 2` times to calculate and append Fibonacci-like numbers into `local!array`.
  - Each iteration computes the sum of the last two elements in `local!array` using `append()` and `sum()` functions.

---

### Using Binet's Formula:

```a!localVariables(
  local!n: 10,
  local!phi: (1 + sqrt(5)) / 2,
  local!psi: (1 - sqrt(5)) / 2,
  a!forEach(
    enumerate(local!n),
    round(
      (
        power(local!phi, fv!item) - power(local!psi, fv!item)
      ) / sqrt(5)
    )
  )
)```

#### Explanation:

- **Purpose:** This snippet uses Binet's formula to calculate Fibonacci-like numbers.
- **Variables:**
  - `local!n`: Number of terms to calculate, set to `10`.
  - `local!phi`: Golden ratio `(1 + sqrt(5)) / 2`.
  - `local!psi`: Conjugate of the golden ratio `(1 - sqrt(5)) / 2`.
- **Functionality:** 
  - Iterates over `local!n` terms to compute Fibonacci-like numbers using Binet's formula.
  - The formula `(phi^item - psi^item) / sqrt(5)` calculates each term, rounded to the nearest integer using the `round()` function.

---

### VU_appendAndReturnListForFibbo

#### Rule Input:

1. list (List of Number (Integer))
2. result (List of Number (Integer))

```a!if(
  a!count(ri!list) < 2,
  { 0, 1 },
  a!append(
    ri!list,
    a!sum(
      {
        index(ri!list, a!length(ri!list), null),
        index(ri!list, a!length(ri!list) - 1, null)
      }
    )
  )
)```

### VU_fibbonacciSequence

```a!reduce(
  rule!VU_appendAndReturnListForFibbo(list: _, result: _),
  {},
  a!enumerate(10)
)```

---
