---
title: SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColAttribute function
ms.assetid: a5387d9e-a243-4cfe-b786-7fad5842b1d6
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9645af8a1e18398b6e0861450d37ed9ab15be75e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcolattribute"></a>SQLColAttribute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Sie können **SQLColAttribute** ein Attribut einer Resultsetspalte für vorbereitete oder ausgeführte ODBC-Anweisungen abgerufen. Aufrufen von **SQLColAttribute** für vorbereitete Anweisungen Ursachen einen Roundtrip zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber erhält Resultset-Spaltendaten als Teil der anweisungsausführung, deshalb wird beim Aufrufen **SQLColAttribute** nach Abschluss des **SQLExecute** oder  **SQLExecDirect** beinhaltet keine Server-Roundtrip erstellt.  
  
> [!NOTE]  
>  ODBC-Spaltenbezeichnerattribute sind nicht für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Resultsets verfügbar.  
  
|Feldbezeichner|Description|  
|----------------------|-----------------|  
|SQL_COLUMN_TABLE_NAME|Verfügbar für Resultsets, die aus Anweisungen abgerufen wurden, die Servercursor erzeugen, oder für ausgeführte SELECT-Anweisungen, die eine FOR BROWSE-Klausel enthalten.|  
|SQL_DESC_BASE_COLUMN_NAME|Verfügbar für Resultsets, die aus Anweisungen abgerufen wurden, die Servercursor erzeugen, oder für ausgeführte SELECT-Anweisungen, die eine FOR BROWSE-Klausel enthalten.|  
|SQL_DESC_BASE_TABLE_NAME|Verfügbar für Resultsets, die aus Anweisungen abgerufen wurden, die Servercursor erzeugen, oder für ausgeführte SELECT-Anweisungen, die eine FOR BROWSE-Klausel enthalten.|  
|SQL_DESC_CATALOG_NAME|Datenbankname. Verfügbar für Resultsets, die aus Anweisungen abgerufen wurden, die Servercursor erzeugen, oder für ausgeführte SELECT-Anweisungen, die eine FOR BROWSE-Klausel enthalten.|  
|SQL_DESC_LABEL|Für alle Resultsets verfügbar. Der Wert ist mit dem Wert des SQL_DESC_NAME-Felds identisch.<br /><br /> Das Feld hat nur dann die Länge Null, wenn die Spalte das Ergebnis eines Ausdrucks ist und der Ausdruck keine zugeordnete Bezeichnung hat.|  
|SQL_DESC_NAME|Für alle Resultsets verfügbar. Der Wert ist mit dem Wert des SQL_DESC_LABEL-Felds identisch.<br /><br /> Das Feld hat nur dann die Länge Null, wenn die Spalte das Ergebnis eines Ausdrucks ist und der Ausdruck keine zugeordnete Bezeichnung hat.|  
|SQL_DESC_SCHEMA_NAME|Der Name des Besitzers. Verfügbar für Resultsets, die aus Anweisungen abgerufen wurden, die Servercursor erzeugen, oder für ausgeführte SELECT-Anweisungen, die eine FOR BROWSE-Klausel enthalten.<br /><br /> Nur verfügbar, wenn der Besitzername für die Spalte in der SELECT-Anweisung angegeben wird.|  
|SQL_DESC_TABLE_NAME|Verfügbar für Resultsets, die aus Anweisungen abgerufen wurden, die Servercursor erzeugen, oder für ausgeführte SELECT-Anweisungen, die eine FOR BROWSE-Klausel enthalten.|  
|SQL_DESC_UNNAMED|SQL_NAMED für alle Spalten in einem Resultset, es sei denn, die Spalte ist das Ergebnis eines Ausdrucks, der keine zugeordnete Bezeichnung als Teil des Ausdrucks hat. Wenn SQL_DESC_UNNAMED SQL_UNNAMED zurückgibt, enthalten alle ODBC-Spaltenbezeichnerattribute leere Zeichenfolgen für die Spalte.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber verwendet die SET FMTONLY-Anweisung zum zu verringern Wenn **SQLColAttribute** heißt für vorbereitete aber nicht ausgeführte Anweisungen.  
  
 Für große Werttypen **SQLColAttribute** werden die folgenden Werte zurück:  
  
|Feldbezeichner|Beschreibung der Änderung|  
|----------------------|---------------------------|  
|SQL_DESC_DISPLAY_SIZE|Die maximale Anzahl von Zeichen, die für das Anzeigen der Spaltendaten benötigt wird. Für große Werttypspalten ist der zurückgegebene Wert SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_LENGTH|Gibt die tatsächliche Länge der Spalte im Resultset zurück. Für große Werttypspalten ist der zurückgegebene Wert SQL_SS_LENGTH_UNLIMITED.|  
|SQL_DESC_OCTET_LENGTH|Gibt die maximal mögliche Länge für große Werttypspalten zurück. SQL_SS_LENGTH_UNLIMITED wird verwendet, um unbegrenzte Größe anzugeben.|  
|SQL_DESC_PRECISION|Gibt den Wert SQL_SS_LENGTH_UNLIMITED für große Werttypspalten zurück.|  
|SQL_DESC_TYPE|Gibt SQL_VARCHAR, SQL_WVARCHAR und SQL_VARBINARY für große Werttypen zurück.|  
|SQL_DESC_TYPE_NAME|Gibt "varchar", "varbinary" und "nvarchar" für große Werttypen zurück.|  
  
 Für alle Versionen werden Spaltenattribute nur für das erste Resultset gemeldet, wenn durch einen vorbereiteten Stapel von SQL-Anweisungen mehrere Resultsets erzeugt werden.  
  
 Die folgenden Spaltenattribute sind Erweiterungen verfügbar gemacht werden, indem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt alle Werte in der *NumericAttrPtr* Parameter. Die Werte werden als SDWORD (lang mit Vorzeichen) zurückgegeben, außer SQL_CA_SS_COMPUTE_BYLIST, bei dem es sich um einen Zeiger auf ein WORD-Array handelt.  
  
|Feldbezeichner|Zurückgegebener Wert|  
|----------------------|--------------------|  
|SQL_CA_SS_COLUMN_HIDDEN*|TRUE, falls die referenzierte Spalte Teil eines verborgenen Primärschlüssels ist, der zur Unterstützung einer Transact-SQL SELECT-Anweisung erstellt wurde, die FOR BROWSE enthält.|  
|SQL_CA_SS_COLUMN_ID|Ordnungsposition einer COMPUTE-Klausel-Ergebnisspalte innerhalb der aktuellen Transact-SQL SELECT-Anweisung.|  
|SQL_CA_SS_COLUMN_KEY*|TRUE, falls die referenzierte Spalte Teil eines Primärschlüssels für die Zeile ist und die Transact-SQL SELECT-Anweisung FOR BROWSE enthält.|  
|SQL_CA_SS_COLUMN_OP|Ganze Zahl, die den Aggregatoperator angibt, der für den Wert in einer COMPUTE-Klauselspalte verantwortlich ist. Die ganzzahligen Werte sind in sqlncli.h definiert.|  
|SQL_CA_SS_COLUMN_ORDER|Ordnungsposition der Spalte innerhalb der ORDER BY-Klausel einer ODBC- oder Transact-SQL SELECT-Anweisung.|  
|SQL_CA_SS_COLUMN_SIZE|Maximale Länge in Byte, die zum Binden eines aus der Spalte abgerufenen Datenwerts an eine SQL_C_BINARY-Variable erforderlich ist.|  
|SQL_CA_SS_COLUMN_SSTYPE|Systemeigener Datentyp der Daten, die in der SQL Server-Spalte gespeichert sind. Die Typwerte sind in sqlncli.h definiert.|  
|SQL_CA_SS_COLUMN_UTYPE|Basisdatentyp des benutzerdefinierten Datentyps der SQL Server-Spalte. Die Typwerte sind in sqlncli.h definiert.|  
|SQL_CA_SS_COLUMN_VARYLEN|TRUE, wenn sich die Länge der Spaltendaten ändern kann, andernfalls FALSE.|  
|SQL_CA_SS_COMPUTE_BYLIST|Zeiger auf ein WORD-Array (kurz ohne Vorzeichen) zur Angabe der Spalten, die im BY-Ausdruck einer COMPUTE-Klausel verwendet werden. Wenn die COMPUTE-Klausel keinen BY-Ausdruck angibt, wird ein NULL-Zeiger zurückgegeben.<br /><br /> Das erste Element des Arrays enthält die Anzahl der BY-Listenspalten. Zusätzliche Elemente sind die Spaltenordinalzahlen.|  
|SQL_CA_SS_COMPUTE_ID|*Computeid* einer Zeile, die das Ergebnis einer COMPUTE-Klausel in der aktuellen Transact-SQL SELECT-Anweisung ist.|  
|SQL_CA_SS_NUM_COMPUTES|Anzahl von COMPUTE-Klauseln, die in der aktuellen Transact-SQL SELECT-Anweisung angegeben ist.|  
|SQL_CA_SS_NUM_ORDERS|Anzahl von Spalten, die in der ORDER BY-Klausel einer ODBC- oder Transact-SQL SELECT-Anweisung angegeben ist.|  
  
 \*   Verfügbar, wenn Anweisungsattribut SQL_SOPT_SS_HIDDEN_COLUMNS auf SQL_HC_ON festgelegt ist.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] treiberspezifische deskriptorfelder, um zusätzliche Informationen, um den Namen der XML-schemaauflistung, die den Schemanamen und der Name des Katalogs, Katalognamens bereitzustellen, eingeführt. Diese Eigenschaften erfordern keine Anführungszeichen oder ein Escapezeichen, wenn sie nicht-alphanumerische Zeichen enthalten. In der folgenden Tabelle sind diese neuen Deskriptorfelder aufgelistet:  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME|CharacterAttributePtr|Der Name des Katalogs, in dem ein XML-schemaauflistungsname definiert ist. Wenn der Katalogname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.<br /><br /> Diese Informationen werden vom SQL_DESC_SS_XML_SCHEMACOLLECTION_CATALOG_NAME-Datensatzfeld vom IRD zurückgegeben, das ein Lese-/Schreibfeld ist.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAM E|CharacterAttributePtr|Der Name des Schemas, in dem eine XML-Schemaauflistung definiert ist. Wenn der Schemaname nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.<br /><br /> Diese Informationen werden vom SQL_DESC_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME-Datensatzfeld vom IRD zurückgegeben, das ein Lese-/Schreibfeld ist.|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_NAME|CharacterAttributePtr|Name der XML-Schemaauflistung. Wenn der Name nicht gefunden werden kann, enthält diese Variable eine leere Zeichenfolge.<br /><br /> Diese Informationen werden vom SQL_DESC_SS_XML_SCHEMACOLLECTION_NAME-Datensatzfeld vom IRD zurückgegeben, das ein Lese-/Schreibfeld ist.|  
  
 Außerdem wurden in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] neue treiberspezifische Deskriptorfelder eingeführt, um zusätzliche Informationen für entweder einen benutzerdefinierten Spaltentyp (UDT) eines Resultsets oder für einen UDT-Parameter einer gespeicherten Prozedur oder einer parametrisierten Abfrage bereitzustellen. Diese Eigenschaften erfordern keine Anführungszeichen oder ein Escapezeichen, wenn sie nicht-alphanumerische Zeichen enthalten. In der folgenden Tabelle sind diese neuen Deskriptorfelder aufgelistet:  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_UDT_CATALOG_NAME|CharacterAttributePtr|Der Name des Katalogs, der den UDT enthält.|  
|SQL_CA_SS_UDT_SCHEMA_NAME|CharacterAttributePtr|Der Name des Schemas, die den UDT enthält.|  
|SQL_CA_SS_UDT_TYPE_NAME|CharacterAttributePtr|Der Name des UDT.|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|CharacterAttributePtr|Die Assembly qualifizierte Name des UDT.|  
  
 Der vorhandene Deskriptorfeldbezeichner SQL_DESC_TYPE_NAME wird verwendet, um den Namen des UDTs anzugeben. Das SQL_DESC_TYPE-Feld für eine UDT-Typspalte ist SQL_SS_UDT.  
  
## <a name="sqlcolattribute-support-for-enhanced-date-and-time-features"></a>SQLColAttribute-Unterstützung für erweiterte Funktionen zu Datum und Uhrzeit  
 Für die Werte für Datum/Uhrzeit-Typen zurückgegeben wird, finden Sie im Abschnitt "Informationen zurückgegeben, in IRD-Feldern" in [Parameter- und Ergebnismetadaten](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolattribute-support-for-large-clr-udts"></a>SQLColAttribute-Unterstützung für große CLR-UDTs  
 **SQLColAttribute** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolattribute-support-for-sparse-columns"></a>SQLColAttribute-Unterstützung für Spalten mit geringer Dichte  
 SQLColAttribute fragt die neue Implementierung Zeile (IRD) Deskriptorfeld, sql_ca_ss_is_column_set ab, um zu bestimmen, ob eine Spalte ist eine **Column_set** Spalte.  
  
 Weitere Informationen finden Sie unter [Sparse Columns Support &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLColAttribute-Funktion](http://go.microsoft.com/fwlink/?LinkId=59334)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
  
