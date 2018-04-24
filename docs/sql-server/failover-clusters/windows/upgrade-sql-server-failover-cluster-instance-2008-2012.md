---
title: Aktualisieren von SQL Server-Instanzen auf Windows Server 2008/2008 R2/2012-Clustern | Microsoft-Dokumentation
ms.date: 1/25/2018
ms.suite: sql
ms.prod: sql
ms.prod_service: database engine
ms.component: failover-clustuers
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a448edf54d4a7aa61b308d133dd1dfbdbfe4f39d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="upgrade-sql-server-instances-running-on-windows-server-20082008-r22012-clusters"></a>Aktualisieren von SQL Server-Instanzen auf Windows Server 2008/2008 R2/2012-Clustern

[!INCLUDE[nextref-longhorn-md](../../../includes/nextref-longhorn-md.md)], [!INCLUDE[winserver2008r2-md](../../../includes/winserver2008r2-md.md)] und [!INCLUDE[win8srv-md](../../../includes/win8srv-md.md)] verhindern, dass Windows Server-Failovercluster direkte Upgrades des Betriebssystems durchführen, sodass die zulässige Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] für einen Cluster eingeschränkt wird. Sobald der Cluster auf mindestens [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] aktualisiert wurde, kann der Cluster immer aktuell bleiben.

## <a name="prerequisites"></a>Voraussetzungen

-   Bevor Sie eine der Migrationsstrategien durchführen, muss ein paralleler Windows Server-Failovercluster mit Windows Server 2016/2012 R2 vorbereitet werden. Alle Knoten, aus denen die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Failoverclusterinstanzen (FCIs) bestehen, müssen zum Windows-Cluster mit den parallelen FCIs hinzugefügt werden. Eigenständige Computer dürfen **nicht** vor der Migration zum Windows-Failovercluster hinzugefügt werden. Benutzerdatenbanken sollten vor der Migration in der neuen Umgebung synchronisiert werden.
-   Auf allen Zielinstanzen muss die gleiche Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] als parallele Instanz in der ursprünglichen Umgebung mit gleichem Instanznamen und -ID ausgeführt werden. Zudem müssen die gleichen Features auf diesen Instanzen installiert sein. Installationspfade und Verzeichnisstrukturen sollten auf den Zielcomputern identisch sein. Dies gilt nicht für Namen von virtuellen Netzwerken von FCIs, die vor der Migration anders sein müssen. Alle Features, die auf der ursprünglichen Instanz aktiviert sind (Always On, FILESTREAM usw.), sollten auch auf der Zielinstanz aktiviert sein.

-   [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)] darf vor der Migration nicht auf dem parallelen Cluster installiert sein.

-   Die Downtime beim Migrieren eines Clusters, der nur Verfügbarkeitsgruppen verwendet (mit oder ohne SQL FCIs) kann durch verteilte Verfügbarkeitsgruppen deutlich gesenkt werden. Dafür ist allerdings erforderlich, dass auf allen Instanzen [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] RTM-Versionen (oder höher) ausgeführt wird.

-   Für alle Migrationsstrategien ist die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Systemadministratorrolle erforderlich. Alle Windows-Benutzer, die von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Diensten (z.B. Windows-Konten, auf denen Replikations-Agents ausgeführt werden) verwendet werden, benötigen Berechtigungen auf Betriebssystemebene auf jedem Computer in der neuen Umgebung.

-   Alle Netzwerkdateifreigaben und dem Netzwerk zugeordnete Laufwerke, die in der ursprünglichen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Clusterumgebung verwendet werden, müssen noch vorhanden sein. Außerdem müssen sie für Zielcluster mit den gleichen Berechtigungen wie für die ursprünglichen Instanzen zugänglich sein.

-   Alle TCP/IP-Ports, die von der ursprünglichen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Instanz aufgelistet werden, dürfen nicht verwendet werden und müssen eingehenden Datenverkehr auf dem Zielcomputer erlauben.
-   Alle Dienste, die mit SQL in Verbindung stehen, müssen vom gleichen Windows-Benutzer installiert und ausgeführt werden.

-   Die Zielinstanzen müssen mit dem gleichen Gebietsschema wie die ursprünglichen Instanzen installiert werden.

## <a name="migration-scenarios"></a>Migrationsszenarios

Die angemessene Migrationsstrategie hängt von einigen Parametern der ursprünglichen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Clustertopologie ab, nämlich dem Gebrauch von [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)] und SQL-Failoverclusterinstanzen. Die gewählte Strategie hängt auch von den Anforderungen der Zielumgebung ab. Wenn die neue Umgebung erfordert, dass jeder Computer oder jede SQL-FCI den ursprünglichen Namen des virtuellen Netzwerks (VNN) beibehält oder wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Topologie davon anhängig ist, dass die neuen Instanzen alle Systemobjekte der ursprünglichen Instanzen erben, müssen Sie sich für eine Strategie entscheiden, in der diese migriert werden.

|                                   | Alle Serverobjekte und VNNs erforderlich | Alle Serverobjekte und VNNs erforderlich | Keine Serverobjekte und VNNs erforderlich\* | Keine Serverobjekte und VNNs erforderlich\* |
|-----------------------------------|--------------------------------------|--------------------------------------------------------------------|------------|------------|
| ***Verfügbarkeitsgruppen? (J/N)***                  | ***J***                              | ***N***                                                            | ***J***    | ***N***    |
| **Der Cluster verwendet nur SQL FCI**         | [Szenario 3](#scenario-3-cluster-has-sql-fcis-only-and-uses-availability-groups)                           | [Szenario 2](#scenario-2-cluster-to-migrate-has-sql-fcis-only-and-no-ag)                                                        | [Szenario 1](#scenario-1-cluster-to-migrate-uses-strictly-availability-groups-windows-server-2008-r2-sp1) | [Szenario 2](#scenario-2-cluster-to-migrate-has-sql-fcis-only-and-no-ag) |
| **Der Cluster verwendet eigenständige Instanzen** | [Szenario 5](#scenario-5-cluster-has-some-non-fci-and-uses-availability-groups)                           | [Szenario 4](#scenario-4-cluster-has-some-non-fci-and-no-availability-groups)                                                         | [Szenario 1](#scenario-1-cluster-to-migrate-uses-strictly-availability-groups-windows-server-2008-r2-sp1) | [Szenario 4](#scenario-4-cluster-has-some-non-fci-and-no-availability-groups) |
\* Dies schließt nicht den Listenernamen der Verfügbarkeitsgruppe ein.

## <a name="scenario-1-windows-cluster-with-sql-server-availability-groups-and-no-failover-cluster-instances-fcis"></a>Szenario 1: Windows-Cluster mit SQL Server-Verfügbarkeitsgruppen und keinen FCIs (Failoverclusterinstanzen)
Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] eingerichtet haben, das Verfügbarkeitsgruppen und keine FCIs verwendet, können Sie zu einem neuen Cluster migrieren, indem Sie eine parallele [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Bereitstellung auf einem anderen Cluster mit Windows Server 2016/2012 R2 durchführen. Anschließend können Sie eine verteilte Verfügbarkeitsgruppe erstellen, wo der Zielcluster der sekundäre Cluster des Produktionsclusters ist. Dafür ist es erforderlich, dass der Benutzer ein Upgrade auf [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] oder höher durchführt.

###  <a name="to-perform-the-upgrade"></a>So führen Sie ein Upgrade durch

1.  Aktualisieren Sie bei Bedarf alle Instanzen auf [!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] oder höher. Auf parallelen Instanzen müssen die gleichen Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] ausgeführt werden.

2.  Erstellen Sie eine Verfügbarkeitsgruppe für den Zielcluster. Wenn der primäre Knoten des Zielclusters keine FCI ist, erstellen Sie einen Listener.

3.  Erstellen Sie eine verteilte Verfügbarkeitsgruppe, wo der Zielcluster die sekundäre Verfügbarkeitsgruppe ist.

    >[!NOTE]
    >Der Parameter LISTENER\_URL für die T-SQL „Verteilte Verfügbarkeitsgruppe erstellen“ verhält sich für Verfügbarkeitsgruppen etwas anders, die über eine SQL-FCI verfügen, die als primäre Instanz dient. Ist dies der Fall bei der primären oder sekundären Verfügbarkeitsgruppe, verwenden Sie den VNN der primären SQL-FCI als Listener-URL an Stelle des Netzwerknamens des Listeners gemeinsam mit dem Port des Datenbankspiegelungsendpunkts.

4.  Verknüpfen Sie die sekundäre Verfügbarkeitsgruppe mit dem verteilten Cluster.

5.  Verknüpfen Sie die sekundäre Datenbank mit der sekundären Verfügbarkeitsgruppe.

    >[!NOTE]
    >Dies erfolgt automatisch, wenn die Zielverfügbarkeitsgruppe das automatische Seeding verwendet. Dies ist nur möglich, wenn die Daten- und Protokollpfade bei allen Replikaten übereinstimmen.

6.  Unterbrechen Sie den Datenverkehr an die primäre Verfügbarkeitsgruppe, und synchronisieren Sie die sekundäre.

7.  Ändern Sie die Commitrichtlinie für beide Verfügbarkeitsgruppen in SYNCHRONOUS_COMMIT, und führen Sie ein Failover auf den Zielcluster durch, sobald der Status SYNCHRONIZED lautet.

8.  Löschen Sie die verteilte Verfügbarkeitsgruppe.

9.  Löschen Sie den Listener in der ursprünglichen Verfügbarkeitsgruppe, oder benennen Sie diesen um.

10. Benennen Sie den Listener der neuen Verfügbarkeitsgruppe um, oder erstellen Sie einen Listener mit dem Namen des Listeners der ursprünglichen Verfügbarkeitsgruppe.

    >[!NOTE]
    >Obwohl der DNS-Eintrag des Listeners der ursprünglichen Verfügbarkeitsgruppe immer noch vorhanden ist, schlagen Versuche fehl, einen Listener mit diesem Namen zu erstellen.

11. Stellen Sie den Datenverkehr zum Listener wieder her.

## <a name="scenario-2-windows-clusters-with-sql-server-failover-cluster-instances-fcis"></a>Szenario 2: Windows-Cluster mit SQL Server-FCIs (Failoverclusterinstanzen)

Wenn Sie über eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Umgebung mit nur SQL-FCI-Instanzen verfügen, können Sie zu einem neuen Cluster migrieren, indem Sie eine parallele [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Umgebung auf einem anderen Windows-Cluster mit Windows Server 2016/2012 R2 erstellen. Die Migration zum Zielcluster führen Sie durch, indem Sie die VNNs der alten SQL-FCIs „stehlen“ und sie auf dem neuen Cluster laden. Dabei kann es zu zusätzlicher Downtime kommen, die davon abhängig ist, wie viel Zeit die DNS-Verteilung in Anspruch nimmt.

###  <a name="to-perform-the-upgrade"></a>So führen Sie ein Upgrade durch

1.  Nutzen Sie eine vollständige Sicherung, und unterbrechen Sie den Datenverkehr in Richtung des ursprünglichen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Clusters.

2.  Nutzen Sie eine Sicherung des Protokollfragments der Benutzerdatenbanken, und führen Sie eine Wiederherstellung in der neuen Umgebung durch.

3.  Schalten Sie im Zielcluster in Failovercluster-Manager jede SQL-FCI-Clusterrolle offline.

4.  Schalten Sie an der gleichen Stelle alle gruppierten Datenträger wieder online, die von jeder SQL-FCI verwendet werden.

5.  Schalten Sie im ursprünglichen Cluster in Failovercluster-Manager jede gruppierte SQL-FCI-Rolle offline.

6.  Schalten Sie an der gleichen Stelle alle gruppierten Datenträger wieder online, die von jeder SQL-FCI verwendet werden.

7.  Kopieren Sie die Systemdatenbanken von dem ursprünglichen Computer auf den parallelen Zielcomputer.

8.  Ändern Sie in der ursprünglichen Umgebung in Failovercluster-Manager den Namen der Ressource „Server Name“ jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle.

9.  Schalten Sie dann nur die umbenannte „Server Name“-Ressource wieder für jede SQL-FCI-Rolle online.

10. Benennen Sie dann im Zielcluster in Failovercluster-Manager die „Server Name“-Ressource jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle in den Namen des ursprünglichen Clusters um.

    >[!NOTE]
    >Fehler, die auftreten, weil der Name bereits von einem anderen Computer verwendet wird, treten nicht mehr auf, sobald die DNS-Einträge für diesen Namen gelöscht wurden.

11. Sobald alle FCIs umbenannt wurden, starten Sie jeden Computer im neuen Cluster neu.

12. Starten Sie alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rollen in Failovercluster-Manager, während die Computer nach dem Neustart wieder online gehen.

## <a name="scenario-3-windows-cluster-has-both-sql-fcis-and-sql-server-availability-groups"></a>Szenario 3: Windows-Cluster mit SQL-FCIs und SQL Server-Verfügbarkeitsgruppen

Wenn Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] eingerichtet haben, das keine eigenständigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Instanzen sondern nur SQL-FCIs verwendet, die in mindestens einer Verfügbarkeitsgruppe enthalten sind, können Sie eine Migration zu einem neuen Cluster mit ähnlichen Methoden wie unter „no Availability Group, no standalone instance“ (keine Verfügbarkeitsgruppe, keine eigenständige Instanz) beschrieben durchführen. Vor dem Kopieren von Systemtabellen auf freigegebene FCI-Datenträger müssen Sie alle Verfügbarkeitsgruppen in der ursprünglichen Umgebung löschen. Erstellen Sie die Verfügbarkeitsgruppen mit den gleichen Schema- und Listenernamen erneut, nachdem alle Datenbanken zum Zielcomputer migriert wurden. Dadurch werden die Windows Server-Failoverclusterressourcen ordnungsgemäß auf den Zielclustern erstellt und verwaltet. **Die Option „Always On“ muss in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] Configuration Manager auf jedem Computer in der Zielumgebung vor der Migration aktiviert werden.**

### <a name="to-perform-the-upgrade"></a>So führen Sie ein Upgrade durch

1.  Unterbrechen Sie den Datenverkehr zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)].

2.  Nutzen Sie eine Sicherung des Protokollfragments der Benutzerdatenbank, und führen Sie eine Wiederherstellung auf dem vorhergesehenen primären Cluster der neuen Umgebung durch, und nutzen Sie NORECOVERY für alle vorhergesehenen sekundären Cluster.

3.  Schalten Sie im Zielcluster in Failovercluster-Manager jede SQL-FCI-Clusterrolle offline.

4.  Schalten Sie an der gleichen Stelle die gruppierten Datenträger jeder SQL-FCI wieder online.

5.  Löschen Sie die Verfügbarkeitsgruppe im ursprünglichen Cluster.

6.  Schalten Sie im ursprünglichen Cluster in Failovercluster-Manager jede gruppierte SQL-FCI-Rolle offline.

7.  Schalten Sie an der gleichen Stelle alle gruppierten Datenträger wieder online, die von jeder SQL-FCI verwendet werden.

8.  Kopieren Sie die Systemdatenbanken von dem ursprünglichen Computer auf den parallelen Zielcomputer.

9.  Ändern Sie in der ursprünglichen Umgebung in Failovercluster-Manager den Namen der Ressource „Server Name“ jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle.

10. Schalten Sie dann nur die umbenannte „Server Name“-Ressource wieder für jede SQL-FCI-Rolle online.

11. Benennen Sie dann im Zielcluster in Failovercluster-Manager die „Server Name“-Ressource jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle in den Namen des ursprünglichen Clusters um.

12. Sobald alle FCIs umbenannt wurden, starten Sie jeden Computer im neuen Cluster neu.

13. Starten Sie alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rollen in Failovercluster-Manager, während die Computer nach dem Neustart wieder online gehen.

14. Erstellen Sie, sobald alle Instanzen wieder online sind, die Verfügbarkeitsgruppe im Replikat, in dem die Datenbanken wiederhergestellt wurden.

15. Verknüpfen Sie alle sekundären Replikate sowie alle sekundären Datenbanken mit der Verfügbarkeitsgruppe.

16. Erstellen Sie einen Listener in der neuen Verfügbarkeitsgruppe mit dem Listenernamen des Listeners der ursprünglichen Verfügbarkeitsgruppe.

## <a name="scenario-4-windows-cluster-with-standalone-sql-server-instances-and-no-availability-groups"></a>Szenario 4: Windows-Cluster mit eigenständigen SQL Server-Instanzen und ohne Verfügbarkeitsgruppen

Die Migration eines Clusters mit eigenständigen Instanzen ähnelt der Migration eines [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Clusters, der nur FCIs aufweist. Statt jedoch den VNN der Netzwerknamenclusterressource der FCI zu ändern, ändern Sie den Computernamen des ursprünglichen eigenständigen Computers und „stehlen“ den Namen des alten Computers auf dem Zielcomputer. Dadurch kommt es zu zusätzlicher Downtime abhängig von nicht eigenständigen Szenarios, da Sie den eigenständigen Zielcomputer nicht zum Windows Server-Failovercluster hinzufügen können, bis Sie den Netzwerknamen des alten Computers kennen.

###  <a name="to-perform-the-upgrade"></a>So führen Sie ein Upgrade durch

1.  Unterbrechen Sie den Datenverkehr zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)].

2.  Nehmen Sie eine Sicherung des Protokollfragments der Benutzerdatenbanken, und führen Sie eine Wiederherstellung auf jedem Computer in der neuen Umgebung durch.

3.  Schalten Sie im Zielcluster in Failovercluster-Manager jede SQL-FCI-Clusterrolle offline.

4.  Schalten Sie an der gleichen Stelle die gruppierten Datenträger wieder online, die von jeder SQL-FCI verwendet werden.

5.  Schalten Sie im ursprünglichen Cluster in Failovercluster-Manager jede gruppierte Rolle der SQL-FCIs offline, und unterbrechen Sie die eigenständigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Instanzen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] Configuration Manager.

6.  Geben Sie jedem eigenständigen Computer im ursprünglichen Cluster einen neuen eindeutigen Computernamen. Starten Sie jeden dieser Computer wie angegeben neu.

7.  Schalten Sie im ursprünglichen Cluster in Failovercluster-Manager die gruppierten Datenträger wieder online, die von SQL-FCIs verwendet werden.

8.  Kopieren Sie die Systemdatenbanken auf die Zielcomputer.

9.  Ändern Sie in der ursprünglichen Umgebung in Failovercluster-Manager die „Server Name“-Ressource jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle in einen neuen, eindeutigen Namen.

10. Schalten Sie dann nur die umbenannte „Server Name“-Ressource wieder für jede SQL-FCI-Rolle online.

11. Geben Sie anschließend auf den parallelen eigenständigen Instanzen den Computern die Namen der ursprünglichen eigenständigen Computer. (Löschen Sie den alten Servernamen, und fügen Sie einen neuen Servernamen mit einem lokalen Parameter hinzu.) Starten Sie die Computer wie angegeben neu.

12. Verknüpfen Sie nach dem Neustart jeden eigenständigen Computer mit dem Windows Server-Zielfailovercluster.

13. Benennen Sie dann im Zielcluster in Failovercluster-Manager die „Server Name“-Ressource jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle in den Namen des ursprünglichen Clusters um.

14. Sobald alle FCIs umbenannt wurden, starten Sie jeden Computer im neuen Cluster neu.

15. Starten Sie alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rollen in Failovercluster-Manager, während die Computer nach dem Neustart wieder online gehen.

## <a name="scenario-5-windows-cluster-with-standalone-sql-server-instances-and-availability-groups"></a>Szenario 5: Windows-Cluster mit eigenständigen SQL Server-Instanzen und Verfügbarkeitsgruppen

Die Migration eines Clusters, der Verfügbarkeitsgruppen mit eigenständigen Replikaten verwendet, ähnelt der Migration eines Clusters, der FCIs mit Verfügbarkeitsgruppen verwendet. Sie müssen weiterhin die ursprünglichen Verfügbarkeitsgruppen löschen und sie auf dem Zielcluster erneut erstellen. Allerdings kommt es durch den Mehraufwand bei der Migration eigenständiger Instanzen zu zusätzlicher Downtime. **Die Option „Always On“ muss vor der Migration auf jeder FCI in der Zielumgebung aktiviert werden.**

###  <a name="to-perform-the-upgrade"></a>So führen Sie ein Upgrade durch

1.  Unterbrechen Sie den Datenverkehr zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)].

2.  Nutzen Sie eine Sicherung des Protokollfragments der Benutzerdatenbank, und führen Sie eine Wiederherstellung auf dem vorhergesehenen primären Cluster der neuen Umgebung durch, und nutzen Sie NORECOVERY für jeden vorhergesehenen sekundären Cluster.

3.  Löschen Sie die Verfügbarkeitsgruppe im ursprünglichen Cluster.

4.  Schalten Sie im Zielcluster in Failovercluster-Manager jede SQL-FCI-Clusterrolle offline.

5.  Schalten Sie an der gleichen Stelle die gruppierten Datenträger wieder online, die von jeder SQL-FCI verwendet werden.

6.  Schalten Sie im ursprünglichen Cluster in Failovercluster-Manager jede gruppierte Rolle der SQL-FCIs offline, und unterbrechen Sie die eigenständigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Instanzen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] Configuration Manager.

7.  Geben Sie jedem eigenständigen Computer im ursprünglichen Cluster einen neuen eindeutigen Computernamen. Starten Sie jeden dieser Computer wie angegeben neu.

8.  Schalten Sie im ursprünglichen Cluster in Failovercluster-Manager die gruppierten Datenträger wieder online, die von SQL-FCIs verwendet werden.

9.  Kopieren Sie die Systemdatenbanken auf die Zielcomputer.

10. Ändern Sie in der ursprünglichen Umgebung in Failovercluster-Manager die „Server Name“-Ressource jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle in einen neuen, eindeutigen Namen.

11. Schalten Sie dann nur die umbenannte „Server Name“-Ressource wieder für jede SQL-FCI-Rolle online.

12. Geben Sie anschließend auf den parallelen eigenständigen Instanzen den Computern die Namen der ursprünglichen eigenständigen Computer. (Löschen Sie den Servernamen in SQL, und fügen Sie einen neuen hinzu.) Starten Sie die Computer wie angegeben neu.

13. Verknüpfen Sie nach dem Neustart jeden eigenständigen Computer mit dem Windows Server-Zielfailovercluster.

14. Benennen Sie dann im Zielcluster in Failovercluster-Manager die „Server Name“-Ressource jeder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rolle in den Namen des ursprünglichen Clusters um.

15. Sobald alle FCIs umbenannt wurden, starten Sie jeden Computer im neuen Cluster neu.

16. Starten Sie alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-FCI-Rollen in Failovercluster-Manager, während die Computer nach dem Neustart wieder online gehen.

17. Sobald alle Instanzen wieder online sind, erstellen Sie die Verfügbarkeitsgruppen auf dem intendierten primären Cluster neu.

18. Verknüpfen Sie alle sekundären Replikate und sekundären Datenbanken miteinander.

19. Erstellen Sie den Verfügbarkeitsgruppenlistener neu mit dem Namen des ursprünglichen.

## <a name="specific-concerns-for-individual-features"></a>Besondere Bedenken bei einzelnen Features

### [!INCLUDE[sshadrc-md](../../../includes/sshadrc-md.md)]

-   **Datenbank-Spiegelungsendpunkt**

    Aus SQL-Sicht migriert der Datenbankspiegelungsendpunkt mit den Systemtabellen zur neuen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Instanz. Stellen Sie vor der Migration sicher, dass die entsprechenden Regeln auf die Firewalls angewendet wurden und dass kein anderer Prozess auf dem gleichen Port lauscht.

-   **Availability Groups (Verfügbarkeitsgruppen)**

    Verfügbarkeitsgruppen und die dazugehörigen Listener können nicht zwischen Instanzen migrieren. Die Windows Server-Failoverclusterressourcen, die von der Verfügbarkeitsgruppe erstellt wurden, können nicht ohne Weiteres in der Zielumgebung neu erstellt werden. Statt Verfügbarkeitsgruppen zu migrieren, sollten diese gelöscht und dann auf dem Zielcluster neu erstellt werden.

-   **Verfügbarkeitsgruppenlistener**

    Diese werden genauso wie Verfügbarkeitsgruppen gelöscht und neu erstellt, statt sie direkt zu migrieren.

### <a name="replication"></a>Replikation

-   **Remote Verteiler, Herausgeber und Abonnenten**

    Das Verhältnis zwischen einem Verteiler und einem Herausgeber hängt nur vom VNN der Computer ab, die diese hosten, der ordnungsgemäß zum neuen Computer aufgelöst werden kann. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Agent-Aufträge werden auch ordnungsgemäß mit den Systemtabellen migriert, sodass die verschiedenen Replikations-Agents weiterhin ausgeführt werden können. Vor der Migration ist es erforderlich, dass Windows-Konten, auf denen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Agent selbst oder ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Agent-Auftrag ausgeführt wird, die gleichen Berechtigungen in der Zielumgebung haben. Die Kommunikation mit dem Herausgeber und den Abonnenten verläuft normal.

-   **Momentaufnahmeordner**

    Vor der Migration ist es erforderlich, dass Netzwerkfreigaben, die von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Features verwendet werden, für Computer in der Zielumgebung mit den gleichen Berechtigungen wie in der ursprünglichen Umgebung zugänglich sind. Stellen Sie vor der Migration sicher, dass dies zutrifft.

### <a name="service-broker"></a>Service Broker

-   **Service Broker-Endpunkt**

    Aus [!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)]-Sicht bestehen keine Bedenken bezüglich des Endpunkts. Sie müssen vor der Migration sicherstellen, dass kein Prozess auf dem gleichen Port lauscht und dass keine Firewallregel diesen Port blockiert bzw. explizit zulässt.

-   **Zertifikate**

    Zertifikate sollten auch gesichert und auf den Zielcomputern wiederhergestellt werden, falls ein Zertifikat auf einem neuen Computer wiederhergestellt werden muss.

-   **Routen**

    Routen hängen vom Namen des virtuellen Netzwerks des Ziels ab, die sowohl für Computernamen als auch SQL-FCI-Netzwerknamen ordnungsgemäß in den korrekten Computer in der neuen Umgebung aufgelöst werden. Jeder andere VNN, auf den verwiesen wird, muss auch auf den neuen Computer umgeleitet werden.

-   **Remotedienstbindungen**

    Remotedienstbindungen funktionieren nach der Migration ordnungsgemäß, da jeder Benutzer, der die Remotedienstbindung verwendet, ordnungsgemäß migriert wird.

### <a name="includessnoversionincludesssnoversionmd-agent"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion.md)] -Agent

-   **Jobs**

    Aufträge werden ordnungsgemäß mit Systemdatenbanken migriert. Jeder Benutzer, der entweder einen SQL Agent-Auftrag oder SQL Agent selbst ausführt, verfügt auf dem Zielcomputer über die gleichen Berechtigungen wie in den Anforderungen angegeben.

-   **Warnungen und Operatoren**

    Warnungen und Operatoren werden ordnungsgemäß mit den Systemdatenbanken migriert.

### <a name="filestream"></a>FILESTREAM

-   **Windows-Dateifreigabeports**

    Die Windows-Dateifreigabeports 139 und 445 müssen beide über Regeln verfügen, die zulassen, dass eingehender Datenverkehr FILESTREAM verwenden kann.

-   **Windows-Freigabe**

    Der Windows-Freigabepfad hängt vom Namen der SQL-FCI-Ressource ab, da darauf über `\\ServerName\ShareName` zugegriffen wird. Die Migration von FILESTREAM erfordert, dass alle Knoten in einer Ziel-FCI FILESTREAM zulassen. Zudem ist beim Verwenden einer Windows-Freigabe erforderlich, dass sie so konfiguriert sind, dass sie den gleichen Namen für die Windows-Freigabe wie der ursprüngliche Computer verwenden. Sobald die Ziel-FCI den korrekten Servernamen abgerufen hat, hostet sie die Windows-Freigabe mit dem gewünschten Pfad.

-   **FILESTREAM-Daten**

    FILESTREAM-Daten sind in der Sicherung beinhaltet.

### <a name="integration-services"></a>Integration Services

-   **SSIS-Projekte**

    SSIS-Projekte werden mit der SSIS-Datenbank migriert. Sobald die SSIS-Datenbank verschoben wird, werden Pakete sofort ausführbar, noch bevor Systemtabellen verschoben wurden.

-   **Dateibasierte Datenquellen**

    Flatfiles, Excel-Dateien, XML-Quellen und andere müssen an der Stelle zugänglich sein, wie sie vom SSIS-Paket angegeben wird.

## <a name="next-steps"></a>Nächste Schritte
- [Abschließen des Datenbankmodul-Upgrades](../../../database-engine/install-windows/complete-the-database-engine-upgrade.md)
- [Ändern des Datenbank-Kompatibilitätsmodus und Verwenden des Abfragespeichers](../../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)
- [Nutzen Sie die Vorteile der neuen Features von SQL Server 2016](http://msdn.microsoft.com/library/d8879659-8efa-4442-bcbb-91272647ae16)
- [Upgraden einer SQL Server-Failoverclusterinstanz](upgrade-a-sql-server-failover-cluster-instance.md)
- [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)
- [Add Features to an Instance of SQL Server 2016 (Setup) (Hinzufügen von Funktionen zu einer Instanz von SQL Server 2016 (Setup))](../../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)
