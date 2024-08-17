# Expression Rules Interview Questions 

1. Write an expression rule which takes 2 input arrays and concatenates each element of both arrays by index.

   **Input:**
   Array 1 - A, B, C, D, E, F
   Array 2 - P, Q, R, S, T, U

   **Output:**
   A-P
   B-Q
   C-R
   D-S
   E-T
   F-U

   **Code:**
   ```apex
   a!localVariables(
     local!arr1: { "A", "B", "C", "D", "E", "F" },
     local!arr2: { "P", "Q", "R", "S", "T", "U" },
     a!forEach(
       merge(local!arr1, local!arr2),
       index(fv!item, 1, null) & "-" & index(fv!item, 2, null)
     )
   )
   ```

2. Write an expression rule to print the below output with the two input arrays.

   **Input:**
   Array 1 - {1, 2, 3, 4, 5}
   Array 2 - {A, B, C, D, E}

   **Output:**
   A5, A4, A3, A2, A1, B1, B2, B3, B4, B5, C5, C4, C3, C2, C1, D1, D2, D3, D4, D5, E5, E4, E3, E2, E1

   **Code:**
   ```apex
   a!localVariables(
     local!arr1: { 1, 2, 3, 4, 5 },
     local!arr2: { "A", "B", "C", "D", "E" },
     a!forEach(
       local!arr2,
       a!localVariables(
         local!item: fv!item,
         local!index: fv!index,
         a!forEach(
           if(
             mod(local!index, 2) = 0,
             local!arr1,
             reverse(local!arr1)
           ),
           local!item & fv!item
         )
       )
     )
   )
   ```

3. Write an expression rule to print all the prime numbers between a given range.

   **Code:**
   ```apex
   a!localVariables(
     local!start: 1,
     local!end: 10,
     a!forEach(
       enumerate(local!end - local!start) + local!start,
       if(
         sum(
           mod(fv!item, enumerate(sqrt(fv!item)) + 1) = 0
         ) <= 1,
         fv!item,
         {}
       )
     )
   )
   ```

   **Output:**
   {1, 2, 3, 5, 7}

4. Write an expression rule to print the below pattern for any given input N.

   **Code:**
   a!localVariables(
     local!n: 5,
     a!forEach(
       enumerate(local!n),
       joinarray(repeat(local!n, " * "), "")
     )
   )

   **Output:**
   ```apex
    *  *  *  *  * 
    *  *  *  *  * 
    *  *  *  *  * 
    *  *  *  *  * 
    *  *  *  *  * 
	```

5. Write an expression rule to print the below pattern for any given input N.

   **Code:**
   a!localVariables(
     local!n: 5,
     a!forEach(
       enumerate(local!n),
       joinarray(repeat(local!n - fv!index + 1, " * "), "")
     )
   )

   **Output:**
   ``apex
    *  *  *  *  * 
    *  *  *  * 
    *  *  *   
    *  *  
    * 
	```

6. Write an expression rule to print the below pattern for any given input N.

   **Code:**
   ```apex
   a!localVariables(
     local!n: 5,
     a!forEach(
       enumerate(local!n),
       joinarray(repeat(fv!index, " * "), "")
     )
   )
   ```

   **Output:**
    * 
    *  *  
    *  *  *  
    *  *  *  *  
    *  *  *  *  * 

7. How to find the power of a number (x to the power of y) without using any Appian function like power()?

   **Code:**
   ```apex
   a!localVariables(
     local!power: 5,
     local!base: 2,
     local!result: repeat(local!base, local!power),
     product(local!result)
   )
   ```

   **Output:**
   25

8. Write an expression rule to print all the numbers between a given range but with different conditions:
   - Condition 1: If the number is divisible by 3, then print "Divisible by 3" instead of that number.
   - Condition 2: If the number is divisible by 5, then print "Divisible by 5" instead of that number.
   - Condition 3: If the number is divisible by both 3 and 5, then print "Divisible by 3 & 5".

   **Code:**
   ```apex
   a!localVariables(
     local!n: 15,
     a!forEach(
       enumerate(local!n) + 1,
       if(
         and(mod(fv!item, { 3, 5 }) = 0),
         "Divisible by 3 & 5",
         if(
           mod(fv!item, { 3 }) = 0,
           "Divisible by 3",
           if(
             mod(fv!item, { 5 }) = 0,
             "Divisible by 5",
             fv!item
           )
         )
       )
     )
   )
   ```


   **Output:**
   {1, 2, "Divisible by 3", 4, "Divisible by 5", "Divisible by 3", 7, 8, "Divisible by 3", "Divisible by 5", 11, "Divisible by 3", 13, 14, "Divisible by 3 & 5"}
