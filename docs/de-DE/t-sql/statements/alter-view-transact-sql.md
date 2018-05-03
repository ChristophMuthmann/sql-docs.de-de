---
title: ALTER VIEW (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/10/2017
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
ms.openlocfilehash: f20a6326f33f0cd41116d3a3c20dcdfad163eea2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
  
 *column*  
 Ist der Name von einer oder von mehreren, durch Trennzeichen voneinander getrennten Spalten, die Teil der angegebenen Sicht sein sollen.  
  
> [!IMPORTANT]  
>  Spaltenberechtigungen bleiben nur erhalten, wenn die Spalten vor und nach der Ausführung von ALTER VIEW den gleichen Namen haben.  
  
> [!NOTE]  
>  In den Spalten für die Sicht gelten die Berechtigungen für einen Spaltennamen über eine CREATE VIEW- oder ALTER VIEW-Anweisung hinaus, unabhängig von der Quelle der zugrunde liegenden Daten. Wenn beispielsweise Berechtigungen für die **SalesOrderID**-Spalte in einer CREATE VIEW-Anweisung erteilt werden, kann die **SalesOrderID**-Spalte beispielsweise zu **OrderRef** mithilfe einer ALTER VIEW-Anweisung umbenannt werden und weiterhin über die mithilfe von **SalesOrderID** der Sicht zugeordneten Berechtigungen verfügen.  
  
 ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Verschlüsselt die [sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md)-Einträge, die den Text der ALTER VIEW-Anweisung enthalten. Mithilfe von WITH ENCRYPTION kann verhindert werden, dass die Sicht als Teil der SQL Server-Replikation veröffentlicht wird.  
  
 SCHEMABINDING  
 Bindet die Sicht an das Schema der zugrunde liegenden Basistabellen. Wird SCHEMABINDING angegeben, ist es nicht möglich, Änderungen der Basistabellen auszuführen, die sich auf die Sichtdefinition auswirken würden. Die Sichtdefinition muss zuerst geändert oder gelöscht werden, um Abhängigkeiten von der zu ändernden Tabelle zu entfernen. Wenn Sie SCHEMABINDING verwenden, muss *select_statement* die zweiteiligen Namen (*schema ***.*** object*) der Tabellen, Sichten oder benutzerdefinierten Funktionen einschließen, auf die verwiesen wird. Alle Objekte, auf die verwiesen wird, müssen in derselben Datenbank vorhanden sein.  
  
 Sichten oder Tabellen, die Bestandteil einer mit der SCHEMABINDING-Klausel erstellten Sicht sind, können erst dann gelöscht werden, wenn die entsprechende Sicht gelöscht oder geändert wird, sodass die Schemabindung nicht mehr vorhanden ist. Andernfalls löst [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus. Darüber hinaus schlägt die Ausführung von ALTER TABLE-Anweisungen für Tabellen fehl, die Bestandteil von Sichten mit Schemabindung sind, falls diese Anweisungen die Sichtdefinition betreffen.  
  
 VIEW_METADATA  
 Gibt an, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Metadateninformationen der Sicht anstelle der Basistabelle(n) an die DB-Library-, ODBC- und OLE DB-APIs zurückgibt, wenn Metadaten des Durchsuchenmodus für eine Abfrage angefordert werden, die auf die Sicht verweist. Metadaten des Durchsuchenmodus sind zusätzliche Metadaten, die von der [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz an die clientbasierten DB-Library-, ODBC- und OLE DB-APIs zurückgegeben werden. Mithilfe dieser Metadaten können die clientbasierten APIs aktualisierbare clientbasierte Cursors implementieren. Metadaten des Durchsuchenmodus enthalten Informationen zu der Basistabelle, zu der die Spalten im Resultset gehören.  
  
 Bei Sichten, die mit VIEW_METADATA erstellt wurden, geben die Metadaten des Durchsuchenmodus den Sichtnamen anstelle der Basistabellennamen zurück, wenn Spalten aus der Sicht im Resultset beschrieben werden.  
  
 Wenn eine Sicht mithilfe von WITH VIEW_METADATA erstellt wurde, sind alle enthaltenen Spalten (außer der **timestamp**-Spalte) aktualisierbar, falls die Sicht INSERT- oder UPDATE INSTEAD OF-Trigger besitzt. Weitere Informationen finden Sie im Abschnitt „Hinweise“ in [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 AS  
 Die Aktionen, die die Sicht ausführen soll.  
  
 *select_statement*  
 Die SELECT-Anweisung, die die Sicht definiert.  
  
 WITH CHECK OPTION  
 Erzwingt, dass alle für die Sicht ausgeführten Datenänderungsanweisungen den Kriterien entsprechen müssen, die innerhalb von *select_statement* festgelegt wurden.  
  
## <a name="remarks"></a>Remarks  
 Weitere Informationen zu ALTER VIEW finden Sie im Abschnitt „Hinweise“ unter [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
