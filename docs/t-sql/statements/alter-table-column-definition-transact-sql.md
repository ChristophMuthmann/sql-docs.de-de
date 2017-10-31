---
title: Column_definition (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- column_definition
- column_definition_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column_definition
- ALTER TABLE statement
- column properties [SQL Server]
- column definitions [SQL Server]
ms.assetid: a1742649-ca29-4d9b-9975-661cdbf18f78
caps.latest.revision: 78
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c63dcea3473198ded46ebf84053fa9d8b36330f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-columndefinition-transact-sql"></a>ALTER TABLE Column_definition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt die Eigenschaften einer Spalte, die in einer Tabelle hinzugefügt werden, mithilfe von [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
column_name <data_type>  
[ FILESTREAM ]  
[ COLLATE collation_name ]   
[ NULL | NOT NULL ]  
[   
    [ CONSTRAINT constraint_name ] DEFAULT constant_expression [ WITH VALUES ]   
    | IDENTITY [ ( seed , increment ) ] [ NOT FOR REPLICATION ]   
]  
[ ROWGUIDCOL ]   
[ SPARSE ]   
[ ENCRYPTED WITH  
  ( COLUMN_ENCRYPTION_KEY = key_name ,  
      ENCRYPTION_TYPE = { DETERMINISTIC | RANDOMIZED } ,   
      ALGORITHM =  'AEAD_AES_256_CBC_HMAC_SHA_256'   
  ) ]  
[ MASKED WITH ( FUNCTION = ' mask_function ') ]  
[ <column_constraint> [ ...n ] ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
        [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
[ CONSTRAINT constraint_name ]   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH FILLFACTOR = fillfactor    
          | WITH ( < index_option > [ , ...n ] )   
        ]   
        [ ON { partition_scheme_name ( partition_column_name )   
            | filegroup | "default" } ]  
  | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
  | CHECK [ NOT FOR REPLICATION ] ( logical_expression )   
}  
```  
  
## <a name="arguments"></a>Argumente  
 *Spaltenname*  
 Der Name der Spalte, die geändert, hinzugefügt oder gelöscht werden soll. *Column_name* kann zwischen 1 und 128 Zeichen bestehen. Bei neuen Spalten, die mit einem Timestamp-Datentyp erstellt *Column_name* kann ausgelassen werden. Wenn kein *Column_name* für angegeben wird eine **Zeitstempel** Spalte mit dem Datentyp, den Namen **Zeitstempel** verwendet wird.  
  
 [ *Type_schema_name***.** ] *Type_name*  
 Der Datentyp für die hinzugefügte Spalte und das Schema, zu dem er gehört.  
  
 *TYPE_NAME* sind möglich:  
  
-   Ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Systemdatentyp.  
  
-   Ein Aliasdatentyp, der auf einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp basiert. Aliasdatentypen müssen mithilfe von CREATE TYPE erstellt werden, damit sie in einer Tabellendefinition verwendet werden können.  
  
-   Ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] einen benutzerdefinierten Typ und das Schema, zu dem er gehört. Ein benutzerdefinierter [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datentyp muss mithilfe von CREATE TYPE erstellt werden, bevor er in einer Tabellendefinition verwendet werden kann.  
  
 Wenn *Type_schema_name* nicht angegeben wird, die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] Verweise *Type_name* in der folgenden Reihenfolge:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentyp.  
  
-   Das Standardschema des aktuellen Benutzers in der aktuellen Datenbank  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
*precision*  
 Die Genauigkeit für den angegebenen Datentyp. Weitere Informationen über gültige Genauigkeitswerte finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
*scale*  
 Die Dezimalstellen für den angegebenen Datentyp. Weitere Informationen zu gültigen Dezimalstellenwerten finden Sie unter [mit einfacher Genauigkeit, Dezimalstellen und Länge &#40; Transact-SQL &#41; ](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
**Max**  
 Gilt nur für die **Varchar**, **Nvarchar**, und **Varbinary** Datentypen. Diese Datentypen werden zum Speichern von Zeichen- und Binärdaten mit einer Länge von 2^31 Byte und Unicode-Daten mit einer Länge von 2^30 Byte verwendet.  
  
**INHALT**  
 Gibt an, dass jede Instanz die **Xml** -Datentyp im *Column_name* können mehrere Elemente der obersten Ebene bilden. CONTENT gilt nur für die **Xml** Daten geben, und kann angegeben werden, nur dann, wenn *Xml_schema_collection* ist ebenfalls angegeben. Fehlt die Angabe, ist CONTENT das Standardverhalten.  
  
DOCUMENT  
 Gibt an, dass jede Instanz die **Xml** -Datentyp im *Column_name* kann nur ein Element der obersten Ebene umfassen. DOCUMENT gilt nur für die **Xml** Daten geben, und kann angegeben werden, nur dann, wenn *Xml_schema_collection* ist ebenfalls angegeben.  
  
 *xml_schema_collection*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gilt nur für die **Xml** Datentyp für den Typ eine XML-schemaauflistung zuordnen. Vor der Eingabe einer **Xml** Spalte an ein Schema, das Schema muss zuerst erstellt werden in der Datenbank mithilfe von [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md).  
  
FILESTREAM  
 Gibt optional das FILESTREAM-Speicherattribut für die Spalte mit einem *Type_name* von **varbinary(max)**.  
  
 Wenn FILESTREAM für eine Spalte angegeben wird, muss die Tabelle auch eine Spalte haben die **"uniqueidentifier"** -Datentyp, der das ROWGUIDCOL-Attribut enthält. Diese Spalte darf keine NULL-Werte zulassen und muss eine UNIQUE- oder eine PRIMARY KEY-Einschränkung für einzelne Spalten enthalten. Der GUID-Wert für die Spalte muss angegeben werden, entweder von einer Anwendung, wenn Daten eingefügt werden, oder durch eine DEFAULT-Einschränkung, die die NEWID ()-Funktion verwendet.  
  
 Die Spalte ROWGUIDCOL kann nicht gelöscht, und die zugehörigen Einschränkungen können nicht geändert werden, wenn für die Tabelle eine FILESTREAM-Spalte definiert ist. Die Spalte ROWGUIDCOL kann nur gelöscht werden, nachdem die letzte FILESTREAM-Spalte gelöscht wurde.  
  
 Wenn das FILESTREAM-Speicherattribut für eine Spalte angegeben wird, werden alle Werte dieser Spalte in einem FILESTREAM-Datencontainer des Dateisystems gespeichert.  
  
 Ein Beispiel für die Verwendung von Spaltendefinitionen veranschaulicht, finden Sie unter [FILESTREAM &#40; SQLServer &#41; ](../../relational-databases/blob/filestream-sql-server.md).  
  
COLLATE *Collation_name*  
 Gibt die Sortierung der Spalte an. Wenn keine Sortierung angegeben ist, wird der Spalte die Standardsortierung der Datenbank zugewiesen. Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname sein. Eine Liste und Weitere Informationen finden Sie unter [Windows-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/windows-collation-name-transact-sql.md) und [SQL Server-Sortierungsname &#40; Transact-SQL &#41; ](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 Die COLLATE-Klausel kann verwendet werden, nur die Sortierungen von Spalten an den **Char**, **Varchar**, **Nchar**, und **Nvarchar** -Datentypen .  
  
 Weitere Informationen zur COLLATE-Klausel finden Sie unter [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 NULL | NOT NULL  
 Bestimmt, ob Nullwerte in der Spalte zulässig sind. NULL ist genau genommen keine Einschränkung, kann jedoch wie NOT NULL verwendet werden.  
  
[Einschränkung *Constraint_name* ]  
 Gibt den Anfang einer DEFAULT-Wertdefinition an. Um die Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechtzuerhalten, ist es möglich, einer DEFAULT-Definition einen Einschränkungsnamen zuzuweisen. *Constraint_name* muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md), außer dass der Name nicht werden mit einem Nummernzeichen gestartet (#). Wenn *Constraint_name* nicht angegeben ist, wird ein vom System generierter Name der DEFAULT-Definition zugewiesen ist.  
  
DEFAULT  
 Ein Schlüsselwort, das den Standardwert für die Spalte angibt. DEFAULT-Definitionen können verwendet werden, um Werte für eine neue Spalte in den vorhandenen Datenzeilen bereitzustellen. DEFAULT-Definitionen können nicht angewendet werden, um **Zeitstempel** Spalten oder Spalten mit einer IDENTITY-Eigenschaft. Wenn ein Standardwert für eine UDT-Spalte angegeben wird, muss der Typ eine implizite Konvertierung von unterstützen *Constant_expression* in den benutzerdefinierten Typ.  
  
*constant_expression*  
 Ist ein Literalwert, ein NULL-Wert oder eine Systemfunktion, die als der Standardwert für die Spalte verwendet. Bei Verwendung in Verbindung mit einer Spalte definiert werden, der eine [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] den benutzerdefinierten Typ muss die Implementierung des Typs eine implizite Konvertierung von unterstützen die *Constant_expression* in den benutzerdefinierten Typ.  
  
WITH VALUES  
 Gibt an, dass der Wert für ein bestimmtes im STANDARDMODUS *Constant_expression* in einer neuen, zu vorhandenen Zeilen hinzugefügten Spalte gespeichert ist. Wenn die hinzugefügte Spalte NULL-Werte zulässt und WITH VALUES angegeben ist, wird der Standardwert in der neuen, der vorhandenen Zeilen hinzugefügten Spalte gespeichert. Ist WITH VALUES für Spalten, die NULL-Werte zulassen, nicht angegeben, wird der Wert NULL in der neuen Spalte in vorhandenen Zeilen gespeichert. Wenn die neue Spalte keine NULL-Werte zulässt, wird der Standardwert in neuen Zeilen gespeichert, unabhängig davon, ob WITH VALUES angegeben ist.  
  
IDENTITY  
 Gibt an, dass die neue Spalte eine Identitätsspalte ist. Von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] wird ein eindeutiger, inkrementeller Wert für die Spalte bereitgestellt. Wenn Sie vorhandenen Tabellen Bezeichnerspalten hinzufügen, werden die ID-Nummern mit den Ausgangswerten und den inkrementellen Werten den vorhandenen Zeilen der Tabelle hinzugefügt. Die Reihenfolge, in der die Zeilen aktualisiert werden, ist nicht sichergestellt. Auch für alle neu hinzugefügten Zeilen werden ID-Nummern generiert.  
  
 Identitätsspalten werden in der Regel in Verbindung mit PRIMARY KEY-Einschränkungen verwendet, um als eindeutiger Zeilenbezeichner für die Tabelle zu dienen. Die IDENTITY-Eigenschaft kann zugewiesen werden, um eine **"tinyint"**, **"smallint"**, **Int**, **"bigint"**, **decimal(p,0)**, oder **numeric(p,0)** Spalte. Es kann nur eine Identitätsspalte pro Tabelle erstellt werden. Das DEFAULT-Schlüsselwort und gebundene Standardwerte können bei einer Identitätsspalte nicht verwendet werden. Entweder müssen sowohl Ausgangswert als auch Inkrement oder keines von beiden angegeben werden. Wenn keine Angabe gemacht wird, ist der Standardwert (1,1).  
  
> [!NOTE]  
>  Es ist nicht möglich, einer vorhandenen Tabellenspalte die IDENTITY-Eigenschaft hinzuzufügen.  
  
 Das Hinzufügen einer Identitätsspalte zu einer veröffentlichten Spalte wird nicht unterstützt, da dies beim Replizieren der Spalte auf den Abonnenten zu einer Nichtkonvergenz führen kann. Die Werte in der Identitätsspalte auf dem Verleger richten sich nach der Ordnung, in der die Zeilen für die betreffende Tabelle physisch gespeichert sind. Die Zeilen sind auf dem Abonnenten möglicherweise anders gespeichert, sodass der Wert für die Identitätsspalte für dieselben Zeilen variieren kann.  
  
 Verwenden Sie zum Deaktivieren der IDENTITY-Eigenschaft einer Spalte können Sie die einzufügenden Werte explizit [SET IDENTITY_INSERT](../../t-sql/statements/set-identity-insert-transact-sql.md).  
  
*Startwert*  
 Für die erste Zeile verwendete Wert wird in die Tabelle geladen werden.  
  
*Inkrement*  
 Der Inkrementwert, der zum Identitätswert der zuvor geladenen Zeile addiert wird.  
  
NOT FOR REPLICATION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Kann für die IDENTITY-Eigenschaft angegeben werden. Wenn diese Klausel für die IDENTITY-Eigenschaft angegeben ist, werden Werte in Identitätsspalten nicht inkrementiert, wenn Replikations-Agents Einfügevorgänge ausführen.  
  
ROWGUIDCOL  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt an, dass die Spalte eine Spalte mit für alle Zeilen global eindeutigen Bezeichnern ist. ROWGUIDCOL kann nur zugewiesen werden, um eine **"uniqueidentifier"** Spalte, und nur ein **"uniqueidentifier"** -Spalte pro Tabelle kann als ROWGUIDCOL-Spalte gekennzeichnet werden. ROWGUIDCOL kann keinen Spalten des benutzerdefinierten Datentyps zugewiesen werden.  
  
 ROWGUIDCOL erzwingt keine Eindeutigkeit der in der Spalte gespeicherten Werte. ROWGUIDCOL generiert auch nicht automatisch Werte für neue Zeilen, die in die Tabelle eingefügt werden. Verwenden Sie entweder die NEWID-Funktion in INSERT-Anweisungen, oder geben Sie die NEWID-Funktion als Standard für die Spalte an, um eindeutige Werte für jede Spalte zu generieren. Weitere Informationen finden Sie unter [NEWID &#40; Transact-SQL &#41; ](../../t-sql/functions/newid-transact-sql.md)und [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
SPARSE  
 Gibt an, dass die Spalte eine Spalte mit geringer Dichte ist. Der Speicher für Spalten mit geringer Dichte ist für NULL-Werte optimiert. Spalten mit geringer Dichte können nicht als NOT NULL festgelegt werden. Zusätzliche Einschränkungen und Weitere Informationen zu Spalten mit geringer Dichte finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
\<Column_constraint >  
 Die Definitionen der spalteneinschränkungsargumente finden Sie unter [Column_constraint &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-column-constraint-transact-sql.md).  
  
 MIT VERSCHLÜSSELT  
 Gibt an, zum Verschlüsseln verwendete Spalten mithilfe der [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) Funktion.  
  
 COLUMN_ENCRYPTION_KEY = *Key_name*  
 Gibt den spaltenverschlüsselungsschlüssel an. Weitere Informationen finden Sie unter [CREATE COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-column-encryption-key-transact-sql.md).  
  
ENCRYPTION_TYPE = {DETERMINISTISCH | ZUFÄLLIGE}  
 Die**deterministische Verschlüsselung** verwendet eine Methode, die immer denselben verschlüsselten Wert für jeden angegebenen Klartextwert generiert. Verwendung der deterministischen Verschlüsselung ermöglicht die Suche mithilfe der Gleichheitsvergleich, gruppieren und das Verknüpfen von Tabellen mit gleichheitsverknüpfung basierend auf verschlüsselten Werten jedoch erlaubt Sie nicht autorisierte Benutzer Informationen zu verschlüsselten Werten erraten, indem Sie Muster untersuchen die verschlüsselte Spalte. Verknüpfen von zwei Tabellen auf deterministisch verschlüsselten Spalten ist nur möglich, wenn beide Spalten mit demselben spaltenverschlüsselungsschlüssel verschlüsselt sind. Die deterministische Verschlüsselung muss eine Spaltensortierung mit einer binary2-Sortierreihenfolge für Zeichenspalten verwenden.  
  
 Die**zufällige Verschlüsselung** verwendet eine Methode, die Daten in einer weniger vorhersagbaren Weise verschlüsselt. Die zufällige Verschlüsselung ist sicherer, verhindert aber die Gleichheitssuche, Gruppierung und Verknüpfung für verschlüsselte Spalten. Nach dem Zufallsprinzip Spalten können nicht indiziert werden.  
  
 Verwenden Sie die deterministische Verschlüsselung für Spalten für die Suchparameter oder gruppierungsparameter, z. B. eine Personalausweisnummer. Verwenden nach dem Zufallsprinzip, für die Daten z. B. eine Kreditkartennummer, die nicht mit anderen Datensätzen gruppiert, oder zum Verknüpfen von Tabellen und die nicht für durchsucht wird, da Sie andere Spalten (z. B. eine Transaktionsnummer) verwenden, um die Zeile zu finden, die was die enthält das verschlüsselte der betreffenden Spalte.  
  
 Spalten müssen einen qualifizierenden Datentyp aufweisen.  
  
ALGORITHMUS  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
Muss **'AEAD_AES_256_CBC_HMAC_SHA_256'**.  
  
 Weitere Informationen einschließlich Feature Einschränkungen finden Sie unter [Always Encrypted &#40; Datenbankmodul &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
  
   
MASKIERTE hinzufügen mit (Funktion = " *Mask_function* ")  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt an, einer dynamischen Datenmaske. *Mask_function* ist der Name der Maskierungsfunktion mit den entsprechenden Parametern. Die folgenden Funktionen sind verfügbar:  
  
-   default()  
  
-   Email()  
  
-   partial()  
  
-   Zufallsvariable()  
  
 Funktionsparameter, finden Sie unter [Dynamic Data Masking](../../relational-databases/security/dynamic-data-masking.md).  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Spalte hinzugefügt wird, dass eine **"uniqueidentifier"** -Datentyp, sie können definiert werden, hat den Standardwert, der die NEWID()-Funktion verwendet, um die eindeutigen Bezeichnerwerte in der neuen Spalte für jede vorhandene Zeile in der Tabelle bereitzustellen.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] erzwingt keine Reihenfolge für die Angabe von DEFAULT, IDENTITY, ROWGUIDCOL oder Spalteneinschränkungen in einer Spaltendefinition.  
  
 Die ALTER TABLE-Anweisung ergibt einen Fehler, wenn die Größe der Datenzeile durch Hinzufügen der Spalte 8060 Bytes überschreitet.  
  
## <a name="examples"></a>Beispiele  
 Beispiele finden Sie unter [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  

