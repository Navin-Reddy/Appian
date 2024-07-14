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


## #2 Sort the given array based on Data Type

### Rule Inputs:
1. `array` (Any Type)
2. `dataType` (Text)
3. `isDesc` (Boolean)

### Code:
```apex
index(
  index(
    todatasubset(
      arrayToPage: a!forEach(
        ri!array,
        {
          value: if(
            ri!dataType = "Integer",
            tointeger(fv!item),
            if(
              ri!dataType = "Decimal",
              todecimal(fv!item),
              tostring(fv!item)
            )
          )
        }
      ),
      pagingConfiguration: a!pagingInfo(
        1,
        -1,
        a!sortInfo(
          field: "value",
          ascending: ri!isDesc <> true
        )
      )
    ),
    "data",
    null
  ),
  "value",
  null
)
```

---

## #3 Check whether Appian Document ID exists

### Rule Inputs:
1. `documentId` (Number (Integer))

### Code:
```apex
and(
  a!isNotNullOrEmpty(ri!documentId),
  find(
    "Document",
    extract(
      getcontentobjectdetailsbyid(id: ri!documentId),
      "Type:",
      "]"
    )
  ) > 0
)
```

---

## #4 Get the Site URL

### Rule Inputs:
1. `siteParam` (Text)

### Code:
```apex
concat(
  regexfirstmatch("^.+?/suite/", a!urlfortask(0)),
  ri!siteParam
)
```
