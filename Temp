# Appian Expression Rules

## #1 Check Is Null Or Empty

### Rule Inputs:
1. `value` (Any Type)

### Code:
```apex
or(
  a!isNullOrEmpty(ri!value),
  trim(ri!value) = "",
  length(ri!value) = 0
)
