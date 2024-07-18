
# HTML Table Construction

### Rule Inputs:
1. columnHeaders (List of Text String)
2. column1 (List of Text String)
3. column2 (List of Text String)
4. column3 (List of Text String)
5. column4 (List of Text String)
6. column5 (List of Text String)
7. column6 (List of Text String)
8. column7 (List of Text String)
9. column8 (List of Text String)
10. column9 (List of Text String)
11. column10 (List of Text String)
12. headerColorHex (Text)
13. baseBkroundHex (Text)
14. stripedBkroundHex (Text)

### Code:
```apex 
if(
  a!isNullOrEmpty(ri!columnHeaders),
  "",
  a!localVariables(
    local!noOfColumnsAllowed: 10,
    local!headerColorHex: if(
      a!isNullOrEmpty(ri!headerColorHex),
      "#b2d1e0",
      ri!headerColorHex
    ),
    local!baseBkroundHex: if(
      a!isNullOrEmpty(ri!baseBkroundHex),
      "#ffffff",
      ri!baseBkroundHex
    ),
    local!stripedBkroundHex: if(
      a!isNullOrEmpty(ri!stripedBkroundHex),
      "#f0f7ff",
      ri!stripedBkroundHex
    ),
    local!maxColumnHeaders: max(
      {
        count(ri!column1),
        count(ri!column2),
        count(ri!column3),
        count(ri!column4),
        count(ri!column5),
        count(ri!column6),
        count(ri!column7),
        count(ri!column8),
        count(ri!column9),
        count(ri!column10)
      }
    ),
    local!maxColumns: if(
      count(ri!columnHeaders) < local!noOfColumnsAllowed,
      count(ri!columnHeaders),
      local!noOfColumnsAllowed
    ),
    local!columnValues: {
      column1: ri!column1,
      column2: ri!column2,
      column3: ri!column3,
      column4: ri!column4,
      column5: ri!column5,
      column6: ri!column6,
      column7: ri!column7,
      column8: ri!column8,
      column9: ri!column9,
      column10: ri!column10
    },
    concat(
      "<table width='100%' cellspacing='0' cellpadding='4' style='margin:0px;padding:4px;border:1px solid #ebebeb;font-size:12px; font-family:arial'>
<tr style='background-color:",
      local!headerColorHex,
      ";font-weight:bold'>",
      joinarray(
        a!forEach(
          items: ri!columnHeaders,
          expression: concat("<td>", fv!item, "</td>")
        ),
        ""
      ),
      "</tr>",
      joinarray(
        a!forEach(
          items: enumerate(local!maxColumnHeaders),
          expression: a!localVariables(
            local!currentIndex: fv!index,
            concat(
              "<tr",
              if(
                mod(tointeger(local!currentIndex), 2) = 0,
                {
                  " style='background-color:",
                  local!stripedBkroundHex,
                  "'>"
                },
                {
                  " style='background-color:",
                  local!baseBkroundHex,
                  "'>"
                }
              ),
              a!forEach(
                items: enumerate(local!maxColumns),
                expression: a!localVariables(
                  local!item: index(
                    local!columnValues,
                    "column" & fv!index,
                    {}
                  ),
                  concat(
                    "<td>",
                    index(local!item, local!currentIndex, ""),
                    "</td>"
                  )
                )
              ),
              "</tr>"
            )
          )
        )
      ),
      "</table>"
    )
  )
)
```
