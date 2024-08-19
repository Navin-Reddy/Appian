# Interview Coding Questions

## #1 Sort the list without native functions

### Rule Inputs:
1. `list` (List of Number (Floating Point))
2. `res` (List of Number (Floating Point))

### Code:
```apex
if(
  a!isNullOrEmpty(ri!list),
  {},
  a!localVariables(
    local!min: min(ri!list),
    local!final: append(ri!res, local!min),
    if(
      length(ri!list) = 1,
      local!final,
      rule!NR_sortWithOutDefaultFunction(
        remove(
          ri!list,
          min(wherecontains(local!min, ri!list))
        ),
        local!final
      )
    )
  )
)
```

### Input:
list: {9, 7, 5, 4, 8, 1, 3, 1}

### Output:
{1, 1, 3, 4, 5, 7, 8, 9}

---

## #2 Return count of letters in the given text

### Code:
```apex
a!localVariables(
  local!text: "navin Reddy",
  local!list: char(code(local!text)),
  a!forEach(
    union(local!list, local!list),
    {
      item: fv!item,
      count: count(wherecontains(fv!item, local!list))
    }
  )
)
```

### Output:
```apex
{
  { item: "n", count: 2 },
  { item: "a", count: 1 },
  { item: "v", count: 1 },
  { item: "i", count: 1 },
  { item: " ", count: 1 },
  { item: "R", count: 1 },
  { item: "e", count: 1 },
  { item: "d", count: 2 },
  { item: "y", count: 1 }
}
```

---

## #3 Reverse the text without reverse function:

### Code:

```apex
a!localVariables(
  local!text: "Navin Reddy",
  local!list: char(code(local!text)),
  joinarray(
    a!forEach(
      local!list,
      local!list[length(local!list) - fv!index + 1]
    ),
    ""
  )
)
```

### Output:
yddeR nivaN
