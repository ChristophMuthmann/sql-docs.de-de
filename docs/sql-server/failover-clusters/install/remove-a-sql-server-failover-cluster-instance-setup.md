---
title: "Entfernen einer SQL Server-Failoverclusterinstanz (Setup) | Microsoft Docs"
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
  - "Cluster [SQL Server], Entfernen einer Failoverclusterinstanz"
  - "Failoverclustering [SQL Server], Entfernen einer Failoverclusterinstanz"
  - "Deinstallieren von Failoverclusterinstanzen"
  - "Entfernen von Failoverclusterinstanzen"
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# Entfernen einer SQL Server-Failoverclusterinstanz (Setup)
  Verwenden Sie diese Prozedur, um eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failoverclusterinstanz zu deinstallieren.  
  
> [!IMPORTANT]  
>  Um einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failovercluster zu aktualisieren oder zu entfernen, müssen Sie ein lokaler Administrator mit der Berechtigung zum Anmelden als Dienst auf allen Knoten des Failoverclusters sein.  
  
 **Vorbereitungen**  
  
 Berücksichtigen Sie die folgenden wichtigen Punkte, bevor Sie einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failovercluster deinstallieren:  
  
-   Wenn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client versehentlich deinstalliert wurde, können die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressourcen nicht gestartet werden. Um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu installieren, führen Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setupprogramm aus, um die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Voraussetzungen zu installieren.  
  
-   Wenn Sie einen Failovercluster deinstallieren, der über mehr als eine SQL IP-Clusterressource verfügt, müssen Sie die zusätzlichen SQL IP-Ressourcen mithilfe der Clusterverwaltung entfernen.  
  
 Informationen zur Syntax für die Eingabeaufforderung finden Sie unter [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
### So deinstallieren Sie einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failovercluster  
  
1.  Zur Deinstallation eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failovercluster verwenden Sie die vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Setup bereitgestellte Funktion Knoten entfernen, um jeden Knoten einzeln zu entfernen. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster &#40;Setup&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## Siehe auch  
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  