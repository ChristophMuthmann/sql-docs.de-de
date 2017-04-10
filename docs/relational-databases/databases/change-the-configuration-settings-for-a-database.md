---
title: "&#196;ndern der Konfigurationseinstellungen f&#252;r eine Datenbank | Microsoft Docs"
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
  - "Datenbankkonfiguration [SQL Server]"
  - "Konfigurationsoptionen (SQL Server), Datenbanken"
  - "Ändern von Datenbank-Konfigurationseinstellungen"
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# &#196;ndern der Konfigurationseinstellungen f&#252;r eine Datenbank
  In diesem Thema wird beschrieben, wie Optionen auf Datenbankebene in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)] geändert werden. Diese Optionen sind für jede Datenbank eindeutig und haben keinen Einfluss auf andere Datenbanken.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So ändern Sie die Optionseinstellungen für eine Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nur der Systemadministrator, der Datenbankbesitzer sowie Mitglieder der festen Serverrollen **sysadmin** und **dbcreator** und der festen Datenbankrolle **db_owner** können diese Optionen ändern.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So ändern Sie die Optionseinstellungen für eine Datenbank  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her, erweitern Sie den Server, erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf eine Datenbank, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Datenbankeigenschaften** auf **Optionen** , um auf die meisten Konfigurationseinstellungen zuzugreifen. Auf den entsprechenden Seiten finden Sie Datei- und Dateigruppenkonfigurationen, Spiegelung und Protokollversand.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So ändern Sie die Optionseinstellungen für eine Datenbank  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel werden die Optionen für das Wiederherstellungsmodell und die Datenseitenüberprüfung für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank festgelegt.  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../relational-databases/databases/codesnippet/tsql/change-the-configuration_1.sql)]  
  
 Weitere Beispiele finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).  
  
## Siehe auch  
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20\(Transact-SQL\).md)   
 [ALTER DATABASE-Datenbankspiegelung &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20HADR%20\(Transact-SQL\).md)   
 [Umbenennen einer Datenbank](../../relational-databases/databases/rename-a-database.md)   
 [Verkleinern einer Datenbank](../../relational-databases/databases/shrink-a-database.md)  
  
  