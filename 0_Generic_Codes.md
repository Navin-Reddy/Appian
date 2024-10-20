# Common Expression Rules

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
```

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
  a!isNotNullOrEmpty(ri!docId),
  a!localVariables(
    local!contentDetails: getcontentobjectdetailsbyid(id: ri!docId),
    {
      find(
        "Document",
        extract(local!contentDetails, "Type:", "]")
      ) > 0,
      extract(local!contentDetails, "State: ", ",") = "Active Published"
    }
  )
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

---

## #5 Generate Document Name

### Rule Inputs:
1. `text` (Text)

### Code:
```apex
regexreplaceall(
  "[\\/:*?""<>|%$&\'()\[\]{}#@!+=~`^,;]",
  ri!text & if(
    rule!NBF_COMMON_checkIsNullOrEmpty(ri!text),
    "",
    " "
  ) & text(now(), "yymmddhhmmss"),
  "_"
)
```

---

## #5 Get Document Name (Published & Unpublished)

### Rule Inputs:
1. `documentId` (Number (Integer))

### Code:
```apex
index(
  index(
    index(
      a!fileUploadField(value: ri!documentId),
      "contents",
      null
    ),
    "value",
    null,
    "name",
    null
  )
)
```
