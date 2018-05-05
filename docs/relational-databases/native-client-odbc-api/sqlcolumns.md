---
title: SQLColumns | Microsoft Docs
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
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
caps.latest.revision: 62
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e735efbd7aa155d8f4618afffc203cf4558fe9ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLColumns** gibt SQL_SUCCESS zurück, unabhängig davon, ob Werte vorhanden sind, für die *CatalogName*, *TableName*, oder *ColumnName* Parameter. **SQLFetch** gibt SQL_NO_DATA zurück, wenn in diesen Parametern ungültige Werte verwendet werden.  
  
> [!NOTE]  
>  Für Datentypen für große Werte werden alle Längenparameter mit einem Wert von SQL_SS_LENGTH_UNLIMITED zurückgegeben.  
  
 **SQLColumns** kann in einem statischen Servercursor ausgeführt werden. Der Versuch auszuführen **SQLColumns** in einem aktualisierbaren (dynamischen oder Keyset-) Cursor wird SQL_SUCCESS_WITH_INFO zurückgegeben. gibt an, dass der Cursortyp geändert wurde.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt die Berichtsinformationen für Tabellen auf Verbindungsservern durch akzeptieren einen zweiteiligen Namen für die *CatalogName* Parameter: *linked_server_name*.  
  
 Für ODBC 2. *x* Anwendungen, die nicht mithilfe von Platzhaltern in *TableName*, **SQLColumns** gibt Informationen über alle Tabellen, deren Namen übereinstimmen *TableName*und vom aktuellen Benutzer gehören. Wenn der aktuelle Benutzer keine Tabelle besitzt, deren Name entspricht, der *TableName* Parameter **SQLColumns** gibt Informationen über alle Tabellen, deren Besitzer andere Benutzer entspricht, in dem der Tabellenname der  *TableName* Parameter. Für ODBC 2. *x* Anwendungen mithilfe von Platzhaltern, **SQLColumns** alle Tabellen, deren Namen Übereinstimmung zurück *TableName*. Für ODBC 3. *x* Anwendungen **SQLColumns** alle Tabellen, deren Namen Übereinstimmung zurück *TableName* unabhängig vom Besitzer oder ob Platzhalter verwendet werden.  
  
 In der folgenden Tabelle werden die vom Resultset zurückgegebenen Spalten aufgeführt:  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|DATA_TYPE|Gibt SQL_VARCHAR, SQL_VARBINARY oder SQL_WVARCHAR für den **varchar(max)** Datentypen.|  
|TYPE_NAME|Gibt "Varchar", "Varbinary" oder "Nvarchar" für die **varchar(max)**, **varbinary(max)**, und **nvarchar(max)** Datentypen.|  
|COLUMN_SIZE|Gibt SQL_SS_LENGTH_UNLIMITED für **varchar(max)** -Datentyp zurück, die Größe der Spalte unbegrenzt ist.|  
|BUFFER_LENGTH|Gibt SQL_SS_LENGTH_UNLIMITED für **varchar(max)** -Datentyp zurück, die Größe des Puffers unbegrenzt ist.|  
|SQL_DATA_TYPE|Gibt SQL_VARCHAR, SQL_VARBINARY oder SQL_WVARCHAR für den **varchar(max)** Datentypen.|  
|CHAR_OCTET_LENGTH|Gibt die maximale Länge einer char- oder binary-Spalte zurück. Gibt 0 zurück, um anzuzeigen, dass die Größe unbegrenzt ist.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Gibt den Namen des Katalogs zurück, in dem ein XML-Schemaauflistungsname definiert ist. Wenn der Katalogname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Gibt den Namen des Schemas zurück, in dem ein XML-Schemaauflistungsname definiert ist. Wenn der Schemaname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.|  
|SS_XML_SCHEMACOLLECTION_NAME|Gibt den Namen einer XML-Schemaauflistung zurück. Wenn der Name nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.|  
|SS_UDT_CATALOG_NAME|Der Name des Katalogs, der den benutzerdefinierten Typ (User-Defined Type, UDT) enthält.|  
|SS_UDT_SCHEMA_NAME|Der Name des Schemas, die den UDT enthält.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Der qualifizierte Name der UDT-Assembly.|  
  
 Für UDTs wird die vorhandene TYPE_NAME-Spalte verwendet, um den Namen des UDTS anzugeben. aus diesem Grund dafür keine weitere Spalte hinzugefügt werden sollen das Resultset der **SQLColumns** oder [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md). Der DATA_TYPE für eine UDT-Spalte oder einen UDT-Parameter ist SQL_SS_UDT.  
  
 Für den benutzerdefinierten Typ von Parametern können Sie die neuen, weiter oben in diesem Abschnitt definierten treiberspezifischen Deskriptoren verwenden, um die zusätzlichen Metadateneigenschaften eines UDT abzurufen oder festzulegen, falls der Server diese Informationen zurückgibt bzw. anfordert.  
  
 Wenn ein Client eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und ruft SQLColumns, mit NULL oder Platzhalter für den katalogeingabeparameter Informationen nicht aus anderen Katalogen zurückgegeben wird. Stattdessen werden nur Informationen über den aktuellen Katalog zurückgegeben. Der Client kann zuerst aufrufen SQLTables, um zu bestimmen, in welchem Katalog sich die gewünschte Tabelle befindet. Der Client dann können diesen Katalogwert für den katalogeingabeparameter in seinem Aufruf von SQLColumns zum Abrufen von Informationen zu den Spalten in dieser Tabelle.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>SQLColumns und Tabellenwertparameter  
 Von SQLColumns zurückgegebene Resultset hängt von der Einstellung von SQL_SOPT_SS_NAME_SCOPE ab. Weitere Informationen finden Sie unter [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Die folgenden Spalten wurden für Tabellenwertparameter hinzugefügt:  
  
|Spaltenname|Datentyp|Inhalt|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|Für eine Spalte vom Datentyp TABLE_TYPE ist dies SQL_TRUE, wenn es sich um eine berechnete Spalte handelt, andernfalls SQL_FALSE.|  
|SS_IS_IDENTITY|Smallint|SQL_TRUE, wenn die Spalte eine Identitätsspalte ist, andernfalls SQL_FALSE.|  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>SQLColumns-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Informationen über die zurückgegebenen Werte für Datum/Uhrzeit-Typen finden Sie unter [Katalogmetadaten](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>SQLColumns-Unterstützung für große CLR-UDTs  
 **SQLColumns** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>SQLColumns-Unterstützung für Spalten mit geringer Dichte  
 Zwei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bestimmte Spalten wurden dem Resultset für SQLColumns hinzugefügt:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**"smallint"**|SQL_TRUE, wenn die Spalte eine Sparsespalte ist, andernfalls SQL_FALSE.|  
|SS_IS_COLUMN_SET|**"smallint"**|Wenn die Spalte ist der **Column_set** Spalte, ist dies SQL_TRUE, andernfalls SQL_FALSE.|  
  
 In Übereinstimmung mit der ODBC-Spezifikation werden SS_IS_SPARSE und SS_IS_COLUMN_SET vor alle treiberspezifischen Spalten, die hinzugefügt wurden, angezeigt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Versionen älter als [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], sowie nach allen Spalten, die von ODBC selbst.  
  
 Von SQLColumns zurückgegebene Resultset hängt von der Einstellung von SQL_SOPT_SS_NAME_SCOPE ab. Weitere Informationen finden Sie unter [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Weitere Informationen zu Spalten mit geringer Dichte in ODBC, finden Sie unter [Sparse Columns Support &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLColumns-Funktion](http://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
