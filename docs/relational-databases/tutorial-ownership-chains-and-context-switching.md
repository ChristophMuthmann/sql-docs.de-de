---
title: 'Tutorial: Besitzketten und Kontextwechsel | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
caps.latest.revision: ''
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1ec6c4b013fabd008d2de3388ea163eae0428dcb
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Anhand des Szenarios in diesem Lernprogramm werden [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Sicherheitskonzepte verdeutlicht, die Besitzketten und Kontextwechsel umfassen.  
  
> [!NOTE]  
> Damit Sie den Code ausführen können, der in diesem Lernprogramm enthalten ist, müssen Sie die Sicherheit für den gemischte Modus konfiguriert und die [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank installiert haben. Weitere Informationen zur Sicherheit für den gemischte Modus finden Sie unter [Auswählen eines Authentifizierungsmodus](../relational-databases/security/choose-an-authentication-mode.md).  
  
## <a name="scenario"></a>Szenario  
In diesem Szenario benötigen zwei Benutzer Konten, über die sie auf die Bestellungsdaten zugreifen können, die in der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank gespeichert sind. Es gelten folgende Anforderungen:  
  
-   Über das erste Konto (TestManagerUser) muss es möglich sein, alle Details in jeder Bestellung anzeigen zu können.  
  
-   Über das zweite Konto (TestEmployeeUser) muss es möglich sein, für Artikel, für die Teillieferungen eingegangen sind, folgende Informationen anzeigen zu können: Bestellnummer, Bestelldatum, Versanddatum, Produktnummern sowie die pro Bestellung bestellten und eingegangenen Artikel.  
  
-   Alle anderen Konten müssen ihre aktuellen Berechtigungen behalten.  
  
Damit die Anforderungen dieses Szenarios erfüllt werden können, ist dieses Beispiel in vier Abschnitte unterteilt, in denen die Konzepte für Besitzketten und Kontextwechsel dargestellt werden:  
  
1.  Konfigurieren der Umgebung.  
  
2.  Erstellen einer gespeicherten Prozedur, damit nach Bestellung auf die Daten zugegriffen werden kann.  
  
3.  Zugreifen auf die Daten über die gespeicherte Prozedur.  
  
4.  Zurücksetzen der Umgebung.  
  
Jeder Codeblock dieses Beispiels wird jeweils sofort erläutert. Informationen, wie Sie das vollständige Beispiel kopieren können, finden Sie unter [Vollständiges Beispiel](#CompleteExample) am Ende dieses Lernprogramms.  
  
## <a name="1-configure-the-environment"></a>1. Konfigurieren der Umgebung  
Verwenden Sie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] sowie den folgenden Code, um die `AdventureWorks2012`-Datenbank zu öffnen. Vergewissern Sie sich mit der [!INCLUDE[tsql](../includes/tsql-md.md)]-Anweisung `CURRENT_USER`, dass der Benutzer dbo als Kontext angezeigt wird.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
Weitere Informationen zur CURRENT_USER-Anweisung finden Sie unter [CURRENT_USER &#40;Transact-SQL&#41;](../t-sql/functions/current-user-transact-sql.md).  
  
Verwenden Sie diesen Code als Benutzer dbo dazu, auf dem Server und in der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]-Datenbank zwei Benutzer zu erstellen.  
  
```  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
Weitere Informationen zur CREATE USER-Anweisung finden Sie unter [CREATE USER &#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md). Weitere Informationen zur CREATE LOGIN-Anweisung finden Sie unter [CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md).  
  
Übertragen Sie mit dem folgenden Code den Besitz des `Purchasing` -Schemas auf das Konto `TestManagerUser` . Dadurch wird es ermöglicht, unter diesem Konto mit allen DML-Anweisungen (Data Manipulation Language, z. B. `SELECT` - und `INSERT` -Berechtigungen) auf die Objekte zuzugreifen, die das Schema enthält. `TestManagerUser` wird auch die Berechtigung zum Erstellen gespeicherter Prozeduren erteilt.  
  
```  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
Weitere Informationen zur GRANT-Anweisung finden Sie unter [GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md). Weitere Informationen zum Aufrufen von gespeicherten Prozeduren finden Sie unter [Gespeicherte Prozeduren &#40;Datenbankmodul&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md). Ein Poster mit allen [!INCLUDE[ssDE](../includes/ssde-md.md)]-Berechtigungen finden Sie unter [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster).  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2. Erstellen einer gespeicherten Prozedur für Zugriff auf Daten  
Um den Kontext innerhalb einer Datenbank zu wechseln, verwenden Sie die EXECUTE AS-Anweisung. EXECUTE AS erfordert IMPERSONATE-Berechtigungen.  
  
Im folgenden Code wird die `EXECUTE AS` -Anweisung dazu verwendet, einen Kontextwechsel auf `TestManagerUser` vorzunehmen und eine gespeicherte Prozedur zu erstellen, die nur die Daten anzeigt, die von `TestEmployeeUser`benötigt werden. Damit die Anforderungen erfüllt werden, ist die gespeicherte Prozedur wie folgt aufgebaut: Sie nimmt eine Variable für die Bestellnummer entgegen, zeigt keine Finanzinformationen an und enthält eine WHERE-Klausel, die die Ergebnisse auf Teillieferungen beschränkt.  
  
```  
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
Momentan kann `TestEmployeeUser` auf keines der Datenbankobjekte zugreifen. Der folgende Code (nach wie vor im `TestManagerUser` -Kontext) erteilt dem Benutzerkonto die Berechtigung, über die gespeicherte Prozedur Informationen aus den Basistabellen abrufen zu können.  
  
```  
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
Die gespeicherte Prozedur gehört, obwohl kein Schema explizit angegeben wurde, zum `Purchasing` -Schema, weil `TestManagerUser` standardmäßig dem `Purchasing` -Schema zugeordnet ist. Wie im folgenden Code gezeigt, können Sie Systemkataloginformationen dazu verwenden, nach Objekten zu suchen.  
  
```  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
Nachdem dieser Abschnitt des Beispiels abgeschlossen ist, wird im Code die `REVERT`-Anweisung dazu verwendet, wieder einen Kontextwechsel auf dbo vorzunehmen.  
  
```  
REVERT;  
GO  
```  
  
Weitere Informationen zur REVERT-Anweisung finden Sie unter [REVERT &#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md).  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3. Zugreifen auf Daten über die gespeicherte Prozedur  
`TestEmployeeUser` hat für die Objekte der [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] -Datenbank keine Berechtigungen, die über eine Anmeldung und die Berechtigungen hinausgehen, die der public-Datenbankrolle zugeordnet sind. Der folgende Code gibt einen Fehler zurück, wenn `TestEmployeeUser` versucht, auf eine der Basistabellen zuzugreifen.  
  
```  
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  
  
Über die gespeicherte Prozedur, die im vorherigen Abschnitt erstellt wurde, kann `TestManagerUser` auf die Basistabellen zugreifen, weil sich die Objekte, auf die in der gespeicherten Prozedur verwiesen wird, über den Besitz des `Purchasing` -Schemas im Besitz von `TestEmployeeUser` befinden. Im folgenden Code, für den weiterhin der `TestEmployeeUser` -Kontext verwendet wird, wird die Bestellnummer 952 als Parameter übergeben.  
  
```  
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4. Zurücksetzen der Umgebung  
Im folgenden Code wird der Befehl `REVERT` verwendet, um den Kontext des aktuellen Kontos auf `dbo`zurückzusetzen, und dann die Umgebung zurückgesetzt.  
  
```  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="CompleteExample"></a>Vollständiges Beispiel  
In diesem Abschnitt wird der vollständige Beispielcode angezeigt.  
  
> [!NOTE]  
> Dieser Code enthält nicht die beiden erwarteten Fehler, die verdeutlichen, dass `TestEmployeeUser` keine Informationen aus Basistabellen auswählen kann.  
  
```  
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  
