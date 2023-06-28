<!-- loiodafece708a524a7b9cabc13fe95406c1 -->

# ALTER SYSTEM REMOVE SQL PLAN CACHE Statement \(System Management\)

Removes the specified entries from the SQL plan cache.



<a name="loiodafece708a524a7b9cabc13fe95406c1__sql_alter_system_clear_sql_plan_cache_1sql_alter_system_clear_sql_plan_cache_syntax"/>

## Syntax

```
ALTER SYSTEM REMOVE SQL PLAN CACHE { ENTRY <plan_id> | <where_clause> }
```



<a name="loiodafece708a524a7b9cabc13fe95406c1__sql_truncate_table_1sql_truncate_table_syntax_elements"/>

## Syntax Elements


<dl>
<dt><b>

*<plan\_id\>*

</b></dt>
<dd>

Specifies a plan cache entry ID to remove.



</dd><dt><b>

*<where\_clause\>*

</b></dt>
<dd>

See the SELECT statement.



</dd>
</dl>



<a name="loiodafece708a524a7b9cabc13fe95406c1__sql_alter_system_clear_sql_plan_cache_1sql_alter_system_clear_sql_plan_cache_description"/>

## Description

The SQL plan cache stores plans generated by previous SQL statement executions. The SAP HANA database uses the plan cache to speed up query execution if the same SQL statement is executed multiple times. The plan cache also collects some statistics regarding plan preparation and execution.

If the specified plan ID does not exist, an error is returned.

Plan cache entry information is available in the M\_SQL\_PLAN\_CACHE monitoring view.



<a name="loiodafece708a524a7b9cabc13fe95406c1__section_acv_mrv_xdb"/>

## Permissions

You must have the OPTIMIZER ADMIN system privilege.



<a name="loiodafece708a524a7b9cabc13fe95406c1__sql_alter_system_clear_sql_plan_cache_1sql_alter_system_clear_sql_plan_cache_examples"/>

## Example

Removes the plan cache entry ID 2374637 from the SQL plan cache:

```
ALTER SYSTEM REMOVE SQL PLAN CACHE ENTRY 2374637;
```

Removes plan cache entries with an execution count of less than five:

```
ALTER SYSTEM REMOVE SQL PLAN CACHE WHERE EXECUTION_COUNT < 5;
```

Removes plan cache entries that are invalidated:

```
ALTER SYSTEM REMOVE SQL PLAN CACHE WHERE IS_VALID = 'FALSE';
```

Removes plan cache entries that access tables with names containing "AAA":

```
ALTER SYSTEM REMOVE SQL PLAN CACHE WHERE ACCESSED_TABLE_NAMES LIKE '%AAA%';
```

**Related Information**  


[ALTER SYSTEM CLEAR SQL PLAN CACHE Statement \(System Management\)](alter-system-clear-sql-plan-cache-statement-system-management-20d107c.md "Removes all of the SQL plans that are not currently being executed from the SAP HANA database plan cache.")

[SELECT Statement \(Data Manipulation\)](select-statement-data-manipulation-20fcf24.md "Queries data from the database.")

[M\_SQL\_PLAN\_CACHE System View](../../020-System-Views-Reference/022-Monitoring-Views/m-sql-plan-cache-system-view-20c57b8.md "Provides statistics for an individual execution plan.")
