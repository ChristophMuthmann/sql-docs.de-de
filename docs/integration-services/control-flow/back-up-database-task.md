---
title: Sichern Sie den Task "Datenbank" | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a71821c8fc7710d86d819d65ef35878a2594f997
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="back-up-database-task"></a>Datenbank sichern (Task)
  Der Task Datenbank sichern führt verschiedene Arten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanksicherungen aus. Weitere Informationen finden Sie unter [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Mithilfe des Tasks Datenbank sichern kann ein Paket eine einzelne Datenbank oder mehrere Datenbanken sichern. Wenn mit dem Task nur eine einzelne Datenbank gesichert wird, können Sie die Sicherungskomponente auswählen: die Datenbank, oder ihre Dateien und Dateigruppen.  
  
## <a name="supported-recover-models-and-backup-types"></a>Unterstützte Wiederherstellungsmodelle und Sicherungstypen  
 In der folgenden Tabelle sind die Wiederherstellungsmodelle und Sicherungstypen aufgeführt, die vom Task Datenbank sichern unterstützt werden.  
  
|Wiederherstellungsmodell|Datenbank|Datenbank - differenziell|Transaktionsprotokoll|Datei oder differenzielle Datei|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Einfach|Required|Optional|Nicht unterstützt|Nicht unterstützt|  
|Full|Required|Optional|Required|Optional|  
|Massenprotokolliert|Required|Optional|Required|Optional|  
  
 Der Task Datenbank sichern kapselt eine BACKUP-Anweisung von Transact-SQL. Weitere Informationen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
## <a name="configuration-of-the-back-up-database-task"></a>Konfiguration des Tasks "Datenbank sichern"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Datenbank sichern“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  

