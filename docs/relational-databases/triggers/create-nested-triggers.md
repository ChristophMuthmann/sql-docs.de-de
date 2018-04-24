---
title: Erstellen von geschachtelten Triggern | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: triggers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d3a37b5abbf9c29dd52a94033980c5b637546487
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-nested-triggers"></a>Erstellen von geschachtelten Triggern
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Sowohl DML-Trigger als auch DDL-Trigger werden geschachtelt, wenn ein Trigger eine Aktion ausführt, die einen anderen Trigger auslöst. Diese Aktionen können andere Trigger auslösen usw. DML- und DDL-Trigger können bis auf 32 Ebenen geschachtelt werden. Sie können über die **Geschachtelte Trigger** -Serverkonfigurationsoption steuern, ob AFTER-Trigger geschachtelt werden können. INSTEAD OF-Trigger (nur DML-Trigger können INSTEAD OF-Trigger sein) können unabhängig von dieser Einstellung geschachtelt werden.  
  
> [!NOTE]  
>  Alle Verweise auf verwalteten Code aus einem Trigger von [!INCLUDE[tsql](../../includes/tsql-md.md)] zählen als eine Ebene hinsichtlich der Schachtelungsgrenze von 32 Ebenen. Methoden, die aus verwaltetem Code aufgerufen werden, werden nicht mitgezählt.  
  
 Wenn geschachtelte Trigger zulässig sind und ein Trigger in der Kette eine Endlosschleife einleitet, wird die Anzahl der maximal zulässigen Schachtelungsebenen überschritten und der Trigger demzufolge beendet.  
  
 Sie können geschachtelte Trigger verwenden, um nützliche Verwaltungsfunktionen durchzuführen, wie z. B. das Speichern einer Sicherungskopie von Zeilen, die von einem vorherigen Trigger betroffen sind. Es ist beispielsweise möglich, einen Trigger für `PurchaseOrderDetail` zu erstellen, der eine Sicherungskopie der `PurchaseOrderDetail` -Zeilen speichert, die vom `delcascadetrig` -Trigger gelöscht wurden. Wenn der `delcascadetrig` -Trigger wirksam ist, führt das Löschen von `PurchaseOrderID` 1965 aus `PurchaseOrderHeader` dazu, dass die entsprechende(n) Zeile(n) aus `PurchaseOrderDetail`gelöscht werden. Zum Speichern der Daten erstellen Sie einen DELETE-Trigger für `PurchaseOrderDetail` , der die gelöschten Daten in einer getrennt erstellten Tabelle, `del_save`, speichert. Zum Beispiel:  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 Das Verwenden geschachtelter Trigger wird nicht für eine Sequenz empfohlen, in der die Reihenfolge wichtig ist. Verwenden Sie getrennte Trigger, um Datenänderungen kaskadierend weiterzugeben.  
  
> [!NOTE]  
>  Da Trigger innerhalb einer Transaktion ausgeführt werden, führt ein Fehler auf einer beliebigen Ebene einer Reihe geschachtelter Trigger zum Abbruch der gesamten Transaktion und zum Rollback für alle Datenänderungen. Fügen Sie PRINT-Anweisungen in die Trigger ein, sodass Sie ermitteln können, wo der Fehler aufgetreten ist.  
  
## <a name="recursive-triggers"></a>Rekursive Trigger  
 Ein AFTER-Trigger kann sich nur dann rekursiv aufrufen, wenn die Datenbankoption RECURSIVE_TRIGGERS festgelegt wurde.  
  
 Die folgenden zwei Rekursionsarten stehen zur Verfügung:  
  
-   Direkte Rekursion  
  
     Diese Rekursion tritt auf, wenn ein Trigger ausgelöst wird und eine Aktion ausführt, die das erneute Auslösen desselben Triggers verursacht. Eine Anwendung aktualisiert z. B. die **T3**-Tabelle, wodurch der **Trig3** -Trigger ausgelöst wird. **Trig3** aktualisiert **T3** erneut, sodass der **Trig3** -Trigger erneut ausgelöst wird.  
  
     Die direkte Rekursion kann auch auftreten, wenn derselbe Trigger erneut aufgerufen wird, jedoch erst nach dem Aufruf eines weiteren Triggers, der einen anderen Typ aufweist (AFTER oder INSTEAD OF). Mit anderen Worten: Die direkte Rekursion eines INSTEAD OF-Triggers kann auftreten, wenn derselbe INSTEAD OF-Trigger ein zweites Mal aufgerufen wird, auch wenn zwischendurch mindestens ein AFTER-Trigger aufgerufen wird. Auf gleiche Weise kann die direkte Rekursion eines AFTER-Triggers auftreten, wenn derselbe AFTER-Trigger ein zweites Mal aufgerufen wird, auch wenn zwischendurch mindestens ein INSTEAD OF-Trigger aufgerufen wird. Beispielsweise aktualisiert eine Anwendung Tabelle **T4**. Durch dieses Update wird das Auslösen von INSTEAD OF-Trigger **Trig4** verursacht. **Trig4** aktualisiert Tabelle **T5**. Durch dieses Update wird das Auslösen von AFTER-Trigger **Trig5** verursacht. **Trig5** aktualisiert wiederum Tabelle **T4**. Dieses Update verursacht erneut das Auslösen von INSTEAD OF-Trigger **Trig4** . Diese Kette von Ereignissen wird als direkte Rekursion für **Trig4**betrachtet.  
  
-   Indirekte Rekursion  
  
     Diese Rekursion tritt auf, wenn ein Trigger ausgelöst wird, der eine Aktion ausführt, die das Auslösen eines anderen Triggers des gleichen Typs verursacht (AFTER oder INSTEAD OF). Dieser zweite Trigger führt eine Aktion aus, die das erneute Auslösen des ursprünglichen Triggers bewirkt. Mit anderen Worten: Die indirekte Rekursion tritt auf, wenn ein INSTEAD OF-Trigger ein zweites Mal aufgerufen wird, jedoch erst, wenn in der Zwischenzeit ein anderer INSTEAD OF-Trigger aufgerufen wird. Die indirekte Rekursion kann gleichermaßen auftreten, wenn ein AFTER-Trigger ein zweites Mal aufgerufen wird, jedoch erst, wenn in der Zwischenzeit ein anderer AFTER-Trigger aufgerufen wird. Beispielsweise aktualisiert eine Anwendung Tabelle **T1**. Durch dieses Update wird das Auslösen von AFTER-Trigger **Trig1** verursacht. **Trig1** aktualisiert Tabelle **T2**. Dieses Update verursacht wiederum das Auslösen von AFTER-Trigger **Trig2** . **Trig2** aktualisiert nun wiederum Tabelle **T1** , wodurch der AFTER-Trigger **Trig1** erneut ausgelöst wird.  
  
 Es wird nur die direkte Rekursion von AFTER-Triggern verhindert, wenn die Datenbankoption RECURSIVE_TRIGGERS auf OFF festgelegt ist. Sie müssen auch die **Geschachtelte Trigger** -Serveroption auf **0**festlegen, um die indirekte Rekursion von AFTER-Triggern zu deaktivieren.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die Verwendung rekursiver Trigger zum Auflösen einer auf sich selbst verweisenden Beziehung (auch als transitiver Abschluss bezeichnet). Die `emp_mgr` -Tabelle definiert z. B. Folgendes:  
  
-   Einen Angestellten (`emp`) in einem Unternehmen.  
  
-   Den Vorgesetzten jedes Angestellten (`mgr`).  
  
-   Die Gesamtzahl der Angestellten in der Hierarchie, die jedem einzelnen Vorgesetzten unterstellt sind (`NoOfReports`).  
  
 Mithilfe eines rekursiven UPDATE-Triggers kann die `NoOfReports` -Spalte auf dem aktuellen Stand gehalten werden, wenn neue Angestelltendatensätze eingefügt werden. Der INSERT-Trigger aktualisiert die `NoOfReports` -Spalte für den Datensatz des Vorgesetzten, wodurch rekursiv die `NoOfReports` -Spalte anderer Datensätze auf den höheren Hierarchieebenen aktualisiert wird.  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 Im Folgenden sehen Sie die Ergebnisse vor dem Update.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 Im Folgenden sehen Sie die Ergebnisse nach dem Update.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **So legen Sie die Option für geschachtelte Trigger fest**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 **So legen Sie die Datenbankoption RECURSIVE_TRIGGERS fest**  
  
-   [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Konfigurieren der Serverkonfigurationsoption Geschachtelte Trigger](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
