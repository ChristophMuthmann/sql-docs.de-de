---
title: table_constraint (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table_constraint
ms.assetid: ac2a11e0-cc77-4e27-b107-4fe5bc6f5195
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 464ce13d973f975fe36a73f94ec9b12cd0eb1bf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-table-tableconstraint-transact-sql"></a>ALTER TABLE table_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Eigenschaften einer PRIMARY KEY-, UNIQUE-, FOREIGN KEY- oder CHECK-Einschränkung bzw. eine DEFAULT-Definition an, die einer Tabelle mit der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)-Anweisung hinzugefügt wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        (column [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        [ WITH ( <index_option>[ , ...n ] ) ]  
        [ ON { partition_scheme_name ( partition_column_name ... )  
          | filegroup | "default" } ]   
    | FOREIGN KEY   
        ( column [ ,...n ] )  
        REFERENCES referenced_table_name [ ( ref_column [ ,...n ] ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | DEFAULT constant_expression FOR column [ WITH VALUES ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>Argumente  
 CONSTRAINT  
 Gibt den Anfang einer PRIMARY KEY-, UNIQUE-, FOREIGN KEY- oder CHECK-Einschränkung oder einer DEFAULT-Definition an.  
  
 *constraint_name*  
 Der Name der Einschränkung. Einschränkungsnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen, wobei der Name nicht mit einem Nummernzeichen (#) beginnen darf. Wenn constraint_name nicht angegeben ist, vergibt das System einen Namen für die Einschränkung.  
  
 PRIMARY KEY  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) mithilfe eines eindeutigen Index erzwingt. Es kann nur eine PRIMARY KEY-Einschränkung für jede Tabelle erstellt werden.  
  
 UNIQUE  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) mit einem eindeutigen Index bietet.  
  
 CLUSTERED | NONCLUSTERED  
 Gibt an, dass ein gruppierter oder nicht gruppierter Index für die PRIMARY KEY- oder UNIQUE-Einschränkung erstellt wird. Für PRIMARY KEY-Einschränkungen wird standardmäßig CLUSTERED verwendet. Für UNIQUE-Einschränkungen wird standardmäßig NONCLUSTERED verwendet.  
  
 Wenn bereits eine gruppierte Einschränkung oder ein gruppierter Index für eine Tabelle vorhanden ist, kann CLUSTERED nicht angegeben werden. Wenn bereits eine gruppierte Einschränkung oder ein gruppierter Index für eine Tabelle vorhanden ist, wird für PRIMARY KEY-Einschränkungen standardmäßig NONCLUSTERED verwendet.  
  
 Die Datentypen **ntext**, **text**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml** und **image** können nicht als Spalten für einen Index angegeben werden.  
  
 *column*  
 Eine Spalte oder Liste von Spalten in Klammern, die in einer neuen Einschränkung verwendet werden.  
  
 [ **ASC** | DESC ]  
 Gibt die Reihenfolge an, in der die Spalte oder die Spalten, die in der Tabelleneinschränkung enthalten sind, sortiert werden. Die Standardeinstellung ist ASC.  
  
 WITH FILLFACTOR **=***fillfactor*  
 Gibt an, wie weit [!INCLUDE[ssDE](../../includes/ssde-md.md)] die einzelnen Indexseiten füllen soll, die zum Speichern der Indexdaten verwendet werden. Vom Benutzer angegebene *fillfactor*-Werte können Zahlen von 1 bis 100 sein. Wenn kein Wert angegeben ist, lautet der Standardwert 0.  
  
> [!IMPORTANT]  
>  Das Verwenden von WITH FILLFACTOR = *fillfactor* als einzige Indexoption, die für die PRIMARY KEY- oder UNIQUE-Einschränkungen gilt, wird hier aus Gründen der Abwärtskompatibilität weiterhin dokumentiert. In zukünftigen Releases wird dies jedoch nicht mehr der Fall sein. Andere Indexoptionen können in der [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md)-Klausel der ALTER TABLE-Anweisung angegeben werden.  
  
 ON { *partition_scheme_name***(***partition_column_name***)** | *filegroup*| **"**default**"** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Speicherort des Indexes an, der für die Einschränkung erstellt wurde. Wenn *partition_scheme_name* angegeben wird, wird der Index partitioniert, und die Partitionen werden den Dateigruppen zugeordnet, die durch *partition_scheme_name* angegeben sind. Wenn *filegroup* angegeben ist, wird der Index in der genannten Dateigruppe erstellt. Wenn **"**default**"** angegeben ist, oder wenn ON nicht für alle festgelegt ist, wird der Index in derselben Dateigruppe erstellt wie die Tabelle. Wenn ON beim Hinzufügen eines gruppierten Index für eine PRIMARY KEY- oder UNIQUE-Einschränkung angegeben ist, wird die gesamte Tabelle beim Erstellen des gruppierten Index in die angegebene Dateigruppe verschoben.  
  
 In diesem Zusammenhang ist DEFAULT kein Schlüsselwort. Stattdessen handelt es sich um einen Bezeichner für die Standarddateigruppe und muss begrenzt sein, wie in ON **"**default**"** oder ON **[**default**]**. Wenn **"**default**"** angegeben ist, muss die QUOTED_IDENTIFIER-Option in der aktuellen Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung.  
  
 FOREIGN KEY REFERENCES  
 Eine Einschränkung, die referenzielle Integrität für die Daten in der Spalte bereitstellt. FOREIGN KEY-Einschränkungen erfordern, dass jeder Wert in der Spalte in der angegebenen Spalte der Tabelle vorhanden ist, auf die verwiesen wird.  
  
 *referenced_table_name*  
 Die Tabelle, auf die die FOREIGN KEY-Einschränkung verweist.  
  
 *ref_column*  
 Eine Spalte oder Liste von Spalten in Klammern, auf die die neue FOREIGN KEY-Einschränkung verweist  
  
 ON DELETE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
 Gibt an, welche Aktion für eine Zeile der geänderten Tabelle ausgeführt werden soll, wenn diese Zeile eine referenzielle Beziehung hat, und die Zeile, auf die verwiesen wird, aus der übergeordneten Tabelle gelöscht wird. Der Standardwert ist NO ACTION.  
  
 NO ACTION  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] löst einen Fehler aus, und für die Aktion zum Löschen der Zeile in der übergeordneten Tabelle wird ein Rollback ausgeführt.  
  
 CASCADE  
 Wenn diese Zeile aus der übergeordneten Tabelle gelöscht wird, werden die entsprechenden Zeilen aus der verweisenden Tabelle gelöscht.  
  
 SET NULL  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf NULL festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle gelöscht wird. Die Fremdschlüsselspalten müssen NULL-Werte zulassen, um diese Einschränkung auszuführen.  
  
 SET DEFAULT  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf die Standardwerte festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle gelöscht wird. Alle Fremdschlüsselspalten müssen Standarddefinitionen aufweisen, damit diese Einschränkung ausgeführt wird. Wenn eine Spalte NULL-Werte zulässt, und es ist kein expliziter Standardwert festgelegt, wird NULL als der implizite Standardwert für die Spalte verwendet.  
  
 Geben Sie CASCADE nicht an, wenn die Tabelle in eine Mergeveröffentlichung einbezogen werden soll, bei der logische Datensätze verwendet werden. Weitere Informationen zu logischen Datensätzen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 ON DELETE CASCADE kann nicht definiert werden, wenn für ON DELETE bereits ein INSTEAD OF-Trigger für die geänderte Tabelle vorhanden ist.  
  
 In der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verfügt beispielsweise die **ProductVendor**-Tabelle über eine referenzielle Beziehung zu der **Vendor**-Tabelle. Der **ProductVendor.VendorID**-Fremdschlüssel verweist dabei auf den **Vendor.VendorID**-Primärschlüssel.  
  
 Wenn eine DELETE-Anweisung für eine Zeile in der **Vendor**-Tabelle ausgeführt wird, und eine ON DELETE CASCADE-Aktion für **ProductVendor.VendorID** festgelegt ist, sucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach mindestens einer abhängigen Zeile in der **ProductVendor**-Tabelle. Sind abhängige Zeilen vorhanden, werden zusätzlich zur Zeile, auf die in der **Vendor**-Tabelle verwiesen wird, die abhängigen Zeilen in der **ProductVendor**-Tabelle gelöscht.  
  
 Ist hingegen NO ACTION angegeben, löst [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus und führt ein Rollback für die Löschaktion der **Vendor**-Zeile aus, wenn in der **ProductVendor**-Tabelle mindestens eine Zeile vorhanden ist, die auf diese Zeile verweist.  
  
 ON UPDATE { **NO ACTION** | CASCADE | SET NULL | SET DEFAULT }  
 Gibt an, welche Aktion für eine Zeile der geänderten Tabelle ausgeführt werden soll, wenn diese Zeile eine referenzielle Beziehung hat und die Zeile, auf die verwiesen wird, in der übergeordneten Tabelle aktualisiert wird. Der Standardwert ist NO ACTION.  
  
 NO ACTION  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst einen Fehler aus, und für die Updateaktion der Zeile in der übergeordneten Tabelle wird ein Rollback ausgeführt.  
  
 CASCADE  
 Wenn diese Zeile in der übergeordneten Tabelle aktualisiert wird, werden die entsprechenden Zeilen in der verweisenden Tabelle aktualisiert.  
  
 SET NULL  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf NULL festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle aktualisiert wird. Die Fremdschlüsselspalten müssen NULL-Werte zulassen, um diese Einschränkung auszuführen.  
  
 SET DEFAULT  
 Alle Werte, aus denen sich der Fremdschlüssel zusammensetzt, werden auf die Standardwerte festgelegt, wenn die entsprechende Zeile in der übergeordneten Tabelle aktualisiert wird. Alle Fremdschlüsselspalten müssen Standarddefinitionen aufweisen, damit diese Einschränkung ausgeführt wird. Wenn eine Spalte NULL-Werte zulässt, und es ist kein expliziter Standardwert festgelegt, wird NULL als der implizite Standardwert für die Spalte verwendet.  
  
 Geben Sie CASCADE nicht an, wenn die Tabelle in eine Mergeveröffentlichung einbezogen werden soll, bei der logische Datensätze verwendet werden. Weitere Informationen zu logischen Datensätzen finden Sie unter [Gruppieren von Änderungen an verknüpften Zeilen mithilfe von logischen Datensätzen](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 ON UPDATE CASCADE, SET NULL oder SET DEFAULT können nicht definiert werden, wenn für ON UPDATE schon ein INSTEAD OF-Trigger für die Tabelle vorhanden ist, die geändert wird.  
  
 In der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank verfügt beispielsweise die **ProductVendor**-Tabelle über eine referenzielle Beziehung zu der **Vendor**-Tabelle. Der **ProductVendor.VendorID**-Fremdschlüssel verweist dabei auf den **Vendor.VendorID**-Primärschlüssel.  
  
 Wenn eine UPDATE-Anweisung für eine Zeile in der **Vendor**-Tabelle ausgeführt wird, und eine ON UPDATE CASCADE-Aktion für **ProductVendor.VendorID** festgelegt ist, sucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach mindestens einer abhängigen Zeile in der **ProductVendor**-Tabelle. Sind abhängige Zeilen vorhanden, werden zusätzlich zur Zeile, auf die in der **Vendor**-Tabelle verwiesen wird, die abhängigen Zeilen in der **ProductVendor**-Tabelle aktualisiert.  
  
 Ist hingegen NO ACTION angegeben, löst [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus und führt für die Updateaktion der **Vendor**-Zeile ein Rollback aus, wenn in der **ProductVendor**-Tabelle mindestens eine Zeile vorhanden ist, die auf diese Zeile verweist.  
  
 NOT FOR REPLICATION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Kann für FOREIGN KEY- und CHECK-Einschränkungen festgelegt werden. Wenn diese Klausel für eine Einschränkung angegeben wird, wird die Einschränkung nicht erzwungen, wenn Replikations-Agents Einfüge-, Update- oder Löschvorgänge ausführen.  
  
 DEFAULT  
 Gibt den Standardwert für die Spalte an. DEFAULT-Definitionen können verwendet werden, um Werte für eine neue Spalte in den vorhandenen Datenzeilen bereitzustellen. DEFAULT-Definitionen können nicht zu Spalten mit **timestamp**-Datentyp, IDENTITY-Eigenschaft, vorhandener DEFAULT-Definition oder gebundenem Standardwert hinzugefügt werden. Wenn die Spalte bereits einen Standardwert hat, muss dieser gelöscht werden, bevor der neue Standardwert hinzugefügt werden kann. Wenn ein Standardwert für einen benutzerdefinierten Spaltentyp angegeben wird, sollte dieser Typ eine implizite Konvertierung von *constant_expression* in den benutzerdefinierten Typ unterstützen. Um die Kompatibilität mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrechtzuerhalten, ist es möglich, einer DEFAULT-Definition einen Einschränkungsnamen zuzuweisen.  
  
 *constant_expression*  
 Ein Literalwert, ein NULL-Wert oder eine Systemfunktion, der bzw. die als Standardwert für die Spalte verwendet wird. Wenn *constant_expression* zusammen mit einer Spalte verwendet wird, die als benutzerdefinierter Datentyp von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] definiert ist, muss die Implementierung des Datentyps eine implizite Konvertierung von *constant_expression* in den benutzerdefinierten Datentyp unterstützen.  
  
 FOR *column*  
 Gibt die einer DEFAULT-Definition auf Tabellenebene zugeordnete Spalte an.  
  
 WITH VALUES  
 Gibt an, dass der in DEFAULT *constant_expression* angegebene Wert in einer neuen Spalte gespeichert wird, die vorhandenen Zeilen hinzugefügt wird. WITH VALUES kann nur angegeben werden, wenn DEFAULT in einer ADD-Klausel für Spalten angegeben ist. Wenn die hinzugefügte Spalte NULL-Werte zulässt und WITH VALUES angegeben ist, wird der Standardwert in der neuen, zu vorhandenen Zeilen hinzugefügten Spalte gespeichert. Ist WITH VALUES für Spalten, die NULL-Werte zulassen, nicht angegeben, wird der NULL-Wert in der neuen Spalte in vorhandenen Zeilen gespeichert. Wenn die neue Spalte keine NULL-Werte zulässt, wird der Standardwert in neuen Zeilen gespeichert, unabhängig davon, ob WITH VALUES angegeben ist.  
  
 CHECK  
 Eine Einschränkung, die Domänenintegrität erzwingt, indem die möglichen Eingabewerte für eine oder mehrere Spalten beschränkt wird.  
  
 *logical_expression*  
 Ein logischer Ausdruck, der in einer CHECK-Einschränkung verwendet wird und TRUE oder FALSE zurückgibt. Werden die CHECK-Einschränkungen zusammen mit *logical_expression* verwendet, kann nicht auf eine andere Tabelle, jedoch auf andere Spalten in derselben Tabelle für dieselbe Zeile verwiesen werden. Der Ausdruck kann keinen Verweis auf einen Aliasdatentyp enthalten.  
  
## <a name="remarks"></a>Remarks  
 Wenn FOREIGN KEY- oder CHECK-Einschränkungen hinzugefügt werden, werden alle vorhandenen Daten auf Einschränkungsverletzungen überprüft, es sei denn, die WITH NOCHECK-Option wurde festgelegt. Bei Verletzungen schlägt die ALTER TABLE-Anweisung fehl, und ein Fehler wird zurückgegeben. Wenn eine neue PRIMARY KEY- oder UNIQUE-Einschränkung zu einer vorhandenen Spalte hinzugefügt wird, müssen die Daten in der/den Spalte(n) eindeutig sein. Wenn doppelte Werte gefunden werden, schlägt die ALTER TABLE-Anweisung fehl. Die WITH NOCHECK-Option hat keine Auswirkungen, wenn PRIMARY KEY- oder UNIQUE-Einschränkungen hinzugefügt werden.  
  
 Jede PRIMARY KEY- und UNIQUE-Einschränkung generiert einen Index. Die Anzahl der UNIQUE- und PRIMARY KEY-Einschränkungen darf nicht dazu führen, dass die Anzahl der Indizes der Tabelle 999 nicht gruppierte Indizes und 1 gruppierten Index übersteigt. FOREIGN KEY-Einschränkungen generieren nicht automatisch einen Index. Fremdschlüsselspalten werden jedoch häufig in Joinkriterien in Abfragen verwendet, indem die Übereinstimmungen zwischen der oder den Spalten in der FOREIGN KEY-Einschränkung einer Tabelle und der oder den Spalten eines Primärschlüssels oder eines eindeutigen Schlüssels in der anderen Tabelle ermittelt werden. Ein Index für die Fremdschlüsselspalte ermöglicht [!INCLUDE[ssDE](../../includes/ssde-md.md)], die verbundenen Daten in der Fremdschlüsseltabelle schnell zu finden.  
  
## <a name="examples"></a>Beispiele  
 Beispiele finden Sie unter [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
