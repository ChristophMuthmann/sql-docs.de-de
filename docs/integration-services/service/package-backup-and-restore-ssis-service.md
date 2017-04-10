---
title: "Paketsicherung und -wiederherstellung (SSIS-Dienst) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SSIS-Pakete, sichern und wiederherstellen"
  - "Sichern von Paketen [Integration Services]"
  - "Pakete [Integration Services], sichern und wiederherstellen"
  - "SQL Server Integration Services-Pakete, sichern und wiederherstellen"
  - "Wiederherstellen von Paketen [Integration Services]"
  - "Integration Services-Pakete, sichern und wiederherstellen"
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Paketsicherung und -wiederherstellung (SSIS-Dienst)
    
> [!IMPORTANT]  
>  In diesem Thema wird der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst beschrieben, ein Windows-Dienst zur Verwaltung von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] unterstützt den Dienst für die Abwärtskompatibilität mit früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Ab [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]können Sie Objekte, z. B. Pakete, auf dem Integration Services-Server verwalten.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete können im Dateisystem oder in „msdb“, einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatenbank, gespeichert werden. In „msdb“ gespeicherte Pakete können mit den Sicherungs- und Wiederherstellungsfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesichert und wiederhergestellt werden.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Sichern und Wiederherstellen der msdb-Datenbank zu erhalten:  
  
-   [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält das Eingabeaufforderungs-Hilfsprogramm **dtutil** (dtutil.exec), das Sie zum Verwalten von Paketen verwenden können. Weitere Informationen finden Sie unter [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
## Konfigurationsdateien  
 Alle im Paket enthaltenen Konfigurationsdateien werden im Dateisystem gespeichert. Diese Dateien werden nicht gesichert, wenn Sie die msdb-Datenbank sichern. Deshalb müssen Sie sicherstellen, dass die Konfigurationsdateien regelmäßig im Rahmen Ihres Plans zur Sicherung von in „msdb“ gespeicherten Paketen gesichert werden. Um Konfigurationen in das Sichern der msdb-Datenbank einzubeziehen, sollten Sie erwägen, anstelle von dateibasierten Konfigurationen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurationstyp zu verwenden.  
  
## Im Dateisystem gespeicherte Pakete  
 Die im Dateisystem gespeicherte Sicherung von Paketen sollte in den Sicherungsplan einbezogen werden, mit dem das Dateisystem des Servers gesichert wird. Die Konfigurationsdatei des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Diensts, deren Standardname MsDtsSrvr.ini.xml lautet, enthält eine Aufstellung der Ordner auf dem Server, die vom Dienst überwacht werden. Sie sollten sicherstellen, dass diese Ordner gesichert werden. Außerdem können Pakete in anderen Ordnern auf dem Server gespeichert werden. Sie sollten sicherstellen, dass diese Ordner in den Sicherungsprozess einbezogen werden.  
  
  