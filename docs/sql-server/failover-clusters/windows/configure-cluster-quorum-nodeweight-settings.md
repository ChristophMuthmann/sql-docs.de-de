---
title: Konfigurieren von Cluster-Quorum-NodeWeight-Einstellungen | Microsoft-Dokumentation
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
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 75d81e8e19e2ee1cf4efe62da164caf0e337e5ab
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>Konfigurieren von Cluster-Quorum-NodeWeight-Einstellungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie NodeWeight-Einstellungen für einen Elementknoten in einem Windows Server-Failoverclustering-Cluster konfiguriert werden. NodeWeight-Einstellungen werden während der Quorumabstimmung verwendet, um Notfallwiederherstellungs- und Multisubnetzszenarien für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] - und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanzen zu unterstützen.  
  
-   **Vorbereitungen:**  [Erforderliche Komponenten](#Prerequisites), [Sicherheit](#Security)  
  
-   **Anzeigen von Quorum-NodeWeight-Einstellungen mit:** [Verwenden von PowerShell](#PowerShellProcedure), [Verwenden von Cluster.exe](#CommandPromptProcedure)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Diese Funktion wird nur in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] oder höheren Versionen unterstützt.  
  
> [!IMPORTANT]  
>  Um NodeWeight-Einstellungen zu verwenden, muss der folgende Hotfix im WSFC-Cluster für alle Server übernommen werden:  
>   
>  [KB2494036](http://support.microsoft.com/kb/2494036): Ein Hotfix ist verfügbar, mit dem sich ein Clusterknoten konfigurieren lässt, der keine Quorumabstimmung in [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] und in [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Ist dieser Hotfix nicht installiert, geben die Beispiele in diesem Thema leere Werte oder NULL-Werte für NodeWeight zurück.  
  
###  <a name="Security"></a> Sicherheit  
 Der Benutzer muss einem Domänenkonto entsprechen, das Mitglied der lokalen Administratorgruppe an jedem Knoten des WSFC-Clusters ist.  
  
##  <a name="PowerShellProcedure"></a> Verwenden von PowerShell  
  
##### <a name="to-configure-nodeweight-settings"></a>So konfigurieren Sie NodeWeight-Einstellungen  
  
1.  Starten Sie eine erhöhte Windows PowerShell mittels **Als Administrator ausführen**.  
  
2.  Importieren Sie das `FailoverClusters` -Modul, um Cluster-Cmdlets zu aktivieren.  
  
3.  Verwenden Sie das `Get-ClusterNode` -Objekt, um die `NodeWeight` -Eigenschaft für jeden Knoten im Cluster festzulegen.  
  
4.  Geben Sie die Clusterknoteneigenschaften in einem lesbaren Format aus.  
  
### <a name="example-powershell"></a>Beispiel (PowerShell)  
 Im folgenden Beispiel wird die NodeWeight-Einstellung geändert, um die Quorumabstimmung für den „Always OnSrv1“-Knoten zu entfernen. Zudem werden die Einstellungen für alle Knoten im Cluster ausgegeben.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = “Always OnSrv1”  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Verwenden von Cluster.exe  
  
> [!NOTE]  
>  Das Hilfsprogramm von cluster.exe ist in der [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] -Version veraltet.  Verwenden Sie PowerShell mit Failoverclustering für künftige Entwicklungen.  Das Hilfsprogramm von cluster.exe wird in der nächsten Version von Windows Server entfernt. Weitere Informationen finden Sie unter [Zuordnen von Cluster.exe-Befehlen zu Windows PowerShell-Cmdlets für Failovercluster](http://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
##### <a name="to-configure-nodeweight-settings"></a>So konfigurieren Sie NodeWeight-Einstellungen  
  
1.  Starten Sie mit **Als Administrator ausführen**eine Eingabeaufforderung mit erweiterten Berechtigungen.  
  
2.  Verwenden Sie **cluster.exe** , um `NodeWeight` -Werte festzulegen.  
  
### <a name="example-clusterexe"></a>Beispiel (Cluster.exe)  
 Im folgenden Beispiel wird der NodeWeight-Wert geändert, um die Quorumabstimmung des „Always OnSrv1“-Knotens im Cluster001-Cluster zu entfernen.  
  
```ms-dos  
cluster.exe Cluster001 node Always OnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Anzeigen von Ereignissen und Protokollen für einen Failovercluster](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog-Failovercluster-Cmdlet](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [WSFC-Quorummodi und Abstimmungskonfiguration &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Anzeigen von Cluster-Quorum-NodeWeight-Einstellungen](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [Failovercluster-Cmdlets in Windows PowerShell, aufgelistet nach Taskfokus](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
