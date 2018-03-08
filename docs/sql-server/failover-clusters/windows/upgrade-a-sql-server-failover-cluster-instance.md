---
title: Aktualisieren einer SQL Server-Failoverclusterinstanz| Microsoft-Dokumentation
ms.custom: 
ms.date: 10/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: failover-clusters
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
caps.latest.revision: "47"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 48d80ca9c0e939f0d70cac411014b41cc1e777b4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>Aktualisieren einer SQL Server-Failoverclusterinstanz
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt das Upgraden eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failoverclusters auf eine neue Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], auf ein neues [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Service Pack oder ein kumulatives Update, wobei die Downtime auf ein einzelnes manuelles Failover (oder bei einem Failback auf den ursprünglichen primären Cluster auf zwei manuelle Failovers) beschränkt ist. Das Gleiche gilt, wenn ein neues Windows Service Pack oder kumulatives Windows-Update einzeln auf allen Failoverclusterknoten installiert wird.  
  
 Das Upgraden des Windows-Betriebssystems eines Failoverclusters wird für Betriebssysteme, die älter als [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] sind, nicht unterstützt. Weitere Informationen zum Upgraden eines Clusterknotens, der unter [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] oder höher ausgeführt wird, finden Sie unter [Perform a rolling upgrade or update (Ausführen eines parallelen Upgrades oder Updates)](#perform-a-rolling-upgrade-or-update).  
  
 Informationen zur Unterstützung:  
  
-   Ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Upgrade kann über die Benutzeroberfläche und über die Befehlszeile ausgeführt werden. Sie können das Upgrade auf jedem Failoverclusterknoten an der Eingabeaufforderung oder über die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setupbenutzeroberfläche ausführen, um die einzelnen Clusterknoten zu aktualisieren.  Weitere Informationen finden Sie unter [Aktualisieren einer SQL Server-Failoverclusterinstanz (Setup)](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) und [Install SQL Server from the Command Prompt (Installieren von SQL Server über die Eingabeaufforderung)](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
-   Die folgenden Szenarien werden bei einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Upgrade nicht unterstützt:  
  
    -   Sie können kein Upgrade von einer eigenständigen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf einen Failovercluster ausführen.  
  
    -   Sie können einem Failovercluster keine Features hinzufügen. Beispielsweise können Sie einem vorhandenen Nur- [!INCLUDE[ssDE](../../../includes/ssde-md.md)] -Failovercluster nicht [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]hinzufügen.  
  
    -   Sie können Failoverclusterknoten nicht zu einer eigenständigen Instanz herabstufen.  
  
    -   Änderungen der Edition des Failoverclusters sind auf bestimmte Szenarien beschränkt. Weitere Informationen finden Sie unter [Unterstützte Versions- und Editionsupgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Während des Failoverclusterupgrades wird die Ausfallzeit auf die Failoverzeit und auf die Ausführungszeit der Upgradeskripts begrenzt. Wenn Sie ein paralleles Upgrade eines Failoverclusters wie unten beschrieben ausführen und vor Beginn des Upgrades alle Voraussetzungen auf allen Knoten erfüllt sind, ist die Downtime minimal. Wenn während des Upgrades von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] speicheroptimierte Tabellen verwendet werden, erfordert das Upgrade zusätzliche Zeit. Weitere Informationen finden Sie unter [Planen und Testen des Upgradeplans für das Datenbankmodul](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Lesen Sie die folgenden wichtigen Informationen, bevor Sie beginnen:  
  
-   [Supported Version and Edition Upgrades (Unterstützte Versions- und Editionsupgrades)](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): Überprüfen Sie, ob Sie von Ihrer Version des Windows-Betriebssystems und Ihrer Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] upgraden können. Sie können beispielsweise kein direktes Upgrade von einer SQL Server 2005-Failoverclusterinstanz auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ausführen und keinen Failovercluster upgraden, der unter [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)] ausgeführt wird.  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): Wählen Sie die passende Upgrademethode und die Schritte aus, die sowohl auf Ihrer Betrachtung der unterstützten Version und Editionsupgrades als auch auf den anderen in Ihrer Umgebung installierten Komponenten basieren, um die Komponenten in der richtigen Reihenfolge upzugraden.  
  
-   [Planen und Testen des Upgradeplans für das Datenbankmodul](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): Überprüfen Sie die Anmerkungen zu dieser Version, die bekannten Upgradeprobleme und die Prüfliste vor dem Upgrade. Entwickeln und testen Sie den Upgradeplan.  
  
-   [Hardware- und Softwareanforderungen für die Installation von SQL Server](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): Überprüfen Sie die Softwareanforderungen für die Installation von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Falls zusätzliche Software erforderlich ist, installieren Sie diese auf jedem Knoten, bevor Sie mit dem Upgradevorgang beginnen, um die Downtime zu minimieren.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>Ausführen eines parallelen Upgrades oder Updates  
 Verwenden Sie für das Upgrade eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusters auf [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup, um das Upgrade jedes Failoverclusterknotens einzeln nacheinander auszuführen. Dabei sollte mit den passiven Knoten begonnen werden. Beim Aktualisieren der einzelnen Knoten wird der jeweilige Knoten nicht als möglicher Besitzer des Failoverclusters angezeigt. Im Fall eines unerwarteten Failovers können die aktualisierten Knoten erst im Failover verwendet werden, wenn der Besitz von Clusterressourcengruppen vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup zu einem aktualisierten Knoten verschoben wurde.  
  
 In der Standardeinstellung wird vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup automatisch festgelegt, wann ein Failover zu einem aktualisierten Knoten auszuführen ist. Dies ist von der Gesamtanzahl der Knoten in der Failoverclusterinstanz und der Anzahl der bereits aktualisierten Knoten abhängig. Wenn bereits mindestens die Hälfte der Knoten aktualisiert wurde und Sie das Upgrade für den nächsten Knoten ausführen, löst das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup einen Failover zu einem aktualisierten Knoten aus. Nach dem Failover zu einem aktualisierten Knoten wird die Clustergruppe in einen aktualisierten Knoten verschoben. Alle aktualisierten Knoten werden in die Liste möglicher Besitzer eingefügt. Alle Knoten, die noch nicht aktualisiert wurden, werden aus der Liste möglicher Besitzer entfernt. Jeder verbleibende Knoten, den Sie aktualisieren, wird der Liste möglicher Besitzer des Failoverclusters hinzugefügt.  
  
 Durch diesen Vorgang wird die Ausfallzeit während der gesamten Failoverclusteraktualisierung auf eine Failoverzeit und die Ausführungszeit für Aktualisierungsskripts begrenzt.  
  
 Führen Sie zum Steuern des Failoververhaltens von Clusterknoten während des Upgradevorgangs den Upgradevorgang über die Eingabeaufforderung aus, und verwenden Sie dabei den /FAILOVERCLUSTERROLLOWNERSHIP-Parameter. Weitere Informationen finden Sie unter [Installieren von SQL Server über die Eingabeaufforderung](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="next-steps"></a>Nächste Schritte  
 [Upgrade von SQL Server mithilfe des Installations-Assistenten &#40;Setup&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Installieren von SQL Server von der Eingabeaufforderung](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Aktualisieren einer SQL Server-Failoverclusterinstanz &#40;Setup&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
