---
title: Erneutes Kompilieren einer gespeicherten Prozedur | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2c8f7940c224d22fc93eea4d2c269658e97f266
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="recompile-a-stored-procedure"></a>Erneutes Kompilieren einer gespeicherten Prozedur
  In diesem Thema wird beschrieben, wie Sie eine gespeicherte Prozedur in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)]erneut kompilieren. Hierzu stehen drei Möglichkeiten zur Verfügung: die **WITH RECOMPILE** -Option in der Prozedurdefinition, beim Aufrufen der Prozedur der **RECOMPILE** -Abfragehinweis in einzelnen Anweisungen oder die gespeicherte Systemprozedur **sp_recompile** . In diesem Thema wird die Verwendung der WITH RECOMPILE-Option beim Erstellen einer Prozedurdefinition und Ausführen einer vorhandenen Prozedur beschrieben. Zudem wird erläutert, wie die gespeicherte Systemprozedur sp_recompile zum erneuten Kompilieren einer vorhandenen Prozedur verwendet wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **Erneutes Kompilieren einer gespeicherten Prozedur mit:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wenn eine Prozedur zum ersten Mal kompiliert oder erneut kompiliert wird, wird der Abfrageplan der Prozedur für den aktuellen Status der Datenbank und die darin enthaltenen Objekte optimiert. Werden bedeutende Änderungen an den Daten oder der Struktur einer Datenbank vorgenommen, wird der Abfrageplan der Prozedur bei der erneuten Kompilierung für diese Änderungen aktualisiert und optimiert. Dies kann die Verarbeitungsleistung der Prozedur verbessern.  
  
-   In manchen Fällen muss die erneute Prozedurkompilierung erzwungen werden, in anderen findet sie automatisch statt. Eine automatische erneute Kompilierung erfolgt bei jedem Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sie findet auch statt, wenn physische Entwurfsänderungen an einer zugrunde liegenden Tabelle vorgenommen wurden, auf die die Prozedur verweist.  
  
-   Eine erneute Kompilierung einer Prozedur kann auch erzwungen werden, um dem "Parametersniffing"-Verhalten bei der Kompilierung von Prozeduren entgegenzuwirken. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Prozeduren ausführt, werden alle bei der Kompilierung von der Prozedur verwendeten Parameterwerte in die Generierung des Abfrageplans einbezogen. Handelt es sich bei diesen Werten um die normalen Werte, mit denen die Prozedur anschließend aufgerufen wird, profitiert die Prozedur bei jeder Kompilierung und Ausführung vom Abfrageplan. Falls die Parameterwerte der Prozedur häufig untypisch sind, kann die Leistung durch Erzwingen einer erneuten Kompilierung der Prozedur und einen neuen Plan auf Grundlage anderer Parameterwerte verbessert werden.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht die erneute Kompilierung von Prozeduren auf Anweisungsebene. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherte Prozeduren erneut kompiliert, wird anstelle der vollständigen Prozedur nur die Anweisung kompiliert, die die erneute Kompilierung verursacht hat.  
  
-   Wenn bei bestimmten Abfragen in einer Prozedur regelmäßig untypische oder temporäre Werte verwendet werden, kann die Prozedurleistung verbessert werden, indem der RECOMPILE-Abfragehinweis in diesen Abfragen verwendet wird. Da anstelle der vollständigen Prozedur nur die Abfragen mit dem Abfragehinweis erneut kompiliert werden, wird das Verhalten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bei der erneuten Kompilierung auf Anweisungsebene imitiert. Zusätzlich zu den aktuellen Parameterwerten der Prozedur verwendet der RECOMPILE-Abfragehinweis beim Kompilieren der Anweisung auch die Werte von lokalen Variablen in der gespeicherten Prozedur. Weitere Informationen finden Sie unter [Abfragehinweis (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 **WITH RECOMPILE** -Option  
 Wenn diese Option beim Erstellen der Prozedurdefinition verwendet wird, erfordert sie die CREATE PROCEDURE-Berechtigung für die Datenbank und die ALTER-Berechtigung für das Schema, in dem die Prozedur erstellt wird.  
  
 Wenn diese Option in einer EXECUTE-Anweisung verwendet wird, erfordert sie EXECUTE-Berechtigungen für die Prozedur. Berechtigungen für die EXECUTE-Anweisung selbst sind nicht erforderlich, es sind jedoch Ausführungsberechtigungen für die Prozedur erforderlich, auf die in der EXECUTE-Anweisung verwiesen sind. Weitere Informationen finden Sie unter [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 **RECOMPILE**-Abfragehinweis  
 Diese Funktion wird beim Erstellen der Prozedur verwendet, und der Hinweis wird in [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen in der Prozedur eingeschlossen. Daher erfordert sie die CREATE PROCEDURE-Berechtigung für die Datenbank und die ALTER-Berechtigung für das Schema, in dem die Prozedur erstellt wird.  
  
 Gespeicherte Systemprozedur**sp_recompile**   
 Erfordert die ALTER-Berechtigung für die angegebene Prozedur.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>So kompilieren Sie eine gespeicherte Prozedur mithilfe der WITH RECOMPILE-Option erneut  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird die Prozedurdefinition erstellt.  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>So kompilieren Sie eine gespeicherte Prozedur mithilfe der WITH RECOMPILE-Option erneut  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird eine einfache Prozedur erstellt, die alle Mitarbeiter (mit Vor- und Nachnamen), ihre Stellenbezeichnungen und ihre Abteilungsnamen aus einer Sicht zurückgibt.  
  
     Kopieren Sie anschließend das zweite Codebeispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie dann auf **Ausführen**. Dadurch wird die Prozedur ausgeführt und der Abfrageplan der Prozedur erneut kompiliert.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspGetAllEmployees WITH RECOMPILE;  
GO  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-sprecompile"></a>So kompilieren Sie eine gespeicherte Prozedur mithilfe von sp_recompile erneut  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird eine einfache Prozedur erstellt, die alle Mitarbeiter (mit Vor- und Nachnamen), ihre Stellenbezeichnungen und ihre Abteilungsnamen aus einer Sicht zurückgibt.  
  
     Kopieren Sie anschließend das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie dann auf **Ausführen**. Dadurch wird die Prozedur nicht ausgeführt, aber für die erneute Kompilierung markiert, sodass ihr Abfrageplan bei der nächsten Ausführung der Prozedur aktualisiert wird.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'HumanResources.uspGetAllEmployees';  
GO  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Ändern einer gespeicherten Prozedur](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Umbenennen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [Anzeigen der Definition einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Anzeigen der Abhängigkeiten einer gespeicherten Prozedur](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
