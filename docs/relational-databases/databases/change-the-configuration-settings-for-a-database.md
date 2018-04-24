---
title: Ändern der Konfigurationseinstellungen für eine Datenbank| Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database configuration [SQL Server]
- configuration options [SQL Server], databases
- modifying database configuration settings
ms.assetid: c29c3385-5043-400f-bb4e-044a4c9a9a4b
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5a52ea35b0af58e3a3299df2f0d2aa289ed3fde0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="change-the-configuration-settings-for-a-database"></a>Ändern der Konfigurationseinstellungen für eine Datenbank
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Optionen auf Datenbankebene in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]geändert werden. Diese Optionen sind für jede Datenbank eindeutig und haben keinen Einfluss auf andere Datenbanken.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Security](#Security)  
  
-   **So ändern Sie die Optionseinstellungen für eine Datenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Nur der Systemadministrator, der Datenbankbesitzer sowie Mitglieder der festen Serverrollen **sysadmin** und **dbcreator** und der festen Datenbankrolle **db_owner** können diese Optionen ändern.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>So ändern Sie die Optionseinstellungen für eine Datenbank  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz her, erweitern Sie den Server, erweitern Sie **Datenbanken**, klicken Sie mit der rechten Maustaste auf eine Datenbank, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Datenbankeigenschaften** auf **Optionen** , um auf die meisten Konfigurationseinstellungen zuzugreifen. Auf den entsprechenden Seiten finden Sie Datei- und Dateigruppenkonfigurationen, Spiegelung und Protokollversand.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-change-the-option-settings-for-a-database"></a>So ändern Sie die Optionseinstellungen für eine Datenbank  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel werden die Optionen für das Wiederherstellungsmodell und die Datenseitenüberprüfung für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Beispieldatenbank festgelegt.  
  
 [!code-sql[DatabaseDDL#AlterDatabase7](../../relational-databases/databases/codesnippet/tsql/change-the-configuration_1.sql)]  
  
 Weitere Beispiele finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [ALTER DATABASE-Datenbankspiegelung &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [Umbenennen einer Datenbank](../../relational-databases/databases/rename-a-database.md)   
 [Verkleinern einer Datenbank](../../relational-databases/databases/shrink-a-database.md)  
  
  
