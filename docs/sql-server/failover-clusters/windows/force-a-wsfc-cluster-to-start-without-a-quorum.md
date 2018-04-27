---
title: Erzwingen des Starts eines WSFC-Clusters ohne Quorum | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: 4a121375-7424-4444-b876-baefa8fe9015
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1dc0a48eda49aaa40b9e40339975bb8f1c1f21f3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="force-a-wsfc-cluster-to-start-without-a-quorum"></a>Erzwingen des Starts eines Clusters ohne Quorum
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie der Start eines Windows Server-Failoverclustering-Clusterknotens ohne Quorum erzwungen wird.  Dies ist möglicherweise für die Notfallwiederherstellung sowie in Multisubnetzszenarien erforderlich, um Daten wiederherzustellen die hohe Verfügbarkeit für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] - und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanzen wieder vollständig einrichten zu können.  
  
-   **Vorbereitungen:**  [Empfehlungen](#Recommendations), [Sicherheit](#Security)  
  
-   **So erzwingen Sie den Start eines Clusters ohne Quorum:**  [Verwenden des Failovercluster-Managers](#FailoverClusterManagerProcedure), [Verwenden von PowerShell](#PowerShellProcedure), [Verwenden von Net.exe](#CommandPromptProcedure)  
  
-   **Nachverfolgung:**  [Nachverfolgung: Nach dem Erzwingen des Clusterstarts ohne ein Quorum](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Ohne anderslautende Angaben sind die in diesem Thema beschriebenen Prozeduren anwendbar, wenn sie von einem beliebigen Knoten im WSFC-Cluster ausgeführt werden.  Sie erzielen jedoch u. U. bessere Ergebnisse und vermeiden Netzwerkprobleme, indem Sie diese Schritte von dem Knoten ausführen, von dem aus der Start ohne Quorum erzwungen werden soll.  
  
###  <a name="Security"></a> Sicherheit  
 Der Benutzer muss einem Domänenkonto entsprechen, das Mitglied der lokalen Administratorgruppe an jedem Knoten des WSFC-Clusters ist.  
  
##  <a name="FailoverClusterManagerProcedure"></a> Verwenden des Failovercluster-Managers  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>So erzwingen Sie den Start eines Clusters ohne Quorum  
  
1.  Öffnen Sie einen Failovercluster-Manager, und stellen Sie eine Verbindung mit dem gewünschten Clusterknoten her, um dessen Onlineschaltung zu erzwingen.  
  
2.  Klicken Sie im **Aktionsbereich** auf **Clusterstart erzwingen**, und klicken Sie dann auf **Ja – Start des Clusters erzwingen**.  
  
3.  Klicken Sie im linken Bereich in der Struktur **Failovercluster-Manager** auf den Clusternamen.  
  
4.  Stellen Sie im Zusammenfassungsbereich sicher, dass für **Quorumkonfiguration** als aktueller Wert  **Warnung: Der Cluster wird im Status "ForceQuorum" ausgeführt**festgelegt ist.  
  
##  <a name="PowerShellProcedure"></a> Verwenden von PowerShell  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>So erzwingen Sie den Start eines Clusters ohne Quorum  
  
1.  Starten Sie eine erhöhte Windows PowerShell mittels **Als Administrator ausführen**.  
  
2.  Importieren Sie das `FailoverClusters` -Modul, um Cluster-Cmdlets zu aktivieren.  
  
3.  Stellen Sie mithilfe von `Stop-ClusterNode` sicher, dass der Clusterdienst beendet wurde.  
  
4.  Verwenden Sie `Start-ClusterNode` mit `–FixQuorum` , um den Start des Clusterdiensts zu erzwingen.  
  
5.  Verwenden Sie `Get-ClusterNode` mit `–Propery NodeWieght = 1` , um den Wert festzulegen, mit dem gewährleistet wird, dass der Knoten ein Abstimmungselement des Quorums ist.  
  
6.  Geben Sie die Clusterknoteneigenschaften in einem lesbaren Format aus.  
  
### <a name="example-powershell"></a>Beispiel (PowerShell)  
 Im folgenden Beispiel wird der Start des OnSrv02-Knotenclusterdiensts ohne Quorum erzwungen. Dabei wird `NodeWeight = 1`festgelegt, und anschließend wird der Clusterknotenstatus vom neu erzwungenen Knoten aus aufgelistet.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "Always OnSrv02"  
Stop-ClusterNode –Name $node  
Start-ClusterNode –Name $node -FixQuorum  
  
(Get-ClusterNode $node).NodeWeight = 1  
  
$nodes = Get-ClusterNode -Cluster $node  
$nodes | Format-Table -property NodeName, State, NodeWeight  
  
```  
  
##  <a name="CommandPromptProcedure"></a> Verwenden von Net.exe  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>So erzwingen Sie den Start eines Clusters ohne Quorum  
  
1.  Stellen Sie mittels Remotedesktop eine Verbindung mit dem gewünschten Clusterknoten her, um dessen Onlineschaltung zu erzwingen.  
  
2.  Starten Sie mit **Als Administrator ausführen**eine Eingabeaufforderung mit erweiterten Berechtigungen.  
  
3.  Stellen Sie mithilfe von **net.exe** sicher, dass der lokale Clusterdienst beendet wurde.  
  
4.  Verwenden Sie **net.exe** mit `/forcequorum` , um den Start des lokalen Clusterdiensts zu erzwingen.  
  
### <a name="example-netexe"></a>Beispiel (Net.exe)  
 Im folgenden Beispiel wird der Start eines Knotenclusterdiensts ohne Quorum erzwungen. Dabei wird `NodeWeight = 1`festgelegt, und anschließend wird der Clusterknotenstatus vom neu erzwungenen Knoten aus aufgelistet.  
  
```ms-dos  
net.exe stop clussvc  
net.exe start clussvc /forcequorum  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Erzwingen des Clusterstarts ohne ein Quorum  
  
-   NodeWeight-Werte sind neu zu bewerten und zu konfigurieren, um vor der erneuten Onlineschaltung anderer Knoten ein neues Quorum korrekt erstellen zu können. Andernfalls wird für den Cluster u. U. wieder der Offlinemodus aktiviert.  
  
     Weitere Informationen finden Sie unter [WSFC-Quorummodi und Abstimmungskonfiguration &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
-   Die Prozeduren in diesem Thema stellen nur einen Schritt zur erneuten Onlineschaltung des WSFC-Clusters dar, wenn ein unvorhergesehener Quorumfehler auftreten sollte.  Sie möchten möglicherweise weitere Maßnahmen ergreifen, um zu verhindern, dass andere WSFC-Clusterknoten die neue Quorumkonfiguration stören.  
  
-   Andere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Funktionen, wie [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], die Datenbankspiegelung und der Protokollversand, erfordern u. U. zudem weitere Aktionen zur Datenwiederherstellung und vollständigen erneuten Einrichtung der hohen Verfügbarkeit.  
  
     **Weitere Informationen:**  
  
     [Ausführen eines erzwungenen manuellen Failovers einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
     [Erzwingen des Diensts in einer Datenbank-Spiegelungssitzung &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
  
     [Failover zu einer sekundären Datenbank für den Protokollversand &#40;SQL Server&#41;](../../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Anzeigen von Ereignissen und Protokollen für einen Failovercluster](http://technet.microsoft.com/en-us/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog-Failovercluster-Cmdlet](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [WSFC-Notfallwiederherstellung durch erzwungenes Quorum &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [Konfigurieren von Cluster-Quorum-NodeWeight-Einstellungen](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)   
 [Failovercluster-Cmdlets in Windows PowerShell, aufgelistet nach Taskfokus](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
