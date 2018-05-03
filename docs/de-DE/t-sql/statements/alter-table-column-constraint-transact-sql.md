---
title: column_constraint (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- column_constraint
- column_constraint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER TABLE statement
- constraints [SQL Server], properties
- constraints [SQL Server], definitions
- column_constraint
ms.assetid: 8119b7c7-e93b-4de5-8f71-c3b7c70b993c
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f02956171b6e8ab84ad89410068a3be21398b7db
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table-columnconstraint-transact-sql"></a>ALTER TABLE column_constraint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Eigenschaften einer PRIMARY KEY-, FOREIGN KEY-, UNIQUE- oder CHECK-Einschränkung an, die Teil einer neuen Spaltendefinition ist, die einer Tabelle mithilfe von [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) hinzugefügt wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
[ CONSTRAINT constraint_name ]   
{   
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor ]   
        [ WITH ( index_option [, ...n ] ) ]  
        [ ON { partition_scheme_name (partition_column_name)   
            | filegroup | "default" } ]   
    | [ FOREIGN KEY ]   
        REFERENCES [ schema_name . ] referenced_table_name   
            [ ( ref_column ) ]   
        [ ON DELETE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]   
        [ NOT FOR REPLICATION ]   
    | CHECK [ NOT FOR REPLICATION ] ( logical_expression )  
}  
```  
  
## <a name="arguments"></a>Argumente  
 CONSTRAINT  
 Gibt den Beginn der Definition für eine PRIMARY KEY-, UNIQUE-, FOREIGN KEY- oder CHECK-Einschränkung an.  
  
 *constraint_name*  
 Der Name der Einschränkung. Einschränkungsnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Zusätzlich darf der Name nicht mit einem Nummernzeichen (#) beginnen. Wenn *constraint_name* nicht angegeben ist, vergibt das System einen Namen für die Einschränkung.  
  
 NULL | NOT NULL  
 Gibt an, ob die Spalte NULL-Werte akzeptiert. Spalten, die keine NULL-Werte zulassen, können nur hinzugefügt werden, wenn für sie ein Standardwert angegeben ist. Wenn die neue Spalte NULL-Werte zulässt und kein Standardwert angegeben ist, enthält sie einen NULL-Wert für jede Zeile in der Tabelle. Wenn die neue Spalte NULL-Werte zulässt und eine Standarddefinition mit der neuen Spalte hinzugefügt wird, kann die Option WITH VALUES verwendet werden, um den Standardwert in der neuen Spalte für jede vorhandene Zeile in der Tabelle zu speichern.  
  
 Wenn die neue Spalte keine NULL-Werte zulässt, muss eine DEFAULT-Definition mit der neuen Spalte hinzugefügt werden. Die neue Spalte wird automatisch mit dem Standardwert in den neuen Spalten in jeder vorhandenen Zeile geladen.  
  
 Wenn das Hinzufügen einer Spalte Änderungen an den Datenzeilen einer Tabelle erfordert, wie z. B. das Hinzufügen von DEFAULT-Werten zu jeder Zeile, werden Sperren für die Tabelle aufrechterhalten, während ALTER TABLE ausgeführt wird. Dies beeinflusst die Möglichkeit, den Inhalt der Tabelle zu ändern, während die Sperre aktiviert ist. Dagegen ist das Hinzufügen einer Spalte, die NULL-Werte zulässt und für die kein Standardwert angegeben ist, lediglich ein Metadatenvorgang. In diesem Fall sind keine Sperren beteiligt.  
  
 Wenn Sie CREATE TABLE oder ALTER TABLE verwenden, beeinflussen Datenbank- und Sitzungseinstellungen die NULL-Zulässigkeit des in einer Spaltendefinition verwendeten Datentyps und überschreiben diese möglicherweise. Es wird empfohlen, nicht berechnete Spalten stets explizit als NULL oder NOT NULL zu definieren oder, im Falle eines benutzerdefinierten Datentyps, zuzulassen, dass die Spalte die standardmäßige NULL-Zulässigkeit des Datentyps verwendet. Weitere Informationen finden Sie unter [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 PRIMARY KEY  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) mithilfe eines eindeutigen Index erzwingt. Es kann nur eine PRIMARY KEY-Einschränkung für jede Tabelle erstellt werden.  
  
 UNIQUE  
 Eine Einschränkung, die Entitätsintegrität für eine angegebene Spalte (oder Spalten) mit einem eindeutigen Index bietet.  
  
 CLUSTERED | NONCLUSTERED  
 Gibt an, dass ein gruppierter oder nicht gruppierter Index für die PRIMARY KEY- oder UNIQUE-Einschränkung erstellt wird. Für PRIMARY KEY-Einschränkungen wird standardmäßig CLUSTERED verwendet. Für UNIQUE-Einschränkungen wird standardmäßig NONCLUSTERED verwendet.  
  
 Wenn bereits eine gruppierte Einschränkung oder ein gruppierter Index für eine Tabelle vorhanden ist, kann CLUSTERED nicht angegeben werden. Wenn bereits eine gruppierte Einschränkung oder ein gruppierter Index für eine Tabelle vorhanden ist, wird für PRIMARY KEY-Einschränkungen standardmäßig NONCLUSTERED verwendet.  
  
 Die Datentypen **ntext**, **text**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **xml** und **image** können nicht als Spalten für einen Index angegeben werden.  
  
 WITH FILLFACTOR **=***fillfactor*  
 Gibt an, wie weit [!INCLUDE[ssDE](../../includes/ssde-md.md)] die einzelnen Indexseiten füllen soll, die zum Speichern der Indexdaten verwendet werden. Vom Benutzer angegebene Füllfaktorwerte können Zahlen von 1 bis 100 sein. Wenn kein Wert angegeben ist, lautet der Standardwert 0.  
  
> [!IMPORTANT]  
>  Das Verwenden von WITH FILLFACTOR = *fillfactor* als einzige Indexoption, die für die PRIMARY KEY- oder UNIQUE-Einschränkungen gilt, wird hier aus Gründen der Abwärtskompatibilität weiterhin dokumentiert. In zukünftigen Releases wird dies jedoch nicht mehr der Fall sein. Andere Indexoptionen können in der [index_option](../../t-sql/statements/alter-table-index-option-transact-sql.md)-Klausel der ALTER TABLE-Anweisung angegeben werden.  
  
 ON { *partition_scheme_name ***(*** partition_column_name***)** | *filegroup* | **"** default **"** }  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Gibt den Speicherort des Indexes an, der für die Einschränkung erstellt wurde. Wenn *partition_scheme_name* angegeben wird, wird der Index partitioniert, und die Partitionen werden den Dateigruppen zugeordnet, die durch *partition_scheme_name* angegeben sind. Wenn *filegroup* angegeben ist, wird der Index in der genannten Dateigruppe erstellt. Wenn **"** default **"** angegeben ist, oder wenn ON nicht für alle festgelegt ist, wird der Index in derselben Dateigruppe erstellt wie die Tabelle. Wenn ON beim Hinzufügen eines gruppierten Index für eine PRIMARY KEY- oder UNIQUE-Einschränkung angegeben ist, wird die gesamte Tabelle beim Erstellen des gruppierten Index in die angegebene Dateigruppe verschoben.  
  
 In diesem Zusammenhang ist default kein Schlüsselwort. Es handelt sich dabei um einen Bezeichner für die Standarddateigruppe. Dieser muss wie in ON **"** default **"** or ON **[** default **]** durch Trennzeichen getrennt werden. Wenn **"** default **"** angegeben ist, muss die QUOTED_IDENTIFIER-Option in der aktuellen Sitzung auf ON festgelegt sein. Dies ist die Standardeinstellung. Weitere Informationen finden Sie unter [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).  
  
 FOREIGN KEY REFERENCES  
 Eine Einschränkung, die referenzielle Integrität für die Daten in der Spalte bereitstellt. FOREIGN KEY-Einschränkungen erfordern, dass jeder Wert in der Spalte in der angegebenen Spalte der Tabelle vorhanden ist, auf die verwiesen wird.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Tabelle gehört, auf die mit der FOREIGN KEY-Einschränkung verwiesen wird.  
  
 *referenced_table_name*  
 Die Tabelle, auf die die FOREIGN KEY-Einschränkung verweist.  
  
 *ref_column*  
 Eine Spalte in Klammern, auf die die neue FOREIGN KEY-Einschränkung verweist.  
  
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
  
 Die CASCADE-Aktion ON DELETE kann nicht definiert werden, wenn für ON DELETE bereits ein INSTEAD OF-Trigger für die Tabelle vorhanden ist, die geändert wird.  
  
 In der Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] verfügt die Tabelle **ProductVendor** beispielsweise über eine referenzielle Beziehung zu der Tabelle **Vendor**. Der **ProductVendor.VendorID**-Fremdschlüssel verweist dabei auf den **Vendor.VendorID**-Primärschlüssel.  
  
 Wenn eine DELETE-Anweisung für eine Zeile in der **Vendor**-Tabelle ausgeführt wird und eine ON DELETE CASCADE-Aktion für **ProductVendor.VendorID** festgelegt ist, sucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach mindestens einer abhängigen Zeile in der **ProductVendor**-Tabelle. Sind abhängige Zeilen vorhanden, werden zusätzlich zur Zeile, auf die in der **Vendor**-Tabelle verwiesen wird, die abhängigen Zeilen in der **ProductVendor**-Tabelle gelöscht.  
  
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
  
 In der Datenbank [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] verfügt die Tabelle **ProductVendor** beispielsweise über eine referenzielle Beziehung zu der Tabelle **Vendor**. Der **ProductVendor.VendorID**-Fremdschlüssel verweist dabei auf den **Vendor.VendorID**-Primärschlüssel.  
  
 Wenn eine UPDATE-Anweisung für eine Zeile in der **Vendor**-Tabelle ausgeführt wird, und eine ON UPDATE CASCADE-Aktion ist für **ProductVendor.VendorID** festgelegt, sucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] nach mindestens einer abhängigen Zeile in der **ProductVendor**-Tabelle. Sind abhängige Zeilen vorhanden, wird zusätzlich zur Zeile, auf die in der **Vendor**-Tabelle verwiesen wird, die abhängige Zeile in der **ProductVendor**-Tabelle aktualisiert.  
  
 Ist hingegen NO ACTION angegeben, löst [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus und führt für die Updateaktion der **Vendor**-Zeile einen Rollback aus, wenn in der **ProductVendor**-Tabelle mindestens eine Zeile vorhanden ist, die auf diese Zeile verweist.  
  
 NOT FOR REPLICATION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Kann für FOREIGN KEY- und CHECK-Einschränkungen festgelegt werden. Wenn diese Klausel für eine Einschränkung angegeben wird, wird die Einschränkung nicht erzwungen, wenn Replikations-Agents Einfüge-, Update- oder Löschvorgänge ausführen.  
  
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
 [column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-definition-transact-sql.md)  
  
  
