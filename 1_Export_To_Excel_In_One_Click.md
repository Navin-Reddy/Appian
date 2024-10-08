
# Export to Excel in Single Click

## #1 Create a Web API (VU Generate Excel) for Generating the Excel Sheet using a!exportDataStoreEntityToExcel()

### Method: POST
### Query Parameters: 
- `jsonData`: Accepts JSON Payload with Match ID and other required details (Filters, Selection).

### Code:
```apex
a!localVariables(
  local!data: a!fromJson(http!request.queryParameters.jsonData),
  a!match(
    value: cast(1, index(local!data, "matchId", null)),
    equals: 1,
    then: a!exportDataStoreEntityToExcel(
      entity: cons!NS_DSE_TEST_TABLE,
      documentName: "Report " & text(now(), "dd-mm-yyyy hh_mm_ss"),
      startingCell: "A1",
      saveInFolder: cons!VU_TEMP_FOLDER,
      filters: a!queryFilter(
        field: "id",
        operator: "<",
        value: index(
          index(local!data, "filters", null),
          "id",
          null
        )
      ),
      sheetNumber: 1,
      onSuccess: a!httpResponse(
        statusCode: 200,
        headers: a!httpHeader(
          name: "Content-Type",
          value: "application/json"
        ),
        body: tointeger(fv!newDocument)
      ),
      onError: a!httpResponse(
        statusCode: 500,
        body: a!toJson(
          {
            error: "System encountered an error while generating the document. Please contact the administrator."
          }
        )
      )
    ),
    equals: 2,
    then: a!exportDataStoreEntityToExcel(
      entity: cons!BMA_PERSON_DSE,
      documentName: "Report " & text(now(), "dd-mm-yyyy hh_mm_ss"),
      startingCell: "A1",
      saveInFolder: cons!VU_TEMP_FOLDER,
      sheetNumber: 1,
      onSuccess: a!httpResponse(
        statusCode: 200,
        headers: a!httpHeader(
          name: "Content-Type",
          value: "application/json"
        ),
        body: tointeger(fv!newDocument)
      ),
      onError: a!httpResponse(
        statusCode: 500,
        body: a!toJson(
          {
            error: "System encountered an error while generating the document. Please contact the administrator."
          }
        )
      )
    ),
    equals: 3,
    then: a!exportDataStoreEntityToExcel(
      entity: cons!BMA_SALES_PERSON_DSE,
      documentName: "Report " & text(now(), "dd-mm-yyyy hh_mm_ss"),
      startingCell: "A1",
      saveInFolder: cons!VU_TEMP_FOLDER,
      sheetNumber: 1,
      onSuccess: a!httpResponse(
        statusCode: 200,
        headers: a!httpHeader(
          name: "Content-Type",
          value: "application/json"
        ),
        body: tointeger(fv!newDocument)
      ),
      onError: a!httpResponse(
        statusCode: 500,
        body: a!toJson(
          {
            error: "System encountered an error while generating the document. Please contact the administrator."
          }
        )
      )
    ),
    default: a!httpResponse(
      statusCode: 500,
      body: a!toJson(
        {
          error: "Invalid match ID. Please contact the administrator."
        }
      )
    )
  )
)
```

---

## #2 Create a Connected System (VU Local API)

### Base URL: 
- `https://<Environment URL>/suite/webapi/vu-generate-excel`
### Authentication: 
- Use the appropriate authentication method as required by your environment.

---

## #3 Create an Integration Object (VU_getGeneratedExcelDocument) to call the Generate Excel Web API using Connected System 

### Method: POST
### Content Type: JSON (application/JSON)
### Query Parameters: 
- `jsonData` (Configured to use `ri!jsonData`)
### Usage: 
- Queries data
### Rule Inputs: 
- `jsonData` - Text

---

## #4 Create a Web API (VU Export to Excel) for fetching the Excel Sheet Document using Integration (#3) Call

### Method: GET
### Query Parameters: 
- `jsonData` (Accepts JSON Payload with Match ID and other required details (Filters, Selection)).

### Code:
```apex
a!localVariables(
  local!intResult: rule!VU_getGeneratedExcelDocument(
    jsonData: http!request.queryParameters.jsonData
  ),
  local!document: tointeger(
    index(
      index(local!intResult, "result", null),
      "body",
      null
    )
  ),
  if(
    a!isNullOrEmpty(local!document),
    a!httpResponse(
      statusCode: 404,
      body: "404 Not Found",
      headers: {}
    ),
    a!httpResponse(
      headers: if(
        a!isNotNullOrEmpty(local!document),
        a!httpHeader(
          name: "Content-Disposition",
          value: concat(
            "attachment; filename=""",
            document(local!document, "name"),
            ".",
            document(local!document, "extension"),
            """"
          )
        ),
        {}
      ),
      body: todocument(local!document)
    )
  )
)
```

---

## #5 Create a generic Expression Rule (VU_generateExportToExcelDocumentLink) for generating the Web API URL with the JSON payload data

### Rule Inputs:
1. `label` (Text)
2. `jsonData` (Text)
3. `showWhen` (Boolean)
4. `openLinkIn` (Text)

### Code:
```apex
a!safeLink(
  ri!label,
  urlwithparameters(
    "https://<Environment URL>/suite/webapi/export-to-excel",
    "jsonData",
    ri!jsonData
  ),
  ri!showWhen,
  ri!openLinkIn
)
```
