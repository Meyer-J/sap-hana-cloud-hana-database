<!-- loio5873a56cd8dc4ef19023c428bf0017e2 -->

# READ\_DEPLOYED

Read the specified deployed files or folders from an HDI container



The SAP HDI Container API includes the `READ_DEPLOYED` command, which enables you to read specific files or folders from the **deployed** file system of an HDI container.



<a name="loio5873a56cd8dc4ef19023c428bf0017e2__section_ylt_tjw_f2b"/>

## Signature

> ### Sample Code:  
> ```sql
> READ_DEPLOYED
>  ( 
>   IN   PATHS        _SYS_DI.TT_FILESFOLDERS, 
>   IN   PARAMETERS   _SYS_DI.TT_PARAMETERS, 
>   OUT  RETURN_CODE  INT, 
>   OUT  REQUEST_ID   BIGINT, 
>   OUT  MESSAGES     _SYS_DI.TT_MESSAGES,
>   OUT  RESULT       _SYS_DI.TT_FILESFOLDERS_METADATA_CONTENT
>  ) 
> ```



<a name="loio5873a56cd8dc4ef19023c428bf0017e2__section_gg2_zfw_f2b"/>

## Parameters

The following parameters can be used with `IN` and `OUT` parameters in the `READ_DEPLOYED` command:



### PATHS \[IN\]

Specifies a list of **deployed** files or folders to read:

**\_SYS\_DI.TT\_FILESFOLDERS**


<table>
<tr>
<th valign="top">

Name



</th>
<th valign="top">

Data Type



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

PATH



</td>
<td valign="top">

NVARCHAR\(511\)



</td>
<td valign="top">

A single path is either a fully qualified path to a **deployed** file \(for example, `/path/to/a/file.txt`'\), or a fully qualified path to a **deployed** folder \(for example, `/path/to/`\).



</td>
</tr>
</table>



### PARAMETERS \[IN\]

Additional parameters can be used to control various aspects of the procedure execution. If no parameters are needed, the empty predefined parameters table `_SYS_DI.T_NO_PARAMETERS` can be used.

**\_SYS\_DI.TT\_PARAMETERS**


<table>
<tr>
<th valign="top">

Name



</th>
<th valign="top">

Data Type



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

KEY



</td>
<td valign="top">

NVARCHAR\(256\)



</td>
<td valign="top">

The key name of the parameter



</td>
</tr>
<tr>
<td valign="top">

VALUE



</td>
<td valign="top">

NVARCHAR\(256\)



</td>
<td valign="top">

The value assigned to the parameter



</td>
</tr>
</table>

The following additional parameters are available:

-   `container_lock_wait_timeout`

-   `ignore_files` true, false \(default\)

-   `ignore_folders` true, false \(default\)

-   `recursive` true, false \(default\)

-   `trace_context`

-   `trace_level.<trace topic>`

-   `message_severity`




### RETURN\_CODE \[OUT\]

The return code indicates if the procedure executed successfully. For more details about which codes are returned, see *The SQL API for SAP HDI* in *Related Information*.



### REQUEST\_ID \[OUT\]

A unique ID is generated for each HDI container API call. For more details about which IDs are generated for API calls, see *The SQL API for SAP HDI* in *Related Information*.



### MESSAGES \[OUT\]

A table is used to display messages that contain information logged during \(and about\) the execution of the procedure. For more details about which codes are returned, see *The SQL API for SAP HDI* in *Related Information*.



### RESULT \[OUT\]

Returns a list of files or folders including metadata:

**\_SYS\_DI.TT\_FILESFOLDERS\_METADATA**


<table>
<tr>
<th valign="top">

Name



</th>
<th valign="top">

Data Type



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

PATH



</td>
<td valign="top">

NVARCHAR\(511\)



</td>
<td valign="top">

A single path is either a fully qualified path to the **deployed** file \(for example, `/path/to/a/file.txt`'\), or a fully qualified path to a **deployed** folder \(for example, `/path/to/`\).



</td>
</tr>
<tr>
<td valign="top">

CREATE\_USER\_NAME



</td>
<td valign="top">

NVARCHAR\(256\)



</td>
<td valign="top">

User associated with the creation of the **deployed** file or folder



</td>
</tr>
<tr>
<td valign="top">

CREATE\_APPUSER\_NAME



</td>
<td valign="top">

NVARCHAR\(256\)



</td>
<td valign="top">

Application user associated with the creation of the **deployed** file or folder



</td>
</tr>
<tr>
<td valign="top">

CREATE\_TIMESTAMP\_UTC



</td>
<td valign="top">

TIMESTAMP



</td>
<td valign="top">

Time stamp indicating when the **deployed** file or folder was created



</td>
</tr>
<tr>
<td valign="top">

MODIFICATION\_USER\_NAME



</td>
<td valign="top">

NVARCHAR\(256\)



</td>
<td valign="top">

User associated with the last modification of the **deployed** file or folder



</td>
</tr>
<tr>
<td valign="top">

MODIFICATION\_APPUSER\_NAME



</td>
<td valign="top">

NVARCHAR\(256\)



</td>
<td valign="top">

Application user associated with the last modification of the **deployed** file or folder



</td>
</tr>
<tr>
<td valign="top">

MODIFICATION\_TIMESTAMP\_UTC



</td>
<td valign="top">

TIMESTAMP



</td>
<td valign="top">

Time stamp indicating when the **deployed** file or folder was last modified



</td>
</tr>
<tr>
<td valign="top">

SIZE



</td>
<td valign="top">

BIGINT



</td>
<td valign="top">

Size of the listed **deployed** file in bytes



</td>
</tr>
<tr>
<td valign="top">

SHA256



</td>
<td valign="top">

NVARCHAR\(64\)



</td>
<td valign="top">

SHA256 hash of the file, if present in the **deployed** file system.



</td>
</tr>
<tr>
<td valign="top">

CONTENT



</td>
<td valign="top">

BLOB



</td>
<td valign="top">

Content of the **deployed** file



</td>
</tr>
</table>



<a name="loio5873a56cd8dc4ef19023c428bf0017e2__section_msx_rt3_w2b"/>

## Examples

The following examples show how to use the `READ_DEPLOYED` API to obtain and display information about the content of the deployed file system, after writing the following content to the file system using the `MAKE` API:

-   Configuration File: `.hdiconfig`

-   Configuration File: `.hdinamespace`

-   Folder: `src1/`

    -   Table file: `src1/t.hdbtable`

    -   View file: `src1/v.hdbview`


-   Folder: `src2/`

    -   Procedure file: `src2/p.hdbprocedure`



The following example shows how to create the files in container C's work file system:

> ### Sample Code:  
> Write Files to the Container's Work File System
> 
> ```sql
> CREATE LOCAL TEMPORARY COLUMN TABLE #PATHS LIKE _SYS_DI.TT_FILESFOLDERS_CONTENT;
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('.hdiconfig', '{ "file_suffixes" : { "hdbtable" : { "plugin_name" : "com.sap.hana.di.table" }, "hdbview" : { "plugin_name" : "com.sap.hana.di.view" }, "hdbprocedure" : { "plugin_name" : "com.sap.hana.di.procedure" } } }');
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('.hdinamespace', '{ "name": "", "subfolder": "ignore" }');
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('src1/', NULL);
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('src1/t.hdbtable', 'COLUMN TABLE T ( A INTEGER )');
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('src1/v.hdbview', 'VIEW V AS SELECT A FROM T');
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('src2/', '');
> INSERT INTO #PATHS (PATH, CONTENT) VALUES ('src2/p.hdbprocedure', 'PROCEDURE P (OUT RESULT INT) LANGUAGE SQLSCRIPT AS BEGIN SELECT COUNT(*) INTO RESULT FROM V; end');
> CALL C#DI.WRITE(#PATHS, _SYS_DI.T_NO_PARAMETERS, ?, ?, ?);
> DROP TABLE #PATHS; 
> ```

Deploy the files to container C's deployed file system:

> ### Sample Code:  
> Deploy Files to the Container's File System
> 
> ```sql
> CREATE LOCAL TEMPORARY COLUMN TABLE #DEPLOY_PATHS LIKE _SYS_DI.TT_FILESFOLDERS;
> INSERT INTO #DEPLOY_PATHS (PATH) VALUES ('.hdiconfig');
> INSERT INTO #DEPLOY_PATHS (PATH) VALUES ('.hdinamespace');
> INSERT INTO #DEPLOY_PATHS (PATH) VALUES ('src1/t.hdbtable');
> INSERT INTO #DEPLOY_PATHS (PATH) VALUES ('src1/v.hdbview');
> INSERT INTO #DEPLOY_PATHS (PATH) VALUES ('src2/p.hdbprocedure');
> CREATE LOCAL TEMPORARY COLUMN TABLE #UNDEPLOY_PATHS LIKE _SYS_DI.TT_FILESFOLDERS;
> CREATE LOCAL TEMPORARY COLUMN TABLE #PATH_PARAMETERS LIKE _SYS_DI.TT_FILESFOLDERS_PARAMETERS;
> CALL C#DI.MAKE(#DEPLOY_PATHS, #UNDEPLOY_PATHS, #PATH_PARAMETERS, _SYS_DI.T_NO_PARAMETERS, ?, ?, ?);
> DROP TABLE #DEPLOY_PATHS;
> DROP TABLE #UNDEPLOY_PATHS;
> DROP TABLE #PATH_PARAMETERS;
> ```

Read non-recursively all files and folders in the deployed file system of container C; this displays objects only at the topmost level:

> ### Sample Code:  
> Read Files and Folders Non-Recursively
> 
> ```sql
> CALL C#DI.READ_DEPLOYED(_SYS_DI.T_NO_FILESFOLDERS, _SYS_DI.T_NO_PARAMETERS, ?, ?, ?, ?);
> ```

Read recursively all files and folders in the deployed file system of container C; this displays all objects at all levels:

> ### Sample Code:  
> Read Files and Folders Recursively
> 
> ```sql
> CREATE LOCAL TEMPORARY COLUMN TABLE #PARAMETERS LIKE _SYS_DI.TT_PARAMETERS;
> INSERT INTO #PARAMETERS ( KEY, VALUE ) VALUES ('recursive', 'true');
> CALL C#DI.READ_DEPLOYED(_SYS_DI.T_NO_FILESFOLDERS, #PARAMETERS, ?, ?, ?, ?);
> DROP TABLE #PARAMETERS; 
> ```

Read recursively all files \(but no folders\) in the deployed file system of container C:

> ### Sample Code:  
> Read Only Files Recursively
> 
> ```sql
> CREATE LOCAL TEMPORARY COLUMN TABLE #PARAMETERS LIKE _SYS_DI.TT_PARAMETERS;
> INSERT INTO #PARAMETERS ( KEY, VALUE ) VALUES ('ignore_folders', 'true');
> INSERT INTO #PARAMETERS ( KEY, VALUE ) VALUES ('recursive', 'true');
> CALL C#DI.READ_DEPLOYED(_SYS_DI.T_NO_FILESFOLDERS, #PARAMETERS, ?, ?, ?, ?);
> DROP TABLE #PARAMETERS; 
> ```

Read recursively all folders \(but no files\) in the deployed file system of container C:

> ### Sample Code:  
> Read Only Folders Recursively
> 
> ```sql
> CREATE LOCAL TEMPORARY COLUMN TABLE #PARAMETERS LIKE _SYS_DI.TT_PARAMETERS;
> INSERT INTO #PARAMETERS ( KEY, VALUE ) VALUES ('ignore_files', 'true');
> INSERT INTO #PARAMETERS ( KEY, VALUE ) VALUES ('recursive', 'true');
> CALL C#DI.READ_DEPLOYED(_SYS_DI.T_NO_FILESFOLDERS, #PARAMETERS, ?, ?, ?, ?);
> DROP TABLE #PARAMETERS; 
> ```

Read specific files or folders in the deployed file system of container C:

> ### Sample Code:  
> Read Specified Files and Folders
> 
> ```sql
> CREATE LOCAL TEMPORARY COLUMN TABLE #PATHS LIKE _SYS_DI.TT_FILESFOLDERS;
> INSERT INTO #PATHS (PATH) VALUES ('src1/');
> INSERT INTO #PATHS (PATH) VALUES ('src2/p.hdbprocedure');
> CREATE LOCAL TEMPORARY COLUMN TABLE #PARAMETERS LIKE _SYS_DI.TT_PARAMETERS;
> INSERT INTO #PARAMETERS ( KEY, VALUE ) VALUES ('recursive', 'false');
> CALL C#DI.READ_DEPLOYED(#PATHS, #PARAMETERS, ?, ?, ?, ?);
> DROP TABLE #PATHS; DROP TABLE #PARAMETERS; 
> ```

**Related Information**  


[WRITE](write-bfd0969.md "Write or create files or folders in an HDI container.")

[MAKE](make-7a0b4c5.md "Trigger a make operation in an HDI container with a specified set of files or folders.")

[LIST\_DEPLOYED](list-deployed-6709ac6.md "Display specific files or folders in an HDI container.")

[The HDI Container API](the-hdi-container-api-40ba784.md "Maintain HDI containers and container content using the HDI container API.")

[The SQL API for SAP HANA Deployment Infrastructure \(HDI\)](../the-sql-api-for-sap-hana-deployment-infrastructure-hdi-035dbbe.md "An SQL application programming interface (API) is available to help maintain the SAP HANA Deployment Infrastructure (HDI).")

