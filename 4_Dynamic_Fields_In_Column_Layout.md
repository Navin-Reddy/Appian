# Display Dynamic Fields In Column Layout

## Interface: 
VU_displayDynamicFieldsInColumnLayout

## Rule Inputs:
1. `fieldComponents` (Any Type)
2. `noOfColumns` (Number (Integer))

## Usage Consideration:
Currently, this method won't support any picker fields.

## Code:
```apex
if(
  or(
    a!isNullOrEmpty(ri!fieldComponents),
    a!isNullOrEmpty(ri!noOfColumns),
    ri!noOfColumns = 0
  ),
  {},
  a!forEach(
    items: enumerate(
      ceiling(
        count(ri!fieldComponents) / ri!noOfColumns
      )
    ),
    expression: a!columnsLayout(
      columns: a!forEach(
        items: index(
          ri!fieldComponents,
          enumerate(ri!noOfColumns) + 1 + (fv!item * ri!noOfColumns),
          null
        ),
        expression: a!columnLayout(contents: fv!item)
      )
    )
  )
)
```
