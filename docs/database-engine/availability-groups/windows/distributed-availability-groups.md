---
title: "Verteilte Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], distributed
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 534cc0e8f798c8d231936e1c89835257832c4b16
ms.contentlocale: de-de
ms.lasthandoff: 08/21/2017

---
# <a name="distributed-availability-groups"></a>Verteilte Verfügbarkeitsgruppen

Verteilte Verfügbarkeitsgruppen sind eine neue Funktion, die in SQL Server 2016 als Variation der bestehenden Funktion für Always On-Verfügbarkeitsgruppen eingeführt. Dieser Artikel erläutert einige Aspekte von verteilten Verfügbarkeitsgruppen und ergänzt die bestehende [SQL Server documentation (SQL Server-Dokumentation)](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation).

> [!NOTE]
> „DAG“ ist nicht die offizielle Abkürzung für *verteilte Verfügbarkeitsgruppe*, da die Abkürzung bereits für die Database Availability Group-Exchange-Funktion verwendet wird. Diese Exchange-Funktion steht nicht in Zusammenhang mit den Verfügbarkeitsgruppen oder verteilten Verfügbarkeitsgruppen in SQL Server.

Informationen zum Konfigurieren einer verteilten Verfügbarkeitsgruppe finden Sie unter [Configure distributed availability groups (Konfigurieren von verteilten Verfügbarkeitsgruppen)](configure-distributed-availability-groups.md).

## <a name="understand-distributed-availability-groups"></a>Grundlegendes zu verteilten Verfügbarkeitsgruppen

Eine verteilte Verfügbarkeitsgruppe ist ein spezieller Typ einer Verfügbarkeitsgruppe, der zwei separate Verfügbarkeitsgruppen umfasst. Die zugrunde liegenden Verfügbarkeitsgruppen werden auf zwei verschiedenen WSFC-Clustern (Windows Server Failover Clustering) konfiguriert. Die Verfügbarkeitsgruppen, die Teil einer verteilten Verfügbarkeitsgruppe sind, müssen sich nicht am selben Ort befinden. Sie können physisch, virtuell, lokal , in der öffentlichen Cloud oder an einem sonstigen Ort sein, der die Bereitstellung von Verfügbarkeitsgruppen unterstützt. Solange zwei Verfügbarkeitsgruppen kommunizieren können, können Sie mit diesen eine verteilte Verfügbarkeitsgruppe konfigurieren.

Die Ressourcen einer herkömmlichen Verfügbarkeitsgruppe werden in einem WSFC-Cluster konfiguriert. Eine verteilte Verfügbarkeitsgruppe kann keine Konfigurationen in einem WSFC-Cluster vornehmen. Sie wird vollständig in SQL Server verwaltet. Informationen zum Anzeigen der Informationen für eine verteilte Verfügungsgruppe finden Sie unter [Viewing distributed availability group information (Anzeigen der Informationen für eine verteilte Verfügbarkeitsgruppe)](#viewing-distributed-availability-group-information). 

Bei einer verteilten Verfügbarkeitsgruppe ist erforderlich, dass die zugrunde liegenden Verfügbarkeitsgruppen über einen Listener verfügen. Anstatt den zugrundeliegenden Servernamen für eine eigenständige Instanz (oder bei einer SQL Server-Failoverclusterinstanz (FCI) den Wert, der der Netzwerknamenressource zugeordnet ist) bereitzustellen, wie es bei einer herkömmlichen Verfügbarkeitsgruppe üblich ist, geben Sie beim Erstellen den für die verteilte Verfügbarkeitsgruppe konfigurierten Listener mithilfe des Parameters „ENDPOINT_URL“ an. Obwohl jede zugrunde liegende Verfügbarkeitsgruppe der verteilten Verfügbarkeitsgruppe über einen Listener verfügt, besitzt eine verteilte Verfügbarkeitsgruppe nicht über einen Listener.

In der folgenden Abbildung finden Sie eine Ansicht auf höchster Ebene für eine verteilte Verfügbarkeitsgruppe, die zwei Verfügbarkeitsgruppen (AG 1 und AG 2) umfasst, von der jede in ihrem eigenen WSFC-Cluster konfiguriert wurde. Die verteilte Verfügbarkeitsgruppe besitzt zwei Replikate in jeder Verfügbarkeitsgruppe, also insgesamt vier Replikate. Jede Verfügbarkeitsgruppe kann so viele Replikate unterstützen, bis die maximale Anzahl erreicht ist. Eine verteilte Verfügbarkeitsgruppe, die auf der Standard Edition basiert, kann also bis zu vier Replikate besitzen und eine auf der Enterprise Edition basierte Verfügbarkeitsgruppe bis zu 18 Replikate.

<a name="fig1"></a>
![Ansicht auf höchster Ebene für eine verteilte Verfügbarkeitsgruppe][1]

Sie können die Datenverschiebung in verteilten Verfügbarkeitsgruppen als „synchron“ oder „asynchron“ konfigurieren. Die Datenverschiebung innerhalb von verteilten Verfügbarkeitsgruppen weicht jedoch geringfügig von der in einer herkömmlichen Verfügbarkeitsgruppe ab. Obwohl jede Verfügbarkeitsgruppe über ein primäres Replikat verfügt, kann nur eine Kopie der Datenbanken, die Teil einer verteilten Verfügbarkeitsgruppe sind, Einfügungen, Updates und Löschungen akzeptieren. AG 1 ist die primäre Verfügbarkeitsgruppe, wie in der folgenden Abbildung dargestellt. Das primäre Replikat sendet Transaktionen an das sekundäre Replikat von AG 1 und an das primäre Replikat von AG 2. Das primäre Replikat von AG 2 aktualisiert dann das sekundäre Replikat von AG 2. 


![Datenverschiebung in verteilten Verfügbarkeitsgruppen][2]

Die einzige Möglichkeit, um dem primären Replikat von AG 2 das Akzeptieren von Einfügungen, Updates und Löschungen zu ermöglichen, ist das Auslösen eines manuellen Failovers der verteilten Verfügbarkeitsgruppe von AG 1. In der obigen Abbildung enthält AG 1 die beschreibbare Kopie der Datenbank, deshalb macht das Auslösen eines Failovers AG 2 zu der Verfügbarkeitsgruppe, die Einfügungen, Updates und Löschungen verarbeiten kann. Weitere Informationen dazu, wie eine verteilte Verfügbarkeitsgruppe ein Failover auf eine andere auslösen kann, finden Sie unter [Failover to a secondary availability group (Failover auf eine sekundäre Verfügbarkeitsgruppe)]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups).

> [!NOTE]
> Verteilte Verfügbarkeitsgruppen in SQL Server 2016 unterstützen die Failover-Funktion nur von einer Verfügbarkeitsgruppe auf eine andere mithilfe der Option „FORCE_FAILOVER_ALLOW_DATA_LOSS“.

## <a name="sql-server-version-and-edition-requirements-for-distributed-availability-groups"></a>Anforderungen für die SQL Server-Version und -Edition für verteilte Verfügbarkeitsgruppen

Verteilte Verfügbarkeitsgruppen funktionieren derzeit nur mit Verfügbarkeitsgruppen, die mit der derselben Hauptversion von SQL Server erstellt werden. Zum Beispiel müssen alle Verfügbarkeitsgruppen, die Teil einer verteilten Verfügbarkeitsgruppe sind, derzeit mit SQL Server 2016 erstellt werden. Da die Funktion für verteilte Verfügbarkeitsgruppen in SQL Server 2012 oder 2014 noch nicht existiert hat, können Verfügbarkeitsgruppen, die mit diesen Versionen erstellt wurden, nicht Teil von verteilten Verfügbarkeitsgruppen werden. 

> [!NOTE]
> Verteilte Verfügbarkeitsgruppen können mit der Standard Edition oder Enterprise Edition konfiguriert werden, eine Mischung der Editionen in einer verteilten Verfügbarkeitsgruppe wird jedoch nicht unterstützt.

Da zwei separate Verfügbarkeitsgruppen vorliegen, weicht der Installationsprozess für ein Service Pack oder ein kumulatives Update auf ein Replikat, das Teil einer verteilten Verfügbarkeitsgruppe ist, geringfügig von dem für eine herkömmliche Verfügbarkeitsgruppe ab:

1. Beginnen Sie mit dem Aktualisieren der Replikate der sekundären Verfügbarkeitsgruppe in der verteilten Verfügbarkeitsgruppe.

2. Patchen Sie die Replikate der primären Verfügbarkeitsgruppe in der verteilten Verfügbarkeitsgruppe.

3. Lösen Sie, genau wie bei einer herkömmlichen Verfügbarkeitsgruppe, ein Failover der primären Verfügbarkeitsgruppe auf eins ihrer eigenen Replikate (nicht auf das primäre Replikat der sekundären Verfügbarkeitsgruppe) aus und patchen Sie dieses. Wenn kein anderes als das primäre Replikat vorhanden ist, ist ein manuelles Failover auf die sekundäre Verfügbarkeitsgruppe erforderlich.

> [!NOTE]
> Es gibt bisher keine Ankündigungen dazu, ob zukünftige Versionen von SQL Server es ermöglichen werden, dass frühere Versionen Teil derselben verteilten Verfügbarkeitsgruppe sein können. Wenn dieses Szenario möglich wäre, wären verteilte Verfügbarkeitsgruppen als Teil des Upgradeplans einer SQL Server-Version denkbar.

### <a name="windows-server-versions-and-distributed-availability-groups"></a>Windows Server-Versionen und verteilte Verfügbarkeitsgruppen

Eine verteilte Verfügbarkeitsgruppe umfasst mehrere Verfügbarkeitsgruppen, von denen jede ihren eigenen zugrunde liegenden WSFC-Cluster besitzt. Eine verteilte Verfügbarkeitsgruppe ist ein nur in SQL Server verfügbares Konstrukt.  Das bedeutet, dass die WSFC-Cluster, auf denen sich die einzelnen Verfügbarkeitsgruppen befinden, verschiedene Hauptversionen von Windows Server verwenden können. Die Hauptversionen von SQL müssen, wie im vorherigen Abschnitt erläutert wurde, identisch sein. Ähnlich wie bei [the initial figure (der ersten Abbildung)](#fig1) zeigt die folgende Abbildung AG 1 und AG 2 als Teil einer verteilten Verfügbarkeitsgruppe, aber jeder der WSFC-Cluster verwendet eine unterschiedliche Version von Windows Server.


![Verteilte Verfügbarkeitsgruppen mit WSFC-Clustern, die unterschiedliche Versionen von Windows Server verwenden][3]

Für die einzelnen WSFC-Cluster und ihre entsprechenden Verfügbarkeitsgruppen gelten die herkömmlichen Regeln. Das bedeutet, dass sie mit einer Domäne verknüpft werden können oder nicht (Windows Server 2016 und höher). Wenn zwei verschiedene Verfügbarkeitsgruppen in einer einzigen verteilten Verfügbarkeitsgruppe vereint werden, gibt es vier Szenarios:

* Beide WSFC-Cluster werden mit derselben Domäne verknüpft.
* Jeder WSFC-Cluster wird mit einer unterschiedlichen Domäne verknüpft.
* Ein WSFC-Cluster ist mit einer Domäne verknüpft und ein WSFC-Cluster ist nicht mit einer Domäne verknüpft.
* Keiner der WSFC-Cluster ist mit einer Domäne verknüpft.

Wenn beide WSFC-Cluster mit derselben Domäne (gilt nicht für vertrauenswürdige Domänen), müssen Sie beim Erstellen der verteilten Verfügbarkeitsgruppe keine weiteren Schritte durchführen. Bei Verfügbarkeitsgruppen und WSFC-Clustern, die nicht mit derselben Domäne verknüpft sind, müssen Sie Zertifikate verwenden, damit die verteilte Verfügbarkeitsgruppe funktioniert. Dabei gehen Sie so vor wie beim Erstellen einer Verfügbarkeitsgruppe für eine domänenunabhängige Verfügbarkeitsgruppe. Weitere Informationen zum Konfigurieren von Zertifikaten für eine verteilte Verfügbarkeitsgruppe finden Sie in den Schritten 3 bis 13 unter [Create a domain-independent availability group (Erstellen einer domänenunabhängigen Verfügbarkeitsgruppe)](domain-independent-availability-groups.md#create-a-domain-independent-availability-group).

Bei einer verteilten Verfügbarkeitsgruppe müssen die primären Replikate in jeder zugrunde liegenden Verfügbarkeitsgruppe jeweils die Zertifikate der anderen besitzen. Wenn Sie bereits Endpunkte haben, die keine Zertifikate verwenden, konfigurieren Sie diese Endpunkte neu, indem Sie die Anweisung [ALTER ENDPOINT](https://docs.microsoft.com/en-us/sql/t-sql/statements/alter-endpoint-transact-sql) verwenden, um das Verwenden von Zertifikaten zu berücksichtigen.

## <a name="distributed-availability-group-usage-scenarios"></a>Verwendungsszenarios für verteilte Verfügbarkeitsgruppen

Im Folgenden finden Sie die drei Hauptverwendungsszenarios für eine verteilte Verfügbarkeitsgruppe: 

* [Disaster recovery and easier multi-site configurations (Notfallwiederherstellung und vereinfachte Konfigurationen für mehrere Standorte)](#disaster-recovery-and-multi-site-scenarios)
* [Migration to new hardware or configurations, which might include using new hardware or changing the underlying operating systems (Migration zu neuer Hardware oder neuen Konfigurationen, die möglicherweise das Verwenden neuer Hardware oder das Ändern des zugrunde liegenden Betriebssystems erfordert)](#migration-using-a-distributed-availability-group)
* [Increasing the number of readable replicas beyond eight in a single availability group by spanning multiple availability groups (Erhöhen der Anzahl der lesbaren Replikate auf mehr als acht in einer einzigen Verfügbarkeitsgruppe, indem mehrere Verfügbarkeitsgruppen umfasst werden)](#scaling-out-readable-replicas-with-distributed-accessibility-groups)

### <a name="disaster-recovery-and-multi-site-scenarios"></a>Szenarios für Notfallwiederherstellung und mehrere Standorte

Bei einer herkömmlichen Verfügbarkeitsgruppe ist erforderlich, dass alle Server Teil desselben WSFC-Clusters sind, wodurch das Umfassen mehrerer Rechenzentren eine Herausforderung darstellen kann. Die folgende Abbildung zeigt eine herkömmliche Architektur für eine Verfügbarkeitsgruppe mit mehreren Standorten, einschließlich des Datenflusses. Es gibt ein primäres Replikat, das Transaktionen an alle sekundären Replikate sendet. Diese Konfiguration ist in einigen Punkten weniger flexibel als eine verteilte Verfügbarkeitsgruppe. Sie müssen beispielsweise Elemente wie Active Directory (sofern vorhanden) und den Zeugen für ein Quorum in den WSFC-Cluster implementieren. Sie müssen gegebenenfalls auch andere Aspekte eines WSFC-Clusters berücksichtigen, zum Beispiel das Ändern von Knotenvoten.

![Herkömmliche Verfügbarkeitsgruppe mit mehreren Standorten][4]

Verteilte Verfügbarkeitsgruppen bieten ein flexibleres Bereitstellungsszenario für Verfügbarkeitsgruppen, die mehrere Rechenzentren umfassen. Sie können verteilte Verfügbarkeitsgruppen sogar statt in der Vergangenheit verwendeten Funktionen, zum Beispiel [log shipping (Protokollversand)]( https://docs.microsoft.com/en-us/sql/database-engine/log-shipping/about-log-shipping-sql-server), verwenden. Anders als bei herkömmlichen Verfügbarkeitsgruppen ist bei verteilten Verfügbarkeitsgruppen jedoch keine verzögerte Anwendung von Transaktionen möglich. Das bedeutet, dass weder Verfügbarkeitsgruppen noch verteilte Verfügbarkeitsgruppen Sie im Fall eines menschlichen Fehlers unterstützen können, wenn beispielsweise Daten falsch aktualisiert oder gelöscht werden.

Verteilte Verfügbarkeitsgruppen sind lose gekoppelt, was in diesem Fall bedeutet, dass sie keinen einzelnen WSFC-Cluster erfordern und von SQL Server verwaltet werden. Da die WSFC-Cluster einzeln verwaltet werden und die Synchronisation zwischen den beiden Verfügbarkeitsgruppen in erster Linie asynchron abläuft, ist die Konfiguration der Notfallwiederherstellung auf einer anderen Website einfacher. Die primären Replikate in jeder Verfügbarkeitsgruppe synchronisieren ihre eigenen sekundären Replikate.

* Für eine verteilte Verfügbarkeitsgruppe wird nur manuelles Failover unterstützt. Im Fall einer Notfallwiederherstellung, bei der Sie die Rechenzentren wechseln müssen, sollten Sie kein automatisches Failover konfigurieren (mit wenigen Ausnahmen). 
* Sie müssen einige der herkömmlichen Elemente oder Parameter für WSFC-Cluster für Subnetze oder mehrere Standorte (z.B: CrossSubnetTreshold) wahrscheinlich nicht festlegen, aber Sie müssen dennoch dafür sorgen, dass die Netzwerklatenz sich für den Datentransport auf einer anderen Ebene befindet. Der Unterschied besteht darin, dass jeder WSFC-Cluster seine eigene Verfügbarkeit verwaltet, der Cluster ist also nicht eine große Entität mit vier Knoten. Sie haben zwei separate WSFC-Cluster mit je zwei Knoten, wie in der vorherigen Abbildung dargestellt.  
* Wir empfehlen eine asynchrone Datenverschiebung, da diese Vorgehensweise für die Notfallwiederherstellung verwendet wird.
* Wenn Sie eine synchrone Datenverschiebung zwischen dem primären Replikat und mindestens einem sekundären Replikat der sekundären Verfügbarkeitsgruppe konfigurieren, und Sie die synchrone Verschiebung auf der verteilten Verfügbarkeitsgruppe konfigurieren, wird die verteilte Verfügbarkeitsgruppe warten, bis alle synchronen Kopien bestätigen, dass sie die Daten empfangen haben.

### <a name="migrate-by-using-a-distributed-availability-group"></a>Migrieren mithilfe einer verteilten Verfügbarkeitsgruppe

Da verteilte Verfügbarkeitsgruppen auch zwei vollkommen unterschiedliche Konfigurationen von Verfügbarkeitsgruppen unterstützen, ermöglichen diese nicht nur eine einfachere Notfallwiederherstellung und Szenarios für mehrere Standorte, sondern auch Migrationsszenarios. Unabhängig davon, ob Sie zu neuer Hardware oder virtuellen Computern (lokal oder durch IaaS in der öffentlichen Cloud) migrieren, ermöglicht eine verteilte Verfügbarkeitsgruppe das Ausführen einer Migration in Fällen, in denen Sie in der Vergangenheit Sicherungen, Kopien und Wiederherstellungen oder Protokollversand verwendet haben. 

Die Migration ist besonders nützlich in Szenarios, in denen Sie das zugrunde liegende Betriebssystem ändern oder aktualisieren, während Sie dieselbe Version von SQL Server behalten. Obwohl Windows Server 2016 ein paralleles Upgrade von Windows Server 2012 R2 auf derselben Hardware zulässt, entscheiden sich die meisten Benutzer für das Bereitstellen von neuer Hardware oder virtuellen Computern. 

Beenden Sie am Ende des Migrationsprozesses den gesamten Datenverkehr zur ursprünglichen Verfügbarkeitsgruppe, und ändern Sie die verteilte Verfügbarkeitsgruppe zur synchronen Datenverschiebung, um die Migration zur neuen Konfiguration abzuschließen. Diese Aktion gewährleistet, dass das primäre Replikat der sekundären Verfügbarkeitsgruppe vollständig synchronisiert wird, sodass keine Daten verloren gehen. Führen Sie ein Failover der verteilten Verfügbarkeitsgruppe auf die sekundäre Verfügbarkeitsgruppe aus, nachdem Sie die Synchronisierung überprüft haben. Weitere Informationen finden Sie unter [Fail over to a secondary availability group (Failover auf eine sekundäre Verfügbarkeitsgruppe)](configure-distributed-availability-groups.md#failover).

Nach der Migration ist die sekundäre Verfügbarkeitsgruppe nun die neue primäre Verfügbarkeitsgruppe, und Sie müssen eventuell eine der folgenden Aktionen durchführen:

* Benennen Sie den Listener auf der sekundären Verfügbarkeitsgruppe um (und löschen oder benennen Sie den alten Listener auf der ursprünglichen primären Verfügbarkeitsgruppe nach Möglichkeit um), oder erstellen Sie ihn mithilfe des Listeners auf der ursprünglichen primären Verfügbarkeitsgruppe neu, sodass Anwendungen und Benutzer auf die neue Konfiguration zugreifen können.
* Wenn eine Umbenennung oder Neuerstellung nicht möglich ist, verweisen Sie Anwendungen und Benutzer auf den Listener auf der sekundären Verfügbarkeitsgruppe.

### <a name="scale-out-readable-replicas-with-distributed-availability-groups"></a>Horizontales Hochskalieren von lesbaren Replikaten mit verteilten Verfügbarkeitsgruppen

Eine einzelne verteilte Verfügbarkeitsgruppe kann je nach Bedarf bis zu 16 sekundäre Replikate ausweisen. Sie kann also bis zu 18 Kopien zum Lesen besitzen, einschließlich der zwei primären Replikat der unterschiedlichen Verfügbarkeitsgruppen. Dieser Ansatz bedeutet, dass mehr als eine Website beinahe Echtzeitzugriff haben kann, um Berichte an zahlreiche Anwendungen zu senden.

Verteilte Verfügbarkeitsgruppen bieten Ihnen ein besseres horizontales Hochskalieren einer schreibgeschützten Farm als eine einzige Verfügbarkeitsgruppe. Für das horizontale Hochskalieren von lesbaren Replikaten mit einer verteilten Verfügbarkeitsgruppe gibt es zwei Möglichkeiten:

* Sie können das primäre Replikat der sekundären Verfügbarkeitsgruppe in einer verteilten Verfügbarkeitsgruppe verwenden, um eine weitere verteilte Verfügbarkeitsgruppe zu erstellen, obwohl sich die Datenbank nicht um Status „RECOVERY“ befindet.
* Sie können auch das primäre Replikat der primären Verfügbarkeitsgruppe verwenden, um eine weitere verteilte Verfügbarkeitsgruppe zu erstellen.

Das heißt, ein primäres Replikat kann Teil von zwei unterschiedlichen verteilten Verfügbarkeitsgruppen sein. Die folgende Abbildung zeigt AG 1 und AG 2, die beide Teil der verteilten AG 1 sind, während AG 2 und AG 3 Teil der verteilten AG 2 sind. Das primäre Replikat von AG 2 ist sowohl ein sekundäres Replikat für die verteilte AG 1 als auch ein primäres Replikat der verteilten AG 2.

![Horizontales Hochskalieren von Lesevorgängen mithilfe von verteilten Verfügbarkeitsgruppen][5]

Die folgende Abbildung zeigt AG 1 als das primäre Replikat von zwei unterschiedliche verteilte Verfügbarkeitsgruppen: von der verteilten AG 1 (bestehend aus AG 1 und AG 2) und der verteilten AG 2 (bestehend aus AG 1 und AG 3).


![Beispiel: eine weitere Möglichkeit zum horizontalen Hochskalieren von Lesevorgängen mithilfe von verteilten Verfügbarkeitsgruppen][6]


In den beiden obigen Beispielen können insgesamt bis zu 27 Replikate in den drei Verfügbarkeitsgruppen vorhanden sein, von denen jedes für schreibgeschützte Abfragen verwendet werden kann. 

[Read-only routing (Schreibgeschütztes Routing)]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server) ist mithilfe von verteilten Verfügbarkeitsgruppen derzeit nicht möglich. Alle Abfragen, die zur Verbindung den Listener verwenden, gehen an das primäre Replikat. Andernfalls müssen Sie jedes Replikat so konfigurieren, dass alle Verbindungen als sekundäres Replikat zugelassen werden und direkt auf diese zugegriffen wird. Dieses Verhalten wird mit einem Update zu SQL Server 2016 oder in einer zukünftigen Version von SQL Server möglicherweise geändert.

## <a name="initialize-secondary-availability-groups-in-a-distributed-availability-group"></a>Initialisieren von sekundären Verfügbarkeitsgruppen in eine verteilte Verfügbarkeitsgruppe

Verteilte Verfügbarkeitsgruppen wurden mit [automatischem Seeding]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group) als Hauptmethode zum Initialisieren des primären Replikats auf die sekundäre Verfügbarkeitsgruppe entwickelt. Eine vollständige Wiederherstellung einer Datenbank auf dem primären Replikat der sekundären Verfügbarkeitsgruppe ist möglich, wenn Sie folgende Aktionen durchführen:

1. Stellen Sie die Datenbanksicherung mit „WITH NORECOVERY“ wieder her.
2. Falls nötig, stellen Sie die richtigen Sicherungen der Transaktionsprotokolle mit „WITH NORECOVERY“ wieder her.
3. Erstellen Sie die sekundäre Verfügbarkeitsgruppe ohne einen Datenbanknamen anzugeben, und legen Sie SEEDING_MODE auf AUTOMATIC fest.
4. Erstellen Sie die verteilte Verfügbarkeitsgruppe mithilfe von automatischem Seeding.

Wenn Sie das primäre Replikat der sekundären Verfügbarkeitsgruppe zu der verteilten Verfügbarkeitsgruppe hinzufügen, wird das Replikat mit der primären Datenbank der primären Verfügbarkeitsgruppe verglichen und die Datenbank wird durch Seeding auf den gleichen Stand wie die Quelle gebracht. Es gibt einige Vorbehalte:

* Die Ausgabe in `sys.dm_hadr_automatic_seeding` auf dem primären Replikat der sekundären Verfügbarkeitsgruppe wird als `current_state` „FAILED“ mit dem Hinweis „Nachrichtentimeout bei der Seedingüberprüfung“ angezeigt.

* Das aktuelle SQL Server-Protokoll auf dem primären Replikat der sekundären Verfügbarkeitsgruppe wird anzeigen, dass das Seeding erfolgreich war und dass die [LSNs]( https://docs.microsoft.com/en-us/sql/relational-databases/sql-server-transaction-log-architecture-and-management-guide) synchronisiert wurden.

* Die Ausgabe, die in `sys.dm_hadr_automatic_seeding` auf dem primären Replikat der primären Verfügbarkeitsgruppe angezeigt wird, zeigt „COMPLETED“ als „current_state“ an. 

* Das Seeding weist bei verteilten Verfügbarkeitsgruppen ebenfalls ein unterschiedliches Verhalten auf. Damit das Seeding auf dem sekundären Replikat beginnt, müssen Sie den Befehl `ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE` auf dem Replikat ausführen. Obwohl diese Bedingung immer noch auf jedes sekundäre Replikat zutrifft, das Teil der zugrunde liegenden Verfügbarkeitsgruppe ist, verfügt das primäre Replikat der sekundären Verfügbarkeitsgruppe schon über die erforderlichen Berechtigungen, um mit dem Seeding zu beginnen, nachdem es zu der verteilten Verfügbarkeitsgruppe hinzugefügt wurde. 

### <a name="view-distributed-availability-group-information"></a>Anzeigen von Informationen zu verteilten Verfügbarkeitsgruppen 
    
Wie bereits erwähnt, ist eine verteilte Verfügbarkeitsgruppe ein nur in SQL Server verfügbares Konstrukt und wird nicht im zugrunde liegenden WSFC-Cluster angezeigt. Die folgende Abbildung zeigt zwei unterschiedliche WSFC-Cluster („CLUSTER_A“ und „CLUSTER_B“), von denen jedes seine eigenen Verfügbarkeitsgruppen besitzt. Im Folgenden werden nur AG 1 in „CLUSTER_A“ und AG 2 in „CLUSTER_B“ erläutert. 

<!-- ![Two WSFC clusters with multiple availability groups through PowerShell Get-ClusterGroup command][7]  -->
<a name="fig7"></a>

```
PS C:\> Get-ClusterGroup -Cluster CLUSTER_A

Name                            OwnerNode             State
----                            ---------             -----
AG1                             DENNIS                Online
Available Storage               GLEN                  Offline
Cluster Group                   JY                    Online
New_RoR                         DENNIS                Online
Old_RoR                         DENNIS                Online
SeedingAG                       DENNIS                Online


PS C:\> Get-ClusterGroup -Cluster CLUSTER_B

Name                            OwnerNode             State
----                            ---------             -----
AG2                             TOMMY                 Online
Available Storage               JC                    Offline
Cluster Group                   JC                    Online
```

Die detaillierten Informationen über eine verteilte Verfügbarkeitsgruppe befindet sich in SQL Server, insbesondere in den dynamischen Verwaltungsansichten für Verfügbarkeitsgruppen. Derzeit werden Informationen über verteilte Verfügbarkeitsgruppen in SQL Server Management Studio nur auf dem primären Replikat der Verfügbarkeitsgruppe angezeigt. Wie in der folgenden Abbildung dargestellt zeigt SQL Server Management Studio unter dem Ordner „Verfügbarkeitsgruppen“ an, dass es eine verteilte Verfügbarkeitsgruppe gibt. Die Abbildung zeigt AG1 als das primäre Replikat einer einzelnen lokalen Verfügbarkeitsgruppe dieser Instanz, nicht aber als das einer verteilten Verfügbarkeitsgruppe.

![Ansicht des primären Replikats des ersten WSFC-Clusters einer verteilten Verfügbarkeitsgruppe in SQL Server Management Studio][8]


Wenn Sie jedoch mit der rechten Maustaste auf die verteilte Verfügbarkeitsgruppe klicken, sind keine Optionen verfügbar (siehe folgende Abbildung) und die erweiterten Verfügbarkeitsdatenbanken, Verfügbarkeitsgruppenlistener und Verfügbarkeitsreplikatordner sind alle leer. SQL Server Management Studio 16 zeigt dieses Ergebnis an, das sich jedoch in einer zukünftigen Version von SQL Server Management Studio ändern könnte.

![Keine Optionen für eine Aktion verfügbar][9]

Wie in der folgenden Abbildung dargestellt zeigen sekundäre Replikate in SQL Server Management Studio nichts an, das sich auf die verteilte Verfügbarkeitsgruppe bezieht. Die Namen dieser Verfügbarkeitsgruppen können den Rollen zugeordnet werden, die im vorherigen Bild ([CLUSTER_A – WSFC-Cluster)](#fig7) angezeigt wurden.

![Ansicht eines sekundären Replikats in SQL Server Management Studio][10]

Die gleichen Konzepte gelten, wenn Sie die dynamischen Verwaltungsansichten verwenden. Indem Sie die folgende Abfrage verwenden, können Sie alle Verfügbarkeitsgruppen (reguläre und verteilte) und die enthaltenen Knoten anzeigen lassen. Dieses Ergebnis wird nur angezeigt, wenn Sie das primäre Replikat in einem der WSFC-Cluster abfragen, die in der verteilten Verfügbarkeitsgruppe enthalten sind. Es gibt eine neue Spalte namens `is_distributed` in der dynamischen Verwaltungsansicht `sys.availability_groups`, die den Wert „1“ enthält, wenn es sich bei der Verfügbarkeitsgruppe um eine verteilte Verfügbarkeitsgruppe handelt. Zum Anzeigen dieser Spalte ist Folgendes nötig:

```sql
SELECT ag.[name] as 'AG Name', 
    ag.Is_Distributed, 
    ar.replica_server_name as 'Replica Name'
FROM    sys.availability_groups ag, 
    sys.availability_replicas ar       
WHERE   ag.group_id = ar.group_id
```

In der folgenden Abbildung wird ein Beispiel für eine Ausgabe des zweiten WSFC-Clusters gezeigt, das in der verteilten Verfügbarkeitsgruppe enthalten ist. SPAG1 besteht aus zwei Replikaten: DENNIS und JY. Die verteilte Verfügbarkeitsgruppe namens „SPDistAG“ verfügt jedoch über die Namen der zwei enthaltenen Verfügbarkeitsgruppen (SPAG1 und SPAG2) statt den Namen der Instanzen, wie es bei herkömmlichen Verfügbarkeitsgruppen der Fall ist. 

![Beispielausgabe der vorangegangenen Abfrage][11]

Jeder Status, der in SQL Server Management Studio auf dem Dashboard und in anderen Bereichen angezeigt wird, ist nur für die lokale Synchronisierung innerhalb dieser Verfügbarkeitsgruppe bestimmt. Führen Sie eine Abfrage der dynamischen Verwaltungsansicht durch, um die Integrität einer verteilten Verfügbarkeitsgruppe anzuzeigen. Die folgende Beispielabfrage erweitert und präzisiert die vorherige Abfrage:

```sql
SELECT ag.[name] as 'AG Name', ag.is_distributed, ar.replica_server_name as 'Underlying AG', ars.role_desc as 'Role', ars.synchronization_health_desc as 'Sync Status'
FROM    sys.availability_groups ag, 
sys.availability_replicas ar,       
sys.dm_hadr_availability_replica_states ars       
WHERE   ar.replica_id = ars.replica_id
and     ag.group_id = ar.group_id 
and ag.is_distributed = 1
```
       
       
![Status der verteilten Verfügbarkeitsgruppe][12]


Sie können die vorherige Abfrage weiter erweitern, indem Sie `sys.dm_hadr_database_replicas_states` hinzufügen, um die zugrunde liegende Leistung in der dynamischen Verwaltungsansicht anzuzeigen. Die dynamische Verwaltungsansicht speichert derzeit nur Informationen über die zweite Verfügbarkeitsgruppe. Die folgende Beispielabfrage, die auf der primären Verfügbarkeitsgruppe ausgeführt wird, erzeugt die unten dargestellte Beispielausgabe:

```
SELECT ag.[name] as 'Distributed AG Name', ar.replica_server_name as 'Underlying AG', dbs.[name] as 'DB', ars.role_desc as 'Role', drs.synchronization_health_desc as 'Sync Status', drs.log_send_queue_size, drs.log_send_rate, drs.redo_queue_size, drs.redo_rate
FROM    sys.databases dbs,
    sys.availability_groups ag,
    sys.availability_replicas ar,
    sys.dm_hadr_availability_replica_states ars,
    sys.dm_hadr_database_replica_states drs
WHERE   drs.group_id = ag.group_id
and ar.replica_id = ars.replica_id
and ars.replica_id = drs.replica_id
and dbs.database_id = drs.database_id
and ag.is_distributed = 1
```

![Leistungsinformationen einer verteilten Verfügbarkeitsgruppe][13]


### <a name="next-steps"></a>Nächste Schritte 

* [Verwenden des Assistenten für Verfügbarkeitsgruppen (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

* [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
* [Erstellen einer Verfügbarkeitsgruppe mit Transact-SQL](create-an-availability-group-transact-sql.md)

Dieser Inhalt wurde von [Allan Hirt](http://mvp.microsoft.com/en-us/PublicProfile/4025254?fullName=Allan%20Hirt), einem Microsoft Most Valued Professional, verfasst.

<!--Image references-->
[1]: ./media/dag-01-high-level-view-distributed-ag.png
[2]: ./media/dag-02-distributed-ag-data-movement.png
[3]: ./media/dag-03-distributed-ags-wsfcs-different-versions-windows-server.png
[4]: ./media/dag-04-traditional-multi-site-ag.png
[5]: ./media/dag-05-scaling-out-reads-with-distributed-ags.png
[6]: ./media/dag-06-another-scaling-out-reads-using-distributed-ags-example.png
[7]: ./media/dag-07-two-wsfcs-multiple-ags-through-get-clustergroup-command.png
[8]: ./media/dag-08-view-smss-primary-replica-first-wsfc-distributed-ag.png
[9]: ./media/dag-09-no-options-available-action.png
[10]: ./media/dag-10-view-ssms-secondary-replica.png
[11]: ./media/dag-11-example-output-of-query-above.png
[12]: ./media/dag-12-distributed-ag-status.png
[13]: ./media/dag-13-performance-information-distributed-ag.png

 

