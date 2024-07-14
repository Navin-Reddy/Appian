# Appian Functions and Examples

## #1 Copy the test to Clipboard:

### Object Name: VU_copyToClipboard

### Rule Inputs:
1. `textToCopy` (Text)

### Code: 
```apex
a!richTextDisplayField(
  labelPosition: "COLLAPSED",
  value: a!richTextItem(
    text: "Click here to copy",
    link: 'type!{http://www.appian.com/ae/types/2009}CopyToClipboardLink'(textToCopy: ri!textToCopy)
  )
)
```

---

## #2 Try Function:

The `try()` function can allow you to handle errors within Appian.

### Code:
```apex
try(
  concat(),
  fn!lastError().details
)
```

### Output:
Expression evaluation error at function 'concat': Too few parameters for function; expected at least 1 parameter, but found 0 parameters.

---

## #3 Eval Function:

The `eval()` function converts text to SAIL code and evaluates it, similar to JavaScript's `eval()`.

### Code:
```apex
eval("len(""Navin"")")
```

### Output:
5

---

## #4 Enum Function:

The `enum()` function is similar to `enumerate()`.

### Code:
```apex
enum(5)
```

### Output:
{1, 2, 3, 4, 5}

---

## #5 Sort Function:

### Code 1:
```apex
sort({4,3,2,1})
```

### Output:
{1, 2, 3, 4}

### Code 2:
```apex
sort({"Z", "A", "D"})
```

### Output:
{"A", "D", "Z"}
```
