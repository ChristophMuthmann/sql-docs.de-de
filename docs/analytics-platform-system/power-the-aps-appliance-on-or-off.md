---
title: Schalten Sie das Gerät ein- oder ausschalten - Analytics Platform System | Microsoft Docs
description: Schalten Sie das Gerät aktiviert oder deaktiviert für Analytics Platform System
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 54829190d03a889ade31383662bf192516934012
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Schalten Sie das Gerät aktiviert oder deaktiviert für Analytics Platform System
In diesem Thema wird beschrieben, wie zum Einschalten oder Ausschalten der Analytics Platform Systemappliance, die Parallel Data Warehouse ausgeführt wird, und optional eine HDInsight-Region ausgeführt werden. Mithilfe dieser Informationen beim Verschieben einer Analytics Platform System Appliance oder Power auf eine Anwendung nach einem schwerwiegenden Stromausfall.  
  
Das Gerät eingeschaltet, ein- oder ausschalten ist nicht identisch mit der Appliance-Dienste starten und beenden. Informationen zu diesem Thema finden Sie unter [PDW-Dienststatus &#40;Analyseplattformsystem&#41;](pdw-services-status.md). Informationen zum Aktivieren oder Deaktivieren einer SQL Server 2008 Parallel Data Warehouse bereitstellen finden Sie unter der SQL Server 2008 Parallel Data Warehouse-Hilfedatei. Informationen zum Aktivieren oder Deaktivieren einer SQL Server 2012 AU1 oder AU2 Parallel Data Warehouse bereitstellen finden Sie unter der Hilfedatei für diesen Versionen.  
  
Wenn diese Anweisungen angeben, Herstellen einer Verbindung mit einem SQL Server PDW-Knoten, die Verbindung kann mit der angeschlossene Geräte (KVM) lokale oder Remote mithilfe von Remotedesktop. Einige Aktionen muss physisch (Netzschalter aktivieren) und (z. B. das Herunterfahren der) kann physische oder mithilfe der Windows-Befehle.  
  
Verbindungen mit SQL Server PDW-Knoten können vorgenommen werden, verwenden die IP-Adressen zugewiesen werden, können Sie die Knoten und aus der **HST01** Computer, indem Sie entweder die **Failovercluster-Manager** (**cluadmin.msc**) oder **Hyper-V-Manager** (**virtmgmt.msc**) Anwendungen und der rechten Maustaste auf den Knotennamen.  
  
## <a name="PowerOff"></a>Schalten Sie das Gerät  
  
### <a name="before-you-begin"></a>Vorbereitungen  
Vor dem Ausschalten der Appliance, sollten Sie alle Aktivitäten auf dem Gerät beenden. Um alle Aktivitäten zu beenden:  
  
-   Verwenden der **Sitzungen** auf der Seite der Verwaltungskonsole, um den aktuellen Benutzer zu identifizieren. Wenden Sie sich an diese, und bitten Sie ihn, melden Sie sich ab.  
  
-   Bei Bedarf können die **KILL** Anweisung, um das Beenden einer Verbindung von Clients zu erzwingen. Seien Sie vorsichtig beim Abbrechen von Verbindungen. Wenn einige transaktionalen Prozessen, z. B. eine lang ausgeführte Update unterbrochen muss rollbackaktivität vor SQL Server die Wiederherstellung der Datenbank abgeschlossen werden kann. Rollback einem teilweise abgeschlossenen Update- oder Delete, kann zeitaufwendig sein.  
  
### <a name="to-power-off-the-appliance"></a>So schalten Sie das Gerät  
  
> [!WARNING]  
> Alle Schritte müssen ausgeführt werden, in der exakten Reihenfolge aufgeführt, und jeder Schritt muss abschließen, bevor der nächste Schritt ausgeführt wird, sofern nicht anders angegeben. Ausführen der Schritte, die außerhalb der Reihenfolge oder ohne zu warten, für die einzelnen Schritte zum Abschließen kann zu Fehlern führen, wenn das Gerät zu einem späteren Zeitpunkt hochgefahren ist.  
  
1.  Herstellen einer Verbindung mit dem Steuerungsknoten PDW (***PDW_region *-CTL01** ), und melden Sie sich mit dem Analytics Platform System Appliance-Domänenadministratorkonto.  
  
2.  Führen Sie `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` So öffnen die **Configuration Manager**.  
  
3.  In der Configuration Manager unter der **Parallel Data Warehouse-Topologie** im Menü klicken Sie auf die **Dienststatus** Registerkarte, und klicken Sie auf **beenden Region** , PDW-Dienste zu beenden.  
  
4.  Wenn unter eine HDInsight-Region, besteht der **HDInsight Topology** im Menü klicken Sie auf die **Dienststatus** Registerkarte, und klicken Sie auf **Region beenden** beim Beenden der HDInsight-Dienste.  
  
5.  Herstellen einer Verbindung mit ***Appliance_domain *-HST01** und melden Sie sich mit dem Domänenadministratorkonto Appliance.  
  
6.  Mithilfe der **Failovercluster-Manager** Herstellen einer Verbindung mit der ***Appliance_domain *-WFOHST01** als Clusterressource konfigurieren, wenn nicht automatisch verbunden, und klicken Sie dann im Navigationsbereich auf **Rollen**. In der **Rollen** Bereich:  
  
    1.  Alle virtuellen Computer mit mehreren auswählen. Diese Maustaste, und wählen **Herunterfahren**.  
  
    2.  Warten Sie, bis alle ausgewählten virtuellen Computer herunterfahren abgeschlossen ist.  
  
7.  Wenn eine HDInsight-Region wird:  
  
    1.  Mit dem HDInsight-Cluster verbinden. Zu diesem Zweck mit der Maustaste auf **Failovercluster-Manager**Option **Verbindung mit Cluster herstellen**, und geben Sie ***Appliance_domain *-WFOHST02** für den Clusternamen.  
  
    2.  Klicken Sie unter dem HDInsight-Cluster auf **Rollen**. In der **Rollen** Bereich:  
  
        1.  Mehrfachauswahl aller virtuellen Maschinen, mit der rechten Maustaste sie, und wählen Sie **Herunterfahren**.  
  
        2.  Warten Sie, bis der virtuelle Computer heruntergefahren.  
  
8.  Schließen der **Failovercluster-Manager** Anwendung.  
  
9. Fahren Sie alle Server außer ***Appliance_domain *-HST01**.  
  
10. Herunterfahren der ***Appliance_domain *-HST01** Server.  
  
11. Schließen Sie die Stromverteilereinheiten (PDUs).  
  
## <a name="PowerOn"></a>Schalten Sie das Gerät  
  
### <a name="to-power-on-the-appliance"></a>So schalten Sie das Gerät  
  
> [!WARNING]  
> Alle Schritte müssen ausgeführt werden, in der exakten Reihenfolge aufgeführt, und jeder Schritt muss abschließen, bevor der nächste Schritt ausgeführt wird, sofern nicht anders angegeben. Schritte außerhalb der Reihenfolge oder ohne zu warten, für die einzelnen Schritte zum Abschließen kann dazu führen, dass Fehler beim Starten.  
  
1.  Schalten Sie die Stromverteilereinheiten (PDUS) und warten Sie die Schalter für den automatischen start.  
  
2.  Schalten Sie die ***Appliance_domain *-HST01** Server.  
  
3.  Melden Sie sich auf ***Appliance_domain *-HST01** als Domänenadministrator Appliance.  
  
4.  Starten Sie die **Hyper-V-Manager** Programm (**virtmgmt.msc**) und Herstellen einer Verbindung mit ***Appliance_domain *-HST01** standardmäßig keine Verbindung hergestellt.  
  
    1.  Wenn Sie anhand des Namens herstellen können, da die ***PDW_region *-AD01** wird nicht ausgeführt wird, versuchen Sie es mithilfe der IP-Adresse.  
  
    2.  In der **VMs** Bereich Suchen ***PDW_region *-AD01** und vergewissern Sie sich, dass er ausgeführt wird. Wenn dies nicht der Fall ist, starten Sie diesen virtuellen Computer, und warten Sie, bis er vollständig gestartet werden soll.  
  
5.  Schalten Sie die restlichen Server in der Einheit.  
  
6.  Während der **HST01** aus als der Appliance-Domänenadministrator angemeldet **Hyper-V-Manager**:  
  
    1.  Herstellen einer Verbindung mit ***Appliance_domain *-HST02**.  
  
    2.  In der **VMs** Bereich Suchen ***PDW_region *-AD02** und vergewissern Sie sich, dass er ausgeführt wird.  Wenn dies nicht der Fall ist, starten Sie diesen virtuellen Computer, und warten Sie, bis er vollständig gestartet werden soll.  
  
7.  Mithilfe der **Failovercluster-Manager** Herstellen einer Verbindung mit der ***Appliance_domain *-WFOHST01** -cluster, wenn nicht automatisch verbunden, und klicken Sie dann in der **Navigation** Bereich, klicken Sie auf **Rollen**. In der **Rollen** Bereich:  
  
    1.  Alle virtuellen Computer mit der rechten Maustaste sie, und klicken Sie dann auf Mehrfachauswahl **starten**.  
  
    2.  Warten Sie, bis alle ausgewählten virtuellen Computer starten, bevor Sie fortfahren mit dem nächsten Schritt abgeschlossen ist.  
  
    3.  Bei Bedarf für die virtuellen Computer, die ein Failover ausgeführt werden, Herunterfahren, verschieben und sie auf den entsprechenden primären Server neu starten.  
  
8.  Wenn das Gerät eine HDInsight-Region aufweist, verbinden Sie mit dem HDInsight-Cluster. (Zu diesem Zweck mit der Maustaste auf **Failovercluster-Manager**Option **Verbindung mit Cluster herstellen**, und geben Sie ***Appliance_domain *-WFOHST01** für den Namen des Clusters.)  
  
    1.  Klicken Sie unter dem HDInsight-Cluster auf **Rollen**. In der **Rollen** Bereich.  
  
        1.  Mehrfachauswahl aller virtuellen Maschinen, mit der rechten Maustaste sie, und wählen Sie **starten**,  
  
        2.  Warten Sie, bis alle ausgewählten virtuellen Computer starten, bevor Sie fortfahren mit dem nächsten Schritt abgeschlossen ist.  
  
        3.  Bei Bedarf für die virtuellen Computer, die ein Failover ausgeführt werden, Herunterfahren Sie, verschieben Sie sie, und starten sie auf den entsprechenden primären Server neu.  
  
9. Trennen von **HST01** gegebenenfalls.  
  
10. Herstellen einer Verbindung mit ***PDW_region *-CTL01** mithilfe des Domänenadministratorkontos Appliance.  
  
11. Führen Sie `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` zum Starten der **Configuration Manager**.  
  
12. In der **Configuration Manager**in der **Parallel Data Warehouse-Topologie** Menü klicken Sie auf die **Dienststatus** Registerkarte, und klicken Sie auf **starten Region**PDW-Dienste zu starten.  
  
13. Verfügt die Anwendung eine HDInsight-Region, in der Menüleiste HDInsight Topology klicken Sie auf die **Dienststatus** Registerkarte, und klicken Sie auf **starten Region** auf die HDInsight-Dienste zu starten.  
  
### <a name="to-verify-the-appliance-health"></a>So überprüfen die Appliance-Integrität  
Nachdem die Anwendung gestartet wurde, öffnen Sie die **Admin Console** und überprüfen Sie die Seite "Integrität" für Warnungen, die fehlerbedingung hinweisen. Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Siehe auch  
[Appliance-Verwaltungsaufgaben &#40;Analyseplattformsystem&#41;](appliance-management-tasks.md)  
  
