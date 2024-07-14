
# Execute SQL Query

## #1 Execute the Create Stored Procedure Script:

```sql
DELIMITER $$

CREATE PROCEDURE sp_sqlexec(IN sqlStatement TEXT)
BEGIN
    -- Variable to hold the prepared statement
    SET @sql = sqlStatement;
    
    -- Prepare and execute the dynamic SQL statement
    PREPARE stmt FROM @sql;
    EXECUTE stmt;
    DEALLOCATE PREPARE stmt;
END$$

DELIMITER ;
```

---

## #2 Create an Appian Constant to hold the Stored Procedure Name:
	
### Constant
- `VU_SP_SQL_EXEC`

### Value: 
- `sp_sqlexec`

---

## #3 Create an Expression Rule for Execute SQL Query:

### Rule Inputs:
1. `datasource` (Text)
2. `sqlQuery` (Text)

### Code:
```javascript
/*Max timeout: The maximum timeout for a stored procedure is 600 seconds.*/
/*Max rows per result set: The maximum number of rows per result set is 1000. */
/*Result sets that exceed this threshold will be truncated.*/
a!toJson(
  if(
    and(
      a!isNotNullOrEmpty(ri!datasource),
      a!isNotNullOrEmpty(ri!sqlQuery)
    ),
    a!localVariables(
      local!queryData: a!executeStoredProcedureForQuery(
        dataSource: ri!datasource,
        procedureName: cons!VU_SP_SQL_EXEC,
        inputs: a!storedProcedureInput(name: "sqlStatement", value: ri!sqlQuery)
      ),
      if(
        a!isNullOrEmpty(index(local!queryData, "error", null)),
        index(
          index(local!queryData, "results", null),
          1,
          null
        ),
        cast(
          197,
          {
            Error: index(local!queryData, "error", null)
          }
        )
      )
    ),
    {}
  )
)
```
