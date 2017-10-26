---
title: "Failoverclustering und Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustering [SQL Server]
- Availability Groups [SQL Server], WSFC clusters
- Failover Cluster Instances [SQL Server], see failover clustering [SQL Server]
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], Failover Cluster Instances
ms.assetid: 613bfbf1-9958-477b-a6be-c6d4f18785c3
caps.latest.revision: 48
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c1184d2ea29ccf64159df67950b5b078010e73a7
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="failover-clustering-and-always-on-availability-groups-sql-server"></a>Failoverclustering und AlwaysOn-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

   [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], die in [!INCLUDE[sssql11](../../../includes/sssql11_md.md)] eingeführte Lösung für hohe Verfügbarkeit und Notfallwiederherstellung, erfordert WSFC (Windows Server-Failoverclustering). [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ist zwar nicht von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclustering abhängig, Sie können aber dennoch eine FCI (Failoverclusterinstanz) verwenden, um ein Verfügbarkeitsreplikat für eine Verfügbarkeitsgruppe zu hosten. Es ist wichtig, dass Sie die Rolle jeder Clusteringtechnologie kennen, und wissen, welche Überlegungen Sie für den Entwurf Ihrer [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Umgebung anstellen müssen.  
  
> [!NOTE]  
>  Informationen zu [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Konzepten finden Sie unter [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 **In diesem Thema:**  
  
-   [Windows Server-Failoverclustering](#WSFC)  
  
-   [SQL Server-Failoverclustering](#SQLServerFC)  
  
-   [Einschränkungen bei Verwendung des WSFC-Failovercluster-Managers für Verfügbarkeitsgruppen](#FCMrestrictions)  
  
##  <a name="WSFC"></a> Windows Server Failover Clustering und Verfügbarkeitsgruppen  
 Für die Bereitstellung von [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ist ein WSFC-Cluster (Windows Server-Failoverclustering) erforderlich. Um für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]aktiviert werden zu können, muss eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in einem WSFC-Knoten befinden, und der WSFC-Cluster und -Knoten müssen online sein. Zudem muss sich jedes Verfügbarkeitsreplikat einer bestimmten Verfügbarkeitsgruppe in einem anderen Knoten desselben WSFC-Clusters befinden. Die einzige Ausnahme besteht darin, dass sich eine Verfügbarkeitsgruppe während der Migration zu einem anderen WSFC-Cluster vorübergehend auf zwei Cluster erstrecken kann.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] basiert zur Überwachung und Verwaltung der aktuellen Rollen der Verfügbarkeitsreplikate, die zu einer gegebenen Verfügbarkeitsgruppe gehören, auf dem Windows-Failoverclustering (WSFC)-Cluster und bestimmt, wie sich ein Failoverereignis auf die Verfügbarkeitsreplikate auswirkt. Für jede erstellte Verfügbarkeitsgruppe wird eine WSFC-Ressourcengruppe erstellt. Der WSFC-Cluster überwacht diese Ressourcengruppe, um den Zustand des primären Replikats auszuwerten.  
  
 Das Quorum für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] basiert unabhängig davon, ob ein bestimmter Clusterknoten Verfügbarkeitsreplikate hostet, auf allen Knoten des WSFC-Clusters. Im Gegensatz zur Datenbankspiegelung ist in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]keine Zeugenrolle verfügbar.  
  
 Die allgemeine Integrität des WSFC-Clusters wird von den Abstimmungen eines Quorums der Clusterknoten bestimmt. Wird der WSFC-Cluster wegen eines nicht geplanten Notfalls oder aufgrund eines persistenten Hardware- oder Kommunikationsfehlers offline geschaltet, ist manueller Eingriff durch den Administrator erforderlich. Ein Windows Server- oder WSFC-Clusteradministrator muss ein Quorum erzwingen und dann die überdauernden Clusterknoten in einer nicht fehlertolerante Konfiguration wieder online schalten.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Registrierungsschlüssel sind Unterschlüssel des WSFC-Clusters. Wenn Sie einen WSFC-Cluster löschen und neu erstellen, müssen Sie die Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] für jede Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deaktivieren und erneut aktivieren, auf der auf dem ursprünglichen WSFC-Cluster ein Verfügbarkeitsreplikat gehostet wurde.  
  
 Informationen zum Ausführen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] auf Windows Server-Failoverclustering (WSFC)-Knoten sowie zum WSFC-Quorum finden Sie unter [Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
### <a name="cross-cluster-migration-of-always-on-availability-groups-for-os-upgrade"></a>Clusterübergreifende Migration von AlwaysOn-Verfügbarkeitsgruppen für Betriebssystemupgrade  
 Ab [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)]unterstützt [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] die clusterübergreifende Migration von Verfügbarkeitsgruppen für Bereitstellungen in einem neuen WSFC-Cluster (Windows Server Failover Clustering). Über die clusterübergreifende Migration wird eine Verfügbarkeitsgruppe oder ein Batch von Verfügbarkeitsgruppen bei minimaler Downtime in das neue Ziel-WSFC-Cluster verschoben. Durch das Verfahren der clusterübergreifenden Migration können Sie beim Aktualisieren auf einen [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] -Cluster Ihre Vereinbarungen zum Servicelevel (SLAs) einhalten. [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] (oder eine höhere Version) muss auf dem Ziel-WSFC-Cluster installiert und für AlwaysOn aktiviert sein. Der Erfolg einer Kreuzclustermigration hängt von gründlicher Planung und Vorbereitung des Ziel-WSFC-Clusters ab.  
  
 Weitere Informationen finden Sie unter [Lösungen mit hoher Verfügbarkeit (SQL Server)](http://msdn.microsoft.com/library/jj873730.aspx).  
  
##  <a name="SQLServerFC"></a> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failoverclusterinstanzen (FCIs) und Verfügbarkeitsgruppen  
 Sie können auf Serverinstanzebene eine zweite Failoverebene einrichten, indem Sie das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclustering zusammen mit dem WSFC-Cluster implementieren. Ein Verfügbarkeitsreplikat kann von einer eigenständigen Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder einer FCI-Instanz gehostet werden. Ein Replikat für eine Verfügbarkeitsgruppe kann jeweils nur von einem FCI-Partner gehostet werden. Bei Ausführung eines Verfügbarkeitsreplikats in einer FCI enthält die Liste möglicher Besitzer für die Verfügbarkeitsgruppe nur den aktiven FCI-Knoten.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] hängt von keiner Form eines gemeinsam verwendeten Speichers ab. Falls Sie jedoch eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz (FCI) zum Hosten von mindestens einem Verfügbarkeitsreplikats verwenden, ist für all diese FCIs der standardmäßigen Installation der SQL Server-Failoverclusterinstanz entsprechend gemeinsam verwendeter Speicher erforderlich.  
  
 Weitere Informationen zu zusätzlichen erforderlichen Komponenten finden Sie im Abschnitt „Voraussetzungen und Einschränkungen zum Hosten eines Verfügbarkeitsreplikats mithilfe einer SQL Server-Failoverclusterinstanz (FCI)“ von [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
### <a name="comparison-of-failover-cluster-instances-and-availability-groups"></a>Vergleich der Failoverclusterinstanzen und Verfügbarkeitsgruppen  
 Unabhängig von der Anzahl der Knoten in der FCI hostet eine ganze FCI ein einzelnes Replikat innerhalb einer Verfügbarkeitsgruppe. In der folgenden Tabelle werden die Unterschiede der Konzepte zwischen Knoten in einer FCI und Replikaten in einer Verfügbarkeitsgruppe beschrieben.  
  
||Knoten in einer FCI|Replikate in einer Verfügbarkeitsgruppe|  
|-|-------------------------|-------------------------------------------|  
|**Verwendet WSFC-Cluster**|Ja|Ja|  
|**Schutzebene**|Instanz|Datenbank|  
|**Speichertyp**|Shared|Nicht freigegeben<br /><br /> Obwohl die Replikate in einer Verfügbarkeitsgruppe keinen Speicher gemeinsam verwenden, verwendet ein Replikat, das von einer FCI gehostet wird, gemäß der Anforderung dieser FCI eine gemeinsame Speicherlösung. Die Speicherlösung wird nur von Knoten in dieser FCI verwendet und nicht zwischen den Replikaten der Verfügbarkeitsgruppe.|  
|**Speicherlösungen**|Direkt angefügt, SAN, Einbindungspunkte, SMB|Hängt von Knotentyp ab|  
|**Lesbare sekundäre**|Nein*|Ja|  
|**Anwendbare Failoverrichtlinieneinstellungen**|WSFC-Quorum<br /><br /> FCI-spezifisch<br /><br /> Verfügbarkeitsgruppeneinstellungen*|WSFC-Quorum<br /><br /> Verfügbarkeitsgruppeneinstellungen|  
|**Failoverressourcen**|Server, Instanz und Datenbank|Nur Datenbank|  
  
 *Während synchrone sekundäre Replikate in einer Verfügbarkeitsgruppe stets in ihren jeweiligen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen ausgeführt werden, haben Sekundärknoten in einer FCI ihre jeweiligen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanzen tatsächlich nicht gestartet und sind daher nicht lesbar. In einer FCI startet ein sekundärer Knoten seine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz nur, wenn der Ressourcengruppenbesitz während eines FCI-Failovers an ihn übergeben wird. Wenn jedoch auf dem aktiven FCI-Knoten eine FCI-gehostete Datenbank zu einer Verfügbarkeitsgruppe gehört, ist die Datenbank lesbar, wenn das lokale Verfügbarkeitsreplikat als lesbares sekundäres Replikat ausgeführt wird.  
  
 **Failoverrichtlinieneinstellungen für die Verfügbarkeitsgruppe gelten für alle Replikate, unabhängig davon, ob sie in einer eigenständigen Instanz oder einer FCI-Instanz gehostet werden.  
  
> [!NOTE]  
>  Weitere Informationen zur **Anzahl der Knoten** innerhalb des Failoverclusterings sowie zu **AlwaysOn-Verfügbarkeitsgruppen** für verschiedene [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Editionen finden Sie unter [Von den SQL Server 2012-Editionen unterstützte Funktionen](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="considerations-for-hosting-an-availability-replica-on-an-fci"></a>Überlegungen zum Hosten eines Verfügbarkeitsreplikats auf einer FCI  
  
> [!IMPORTANT]  
>  Wenn Sie planen, in einer SQL Server-Failoverclusterinstanz (FCI) ein Verfügbarkeitsreplikat zu hosten, stellen Sie sicher, dass die Windows Server 2008-Hostknoten die AlwaysOn-Voraussetzungen und -Einschränkungen für Failoverclusterinstanzen (FCIs) erreichen. Weitere Informationen finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)zu unterstützen.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failoverclusterinstanzen (FCIs) unterstützen kein automatisches AlwaysOn-Failover durch Verfügbarkeitsgruppen. Daher können die Verfügbarkeitsreplikate, die von einer FCI gehostet werden, nur für manuelles Failover konfiguriert werden.  
  
 Möglicherweise muss ein Windows Server Failover Clustering (WSFC)-Cluster so konfiguriert werden, dass er freigegebene Datenträger enthält, die nicht auf allen Knoten verfügbar sind. Denken Sie beispielsweise an ein WSFC-Cluster über zwei Datenzentren mit drei Knoten. Zwei der Knoten hosten im primären Rechenzentrum eine SQL Server-Failoverclusteringinstanz (FCI) und haben Zugriff auf dieselben freigegebenen Datenträger. Der dritte Knoten hostet eine eigenständige Instanz von SQL Server in einem anderen Rechenzentrum und verfügt nicht über Zugriff auf die freigegebenen Datenträger vom primären Rechenzentrum. Diese WSFC-Clusterkonfiguration unterstützt die Bereitstellung einer Verfügbarkeitsgruppe, wenn die FCI das primäre Replikat hostet und die eigenständige Instanz das sekundäre Replikat hostet.  
  
 Bei Auswahl einer FCI zum Hosten eines Verfügbarkeitsreplikats für eine angegebene Verfügbarkeitsgruppe muss gewährleistet sein, dass ein FCI-Failover nicht möglicherweise bewirkt, dass ein einzelner WSFC-Knoten versucht, zwei Verfügbarkeitsreplikate für dieselbe Verfügbarkeitsgruppe zu hosten.  
  
 Im folgenden Beispielszenario wird veranschaulicht, wie diese Konfiguration zu Problemen führen könnte:  
  
 Marcel konfiguriert einen WSFC-Cluster mit zwei Knoten, `NODE01` und `NODE02`. Er installiert eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failoverclusterinstanz, `fciInstance1`, auf `NODE01` und `NODE02` , wobei `NODE01` der aktuelle Besitzer für `fciInstance1`ist.  
 Auf `NODE02`installiert Marcel eine andere Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], `Instance3`, die eine eigenständige Instanz ist.  
 Auf `NODE01`aktiviert Marcel fciInstance1 für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Auf `NODE02`aktiviert er `Instance3` für [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Dann richtet er eine Verfügbarkeitsgruppe ein, für die `fciInstance1` das primäre Replikat hostet, und `Instance3` hostet das sekundäre Replikat.  
 An einen bestimmten Punkt ist `fciInstance1` auf `NODE01`nicht mehr verfügbar, und der WSFC-Cluster verursacht einen Failover von `fciInstance1` auf `NODE02`. Nach dem Failover ist `fciInstance1` eine [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-fähige Instanz, die unter der primären Rolle auf `NODE02`ausgeführt wird. `Instance3` befindet sich jetzt jedoch auf demselben WSFC-Knoten wie `fciInstance1`. Dies verstößt gegen die [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Einschränkung.  
 Um das Problem in diesem Szenario zu beheben, muss sich die eigenständige Instanz, `Instance3`, auf einem anderen Knoten im selben WSFC-Cluster wie `NODE01` und `NODE02`befinden.  
  
 Weitere Informationen zur [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Failover-Clusterunterstützung finden Sie unter [AlwaysOn-Failoverclusterinstanzen &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
##  <a name="FCMrestrictions"></a> Einschränkungen bei Verwendung des WSFC-Failovercluster-Managers für Verfügbarkeitsgruppen  
 Verwenden Sie den Failovercluster-Manager nicht zum Bearbeiten von Verfügbarkeitsgruppen, beispielsweise:  
  
-   Fügen Sie im Clusterdienst (Ressourcengruppe) keine Ressourcen für die Verfügbarkeitsgruppe hinzu, bzw. entfernen Sie keine Ressourcen.  
  
-   Ändern Sie keine Verfügbarkeitsgruppeneigenschaften, z. B. die möglichen und bevorzugten Besitzer. Diese Eigenschaften werden automatisch von der Verfügbarkeitsgruppe festgelegt.  
  
-   Verwenden Sie den Failovercluster-Manager nicht zum Verschieben von Verfügbarkeitsgruppen auf verschiedene Knoten oder zum Ausführen eines Failovers für Verfügbarkeitsgruppen. Der Synchronisierungsstatus der Verfügbarkeitsreplikate ist dem Failovercluster-Manager nicht bekannt, sodass ein solcher Vorgang die Downtime verlängern kann. Sie müssen [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]verwenden.  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   **Blogs:**  
  
     [Konfigurieren von Windows-Failoverclustering für SQL Server (Verfügbarkeitsgruppe oder Failoverclusterinstanz) mit beschränkter Sicherheit](https://blogs.msdn.microsoft.com/sqlalwayson/2012/06/05/configure-windows-failover-clustering-for-sql-server-availability-group-or-fci-with-limited-security/)  
  
     [SQL Server AlwaysOn-Teamblogs: Der offizielle SQL Server AlwaysOn-Teamblog](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server-Technikblogs](http://blogs.msdn.com/b/psssql/)  
  
-   **Whitepaper:**  
  
     [AlwaysOn-Architekturhandbuch: Erstellen einer Lösung für hohe Verfügbarkeit und Notfallwiederherstellung unter Verwendung von Failoverclusterinstanzen und Verfügbarkeitsgruppen](http://msdn.microsoft.com/library/jj215886.aspx)  
  
     [Microsoft SQL Server AlwaysOn-Lösungshandbuch zu hoher Verfügbarkeit und Notfallwiederherstellung](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft-Whitepapers für SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Whitepapers des SQL Server-Kundenberatungsteams](http://sqlcat.com/)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen (SQL Server)](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen (Transact-SQL)](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [AlwaysOn-Failoverclusterinstanzen &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)  
  
  

