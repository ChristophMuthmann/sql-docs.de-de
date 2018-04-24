---
title: SCOPE_IDENTITY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SCOPE_IDENTITY
- SCOPE_IDENTITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], SCOPE_IDENTITY function
- SCOPE_IDENTITY function
- last-inserted identity values
- identity values [SQL Server], last-inserted
ms.assetid: eef24670-059b-4f10-91d4-a67bc1ed12ab
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7b202e6ea16d72c0fa3c2a15ae24362f342a8719
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="scopeidentity-transact-sql"></a>SCOPE_IDENTITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den letzten Identitätswert zurück, der in eine Identitätsspalte im selben Gültigkeitsbereich eingefügt wurde. Ein Gültigkeitsbereich ist ein Modul: eine gespeicherte Prozedur, ein Trigger, eine Funktion oder ein Batch. Wenn sich daher zwei Anweisungen in der selben gespeicherten Prozedur, in derselben Funktion oder im selben Batch befinden, bindenden sie sich im selben Gültigkeitsbereich.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SCOPE_IDENTITY()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Remarks  
 Bei SCOPE_IDENTITY, IDENT_CURRENT und @@IDENTITY handelt es sich um ähnliche Funktionen, denn sie geben Werte zurück, die in Identitätsspalten eingefügt wurden.  
  
 IDENT_CURRENT ist nicht durch einen Gültigkeitsbereich oder eine Sitzung begrenzt, sondern auf eine angegebene Tabelle. IDENT_CURRENT gibt den für eine bestimmte Tabelle in einer beliebigen Sitzung und einem beliebigen Gültigkeitsbereich generierten Wert zurück. Weitere Informationen finden Sie unter [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md).  
  
 SCOPE_IDENTITY und @@IDENTITY geben die letzten Identitätswerte zurück, die in einer beliebigen Tabelle in der aktuellen Sitzung generiert wurden. SCOPE_IDENTITY gibt jedoch nur im aktuellen Gültigkeitsbereich eingefügte Werte zurück, @@IDENTITY ist nicht auf einen bestimmten Gültigkeitsbereich begrenzt.  
  
 Beispiel: Es gibt zwei Tabellen, T1 und T2, und für T1 wurde ein INSERT-Trigger definiert. Wenn eine Zeile in T1 eingefügt wird, wird der Trigger ausgelöst und fügt eine Zeile in T2 ein. Dieses Szenario veranschaulicht zwei Gültigkeitsbereiche: die Einfügung für T1 und die Einfügung für T2 durch den Trigger.  
  
 Wenn T1 und T2 Identitätsspalten aufweisen, geben @@IDENTITY und SCOPE_IDENTITY nach einer INSERT-Anweisung für T1 verschiedene Werte zurück. @@IDENTITY gibt den letzten Identitätsspaltenwert zurück, der in einem beliebigen Gültigkeitsbereich in der aktuellen Sitzung eingefügt wurde. Das ist der Wert, der in T2 eingefügt wurde. SCOPE_IDENTITY() gibt den IDENTITY-Wert zurück, der in T1 eingefügt wurde. Dies war die letzte Einfügung, die im selben Gültigkeitsbereich durchgeführt wurde. Die SCOPE_IDENTITY()-Funktion gibt den NULL-Wert zurück, wenn sie aufgerufen wird, bevor INSERT-Anweisungen für eine Identitätsspalte im Gültigkeitsbereich auftreten.  
  
 Fehlgeschlagene Anweisungen oder Transaktionen können die aktuelle Identität für eine Tabelle ändern und zu Lücken in den Identitätsspaltenwerten führen. Für den Identitätswert erfolgt kein Rollback, auch wenn für die Transaktion, die versuchte, den Wert in die Tabelle einzufügen, kein Commit ausgeführt wird. Wenn beispielsweise eine INSERT-Anweisung aufgrund einer IGNORE_DUP_KEY-Verletzung fehlschlägt, wird der aktuelle Identitätswert für die Tabelle trotzdem inkrementiert.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-identity-and-scopeidentity-with-triggers"></a>A. Verwenden von @@IDENTITY und SCOPE_IDENTITY mit Triggern  
 Im folgenden Beispiel werden zwei Tabellen, `TZ` und `TY`, sowie ein INSERT-Trigger für `TZ` erstellt. Wenn eine Zeile in die Tabelle `TZ` eingefügt wird, wird der Trigger (`Ztrig`) ausgelöst und fügt eine Zeile in `TY` ein.  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE TZ (  
   Z_id  int IDENTITY(1,1)PRIMARY KEY,  
   Z_name varchar(20) NOT NULL);  
  
INSERT TZ  
   VALUES ('Lisa'),('Mike'),('Carla');  
  
SELECT * FROM TZ;  
```     
Resultset: So sieht die Tabelle TZ aus.  
  
```  
Z_id   Z_name  
-------------  
1      Lisa  
2      Mike  
3      Carla  
```  
```sql 
CREATE TABLE TY (  
   Y_id  int IDENTITY(100,5)PRIMARY KEY,  
   Y_name varchar(20) NULL);  
  
INSERT TY (Y_name)  
   VALUES ('boathouse'), ('rocks'), ('elevator');  
  
SELECT * FROM TY;  
```   
Resultset: So sieht die TY aus:  
```  
Y_id  Y_name  
---------------  
100   boathouse  
105   rocks  
110   elevator  
```  

Erstellen Sie den Trigger, der eine Zeile in die Tabelle TY einfügt, wenn eine Zeile in Tabelle TZ eingefügt wird.  
```sql  
CREATE TRIGGER Ztrig  
ON TZ  
FOR INSERT AS   
   BEGIN  
   INSERT TY VALUES ('')  
   END;  
```  
Lösen Sie den Trigger aus, und bestimmen Sie, welche Identitätswerte Sie mit den @@IDENTITY and SCOPE_IDENTITY-Funktionen abrufen.   
```sql
INSERT TZ VALUES ('Rosalie');  
  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
/*SCOPE_IDENTITY returns the last identity value in the same scope. This was the insert on table TZ.*/`  
SCOPE_IDENTITY  
4  

/*@@IDENTITY returns the last identity value inserted to TY by the trigger. 
  This fired because of an earlier insert on TZ.*/
@@IDENTITY  
115  
```  
  
### <a name="b-using-identity-and-scopeidentity-with-replication"></a>B. Verwenden von @@IDENTITY und SCOPE_IDENTITY() mit Replikation  
 In den folgenden Beispielen wird veranschaulicht, wie `@@IDENTITY` und `SCOPE_IDENTITY()` für Einfügungen in einer Datenbank verwendet werden, die für die Mergereplikation veröffentlicht wird. Beide Tabellen in den Beispielen befinden sich in der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank: `Person.ContactType` wird nicht veröffentlicht, und `Sales.Customer` wird veröffentlicht. Mit der Mergereplikation werden Tabellen, die veröffentlicht werden, Trigger hinzugefügt. Aus diesem Grund kann `@@IDENTITY` den Wert aus dem Einfügevorgang in eine Replikationssystemtabelle zurückgeben statt aus dem Einfügevorgang in eine Benutzertabelle.  
  
 Die `Person.ContactType`-Tabelle besitzt den maximalen Identitätswert 20. Wenn Sie eine Zeile in die Tabelle einfügen, wird von `@@IDENTITY` und `SCOPE_IDENTITY()` derselbe Wert zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Person.ContactType ([Name]) VALUES ('Assistant to the Manager');  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```  
SCOPE_IDENTITY  
21  
@@IDENTITY  
21
```  
  
 Die `Sales.Customer`-Tabelle besitzt den maximalen Identitätswert 29483. Wenn Sie eine Zeile in die Tabelle einfügen, werden von `@@IDENTITY` und `SCOPE_IDENTITY()` jeweils unterschiedliche Werte zurückgegeben. `SCOPE_IDENTITY()` gibt den Wert aus dem Einfügevorgang in die Benutzertabelle zurück, `@@IDENTITY` hingegen gibt den Wert aus dem Einfügevorgang in die Replikationssystemtabelle zurück. Verwenden Sie `SCOPE_IDENTITY()` für Anwendungen, für die der Zugriff auf den eingefügten Identitätswert erforderlich ist.  
  
```sql  
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 ```
 SCOPE_IDENTITY  
 29484  
 @@IDENTITY  
 89
 ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)  
  
  
