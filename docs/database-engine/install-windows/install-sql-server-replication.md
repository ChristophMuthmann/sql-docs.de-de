---
title: "Installieren der SQL&#160;Server-Replikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Komponenten [SQL Server-Replikation]"
  - "Befehlszeileninstallationen [SQL Server-Replikation]"
  - "Installieren der Replikation"
  - "Replikation [SQL Server], installieren"
  - "Eingabeaufforderung [SQL Server-Replikation]"
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 41
---
# Installieren der SQL&#160;Server-Replikation
  Die Replikationskomponenten können mithilfe des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder über die Eingabeaufforderung installiert werden. Installieren Sie die Replikation, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren oder wenn Sie eine vorhandene Instanz ändern.  
  
 Nachdem die Replikationskomponenten installiert wurden, müssen Sie den Server konfigurieren, um die Replikation verwenden zu können. Weitere Informationen finden Sie unter [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
> [!IMPORTANT]  
>  Wenn Sie Replikationskomponenten während der Änderung einer vorhandenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installieren, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent nach Abschluss der Installation beenden und neu starten. Dadurch wird sichergestellt, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent die Subsysteme des Replikations-Agents erkennt und Replikations-Agents in Auftragsschritten aufrufen kann.  
  
## Installieren der Replikation mithilfe des Setups  
 **So installieren Sie die Replikation, wenn Sie eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Wählen Sie zum Installieren der Replikationskomponenten, einschließlich der Replikationsverwaltungsobjekte (Replication Management Objects, RMO), auf der Seite **Funktionsauswahl** des Installations-Assistenten die Option **SQL Server-Replikation** aus.  
  
## Installieren der Replikation an der Eingabeaufforderung  
 **So installieren Sie die Replikation, wenn Sie eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Siehe [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## Siehe auch  
 [Installieren von SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)   
 [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  