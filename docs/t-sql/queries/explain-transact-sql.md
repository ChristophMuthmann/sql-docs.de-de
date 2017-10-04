---
title: "Erklären Sie (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b83d9a72ce1adbb37a80da8bfd52824b02fa16b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="explain-transact-sql"></a>Erklären Sie (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt den Abfrageplan für eine [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] -Anweisung ohne die Anweisung ausführen. Verwendung **Erklärung** Preview, welche Vorgänge die datenverschiebung erfordern, und die geschätzten Kosten der Abfragevorgänge anzeigen.  
  
 Weitere Informationen zu Abfragen finden Sie unter "Grundlegendes zu Abfragepläne" in der [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="syntax"></a>Syntax  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *SQL_statement*  
 Die [!INCLUDE[DWsql](../../includes/dwsql-md.md)] Anweisung auf dem **Erklärung** wird ausgeführt. *SQL_statement* kann einen der folgenden Befehle: **wählen**, **einfügen**, **UPDATE**, **löschen**,  **Wählen Sie erstellen für Tabelle als**, **CREATE REMOTE TABLE**.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **SHOWPLAN** Berechtigung und die Berechtigung zum Ausführen von *SQL_statement*. Finden Sie unter [Berechtigungen: GRANT, DENY, REVOKE &#40; Azure SQL Datawarehouse, Parallel Datawarehouse &#41; ](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>Rückgabewert  
 Der Rückgabewert der **Erklärung** Befehl ist ein XML-Dokument mit der Struktur unten angezeigt. Dieses XML-Dokument enthält alle Vorgänge im Abfrageplan für die angegebene Abfrage, die jede eingeschlossen, durch die `<dsql_operation>` Tag. Der Rückgabewert ist vom Typ **nvarchar(max)**.  
  
 Der zurückgegebene Abfrageplan Steuerelementansicht sequenzielle SQL-Anweisungen; Beim Ausführen der Abfrage kann es parallelisierte Vorgänge umfassen, damit einige der sequenziellen Anweisungen gezeigt zur gleichen Zeit ausgeführt werden kann.  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 Die XML-Tags werden diese Informationen enthalten:  
  
|XML-Tag|Zusammenfassungen, Attribute und Inhalt|  
|-------------|--------------------------------------|  
|\<Dsql_query >|Oberste Ebene/Dokumentelement.|
|\<SQL >|Als Echo *SQL_statement*.|  
|\<Params >|Dieses Tag ist zu diesem Zeitpunkt nicht verwendet.|  
|\<Dsql_operations >|Fasst zusammen und enthält die Abfrageschritte für die und Kosteninformationen für die Abfrage enthält. Enthält auch alle von der `<dsql_operation>` blockiert. Dieses Tag enthält Informationen zur Anzahl für die gesamte Abfrage:<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *Grenzwerte* die geschätzte Gesamtzeit für die Abfrage in Millisekunden ausgeführt wird.<br /><br /> *Total_number_operations* ist die Gesamtanzahl von Vorgängen für die Abfrage. Ein Vorgang, der parallelisiert wird, und führen Sie auf mehreren Knoten wird als einzelner Vorgang gezählt.|  
|\<Dsql_operation >|Beschreibt einen einzelnen Vorgang innerhalb des Abfrageplans. Die \<Dsql_operation >-Tag enthält den Vorgangstyp als Attribut:<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *Operation_type* ist einer der Werte in den [Abfragen von Daten (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c).<br /><br /> Der Inhalt der `\<dsql_operation>` Block ist abhängig von den Vorgangstyp.<br /><br /> Finden Sie in der folgenden Tabelle aus.|  
  
|Vorgangstyp|Inhalt|Beispiel|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE, DISTRIBUTE_REPLICATED_TABLE_MOVE MASTER_TABLE_MOVE, PARTITION_MOVE, SHUFFLE_MOVE und TRIM_MOVE|`<operation_cost>`Element mit diesen Attributen. Berücksichtigt nur den lokalen Vorgang:<br /><br /> -   *Kosten* sind die Kosten für die lokalen Operator und zeigt die geschätzte Zeit für den Vorgang zum Ausführen in ms.<br />-   *Accumulative_cost* ist die Summe aller betrachtete Vorgänge im Plan einschließlich addierten Werte für parallele Vorgänge in ms.<br />-   *Average_rowsize* ist die geschätzte durchschnittliche Zeilengröße (in Byte) von Zeilen abgerufen, und übergeben während des Vorgangs.<br />-   *Output_rows* ist die Ausgabe (Knoten) Kardinalität und zeigt die Anzahl der Ausgabezeilen.<br /><br /> `<location>`: Der Knoten oder Verteilungen, in dem der Vorgang wiederholt werden soll. Optionen sind: "Control", "ComputeNode", "AllComputeNodes", "AllDistributions", "SubsetDistributions", "Vertrieb" und "SubsetNodes".<br /><br /> `<source_statement>`: Die Quelldaten für die zufällige verschieben.<br /><br /> `<destination_table>`: Die interne temporäre Tabelle werden in die Daten verschoben werden.<br /><br /> `<shuffle_columns>`: (Gilt nur für SHUFFLE_MOVE Vorgänge). Eine oder mehrere Spalten, die als verteilungsspalten für die temporäre Tabelle verwendet werden.|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`: Finden Sie unter `<operation_cost>` oben.<br /><br /> `<DestinationCatalog>`: Der Zielknoten oder Knoten.<br /><br /> `<DestinationSchema>`: Das Zielschema in Zielkatalog.<br /><br /> `<DestinationTableName>`: Der Name der Zieltabelle oder "TableName".<br /><br /> `<DestinationDatasource>`: Der Name oder die Verbindungszeichenfolge der Informationen für die Ziel-Datenquelle.<br /><br /> `<Username>`und `<Password>`: Diese Felder anzugeben, dass Benutzername und Kennwort für das Ziel möglicherweise erforderlich.<br /><br /> `<BatchSize>`: Die Batchgröße für den Kopiervorgang.<br /><br /> `<SelectStatement>`: Die select-Anweisung verwendet, um die Kopie auszuführen.<br /><br /> `<distribution>`: Die Verteilung, in dem der Kopiervorgang ausgeführt wird.|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`: Die Quelltabelle für den Vorgang.<br /><br /> `<destionation_table>`: Die Zieltabelle für den Vorgang.|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`: Finden Sie unter `<location>` oben.<br /><br /> `<sql_operation>`: Gibt die SQL-Befehl, der auf einem Knoten ausgeführt werden.|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`: Der Zielkatalog.<br /><br /> `<DestinationSchema>`: Das Zielschema in Zielkatalog.<br /><br /> `<DestinationTableName>`: Der Name der Zieltabelle oder "TableName".<br /><br /> `<DestinationDatasource>`: Der Name der Ziel-Datenquelle.<br /><br /> `<Username>`und `<Password>`: Diese Felder anzugeben, dass Benutzername und Kennwort für das Ziel möglicherweise erforderlich.<br /><br /> `<CreateStatement>`: Der Table-Anweisung der Erstellung für die Zieldatenbank.|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`: Der Bezeichner für das Resultset.|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`: Der Bezeichner für das erstellte Objekt.|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 **Erklären Sie** angewendet werden können, um *optimierbarer* Abfragen nur Abfragen, die verbessert oder geändert werden können basierend auf den Ergebnissen des ein **ERLÄUTERN** Befehl. Die unterstützten **Erklärung** Befehle sind oben aufgeführt. Bei dem Versuch, verwenden Sie **Erklärung** mit einer Abfrage mit nicht unterstützten Typ entweder einen Fehler zurück oder echo die Abfrage.  
  
 **Erklären Sie** wird in einer Benutzertransaktion nicht unterstützt.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt eine **Erklärung** Befehl ausführen, auf eine **wählen** -Anweisung und das XML-Ergebnis.  
  
 **Senden einer EXPLAIN-Anweisung**  
  
 Der übermittelte Befehl in diesem Beispiel lautet:  
  
```  
USE AdventureWorksPDW2012;  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 Nach der Ausführung der Anweisung mit der **Erklärung** Option, die Registerkarte "Message" stellt eine einzelne Zeile mit dem Titel **erläutern**, und den XML-Text ab `\<?xml version="1.0" encoding="utf-8"?>` klicken Sie auf der öffnen Sie des gesamten Texts in XML-Code ein XML-Fenster. Um die folgenden Kommentare besser zu verstehen, sollten Sie die Anzeige von Zeilennummern im SSDT aktivieren.  
  
#### <a name="to-turn-on-line-numbers"></a>So aktivieren Sie Zeilennummern  
  
1.  Mit der Ausgabe angezeigt werden der **erläutern** Registerkarte SSDT, die **TOOLS** klicken Sie im Menü **Optionen**.  
  
2.  Erweitern Sie die **Texteditor** Abschnitt, erweitern Sie **XML**, und klicken Sie dann auf **allgemeine**.  
  
3.  In der **Anzeige** Bereich Kontrollkästchen **Zeilennummern**.  
  
4.  Klicken Sie auf **OK**.  
  
 **Beispielausgabe für die Erklärung**  
  
 Das XML-Ergebnis der **Erklärung** Befehl mit Zeilennummern aktiviert ist:  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **Bedeutung der Ausgabe erklären**  
  
 Die oben angezeigten Ausgabe enthält 144 nummerierte Zeilen. Die Ausgabe dieser Abfrage kann sich geringfügig unterscheiden. Die folgende Liste beschreibt wichtige Abschnitte.  
  
-   Zeilen 3 bis 16 enthalten eine Beschreibung der Abfrage, die analysiert wird.  
  
-   Zeile 17, gibt an, dass die Gesamtanzahl von Vorgängen 9 ist. Sie können ermittelt den Beginn jedes Vorgangs durch die Suche nach den Wörtern **Dsql_operation**.  
  
-   Zeile 18 startet 1-Vorgang. Linien 18 und 19 darauf hinweisen, dass eine **RND_ID** Vorgang erstellt eine zufällige ID-Nummer, die für eine Beschreibung des Objekts verwendet werden. Das Objekt in der Ausgabe, die oben beschriebenen **TEMP_ID_16893**. Ihre wird unterschiedlich sein.  
  
-   Zeile 20 startet 2-Vorgang. Zeilen 21 bis 25: Klicken Sie auf allen Serverknoten, erstellen Sie eine temporäre Tabelle namens **TEMP_ID_16893**.  
  
-   Zeile 26 startet 3-Vorgang. Zeilen 27 bis 37: Verschieben von Daten auf **TEMP_ID_16893** mithilfe einer broadcast verschieben. An jede Serverknoten gesendete Abfrage wird bereitgestellt. Zeile 37 gibt an, die Zieltabelle ist **TEMP_ID_16893**.  
  
-   Zeile 38 wird die 4-Vorgang gestartet. Zeilen 39 bis 40: eine Zufalls-ID für eine Tabelle erstellen. **TEMP_ID_16894** ist die ID-Nummer im obigen Beispiel. Ihre wird unterschiedlich sein.  
  
-   Zeile 41 startet 5-Vorgang. Zeilen 42 bis 46: Erstellen Sie auf allen Knoten eine temporäre Tabelle namens **TEMP_ID_16894**.  
  
-   Zeile 47 startet 6-Vorgang. Zeilen 48 bis 91 sein: Verschieben von Daten aus verschiedenen Tabellen (einschließlich **TEMP_ID_16893**) zu Tabelle **TEMP_ID_16894**, mithilfe einer zufälligen Verschiebevorgang. An jede Serverknoten gesendete Abfrage wird bereitgestellt. 90-Zeile gibt an, die Zieltabelle als **TEMP_ID_16894**. Zeile 91 gibt die Spalten an.  
  
-   Zeile 92 startet 7-Vorgang. Zeilen 93 über 97: auf allen Serverknoten, löschen Sie temporäre Tabelle **TEMP_ID_16893**.  
  
-   Zeile 98 startet 8-Vorgang. Zeilen 99 über 135: Ergebnisse an den Client zurückzugeben. Verwendet die Abfrage zur Verfügung gestellt, um Ergebnisse zu erhalten.  
  
-   Zeile 136 startet 9-Vorgang. Zeilen 137 bis 140: Löschen Sie temporäre Tabelle, auf allen Knoten **TEMP_ID_16894**.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Das folgende Beispiel zeigt eine **Erklärung** Befehl ausführen, auf eine **wählen** -Anweisung und das XML-Ergebnis.  
  
 **Senden einer EXPLAIN-Anweisung**  
  
 Der übermittelte Befehl in diesem Beispiel lautet:  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 Nach der Ausführung der Anweisung mit der **Erklärung** Option, die Registerkarte "Message" stellt eine einzelne Zeile mit dem Titel **erläutern**, und den XML-Text ab `\<?xml version="1.0" encoding="utf-8"?>` klicken Sie auf der öffnen Sie des gesamten Texts in XML-Code ein XML-Fenster. Um die folgenden Kommentare besser zu verstehen, sollten Sie die Anzeige von Zeilennummern im SSDT aktivieren.  
  
#### <a name="to-turn-on-line-numbers"></a>So aktivieren Sie Zeilennummern  
  
1.  Mit der Ausgabe angezeigt werden der **erläutern** Registerkarte SSDT, die **TOOLS** klicken Sie im Menü **Optionen**.  
  
2.  Erweitern Sie die **Texteditor** Abschnitt, erweitern Sie **XML**, und klicken Sie dann auf **allgemeine**.  
  
3.  In der **Anzeige** Bereich Kontrollkästchen **Zeilennummern**.  
  
4.  Klicken Sie auf **OK**.  
  
 **Beispielausgabe für die Erklärung**  
  
 Das XML-Ergebnis der **Erklärung** Befehl mit Zeilennummern aktiviert ist:  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **Bedeutung der Ausgabe erklären**  
  
 Die oben angezeigten Ausgabe enthält 144 nummerierte Zeilen. Die Ausgabe dieser Abfrage kann sich geringfügig unterscheiden. Die folgende Liste beschreibt wichtige Abschnitte.  
  
-   Zeilen 3 bis 16 enthalten eine Beschreibung der Abfrage, die analysiert wird.  
  
-   Zeile 17, gibt an, dass die Gesamtanzahl von Vorgängen 9 ist. Sie können ermittelt den Beginn jedes Vorgangs durch die Suche nach den Wörtern **Dsql_operation**.  
  
-   Zeile 18 startet 1-Vorgang. Linien 18 und 19 darauf hinweisen, dass eine **RND_ID** Vorgang erstellt eine zufällige ID-Nummer, die für eine Beschreibung des Objekts verwendet werden. Das Objekt in der Ausgabe, die oben beschriebenen **TEMP_ID_16893**. Ihre wird unterschiedlich sein.  
  
-   Zeile 20 startet 2-Vorgang. Zeilen 21 bis 25: Klicken Sie auf allen Serverknoten, erstellen Sie eine temporäre Tabelle namens **TEMP_ID_16893**.  
  
-   Zeile 26 startet 3-Vorgang. Zeilen 27 bis 37: Verschieben von Daten auf **TEMP_ID_16893** mithilfe einer broadcast verschieben. An jede Serverknoten gesendete Abfrage wird bereitgestellt. Zeile 37 gibt an, die Zieltabelle ist **TEMP_ID_16893**.  
  
-   Zeile 38 wird die 4-Vorgang gestartet. Zeilen 39 bis 40: eine Zufalls-ID für eine Tabelle erstellen. **TEMP_ID_16894** ist die ID-Nummer im obigen Beispiel. Ihre wird unterschiedlich sein.  
  
-   Zeile 41 startet 5-Vorgang. Zeilen 42 bis 46: Erstellen Sie auf allen Knoten eine temporäre Tabelle namens **TEMP_ID_16894**.  
  
-   Zeile 47 startet 6-Vorgang. Zeilen 48 bis 91 sein: Verschieben von Daten aus verschiedenen Tabellen (einschließlich **TEMP_ID_16893**) zu Tabelle **TEMP_ID_16894**, mithilfe einer zufälligen Verschiebevorgang. An jede Serverknoten gesendete Abfrage wird bereitgestellt. 90-Zeile gibt an, die Zieltabelle als **TEMP_ID_16894**. Zeile 91 gibt die Spalten an.  
  
-   Zeile 92 startet 7-Vorgang. Zeilen 93 über 97: auf allen Serverknoten, löschen Sie temporäre Tabelle **TEMP_ID_16893**.  
  
-   Zeile 98 startet 8-Vorgang. Zeilen 99 über 135: Ergebnisse an den Client zurückzugeben. Verwendet die Abfrage zur Verfügung gestellt, um Ergebnisse zu erhalten.  
  
-   Zeile 136 startet 9-Vorgang. Zeilen 137 bis 140: Löschen Sie temporäre Tabelle, auf allen Knoten **TEMP_ID_16894**.  
  
  


