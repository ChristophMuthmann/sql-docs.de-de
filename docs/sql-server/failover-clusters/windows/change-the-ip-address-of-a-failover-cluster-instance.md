---
title: "&#196;ndern der IP-Adresse einer Failoverclusterinstanz | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ändern von IP-Adressen"
  - "Failoverclustering [SQL Server], IP-Adressen"
  - "IP-Adressen [SQL Server]"
  - "Cluster [SQL Server], IP-Adressen"
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
caps.latest.revision: 33
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 33
---
# &#196;ndern der IP-Adresse einer Failoverclusterinstanz
  In diesem Thema wird beschrieben, wie die IP-Adressressource in einer Always On-Failoverclusterinstanz (FCI) mithilfe des Failovercluster-Manager-Snap-Ins geändert wird. Das Failovercluster-Manager-Snap-In ist die Clusterverwaltungsanwendung für den WSFC (Windows Server Failover Clustering)-Dienst.  
  
-   **Vorbereitungen:**  [Sicherheit](#Security)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Bevor Sie beginnen, lesen Sie sich das folgende Thema in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Onlinedokumentation durch: [Vor dem Installieren des Failoverclusterings](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Zum Warten oder Aktualisieren einer FCI müssen Sie ein lokaler Administrator sein und über die Berechtigung verfügen, sich bei allen Knoten der FCI als Dienst anzumelden.  
  
##  <a name="WSFC"></a> Verwenden des Failovercluster-Manager-Snap-Ins  
 **So ändern Sie die IP-Adressressource für eine FCI**  
  
1.  Öffnen Sie des Failovercluster-Manager-Snap-In.  
  
2.  Erweitern Sie den Knoten **Dienste und Anwendungen** im linken Bereich, und klicken Sie auf die FCI.  
  
3.  Klicken Sie im rechten Bereich unter der Kategorie **Servername** mit der rechten Maustaste auf die SQL Server-Instanz, und wählen Sie die Option **Eigenschaften**, um das Dialogfeld **Eigenschaften** zu öffnen.  
  
4.  Ändern Sie auf der Registerkarte **Allgemein** die IP-Adressressource.  
  
5.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
6.  Klicken Sie im rechten Fensterbereich mit der rechten Maustaste auf „SQL IP Address1(Name der Failoverclusterinstanz)“, und wählen Sie **Offline schalten** aus. SQL IP Address1(failover cluster instance name), SQL Network Name(failover cluster instance name) und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Statusänderung von Online in Ausstehende Offlineschaltung und anschließend Offline werden angezeigt.  
  
7.  Klicken Sie im rechten Fensterbereich mit der rechten Maustaste auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], und klicken Sie dann auf **Online schalten**. SQL IP Address1(failover cluster instance name), SQL Network Name(failover cluster instance name) und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Statusänderung von Offline in Ausstehende Onlineschaltung und anschließend Online werden angezeigt.  
  
8.  Schließen Sie das Failovercluster-Manager-Snap-In.  
  
  