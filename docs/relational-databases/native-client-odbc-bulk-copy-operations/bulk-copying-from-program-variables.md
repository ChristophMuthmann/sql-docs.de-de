---
title: Massenkopieren aus Programmvariablen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5e0bcb033e4e99bdba8dc7167d3823e103c9cfd9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="bulk-copying-from-program-variables"></a>Massenkopieren aus Programmvariablen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Sie können Massenkopiervorgänge direkt aus Programmvariablen durchführen. Nachdem Sie Variablen zum Speichern der Daten für eine Zeile und der Aufruf [Bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) rufen Sie zum Starten des Massenkopiervorgangs [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) für jede Spalte an den Speicherort und Format der Programmvariablen zugeordnet werden soll mit der Spalte. Füllen Sie jede Variable mit Daten, und rufen dann [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) auf eine Datenzeile an den Server gesendet. Wiederholen Sie den Prozess Variablen füllen und Aufrufen von **Bcp_sendrow** aufrufen, bis alle Zeilen an den Server gesendet wurden, klicken Sie dann [Bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) um anzugeben, dass der Vorgang abgeschlossen ist.  
  
 Die **Bcp_bind *** pData* Parameter enthält die Adresse der Variablen an die Spalte gebunden wird. Die Daten für die einzelnen Spalten können auf zweierlei Weise gespeichert werden:  
  
-   Zuordnen einer Variable für die Daten.  
  
-   Zuordnen einer Indikatorvariable, unmittelbar gefolgt von der Datenvariable.  
  
 Die Indikatorvariable gibt die Datenlänge für Spalten mit variabler Länge an und zeigt gegebenenfalls an, dass NULL-Werte für die Spalte zulässig sind. Wenn nur eine Datenvariable verwendet wird, klicken Sie dann die Adresse dieser Variablen wird gespeichert der **Bcp_bind *** pData* Parameter. Wenn eine Indikatorvariable verwendet wird, wird die Adresse dieser Indikatorvariablen gespeichert, der **Bcp_bind *** pData* Parameter. Die Massenkopierfunktionen berechnen den Speicherort der Datenvariablen durch Hinzufügen der **Bcp_bind *** CbIndicator* und *pData* Parameter.  
  
 **Bcp_bind** unterstützt drei Methoden für den Umgang mit Daten variabler Länge:  
  
-   Verwendung *CbData* mit nur einer Datenvariable. Platzieren Sie die Länge der Daten in *CbData*. Rufen Sie jedes Mal die Länge der Daten, die massenimportiert werden sollen, [Bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)zurücksetzen *CbData*. Wenn eine der anderen zwei Methoden verwendet wird, geben Sie SQL_VARLEN_DATA für *CbData*. Wenn alle Datenwerte, die eingegeben wird, für eine Spalte NULL sind, geben Sie SQL_NULL_DATA für *CbData*.  
  
-   Verwenden von Indikatorvariablen. Speichern Sie beim Verschieben des jeweiligen neuen Datenwerts in die Datenvariable die Länge des Werts in der Indikatorvariable. Wenn eine der anderen zwei Methoden verwendet wird, geben Sie 0 für *CbIndicator*.  
  
-   Verwenden von Abschlusszeichenzeigern. Laden der **Bcp_bind *** pTerm* Parameter mit der Adresse des Bitmusters, das die Daten beendet. Wenn eine der anderen zwei Methoden verwendet wird, geben Sie NULL für *pTerm*.  
  
 Alle drei genannten Methoden können verwendet werden, auf dem gleichen **Bcp_bind** aufzurufen, in diesem Fall wird die Spezifikation, die die kleinste Menge der zu kopierenden führt verwendet.  
  
 Die **Bcp_bind *** Typ* Parameter verwendet DB-Library-Datentypbezeichner, nicht ODBC-Datentypbezeichner. DB-Library-Datentypbezeichner werden in sqlncli.h zur Verwendung mit der ODBC definiert **Bcp_bind** Funktion.  
  
 Funktionen zum Massenkopieren unterstützen nicht alle ODBC C-Datentypen. Die Funktionen zum Massenkopieren unterstützen z. B. nicht die ODBC SQL_C_TYPE_TIMESTAMP-Struktur, verwenden Sie daher [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) oder [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) um ODBC SQL_TYPE_TIMESTAMP-Daten in eine SQL_C_CHAR-Variable zu konvertieren. Wenn Sie anschließend mithilfe **Bcp_bind** mit einer *Typ* von SQLCHARACTER die Variable zum Binden einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **"DateTime"** Spalte, die Funktionen zum Massenkopieren konvertiert die timestampescapeklausel der Zeichenvariablen in das geeignete Datetime-Format.  
  
 Die folgende Tabelle enthält die empfohlenen Datentypen für Zuordnungen eines ODBC SQL-Datentyps zu einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp.  
  
|ODBC SQL-Datentyp|ODBC C-Datentyp|Bcp_bind *Typ* Parameter|SQL Server-Datentyp|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**character**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **unterschiedliche Zeichen**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**text**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **DEC**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (mit Vorzeichen)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (ohne Vorzeichen)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (mit Vorzeichen)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (ohne Vorzeichen)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (mit Vorzeichen)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (ohne Vorzeichen)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **DEC**|  
|SQL_BIGINT (mit und ohne Vorzeichen)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binary**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **Binary varying**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**image**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist nicht signiert haben **"tinyint"** ohne Vorzeichen **"smallint"**, oder ohne Vorzeichen **Int** Datentypen. Um den Verlust von Datenwerten zu vermeiden, beim Migrieren dieser Datentypen, erstellen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle mit dem nächstgrößeren ganzzahligen Datentyp. Um zu verhindern, dass Benutzer später Werte außerhalb des für den ursprünglichen Datentyp zulässigen Bereichs hinzufügen, wenden Sie eine Regel auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Spalte an, mit der die zulässigen Werte entsprechend eingeschränkt werden:  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Interval-Datentypen unterstützt nicht direkt. Eine Anwendung kann jedoch intervallescapesequenzen speichern, als Zeichenfolgen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zeichenspalte. Die Anwendung kann sie zur späteren Verwendung lesen, sie können aber nicht in [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwendet werden.  
  
 Die Funktionen zum Massenkopieren verwendet werden können, zum schnellen Laden von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die aus einer ODBC-Datenquelle gelesen wurden. Verwenden Sie [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md) verwenden, um die Spalten eines Resultsets an Programmvariablen zu binden, klicken Sie dann **Bcp_bind** dieselben Programmvariablen an einen Massenkopiervorgang zu binden. Aufrufen von [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) oder **SQLFetch** dann eine Zeile mit Daten aus der ODBC-Datenquelle abruft, in der Programmvariablen, und der Aufruf [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) Massenkopie der Daten aus den Programmvariablen nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Eine Anwendung kann mithilfe der [Bcp_colptr](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) Funktion jedes Mal, wenn er die Adresse der ursprünglich im angegebenen Datenvariable ändern muss die **Bcp_bind** *pData* Parameter. Eine Anwendung kann mithilfe der [Bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) Funktion jedes Mal, wenn der ursprünglich angegebene Datenlänge ändern muss die **Bcp_bind *** CbData* Parameter.  
  
 Sie können nicht gelesen werden Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Programmvariablen mit Massenkopiervorgängen besteht wie eine "Bcp_readrow"-Funktion keine Aktion. Sie können nur Daten aus der Anwendung an den Server senden.  
  
## <a name="see-also"></a>Siehe auch  
 [Durchführen von Massenkopiervorgängen &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
