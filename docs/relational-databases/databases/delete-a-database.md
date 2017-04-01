---
title: "L&#246;schen einer Datenbank | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbank entfernen [SQL Server], SQL Server Management Studio"
  - "Entfernen von Datenbanken"
  - "Löschen von Datenbanken"
  - "Datenbanken löschen"
  - "Datenbanken [SQL Server], löschen"
  - "Datenbank entfernen [SQL Server]"
ms.assetid: 1fd8c0f5-03e1-449a-af45-b8cacb479d9c
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# L&#246;schen einer Datenbank
  In diesem Thema wird beschrieben, wie eine benutzerdefinierte Datenbank unter [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] gelöscht wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie eine Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:** [Nach dem Löschen einer Datenbank](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Systemdatenbanken können nicht gelöscht werden.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Löschen Sie alle Datenbankmomentaufnahmen, die in der Datenbank vorhanden sind. Weitere Informationen finden Sie unter [Löschen einer Datenbank-Momentaufnahme &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md).  
  
-   Wenn für die Datenbank der Protokollversand konfiguriert ist, entfernen Sie diesen.  
  
-   Wenn die Datenbank für die Transaktionsreplikation oder für die Mergereplikation veröffentlicht ist bzw. Abonnent der Mergereplikation ist, entfernen Sie die Replikation aus der Datenbank.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Ziehen Sie in Betracht, eine vollständige Sicherung der Datenbank vorzunehmen. Eine gelöschte Datenbank kann nur neu erstellt werden, indem eine Sicherungskopie wiederhergestellt wird.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Für die Ausführung von DROP DATABASE benötigt ein Benutzer zumindest die CONTROL-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So löschen Sie eine Datenbank  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf die zu löschende Datenbank, und klicken Sie dann auf **Löschen**.  
  
3.  Bestätigen Sie, dass die richtige Datenbank ausgewählt ist, und klicken Sie dann auf **OK**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So löschen Sie eine Datenbank  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel werden die Datenbanken `Sales` und `NewSales` entfernt.  
  
```tsql  
USE master ;  
GO  
DROP DATABASE Sales, NewSales ;  
GO  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Löschen einer Datenbank  
 Sichern Sie die **master** -Datenbank. Wenn die **master** -Datenbank wiederhergestellt werden muss, können Fehlermeldungen auftreten, falls in den Systemkatalogsichten weiterhin Verweise auf Datenbanken bestehen, die seit der letzten Sicherung der **master** -Datenbank gelöscht wurden.  
  
## Siehe auch  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  