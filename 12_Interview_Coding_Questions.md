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

---

## #2 Return count of letters in the given text

### Code:
```apex
a!localVariables(
  local!text: "Navin Reddy",
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
