---
title: Ändern einer gespeicherten Prozedur | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e1086da5c6be1703f0064d641c546c3eee211140
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="modify-a-stored-procedure"></a>Ändern einer gespeicherten Prozedur
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
    
##  <a name="Top"></a> In diesem Thema wird beschrieben, wie eine gespeicherte Prozedur mit [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]geändert wird.  
  
-   **Vorbereitungen:**  [Einschränkungen](#Restrictions), [Sicherheit](#Security)  
  
-   **So ändern Sie eine Prozedur mithilfe von:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -gespeicherte Prozeduren können nicht in CLR-gespeicherte Prozeduren geändert werden und umgekehrt.  
  
 Wenn die vorherige Prozedurdefinition mit WITH ENCRYPTION oder WITH RECOMPILE erstellt wurde, sind diese Optionen nur dann aktiviert, wenn sie in der ALTER PROCEDURE-Anweisung enthalten sind.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert ALTER PROCEDURE-Berechtigung für die Prozedur.  
  
##  <a name="Procedures"></a> Vorgehensweise: Ändern einer gespeicherten Prozedur  
 Sie können eine der folgenden Anwendungen verwenden:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So ändern Sie eine Prozedur in Management Studio**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, erweitern Sie die Datenbank, zu der die Prozedur gehört, und erweitern Sie dann **Programmierbarkeit**.  
  
3.  Erweitern Sie **Gespeicherte Prozeduren**, klicken Sie mit der rechten Maustaste auf die zu ändernde Prozedur, und klicken Sie dann auf **Ändern**.  
  
4.  Ändern Sie den Text der gespeicherten Prozedur.  
  
5.  Zum Testen der Syntax klicken Sie im Menü **Abfrage** auf **Analysieren**.  
  
6.  Um die Änderungen an der Prozedurdefinition zu speichern, klicken Sie im Menü **Abfrage** auf **Ausführen**.  
  
7.  Um die aktualisierte Prozedurdefinition als [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript zu speichern, klicken Sie im Menü **Datei** auf **Speichern unter**. Nehmen Sie den Dateinamen an oder ersetzen Sie ihn durch einen neuen Namen, und klicken Sie dann auf **Speichern**.  
  
> [!IMPORTANT]  
>  Überprüfen Sie alle Benutzereingaben. Verketten Sie keine Benutzereingaben, bevor Sie sie überprüft haben. Führen Sie niemals Befehle aus, die sich aus nicht überprüften Benutzereingaben zusammensetzen.  
  
###  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie eine Prozedur im Abfrage-Editor**  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, und erweitern Sie die Datenbank, der die Prozedur angehört. Oder wählen Sie die Datenbank über die Symbolleiste aus der Liste der verfügbaren Datenbanken aus. Wählen Sie für dieses Beispiel die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank aus.  
  
3.  Klicken Sie im Menü **Datei** auf **Neue Abfrage**.  
  
4.  Kopieren Sie das folgenden Beispiel, und fügen Sie es in den Abfrage-Editor ein. Im ersten Beispiel wird die `uspVendorAllInfo` -Prozedur erstellt. Diese Prozedur gibt die Namen, die gelieferten Produkte, die Bonität und die Verfügbarkeit aller Hersteller in der [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] -Datenbank, die das Unternehmen beliefern, zurück.  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  Klicken Sie im Menü **Datei** auf **Neue Abfrage**.  
  
6.  Kopieren Sie das folgenden Beispiel, und fügen Sie es in den Abfrage-Editor ein. Im Beispiel wird die `uspVendorAllInfo` -Prozedur geändert. Die EXECUTE AS CALLER-Klausel wird entfernt, und der Textkörper der Prozedur wird so geändert, dass nur Hersteller zurückgegeben werden, die das angegebene Produkt liefern. Mit den Funktionen `LEFT` und `CASE` wird die Darstellung des Resultsets angepasst.  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  Um die Änderungen an der Prozedurdefinition zu speichern, klicken Sie im Menü **Abfrage** auf **Ausführen**.  
  
8.  Um die aktualisierte Prozedurdefinition als [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript zu speichern, klicken Sie im Menü **Datei** auf **Speichern unter**. Nehmen Sie den Dateinamen an oder ersetzen Sie ihn durch einen neuen Namen, und klicken Sie dann auf **Speichern**.  
  
9. Um die geänderte gespeicherte Prozedur auszuführen, führen Sie das folgende Beispiel aus.  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
  
