# Convert Base64 String to Appian Document

## Visual Flow:

```
Process ───►  Integration Call ───► Web API ───►  Integration Object ───►  Process
    |              |                  |                         |               |
    | (Passed Process ID,             |   (Returns the          |               |
    | Folder, Document Name           |   Base64 String)        |               |
    | as Input)                       |                         |               |
    |              |                  |                         |               |
    └──────────────┼──────────────────┼─────────────────────────┼───────────────┘
                   |                  |                         |
                   └──────────────────┼─────────────────────────┘
                                      |
                          (Calls the API, Passes the Base64)
```

### Description:

- **Process:** Initiates the flow with input parameters including the Base64 string, folder, and document name.
  
- **Integration Call:** Executes an integration call to initiate the Web API.
  
- **Web API:** Retrieves the Base64 string from process instance.
  
- **Integration Object:** Converts the retrieved Base64 string into an Appian Document.
  
- **Process:** Concludes the flow after processing the Base64 string into an Appian Document.

---

## Steps:

### #1 Create a Web API Object: VU_base64ToDocument

**Object Name:** VU_base64ToDocument  
**Method:** POST

**Code Explanation:**
- This Web API object accepts a JSON payload containing an Appian Process ID (`ppId`).
- It retrieves the Base64 string from a process using the Process ID and returns it as a JSON response.

**Code:**
```apex
a!httpResponse(
  headers: a!httpHeader(
    name: "content/type",
    value: "application/json"
  ),
  body: a!toJson(
    {
      base64: index(
        index(
          getexternalpvsactivity(
            index(
              a!fromJson(index(http!request, "body", null)),
              "ppId",
              null
            ),
            "body"
          ),
          "pvs",
          null
        ),
        "body",
        null
      )
    }
  )
)
```

---

### #2 Create an Integration Object: VU_convertBase64ToDocument

**Object Name:** VU_convertBase64ToDocument  
**Method:** POST  
**Usage:** Modifies data

**Rule Inputs:**
1. `ppId` (Number (Integer))
2. `docName` (Text)
3. `folder` (Folder)
4. `docExt` (Text)

**Configurations:**
- Convert base64 values to Appian documents: True
- Response Body Location:
  - Name: `concat(a!defaultValue(ri!docName, concat("Document_", ri!ppId)), ".", ri!docExt)`
  - Save Documents In: `ri!folder`

**Code Explanation:**
- This integration object calls the `VU_base64ToDocument` Web API to retrieve the Base64 string.
- It then converts the Base64 string into an Appian Document and specifies where to save it (`folder`) with the specified `docName` and `docExt`.
- The result (`newDocId`) is captured for further processing.

**Code:**
```apex
a!toJson({ ppId: ri!ppId })
```

---

### #3 Build a Process Model: VU Base64 Conversions

**Name:** VU Base64 Conversions

**Process Variables:**
| Name         | Type             | Multiple | Default Value | Parameter | Required | Hidden |
|--------------|------------------|----------|---------------|-----------|----------|--------|
| newDocId     | Document         | No       |               | No        | No       | No     |
| Error        | IntegrationError | No       |               | No        | No       | No     |
| body         | Text             | No       |               | Yes       | No       | No     |
| isBase64ToDoc| Boolean          | No       | False         | Yes       | No       | No     |

**Process Flow:**

```
Start Node ─────────────────────► Is Base64 to Document ──(If `pv!isBase64ToDoc` is TRUE)──► Call Base64 to Doc ───► End Node
                               └──(If none of the above are TRUE)──► End Node
```
                               

**Node 1: Start Node**
- **Node Type:** Start Node

**Node 2: Is Base 64 to Document?**
- **Node Type:** XOR

| Condition                     | Result                    |
|-------------------------------|---------------------------|
| If `pv!isBase64ToDoc`         | go to Call Base64 to Doc  |
| If none of the above are TRUE | go to End Node            |

**Node 3: Call Base64 to Doc**
- **Node Type:** Call Integration

**Inputs:**
| Name         | Type             | Multiple | Value                      | Save Into | Required | Generated | Hidden from designer |
|--------------|------------------|----------|----------------------------|-----------|----------|-----------|----------------------|
| Integration  | Integration      | No       | VU_convertBase64ToDocument |           | Yes      | No        | Yes                  |
| docExt       | Text             | No       |                            |           | No       | Yes       | No                   |
| docName      | Text             | No       |                            |               | No       | Yes       | No                   |
| folder       | Folder           | No       | =cons!NS_TEMP_FOLDER       |           | No       | Yes       | No                   |
| ppId         | Number (Integer) | No       | =pp!id                     |           | No       | Yes       | No                   |

**Outputs:**
| Expression                                                       | Operation                    | Variable |
|------------------------------------------------------------------|------------------------------|----------|
| AC!Error                                                         | is stored as                 | Error    |
| index( index(ac!Result, "body", null), "base64", null )          | is stored as                 | newDocId |

**Node 4: End Node**
- **Node Type:** End Node

---

**Usage Consideration:**
- The maximum document size limit is 75MB.
- To overcome the 5MB limit in Integration requests, the process ID (`ppId`) is used to fetch Base64 data from the Process using Query Process Analytics or the `getexternalpvsactivity` plugin function.
