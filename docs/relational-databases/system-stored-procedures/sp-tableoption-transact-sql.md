---
title: Sp_tableoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c6bfbbed0bdb29be74871fcc62a76fce2f3555d5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sptableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Legt Optionswerte für benutzerdefinierte Tabellen fest. Sp_tableoption kann verwendet werden, zum Steuern des Verhaltens in Zeilen für Tabellen mit **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml**, **Text**, **Ntext**, **Image**, oder großen benutzerdefinierten Typspalten.  
  
> [!IMPORTANT]  
>  Die Funktion text in row wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Zum Speichern von Daten mit umfangreichen Werten, es wird empfohlen, die Verwendung der **varchar(max)**, **nvarchar(max)** und **varbinary(max)** Datentypen.  
  

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>Argumente  
 [ @TableNamePattern =] '*Tabelle*"  
 Der qualifizierte oder nicht qualifizierte Name einer benutzerdefinierten Datenbanktabelle. Bei Angabe eines voll gekennzeichneten Tabellennamens (einschließlich eines Datenbanknamens) muss der Datenbankname der Name der aktuellen Datenbank sein. Tabellenoptionen für mehrere Tabellen können nicht gleichzeitig festgelegt werden. *Tabelle* ist **nvarchar(776)**, hat keinen Standardwert.  
  
 [ @OptionName =] '*Option_name*"  
 Der Name einer Tabellenoption. *Option_name* ist **varchar(35)**, hat keinen Standardwert NULL. *Option_name* kann einen der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|table lock on bulk load|Eine deaktivierte Option (Standard) führt dazu, dass der Massenladevorgang auf benutzerdefinierten Tabellen Zeilensperren erhält. Wenn diese Option aktiviert ist, erhalten die Massenladevorgänge auf benutzerdefinierten Tabellen eine Massenupdatesperre.|  
|insert row lock|Nicht mehr unterstützt.<br /><br /> Diese Option wirkt sich nicht auf das Sperrverhalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus und ist nur aus Gründen der Kompatibilität mit vorhandenen Skripts und Prozeduren enthalten.|  
|text in row|Beim Wert OFF oder 0 (deaktivierte Option, Standard) wird das aktuelle Verhalten nicht geändert, und es gibt keine BLOBs in Zeilen.<br /><br /> Wenn angegeben und @OptionValue ist ON (aktiviert) oder einen ganzzahligen Wert von 24 bis 7000 aufweist, werden neue **Text**, **Ntext**, oder **Image** -Zeichenfolgen direkt in der Datenzeile gespeichert. Alle vorhandenen BLOB-Daten (BLOB: **Text**, **Ntext**, oder **Image** Daten) wird für den Text im Zeilenformat geändert werden, wenn der BLOB-Wert aktualisiert wird. Weitere Informationen finden Sie in den Hinweisen.|  
|LARGE VALUE TYPES OUT OF ROW|1 = **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml** und umfangreichen benutzerdefinierten Typ (UDT) Spalten in der Tabelle gespeichert sind außerhalb von Zeilen mit einem 16-Byte-Zeiger auf den Stamm.<br /><br /> 0 = **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **Xml** und große UDT-Werte werden direkt in der Datenzeile bis zu einem Höchstwert gespeichert. von 8.000 Bytes und so lange wie der Wert in den Datensatz passen. Überschreitet der Wert die Größe des Datensatzes, wird ein Zeiger innerhalb der Zeilen gespeichert, während der Rest außerhalb der Zeilen im LOB-Speicherbereich gespeichert wird. Der Standardwert ist 0 (null).<br /><br /> Großer benutzerdefinierter Typ (UDT) gilt für: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. <br /><br /> Verwenden Sie die TEXTIMAGE_ON-Option von [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) zum Angeben eines Speicherorts für die Speicherung großer Datentypen. |  
|vardecimal-Speicherformat|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Bei TRUE, ON oder 1 ist die festgelegte Tabelle für das vardecimal-Speicherformat aktiviert. Bei FALSE, OFF oder 0 ist die Tabelle für das vardecimal-Speicherformat nicht aktiviert. Das Vardecimal-Speicherformat kann aktiviert werden, nur, wenn die Datenbank das Vardecimal-Speicherformat aktiviert wurde, mithilfe von [Sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md). In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher, **Vardecimal** Speicherformat ist veraltet. Verwenden Sie stattdessen die ROW-Komprimierung. Weitere Informationen finden Sie unter [Data Compression](../../relational-databases/data-compression/data-compression.md). Der Standardwert ist 0 (null).|  
  
 [ @OptionValue =] '*Wert*"  
 Ist, ob die *Option_name* ist aktiviert (TRUE, ON oder 1) oder deaktiviert (FALSE, OFF oder 0). *Wert* ist **varchar(12)**, hat keinen Standardwert. *Wert* wird Groß-/Kleinschreibung nicht beachtet.  
  
 Gültige Werte für die text in row-Option sind: 0, ON, OFF oder eine Ganzzahl zwischen 24 und 7000. Wenn *Wert* ist, gibt der Standardgrenzwert 256 Bytes.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder eine Fehlernummer (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_tableoption kann nur verwendet werden, um die Optionswerte für benutzerdefinierte Tabellen festzulegen. Verwenden Sie OBJECTPROPERTY, um Tabelleneigenschaften anzuzeigen.  
  
 Die text in row-Option von sp_tableoption kann nur für Tabellen aktiviert oder deaktiviert werden, die Textspalten enthalten. Wenn die Tabelle nicht über eine Textspalte verfügt, löst [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Fehler aus.  
  
 Wenn die Text in Row-Option aktiviert ist, die @OptionValue Parameter kann Benutzer in einer Zeile für ein BLOB zu speichernde Maximalgröße angeben. Der Standardwert ist 256 Bytes. Gültige Werte sind 24 bis 7000 Bytes.  
  
 **Text**, **Ntext**, oder **Image** Zeichenfolgen werden in der Datenzeile gespeichert, wenn Folgendes zutrifft:  
  
-   text in row ist aktiviert.  
  
-   Die Länge der Zeichenfolge ist kürzer als die im angegebenen Grenzwert @OptionValue  
  
-   Es steht genügend Speicherplatz in der Datenzeile zur Verfügung.  
  
 Wenn BLOB-Zeichenfolgen in der Datenzeile gespeichert werden, lesen und Schreiben der **Text**, **Ntext**, oder **Image** Zeichenfolgen können so schnell wie das Lesen oder Schreiben von Zeichenfolgen und Binärzeichenfolgen sein. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann nicht auf separate Seiten zugreifen, um die BLOB-Zeichenfolge zu lesen oder zu schreiben.  
  
 Wenn eine **Text**, **Ntext**, oder **Image** Zeichenfolge ist größer als die angegebenen Grenzwert oder den verfügbaren Speicherplatz in der Zeile, die Zeiger werden stattdessen in der Zeile gespeichert. Die Bedingungen zum Speichern der BLOB-Zeichenfolgen sind jedoch trotzdem gültig: Für die Zeiger muss genügend Speicherplatz in der Datenzeile vorhanden sein.  
  
 BLOB-Zeichenfolgen und -Zeiger, die in der Zeile einer Tabelle gespeichert werden, werden ähnlich wie Zeichenfolgen mit variabler Länge behandelt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet nur so viele Bytes, wie erforderlich sind, um die Zeichenfolge oder den Zeiger zu speichern.  
  
 Vorhandene BLOB-Zeichenfolgen werden nicht sofort konvertiert, wenn text in row aktiviert ist. Die Zeichenfolgen werden erst konvertiert, wenn sie aktualisiert werden. Ebenso, wenn der Text in Row-Option-Grenzwert erhöht die **Text**, **Ntext**, oder **Image** Zeichenfolgen bereits in der Datenzeile werden nicht konvertiert werden, um den neuen Grenzwert entsprechen bis zum Zeitpunkt werden sie aktualisiert werden.  
  
> [!NOTE]  
>  Wenn die text in row-Option deaktiviert oder der Grenzwert für diese Option verringert wird, müssen alle BLOBs konvertiert werden. Dieser Vorgang kann je nach der Anzahl der zu konvertierenden BLOB-Zeichenfolgen viel Zeit in Anspruch nehmen. Während des Konvertierungsvorgangs ist die Tabelle gesperrt.  
  
 Für eine Tabellenvariable sowie eine Funktion, die eine Tabellenvariable zurückgibt, ist die text in row-Option automatisch mit dem inline limit-Standardwert von 256 aktiviert. Diese Option kann nicht geändert werden.  
  
 Die Text in Row-Option unterstützt die Funktionen TEXTPTR, WRITETEXT, UPDATETEXT und READTEXT. Benutzer können Teile eines BLOBs mit der SUBSTRING()-Funktion lesen, sollten jedoch berücksichtigen, dass Textzeiger in Zeilen andere Grenzwerte für Dauer und Anzahl haben als andere Textzeiger.  
  
 Wenn Sie eine Tabelle vom vardecimal-Speicherformat zurück in das normale decimal-Speicherformat konvertieren möchten, muss sich die Datenbank im SIMPLE-Wiederherstellungsmodus befinden. Durch das Ändern des Wiederherstellungsmodus wird die Protokollkette für Sicherungszwecke unterbrochen. Daher sollten Sie eine vollständige Datenbanksicherung erstellen, nachdem Sie das vardecimal-Speicherformat aus einer Tabelle entfernt haben.  
  
 Wenn Sie eine vorhandene LOB-Datentypspalte (Text, Ntext oder Image), um kleine bis mittelgroße große Werttypen (varchar(max), nvarchar(max) oder varbinary(max)), und führen Sie die meisten Anweisungen nicht die große werttypspalten in Ihrer Umgebung verweisen konvertieren, sollten Sie Ändern von **Large_value_types_out_of_row** auf **1** um eine optimale Leistung zu erhalten. Wenn die **Large_value_types_out_of_row** Optionswert geändert wird, werden vorhandene varchar(max), nvarchar(max), varbinary(max) und XML-Werte werden nicht sofort konvertiert. Der Speicherung der Zeichenfolgen ändert sich, wenn diese anschließend aktualisiert werden. Alle neuen Werte, die in eine Tabelle eingefügt werden, werden gemäß der aktivierten Tabellenoption gespeichert. Sofortige Ergebnisse erzielen Sie, entweder erstellen Sie eine Kopie der Daten und füllen Sie die Tabelle nach dem Ändern der **Large_value_types_out_of_row** festlegen oder aktualisieren Sie jede kleine bis mittelgroße umfangreichen Typen auf sich selbst, damit die Speicherung der Zeichenfolgen wird geändert, mit der Tabellenoption aktiviert. Erstellen Sie die Indizes für die Tabelle nach der Aktualisierung oder Neuauffüllung neu, um die Tabelle zu komprimieren. 
    
  
## <a name="permissions"></a>Berechtigungen  
 Für die Ausführung von sp_tableoption ist die ALTER-Berechtigung für die Tabelle erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>A. Speichern von XML-Daten außerhalb der Zeile  
 Das folgende Beispiel gibt an, dass die **Xml** Daten in der `HumanResources.JobCandidate` Tabelle außerhalb von Zeilen gespeichert werden.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. Aktivieren des vardecimal-Speicherformats für eine Tabelle  
 Im folgende Beispiel ändert die `Production.WorkOrderRouting` Tabelle zum Speichern der `decimal` -Datentyp in der `vardecimal` Speicherformat.  

```sql  
USE master;  
GO  
-- The database must be enabled for vardecimal storage format  
-- before a table can be enabled for vardecimal storage format  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'Production.WorkOrderRouting',   
   'vardecimal storage format', 'ON';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
