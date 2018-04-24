---
title: Hinzufügen von Abhängigkeiten zu einer Ressource von SQL Server | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: failover-clusters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- resource dependencies [SQL Server]
- failover clustering [SQL Server], dependencies
- clusters [SQL Server], dependencies
- dependencies [SQL Server], clustering
ms.assetid: 25dbb751-139b-4c8e-ac62-3ec23110611f
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a0b7dc1fee54afb366518547f4c2c9518843d0ed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="add-dependencies-to-a-sql-server-resource"></a>Hinzufügen von Abhängigkeiten zu einer Ressource von SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie einer AlwaysOn-Failoverclusterinstanz-Ressource mithilfe des Failovercluster-Manager-Snap-Ins Abhängigkeiten hinzugefügt werden. Das Failovercluster-Manager-Snap-In ist die Clusterverwaltungsanwendung für den WSFC (Windows Server Failover Clustering)-Dienst.  
  
-   **Vorbereitungen:**  [Einschränkungen](#Restrictions), [Voraussetzungen](#Prerequisites)  
  
-   **Hinzufügen einer Abhängigkeit zu einer SQL Server-Ressource mit:** [Windows-Failovercluster-Manager](#WinClusManager)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Beachten Sie, dass, wenn Sie der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Gruppe weitere Ressourcen hinzufügen, diese Ressourcen immer über eigene eindeutige SQL-Netzwerknamen und SQL-IP-Adressen verfügen müssen.  
  
 Verwenden Sie die vorhandenen Ressourcen an SQL-Netzwerknamen und SQL-IP-Adressen nur für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressourcen gemeinsam mit anderen Ressourcen verwendet werden, können die folgenden Probleme auftreten:  
  
-   Unerwartete Ausfallzeiten können auftreten.  
  
-   Service Pack-Installationen können fehlschlagen.  
  
-   Das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setupprogramm kann nicht erfolgreich ausgeführt werden. Wenn dieses Problem auftritt, können Sie keine zusätzlichen Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installieren oder Routinewartungsmaßnahmen ausführen.  
  
 Beachten Sie diese zusätzlichen Probleme:  
  
-   FTP mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikation: Bei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen, die FTP mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikation verwenden, muss der FTP-Dienst einen der physischen Datenträger verwenden, die auch die für den FTP-Dienst eingerichtete [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installation verwendet.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource: Wenn Sie einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Gruppe eine Ressource hinzufügen und auf der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource eine Abhängigkeit besteht, die die Verfügbarkeit von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sicherstellt, empfiehlt [!INCLUDE[msCoName](../../../includes/msconame-md.md)] das Hinzufügen einer Abhängigkeit auf der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Ressource. Fügen Sie keine Abhängigkeit auf der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource hinzu. Konfigurieren Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agent-Ressource so, dass bei einem Ausfall der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Agentressource die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Gruppe nicht beeinträchtigt. Auf diese Weise stellen Sie sicher, dass der Computer, auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt wird, hochverfügbar ist.  
  
-   Dateifreigabe- und Druckerressourcen: Dateifreigabe- und Druckerclusterressourcen sollten nicht dieselben physischen Datenträgerressourcen verwenden wie der Computer, auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt wird. Bei Verwendung derselben physischen Datenträgerressourcen kann es auf dem Computer, auf dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ausgeführt wird, zu Leistungsabfällen und Dienstausfällen kommen.  
  
-   Überlegungen zu MS DTC: Nachdem Sie das Betriebssystem installiert und die FCI konfiguriert haben, müssen Sie [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) mithilfe des Failovercluster-Manager-Snap-Ins für die Arbeit in einem Cluster konfigurieren. Wenn MS DTC nicht für die Ausführung in einem Cluster konfiguriert wird, führt dies nicht zu einer Blockierung des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setups, aber die Funktionalität der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anwendung kann beeinträchtigt sein, falls MS DTC nicht ordnungsgemäß konfiguriert wurde.  
  
     Wenn Sie MS DTC in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Gruppe installieren und gleichzeitig andere Ressourcen von MS DTC abhängig sind, steht MS DTC nicht zur Verfügung, wenn diese Gruppe offline ist oder ein Failover eintritt. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfiehlt, MS DTC möglichst in eine eigene Gruppe mit eigener physischer Datenträgerressource einzufügen.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in einer WSFC-Ressourcengruppe mit mehreren Laufwerken installieren und die Daten auf einem dieser Laufwerke speichern möchten, wird festgelegt, dass die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource ausschließlich von diesem Laufwerk abhängig ist. Um Daten oder Protokolle auf einem anderen Datenträger zu speichern, müssen Sie zuerst der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource eine Abhängigkeit für den zusätzlichen Datenträger hinzufügen.  
  
##  <a name="WinClusManager"></a> Verwenden des Failovercluster-Manager-Snap-Ins  
 **So fügen Sie einer SQL Server-Ressource eine Abhängigkeit hinzu**  
  
-   Öffnen Sie des Failovercluster-Manager-Snap-In.  
  
-   Suchen Sie die Gruppe, die die anwendbare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource enthält, für die Sie eine Abhängigkeit erstellen möchten.  
  
-   Wenn sich die Ressource für den Datenträger bereits in dieser Gruppe befindet, fahren Sie mit Schritt 4 fort. Andernfalls wechseln Sie zu der Gruppe, die den Datenträger enthält. Wenn diese Gruppe und die Gruppe, die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] enthält, nicht zum selben Knoten gehören, verschieben Sie die Gruppe mit der Ressource für den Datenträger zu dem Knoten mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Gruppe.  
  
-   Wählen Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Ressource aus, öffnen Sie das Dialogfeld **Eigenschaften** , und fügen Sie den Datenträger auf der Registerkarte **Abhängigkeiten** den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abhängigkeiten hinzu.  
  
  
