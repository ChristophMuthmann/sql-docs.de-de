---
title: "Datenbankintegrit&#228;t &#252;berpr&#252;fen (Task) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.checkdatabaseintegritytask.f1"
helpviewer_keywords: 
  - "Datenintegrität [Integration Services]"
  - "Datenbankintegrität überprüfen (Task) [Integration Services]"
  - "Überprüfen der Datenbankintegrität"
  - "Datenbank-Konsistenzprüfungen [Integration Services]"
  - "Überprüfen der Datenbankintegrität"
  - "Integritätsprüfungen [Integration Services]"
ms.assetid: 5a82fe99-4503-429f-9337-e6bac7649fe4
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Datenbankintegrit&#228;t &#252;berpr&#252;fen (Task)
  Der Task Datenbankintegrität überprüfen überprüft die Zuordnung und strukturelle Integrität aller Objekte in der angegebenen Datenbank. Mit dem Task können Sie eine einzelne Datenbank oder mehrere Datenbanken überprüfen und auswählen, ob auch die Datenbankindizes überprüft werden sollen.  
  
 Der Task "Datenbankintegrität überprüfen" kapselt die DBCC CHECKDB-Anweisung. Weitere Informationen finden Sie unter [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).  
  
## Konfiguration des Tasks "Datenbankintegrität überprüfen"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task 'Datenbankintegrität überprüfen' &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/check-database-integrity-task-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
  