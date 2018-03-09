---
title: SQLBindParameter | Microsoft Docs
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
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6eceb24668a73eb94224f2c4d6f09f272595a92a
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="sqlbindparameter"></a>SQLBindParameter
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBindParameter** können vermeiden, den Aufwand der Datenkonvertierung zum Bereitstellen von Daten für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber, was zu erheblichen Verbesserung der Leistung für sowohl die Client- und Serverkomponenten von Anwendungen. Zu den weiteren Vorteilen gehören geringere Verluste der Genauigkeit, wenn ungefähre numerische Datentypen eingefügt oder aktualisiert werden.  
  
> [!NOTE]  
>  Beim Einfügen von **Char** und **Wchar** Daten in eine Image-Spalte, die Größe der Daten übergeben werden vom Typ verwendet werden, im Gegensatz zu der Größe der Daten nach der Konvertierung in ein binäres Format.  
  
 Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber einen Fehler in einem einzelnen Arrayelement eines Parameterarrays entdeckt, setzt der Treiber die Ausführung der Anweisung für die verbleibenden Arrayelemente fort. Wenn die Anwendung ein Array mit Parameterstatuselementen für die Anweisung gebunden hat, können die Zeilen der Parameter, die Fehler generieren, aus dem Array ermittelt werden.  
  
 Wenn Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Native Client-ODBC-Treiber verwenden, geben Sie SQL_PARAM_INPUT an, wenn Eingabeparameter gebunden werden. Geben Sie nur SQL_PARAM_OUTPUT oder SQL_PARAM_INPUT_OUTPUT an, wenn mit dem OUTPUT-Schlüsselwort definierte gespeicherte Prozedurparameter gebunden werden.  
  
 [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md) mit nicht zuverlässig ist die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-ODBC-Treiber, wenn ein Arrayelement eines gebundenen Parameterarrays einen Fehler bei der anweisungsausführung verursacht. Das ODBC-Anweisungsattribut SQL_ATTR_PARAMS_PROCESSED_PTR meldet die Anzahl von Zeilen, die vor dem Auftreten des Fehler verarbeitet wurden. Die Anwendung kann dann das Parameterstatusarray durchlaufen, um ggf. die Anzahl erfolgreich verarbeiteter Anweisungen zu ermitteln.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Binden von Parametern für SQL-Zeichentypen  
 Wenn die übergebene SQL-Datentyp ein Zeichentyp ist *ColumnSize* ist die Größe in Zeichen (nicht Bytes). Wenn die Länge der Datenzeichenfolge in Byte 8.000, ist *ColumnSize* sollte festgelegt werden, um **SQL_SS_LENGTH_UNLIMITED**, der angibt, dass es keine Begrenzung auf die Größe des SQL-Typs.  
  
 Für die Instanz, wenn der SQL-Datentyp ist **SQL_WVARCHAR**, *ColumnSize* darf nicht größer als 4000 sein. Wenn die tatsächliche Datenlänge über 4.000 Zeichen hinausgeht, wird *ColumnSize* sollte festgelegt werden, um **SQL_SS_LENGTH_UNLIMITED** , damit **nvarchar(max)** wird vom Treiber verwendet werden.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter und Tabellenwertparameter  
 Wie andere Parametertypen werden Tabellenwertparameter von SQLBindParameter gebunden.  
  
 Nachdem ein Tabellenwertparameter gebunden wurde, werden seine Spalten ebenfalls gebunden. Rufen Sie zum Binden der Spalten [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) um SQL_SOPT_SS_PARAM_FOCUS auf die Ordnungszahl für den Tabellenwertparameter festzulegen. Rufen Sie dann SQLBindParameter für jede Spalte in der Tabellenwertparameter. Um zu den Parameterbindungen der obersten Ebene zurückzukehren, legen Sie SQL_SOPT_SS_PARAM_FOCUS auf 0 fest.  
  
 Informationen zum Zuordnen von Parametern zu deskriptorfeldern für Tabellenwertparameter finden Sie unter [Bindung und Data Transfer of Table-Valued-Parametern und Spaltenwerte](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>SQLBindParameter-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Parameterwerte von Datum-/Uhrzeit-Typen werden konvertiert, wie in beschrieben [Konvertierungen von C-in SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Beachten Sie diese Parameter vom Typ **Zeit** und **"DateTimeOffset"** benötigen *ValueType* als angegebenen **SQL_C_DEFAULT** oder **SQL_C_BINARY** , wenn die entsprechenden Strukturen (**SQL_SS_TIME2_STRUCT** und **sql_ss_timestampoffset_struct-Wert**) verwendet werden.  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>SQLBindParameter-Unterstützung für große CLR-UDTs  
 **SQLBindParameter** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLBindParameter-Funktion](http://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
