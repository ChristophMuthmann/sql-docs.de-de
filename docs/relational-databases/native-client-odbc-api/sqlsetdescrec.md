---
title: SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 257d60cfd6c25fa0234355214ac7db227f54743e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In diesem Thema wird erläutert, SQLSetDescRec Funktionen, die spezifisch für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec und Tabellenwertparameter  
 SQLSetDescRec kann verwendet werden, um deskriptorfelder für Tabellenwertparameter und Tabellenwertparameter-Spalten festzulegen. Tabellenwertparameter-Spalten sind nur verfügbar, wenn das Deskriptorheaderfeld SQL_SOPT_SS_PARAM_FOCUS auf die Ordnungszahl eines Datensatzes festgelegt ist, für den SQL_DESC_TYPE auf SQL_SS_TABLE eingestellt ist. Weitere Informationen zu SQL_SOPT_SS_PARAM_FOCUS finden Sie unter [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 In der folgenden Tabelle wird die Zuordnung zwischen Parametern und Deskriptorfeldern beschrieben.  
  
|Parameter|Zugehöriges Attribut für Parametertypen, die keine Tabellenwertparameter sind, einschließlich Tabellenwertparameter-Spalten.|Verknüpftes Attribut für Tabellenwertparameter|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Typ*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*SubType*|Wird ignoriert.|Für Datensätze des Typs SQL_DATETIME oder SQL_INTERVAL wird es auf SQL_DESC_DATETIME_INTERVAL_CODE festgelegt.|  
|*Länge*|SQL_DESC_OCTET_LENGTH|Die Länge des Typnamens des Tabellenwertparameters. Kann SQL_NTS sein, wenn der Typname NULL-termininiert ist, oder Null (0), wenn der Typname des Tabellenwertparameters nicht erforderlich ist.|  
|*Genauigkeit*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*Dezimalstellen*|SQL_DESC_SCALE|Nicht verwendet. Dieser Parameter sollte 0 (null) sein.|  
|*DataPtr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> Dies ist ein optionaler Parameter für gespeicherte Prozeduren, und NULL kann angegeben werden, wenn er nicht erforderlich ist. Dieser Parameter muss für SQL-Anweisungen angegeben werden, die keine Prozeduraufrufe sind.<br /><br /> *DataPtr* dient auch als eindeutiger Wert, der die Anwendung verwenden kann, um diese Tabellenwertparameter zu identifizieren, wenn Variablen zeilenbindung verwendet wird.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> Bei einem Tabellenwertparameter ist dies die Anzahl der zu übertragenden Zeilen oder SQL_DATA_AT_EXEC. Dies ist ein Zeiger auf einen Wert, der die Anzahl von Zeilen mit SQLExecDirect übertragen hat.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>SQLSetDescRec-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Die für Datums-/Uhrzeittypen zulässigen Werte lauten wie folgt:  
  
||*Typ*|*SubType*|*Länge*|*Genauigkeit*|*Dezimalstellen*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|Datum|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|Uhrzeit|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>SQLSetDescRec-Unterstützung für große CLR-UDTs  
 **SQLSetDescRec** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLSetDescRec](http://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
