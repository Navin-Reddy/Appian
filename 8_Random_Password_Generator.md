# Random Password Generator

## Description
This script generates a random password using a mix of special characters, alphabetic characters, and hexadecimal values. It ensures a strong and varied password by combining different character types and random values.

## Code

```apex
a!localVariables(
  local!specialCharacters: {
    "!",
    "@",
    "#",
    "$",
    "%",
    "^",
    "]",
    "*",
    "(",
    ")",
    "[",
    "]",
    ";",
    "[",
    ">",
    "?",
    "/",
    "\",
    "|",
    "~"
  },
  local!alphabetCharacters: {
    "A",
    "B",
    "C",
    "D",
    "E",
    "F",
    "G",
    "H",
    "I",
    "J",
    "K",
    "L",
    "M",
    "N",
    "O",
    "P",
    "Q",
    "R",
    "S",
    "T",
    "U",
    "V",
    "W",
    "X",
    "Y",
    "Z"
  },
  joinarray(
    {
      lower(dec2hex(tointeger(rand(2) * 256), 2)),
      local!specialCharacters[mod(rand(1) * 256, 19) + 1],
      local!alphabetCharacters[mod(rand(2) * 256, 25) + 1],
      mod(rand(1) * 256, 100),
      local!specialCharacters[mod(rand(2) * 256, 19) + 1],
      dec2hex(tointeger(rand(1) * 256), 2),
      local!specialCharacters[mod(rand(2) * 256, 19) + 1],
      lower(
        local!alphabetCharacters[mod(rand(2) * 256, 25) + 1]
      ),
      dec2hex(datetext(now(), "SSss"), 1)
    }
  )
)
```
