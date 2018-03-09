---
title: SQLPutData | Microsoft Docs
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
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf27150c9e6c0da3f32cd3295c358c80da44b767
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Die folgenden Einschränkungen gelten beim Senden von mehr als 65.535 Byte Daten mit SQLPutData (für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Version 4. 21a) oder 400 KB Daten (für SQL Server, Version 6.0 und höher) für eine SQL_LONGVARCHAR (**Text**), SQL_WLONGVARCHAR (**Ntext**) oder SQL_LONGVARBINARY (**Image**) Spalte:  
  
-   Der referenzierte Parameter kann die *Insert_value* in einer INSERT-Anweisung.  
  
-   Der referenzierte Parameter kann eine *Ausdruck* in der SET-Klausel einer UPDATE-Anweisung.  
  
 Das Abbrechen einer Sequenz von SQLPutData aufrufen, aus denen Daten in Blöcken zu einem Server mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bewirkt, dass ein teilweises Update des Spaltenwerts bei Verwendung von Version 6.5 oder früher. Die **Text**, **Ntext**, oder **Image** Spalte, auf die verwiesen wurde, wenn SQLCancel aufgerufen wurde, ein platzhalterzwischenwert festgelegt ist.  
  
> [!NOTE]  
>  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Treiber unterstützt das Herstellen einer Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version 6.5 und niedriger nicht.  
  
## <a name="diagnostics"></a>Diagnose  
 Es ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-spezifischen SQLSTATE für SQLPutData:  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|22026|Zeichenfolgendaten, nicht übereinstimmende Länge|Wenn die Länge der Daten in Bytes, die gesendet werden von einer Anwendung beispielsweise mit SQL_LEN_DATA_AT_EXEC angegeben wurde (*n*), in denen  *n*  ist größer als 0 ist, die Gesamtanzahl der Bytes, die von der Anwendung über SQLPutData müssen der angegebene Länge entsprechen.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData und Tabellenwertparameter  
 SQLPutData wird von einer Anwendung verwendet, wenn Variablen zeilenbindung mit Tabellenwertparametern verwenden. Die *StrLen_Or_Ind* Parameter gibt an, dass er für den Treiber zum Sammeln von Daten für die nächste Zeile bzw. Zeilen des Tabellenwertparameter-Daten bereit ist oder keine weiteren Zeilen verfügbar sind:  
  
-   Ein Wert größer als 0 gibt an, dass der nächste Satz von Zeilenwerten verfügbar ist.  
  
-   Der Wert 0 gibt an, dass es keine Zeilen mehr gibt, die gesendet werden sollen.  
  
-   Ein Wert unter 0 zeigt einen Fehler an und führt dazu, dass ein Diagnosedatensatz mit SQLState HY090 aufgezeichnet und die Meldung „Ungültige Zeichenfolge oder Pufferlänge“ ausgegeben wird.  
  
 Die *DataPtr* Parameter wird ignoriert, jedoch muss auf einen Wert ungleich NULL festgelegt werden. Weitere Informationen finden Sie im Abschnitt auf Variablen zeilenbindung in [Bindung und Data Transfer of Table-Valued-Parametern und Spaltenwerte](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Wenn *StrLen_Or_Ind* verfügt über einen anderen Wert als SQL_DEFAULT_PARAM oder eine Zahl zwischen 0 und SQL_PARAMSET_SIZE (d. h. die *ColumnSize* -Parameter von SQLBindParameter), ist ein Fehler auftritt. Dieser Fehler bewirkt, dass SQLPutData SQL_ERROR: SQLSTATE=HY090, "Ungültige Zeichenfolge oder Pufferlänge" zurückgibt.  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>SQLPutData-Unterstützung für verbesserte Funktionen für Datum/Uhrzeit  
 Parameterwerte von Datum-/Uhrzeit-Typen werden konvertiert, wie in beschrieben [Konvertierungen von C-in SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>SQLPutData-Unterstützung für große CLR-UDTs  
 **SQLPutData** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLPutData-Funktion](http://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
