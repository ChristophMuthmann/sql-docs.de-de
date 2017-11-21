---
title: ALTER VIEW (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
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
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
ms.assetid: 03eba220-13e2-49e3-bd9d-ea9df84dc28c
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 006b9fce1e13833c977d26d4bc0f13a602f2c96c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-view-transact-sql"></a>ALTER VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ändert eine zuvor erstellte Sicht. Darunter fallen auch indizierte Sichten. ALTER VIEW wirkt sich nicht auf abhängige gespeicherte Prozeduren oder Trigger aus und ändert keine Berechtigungen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER VIEW [ schema_name . ] view_name [ ( column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ] [ ; ]  
  
<view_attribute> ::=   
{   
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Ist der Name des Schemas, zu dem die Sicht gehört.  
  
 *view_name*  
 Die zu ändernde Sicht.  
  
 *Spalte*  
 Ist der Name von einer oder von mehreren, durch Trennzeichen voneinander getrennten Spalten, die Teil der angegebenen Sicht sein sollen.  
  
> [!IMPORTANT]  
>  Spaltenberechtigungen bleiben nur erhalten, wenn die Spalten vor und nach der Ausführung von ALTER VIEW den gleichen Namen haben.  
  
> [!NOTE]  
>  In den Spalten für die Sicht gelten die Berechtigungen für einen Spaltennamen über eine CREATE VIEW- oder ALTER VIEW-Anweisung hinaus, unabhängig von der Quelle der zugrunde liegenden Daten. Angenommen, Berechtigungen für die **SalesOrderID** Spalte in einer CREATE VIEW-Anweisung, eine ALTER VIEW-Anweisung kann Umbenennen der **SalesOrderID** -Spalte beispielsweise im Vergleich zu **OrderRef**, und die Ansicht mit zugeordneten Berechtigungen haben weiterhin **SalesOrderID**.  
  
 ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Verschlüsselt die Einträge in [sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) , die den Text der ALTER VIEW-Anweisung enthalten. Mithilfe von WITH ENCRYPTION kann verhindert werden, dass die Sicht als Teil der SQL Server-Replikation veröffentlicht wird.  
  
 SCHEMABINDING  
 Bindet die Sicht an das Schema der zugrunde liegenden Basistabellen. Wird SCHEMABINDING angegeben, ist es nicht möglich, Änderungen der Basistabellen auszuführen, die sich auf die Sichtdefinition auswirken würden. Die Sichtdefinition muss zuerst geändert oder gelöscht werden, um Abhängigkeiten von der zu ändernden Tabelle zu entfernen. Wenn Sie SCHEMABINDING verwenden die *Select_statement* umfasst die mit dem zweiteiligen Namen (*Schema***.** *Objekt*) von Tabellen, Sichten oder benutzerdefinierten Funktionen, auf die verwiesen werden. Alle Objekte, auf die verwiesen wird, müssen in derselben Datenbank vorhanden sein.  
  
 Sichten oder Tabellen, die Bestandteil einer mit der SCHEMABINDING-Klausel erstellten Sicht sind, können erst dann gelöscht werden, wenn die entsprechende Sicht gelöscht oder geändert wird, sodass die Schemabindung nicht mehr vorhanden ist. Andernfalls löst [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus. Darüber hinaus schlägt die Ausführung von ALTER TABLE-Anweisungen für Tabellen fehl, die Bestandteil von Sichten mit Schemabindung sind, falls diese Anweisungen die Sichtdefinition betreffen.  
  
 VIEW_METADATA  
 Gibt an, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Metadateninformationen der Sicht anstelle der Basistabelle(n) an die DB-Library-, ODBC- und OLE DB-APIs zurückgibt, wenn Metadaten des Durchsuchenmodus für eine Abfrage angefordert werden, die auf die Sicht verweist. Metadaten des Durchsuchenmodus sind zusätzliche Metadaten, die von der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz an die clientbasierten DB-Library-, ODBC- und OLE DB-APIs zurückgegeben werden. Mithilfe dieser Metadaten können die clientbasierten APIs aktualisierbare clientbasierte Cursors implementieren. Metadaten des Durchsuchenmodus enthalten Informationen zu der Basistabelle, zu der die Spalten im Resultset gehören.  
  
 Bei Sichten, die mit VIEW_METADATA erstellt wurden, geben die Metadaten des Durchsuchenmodus den Sichtnamen anstelle der Basistabellennamen zurück, wenn Spalten aus der Sicht im Resultset beschrieben werden.  
  
 Wenn eine Sicht erstellt wird, mithilfe von WITH VIEW_METADATA alle enthaltenen Spalten außer einem **Zeitstempel** Spalte, aktualisierbar, falls die Sicht INSERT- oder UPDATE INSTEAD OF-Trigger sind. Weitere Informationen finden Sie im Abschnitt "Hinweise" in [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 AS  
 Die Aktionen, die die Sicht ausführen soll.  
  
 *select_statement*  
 Die SELECT-Anweisung, die die Sicht definiert.  
  
 WITH CHECK OPTION  
 Erzwingt, dass alle datenänderungsanweisungen, die ausgeführt werden, für die Sicht, die innerhalb von festgelegten Kriterien folgen *Select_statement*.  
  
## <a name="remarks"></a>Hinweise  
 Weitere Informationen zu ALTER VIEW finden Sie unter "Hinweise" in [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
> [!NOTE]  
>  Wenn die vorherige Sichtdefinition mithilfe von WITH ENCRYPTION oder CHECK OPTION erstellt wurde, sind diese Optionen nur dann aktiviert, wenn sie in der ALTER VIEW-Anweisung enthalten sind.  
  
 Wird eine derzeit verwendete Sicht mithilfe von ALTER VIEW geändert, belegt [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Sicht mit einer exklusiven Schemasperre. Wenn die Sperre erteilt wird und keine aktiven Benutzer der Sicht vorhanden sind, löscht [!INCLUDE[ssDE](../../includes/ssde-md.md)] alle Kopien der Sicht aus dem Prozedurcache. Vorhandene Pläne, die auf die Sicht verweisen, bleiben im Cache, werden aber beim Aufrufen erneut kompiliert.  
  
 ALTER VIEW kann auf indizierte Sichten angewendet werden; ALTER VIEW löscht jedoch vorbehaltlos alle Indizes in der Sicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Ausführung von ALTER VIEW wird zumindest die ALTER-Berechtigung für OBJECT benötigt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Sicht mit allen Mitarbeitern und deren Anstellungsdaten mit der Bezeichnung `EmployeeHireDate` erstellt. Die Berechtigungen werden der Sicht erteilt, doch die Anforderungen werden geändert, sodass Mitarbeiter ausgewählt werden, deren Anstellungsdatum vor einem bestimmten Datum liegt. Dann wird die Sicht mithilfe von `ALTER VIEW` ersetzt.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
 Die Sicht muss geändert werden, damit nur die Mitarbeiter enthalten sind, die vor `2002` eingestellt wurden. Wird ALTER VIEW nicht verwendet, sondern die Sicht gelöscht und erneut erstellt, müssen die zuvor verwendete GRANT-Anweisung sowie alle anderen Anweisungen im Zusammenhang mit Berechtigungen für diese Sicht erneut eingegeben werden.  
  
```  
ALTER VIEW HumanResources.EmployeeHireDate  
AS  
SELECT p.FirstName, p.LastName, e.HireDate  
FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
ON e.BusinessEntityID = p.BusinessEntityID  
WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DROP VIEW &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  

