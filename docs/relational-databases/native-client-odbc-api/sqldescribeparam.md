---
title: SQLDescribeParam | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
caps.latest.revision: "61"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfe8843e8b3062f058cfc8de0235dfeecf029004
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Beschreiben Sie die Parameter der SQL-Anweisung, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber erstellt und führt eine [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT-Anweisung beim SQLDescribeParam für ein vorbereitetes ODBC-Anweisungshandle aufgerufen wird. Die Metadaten des Resultsets bestimmen die Eigenschaften der Parameter in der vorbereiteten Anweisung. SQLDescribeParam kann jeden Fehlercode zurückgeben, die möglicherweise SQLExecute oder SQLExecDirect zurückgeben.  
  
 Verbesserungen im Datenbankmodul ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLDescribeParam genauere Beschreibungen der erwarteten Ergebnisse abrufen können. Diese genaueren Ergebnisse unterscheidet sich möglicherweise von der Rückgabewerte SQLDescribeParam in früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Metadatenermittlung](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 Neue Funktion in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *ParameterSizePtr* jetzt gibt einen Wert, der gemäß der Definition für die Größe in Zeichen für die Spalte oder des Ausdrucks der entsprechenden parametermarkierung entspricht der [ODBC Spezifikation](http://go.microsoft.com/fwlink/?LinkId=207044). In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client *ParameterSizePtr* möglicherweise der entsprechende Wert der **SQL_DESC_OCTET_LENGTH** für den Typ oder ein irrelevanter spaltengrößenwert, die angegeben wurde Um SQLBindParameter für einen Typ, dessen Wert der ignoriert werden sollen (**SQL_INTEGER**, z. B.).  
  
 Der Treiber unterstützt das aufrufende SQLDescribeParam in den folgenden Situationen nicht:  
  
-   Nach dem SQLExecDirect für eine beliebige [!INCLUDE[tsql](../../includes/tsql-md.md)] Update- oder DELETE-Anweisungen, die mit der FROM-Klausel.  
  
-   Für eine ODBC- oder [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, die einen Parameter in einer HAVING-Klausel enthält oder die mit dem Ergebnis einer SUM-Funktion verglichen wird.  
  
-   Für eine ODBC- oder [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung abhängig von einer Unterabfrage, die Parameter enthält.  
  
-   Für ODBC SQL-Anweisungen, die Parametermarkierungen in beiden Ausdrücken eines Vergleichs oder quantifizierten Prädikats enthalten.  
  
-   Für Abfragen, bei denen einer der Parameter ein Parameter für eine Funktion ist.  
  
-   Wenn es Kommentare sind (/ * \*/) in der [!INCLUDE[tsql](../../includes/tsql-md.md)] Befehl.  
  
 Bei der Verarbeitung von Batches von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen die, der Treiber nicht unterstützt, ist aufrufen SQLDescribeParam für parametermarkierungen in Anweisungen nach der ersten Anweisung im Batch.  
  
 Beim Beschreiben von der Parameters von vorbereiteten gespeicherte Prozeduren verwendet SQLDescribeParam die gespeicherten Systemprozedur [Sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) um Parametereigenschaften abzurufen. Sp_sproc_columns kann Daten für gespeicherte Prozeduren innerhalb der aktuellen Benutzerdatenbank melden. Vorbereiten der Name einer vollqualifizierten gespeicherten Prozedur ermöglicht SQLDescribeParam über Datenbanken hinweg ausgeführt. Z. B. die gespeicherte Systemprozedur [Sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) vorbereitet und in jeder Datenbank wie ausgeführt werden können:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 Ausführen von SQLDescribeParam nach erfolgreicher Vorbereitung beim Verbinden mit einer beliebigen Datenbank ein leeres Rowset zurückgegeben, aber **master**. Der gleiche Aufruf, wie folgt vorbereitet bewirkt, dass SQLDescribeParam unabhängig von der aktuellen Benutzerdatenbank erfolgreich ist:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Bei Datentypen mit umfangreichen Werten den Wert im zurückgegebenen *DataTypePtr* ist SQL_VARCHAR, SQL_VARBINARY oder SQL_NVARCHAR. Um anzugeben, dass die Größe des Typparameters umfangreichen Daten "Unbegrenzt" ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber legt *ParameterSizePtr* auf 0. Tatsächliche Größenwerte werden für Standard zurückgegeben **Varchar** Parameter.  
  
> [!NOTE]  
>  Wenn der Parameter bereits mit einer Maximalgröße für den SQL_VARCHAR-, SQL_VARBINARY- oder SQL_WVARCHAR-Parameter gebunden wurde, wird die gebundene Größe des Parameters und nicht "unbegrenzt" zurückgegeben.  
  
 Um einen Eingabeparameter mit "unbegrenzter" Größe zu binden, muss Data-at-Execution verwendet werden. Es ist nicht möglich, einen Output-Parameter von "unbegrenzter" Größe zu binden (es gibt keine Methode für das streaming von Daten aus einer Output-Parameter, z. B. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) für Resultsets verwendet wird).  
  
 Für Ausgabeparameter muss ein Puffer gebunden werden und wenn der Wert zu umfangreich ist, wird der Puffer aufgefüllt und eine SQL_SUCCESS_WITH_INFO-Meldung wird zusammen mit einer Warnung "Zeichenfolgendaten werden rechts abgeschnitten" zurückgegeben. Die abgeschnittenen Daten werden anschließend verworfen.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam und Tabellenwertparameter  
 Eine Anwendung kann die Tabellenwertparameter-Informationen für eine vorbereitete Anweisung mit SQLDescribeParam abrufen. Weitere Informationen finden Sie unter [Tabellenwertparameter Parametermetadaten für vorbereitete Anweisungen](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Weitere Informationen zu Tabellenwertparametern im Allgemeinen finden Sie unter [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>SQLDescribeParam-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Die für Datums-/Uhrzeittypen zurückgegebenen Werte lauten wie folgt:  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|Uhrzeit|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>SQLDescribeParam-Unterstützung für große CLR-UDTs  
 **SQLDescribeParam** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQLDescribeParam-Funktion](http://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
