---
title: "Always On-Verfügbarkeitsgruppen für SQLServer on Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: 54fec5a177d5edf463853d230a56c28eeb1b0f7c
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="always-on-availability-groups-on-linux"></a>Always On-Verfügbarkeitsgruppen unter Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel beschreibt die Merkmale der AlwaysOn-Verfügbarkeitsgruppen (Testreihen) unter Linux-basierte [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Installationen. Dazu gehören auch Unterschiede zwischen Linux- und Windows Server-Failovercluster (WSFC)-Basis Testreihen. Finden Sie unter der [Dokumentation zu Windows-basierten](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) für die Grundlagen der-Verfügbarkeitsgruppen identisch unter Windows und Linux außer dem WSFC Arbeit.

Aus Sicht der allgemeinen Verfügbarkeitsgruppen unter [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux sind dieselben wie WSFC-basierte Implementierungen werden. Das bedeutet, dass alle Einschränkungen und Funktionen identisch, abgesehen von einigen Ausnahmen sind. Die Hauptunterschiede sind:

-   Microsoft Distributed Transaction Coordinator (DTC) wird nicht unterstützt, unter Linux in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Wenn Ihre Anwendungen die Verwendung von verteilten Transaktionen erfordern und eine AG, bereitstellen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Windows.
-   Linux-basierte Bereitstellungen verwenden Schrittmacher anstelle eines WSFC.
-   Im Gegensatz zu den meisten Konfigurationen für Testreihen unter Windows mit Ausnahme der Arbeitsgruppe Clusterszenario erfordert Schrittmacher nie Active Directory-Domänendienste (AD DS).
-   Zum Fehlschlagen einer AG von einem Knoten zu einem anderen unterscheidet sich zwischen Linux- und Windows.
-   Bestimmte Einstellungen wie z. B. `required_synchronized_secondaries_to_commit` kann nur über Schrittmacher unter Linux geändert werden, während der Installation ein WSFC-basierte Transact-SQL verwendet.

## <a name="number-of-replicas-and-cluster-nodes"></a>Anzahl der Replikate und Clusterknoten

Ein VG in [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] zwei Replikate mit insgesamt haben kann: ein primäres und ein sekundäres Replikat, das nur aus Gründen der Verfügbarkeit verwendet werden kann. Es kann nicht für alles andere, z. B. lesbare Abfragen verwendet werden. Einer AG in [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] können bis zu neun Gesamtanzahl der Replikate verfügen: eine primäre und bis zu acht sekundäre Datenbanken, von denen bis zu drei (einschließlich der primären) kann synchron sein. Wenn einen Cluster zugrunde liegen, kann es sein maximal 16 Knoten insgesamt, wenn Corosync beteiligt ist. Eine verfügbarkeitsgruppe kann höchstens neun 16 Knoten mit umfassen [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)], und zwei mit [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Eine zwei Replikaten-Konfiguration, die Möglichkeit, die für ein anderes Replikat ein automatisches Failover erfordert, erfordert die Verwendung eines Replikats Konfiguration nur, wie in beschrieben [Konfiguration nur Replikat und Quorum](#configuration-only-replica-and-quorum). Konfiguration nur Replikate wurden in eingeführt [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] kumulative Update 1 (CU1), damit, die mindestens erforderliche Version für diese Konfiguration bereitgestellt werden soll.

Wenn Schrittmacher verwendet wird, muss er ordnungsgemäß konfiguriert werden, damit einsatzbereit bleibt. Das bedeutet, dass Quorum- und STONITH hinsichtlich der Schrittmacher zusätzlich zu anderen ordnungsgemäß implementiert werden muss [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Anforderungen z. B. ein nur-Konfiguration-Replikat.

Lesbare sekundäre Replikate werden nur unterstützt, mit [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Typ und Failover Cluster-Modus

Neu bei [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] kann durch die Verwendung eines Cluster-Typs für Testreihen. Linux, es gibt zwei gültige Werte: extern und None. Ein Cluster von externen also Schrittmacher unterhalb der Verfügbarkeitsgruppe verwendet wird. Verwendung von externen für Clustertyp erfordert, dass der Failovermodus als auch auf externe festgelegt werden (ebenfalls neu in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Automatisches Failover wird unterstützt, jedoch im Gegensatz zu einem WSFC ist Failovermodus auf externe, nicht automatisch festgelegt, wenn Schrittmacher verwendet wird. Im Gegensatz zu einem WSFC wird der Schrittmacher Teil der Verfügbarkeitsgruppe erstellt, nachdem der AG konfiguriert ist.

Ein Cluster ohne bedeutet, dass keine Notwendigkeit für besteht noch die Verfügbarkeitsgruppe verwendet wird, Schrittmacher. Sogar auf Servern, die Schrittmacher konfiguriert wurde, ist eine AG mit einem Cluster keine "" konfiguriert, Schrittmacher nicht sehen oder verwalten, AG. Ein Clustertyp ' None ' unterstützt nur Manuelles Failover von einem primären zu einem sekundären Replikat. Eine AG erstellt keine zielt in erster Linie für die-Horizontales Skalieren von Lesevorgängen Szenario als auch für Upgrades. Während sie in Szenarien wie die Wiederherstellung im Notfall oder lokale Verfügbarkeit arbeiten kann, wenn kein automatisches Failover erforderlich ist, wird nicht empfohlen. Der Listener Story ist auch ohne Schrittmacher komplexer.

Clustertyp befindet sich in der [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] dynamische verwaltungssicht (DMV) `sys.availability_groups`, in den Spalten `cluster_type` und `cluster_type_desc`.

## <a name="requiredsynchronizedsecondariestocommit"></a>erforderliche\_synchronisiert\_sekundäre Replikate\_auf\_Commit

Neu bei [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] ist eine Einstellung, mit der Testreihen aufgerufen `required_synchronized_secondaries_to_commit`. Das weist der Verfügbarkeitsgruppe auf die Anzahl der sekundären Replikate, die im Gleichschritt mit dem primären Replikat werden muss. Dadurch können z. B. Automatisches Failover (nur bei Schrittmacher Cluster mit einem externen integriert), und das Verhalten der z. B. die Verfügbarkeit der primären steuert, wenn die richtige Anzahl sekundärer Replikate entweder online oder offline ist. Erfahren Sie, wie dies funktioniert, erfahren Sie unter [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md). Die `required_synchronized_secondaries_to_commit` Wert ist standardmäßig festgelegt und Beibehalten von Schrittmacher /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Sie können diesen Wert manuell überschreiben.

Die Kombination von `required_synchronized_secondaries_to_commit` und die neue Sequenznummer (befindet sich in `sys.availability_groups`) informiert Schrittmacher und [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] , z. B. Automatisches Failover auftreten kann. In diesem Fall müsste ein sekundäres Replikat derselben Sequenznummer wie die primäre Datenbank, was bedeutet, dass es mit der neuesten Konfigurationsinformationen auf dem neuesten Stand ist.

Es gibt drei Werte, die für die festgelegt werden können `required_synchronized_secondaries_to_commit`: 0, 1 oder 2. Sie steuern das Verhalten von Was geschieht, wenn ein Replikat nicht mehr verfügbar ist. Die Zahlen entsprechen die Anzahl der sekundären Replikate, die mit dem primären Replikat synchronisiert werden müssen. Das Verhalten ist wie folgt unter Linux:

-   0 – ist kein automatisches Failover möglich, da kein sekundäres Replikat synchronisiert werden muss. Die primäre Datenbank ist jederzeit verfügbar.
-   1 – ein sekundäres Replikat muss im synchronisiert-Status mit dem primären Replikat; Automatisches Failover ist möglich. Die primäre Datenbank ist nicht verfügbar, bis ein sekundäres Replikat für synchrone verfügbar ist.
-   2 – beide sekundäre Replikate in einer drei oder mehr Knoten AG-Konfiguration müssen mit dem primären Replikat synchronisiert werden; Automatisches Failover ist möglich.

`required_synchronized_secondaries_to_commit` steuert nicht nur das Verhalten von Failovers mit synchronen Replikate, jedoch mit Verlust von Daten. Mit einem Wert von 1 oder 2 ist ein sekundäres Replikat immer synchronisiert werden, erforderlich, daher tritt immer Datenredundanz. Bedeutet, dass keine Daten verloren.

So ändern Sie den Wert der `required_synchronized_secondaries_to_commit`, verwenden Sie die folgende Syntax:

>[!NOTE]
>Ändern des Werts führt dazu, dass die Ressource neu starten, d. h. einen kurzen Ausfall. Die einzige Möglichkeit, dieses Problem zu vermeiden werden der Ressourcensatz nicht vom Cluster verwaltet wird, vorübergehend sein.

**Red Hat Enterprise Linux (RHEL) und Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

wobei *AGResourceName* ist der Name der Ressource für die Verfügbarkeitsgruppe konfiguriert und *Wert* ist 0, 1 oder 2. Um es wieder auf den Standardwert von Schrittmacher verwalten den Parameter festzulegen, führen Sie der gleichen Anweisung ohne Wert.

Automatisches Failover einer Verfügbarkeitsgruppe ist möglich, wenn die folgenden Bedingungen erfüllt sind:

-   Das primäre und das sekundäre Replikat werden auf synchrone datenverschiebung festgelegt.
-   Die sekundäre Datenbank dem Status synchronisiert (nicht synchronisiert), was bedeutet, dass die beiden am selben Datenpunkt sind.
-   Der Typ des Clusters wird auf externen festgelegt. Automatisches Failover ist nicht möglich, mit einem Clustertyp ' None '.
-   Die `sequence_number` des sekundären Replikats zu der primären hat die höchste Sequenznummer – das heißt, des sekundären Replikats des `sequence_number` vom ursprünglichen primären Replikat entspricht.

Wenn diese Bedingungen erfüllt sind, und der Server, die das primäre Replikat hostet fehlschlägt, wird in die Verfügbarkeitsgruppe auf ein synchrones Replikat Besitz geändert werden. Das Verhalten für synchrone Replikate (von denen es drei kann insgesamt: ein primäres und zwei sekundäre Replikate) können weitere gesteuert werden, indem `required_synchronized_secondaries_to_commit`. Dies funktioniert mit Testreihen unter Windows und Linux jedoch vollständig anders konfiguriert ist. Unter Linux wird der Wert automatisch vom Cluster für die AG-Ressource selbst konfiguriert werden.

## <a name="configuration-only-replica-and-quorum"></a>Nur Configuration-Replikat und quorum

Neue Funktion in [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] ab CU1 ist ein Replikat nur Konfiguration. Da Schrittmacher eines WSFC unterscheidet, besonders bei der Quorum- und erfordern STONITH, funktioniert müssen nur eine Konfiguration mit zwei Knoten nicht bei einer AG. Für eine FCI können die Quorum-Mechanismen von Schrittmacher Ordnung, sein, da alle Vermittlung der FCI-Failover auf den Cluster-Schicht passiert. Für eine AG, erfolgt die Vermittlung unter Linux in [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], wo alle Metadaten gespeichert werden. Hier kommt das Replikat nur Konfiguration ins Spiel.

Ohne etwas anderes wäre eine dritte Knoten und mindestens ein synchronisiertes Replikat erforderlich. Dies funktioniert nicht für [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)], da es nur zwei Replikate in einer Verfügbarkeitsgruppe teilnehmen aufweisen kann. Das Replikat nur Konfiguration speichert AG-Ebenenkonfiguration in der master-Datenbank identisch mit den anderen Replikaten in der verfügbarkeitsgruppenkonfiguration an. Das Replikat Konfiguration nur die Benutzerdatenbanken auf Einbeziehung in die AG keinen. Die Konfigurationsdaten werden von der primären synchron gesendet. Konfigurationsdaten werden anschließend während Failover ausgeführt werden, wird, ob sie automatisch oder manuell eingestellt sind.

Für eine Verfügbarkeitsgruppe Quorum beibehalten und automatische Failover mit einem externen Cluster aktivieren muss er entweder:

-   Haben Sie drei synchroner Replikate ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] nur); oder
-   Haben Sie zwei Replikate (Primäres und sekundäres) als auch eines Replikats Konfiguration.

Ein manuelles Failover möglich, unabhängig davon, ob externe oder keine cluster-Typen für die AG-Konfigurationen. Während ein Replikats Konfiguration nur mit einer Verfügbarkeitsgruppe kann, die einen Cluster ' None ' verfügt konfiguriert werden, wird es nicht empfohlen, da es die Bereitstellung erschwert. Ändern Sie für diese Konfigurationen manuell `required_synchronized_secondaries_to_commit` Wert von mindestens 1 und haben muss, damit mindestens ein synchronisiertes Replikat vorhanden ist.

Ein Replikat nur Konfiguration aufgenommen werden kann, auf eine beliebige Edition von [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], einschließlich [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Diese Lizenzierungskosten wird minimiert und sichergestellt, generische Vergleich funktioniert mit Testreihen in [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Dies bedeutet, dass das dritte erforderlichen Server muss lediglich für die Mindestspezifikation erfüllen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], da es keine Transaktion Benutzerdatenverkehr für die AG empfängt.

Wenn ein Replikat nur Konfiguration verwendet wird, hat er das folgende Verhalten:

-   Standardmäßig `required_synchronized_secondaries_to_commit` auf 0 festgelegt ist. Dies kann auf 1 manuell geändert werden, falls gewünscht.
-   Ausfall des primären und `required_synchronized_secondaries_to_commit` gleich 0 ist, das sekundäre Replikat zum neuen primären und zum Lesen und Schreiben von verfügbar sein wird. Wenn der Wert 1 beträgt, automatisches Failover ausgeführt wird, sondern akzeptiert keine neue Transaktionen aus, bis das andere Replikat online ist.
-   Wenn ein sekundäres Replikat ein Fehler auftritt und `required_synchronized_secondaries_to_commit` ist 0, das primäre Replikat weiterhin Transaktionen akzeptiert, aber wenn das primäre zu diesem Zeitpunkt ein Fehler auftritt, besteht kein Schutz der Daten noch um ein Failover möglich (manuell oder automatisch), da ein sekundäres Replikat nicht verfügbar ist.
-   Schlägt die Konfiguration nur Replikate die Verfügbarkeitsgruppe funktioniert normal, aber kein automatisches Failover ist möglich.
-   Wenn ein sekundäres Replikat und das Replikat nur Konfiguration ein Fehler auftritt, das primäre kann keine Transaktionen akzeptieren und niemanden ausgegeben für das primäre für ein.

In CU1 liegt ein bekannte Fehler an der Protokollierung in der corosync.log-Datei, die generiert wird, über `mssql-server-ha`. Wenn ein sekundäres Replikat nicht in der Lage, den primären aufgrund der Anzahl der erforderlichen Replikate verfügbar ist, wird die aktuelle Nachricht auf, "1 Sequenznummern empfangen soll, aber nur 2 empfangen. Nicht genügend Replikate sind online, um das lokale Replikat sicher höher stufen." Die Zahlen sollten rückgängig gemacht werden soll, und es müsste angegeben ", 2 Sequenznummern empfangen, aber nur 1 empfangen. Nicht genügend Replikate sind online, um das lokale Replikat sicher höher stufen." 

## <a name="multiple-availability-groups"></a>Mehrere Verfügbarkeitsgruppen 

Mehrere AG kann pro Schrittmacher Cluster oder eine Gruppe von Servern erstellt werden. Als einzige Beschränkung gilt Systemressourcen verfügbar sind. AG Besitz wird vom Master angezeigt. Verschiedene Testreihen können im Besitz von verschiedenen Knoten eines; Sie müssen nicht alle auf demselben Knoten ausgeführt werden.

## <a name="drive-and-folder-location-for-databases"></a>Laufwerk- und Ordnerpfad Speicherort für Datenbanken

Wie auf Windows-basierten Testreihen sollten das Laufwerk und die Ordnerstruktur für die Benutzerdatenbanken auf Einbeziehung in einer AG identisch sein. Angenommen, in die Benutzerdatenbanken sind `/var/opt/mssql/userdata` auf Server A, sollte dieser Ordner auf Server b vorhanden sein Die einzige Ausnahme hierbei ist in den Abschnitt erwähnt wurden [Interoperabilität mit Windows-basierten Verfügbarkeitsgruppen und Replikate](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>Der Listener unter Linux

Der Listener ist die optionale Funktionen für eine Verfügbarkeitsgruppe. Es stellt einen einzelnen Zugriffspunkt für alle Verbindungen (Lese-/Schreibzugriff auf das primäre Replikat und/oder ohne Schreibzugriff auf sekundäre Replikate), damit Anwendungen und Endbenutzern nicht müssen wissen, welche Server die Daten gehostet wird. In einem WSFC ist dies die Kombination von einer Netzwerknamenressource und einer IP-Adressressource, die dann in AD DS (falls erforderlich) registriert wurde, sowie DNS. In Kombination mit der AG-Ressource selbst stellt er diese Abstraktion bereit. Weitere Informationen auf einen Listener finden Sie unter [Listener, Clientkonnektivität und Anwendungsfailover](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

Der Listener unter Linux ist anders konfiguriert, aber die Funktionen sind identisch. Es ist kein Konzept für eine Netzwerknamenressource in Schrittmacher, noch wird ein Objekt in AD DS erstellt; Es ist nur eine IP-Adressressource erstellt in Schrittmacher, die auf einem Knoten ausgeführt werden kann. Ein Eintrag zugeordneten IP-Adressressource für den Listener in DNS mit einem "Angezeigter Name" muss erstellt werden. Die IP-Adressressource für den Listener wird nur auf dem Server, die das primäre Replikat für diese verfügbarkeitsgruppe hosten aktiv sein.

Wenn Schrittmacher verwendet wird, und eine IP-Adressressource wird erstellt, die der Listener zugeordnet ist, wird ein kurzen Ausfall wie die IP-Adresse auf einem Server beendet und gestartet, auf dem anderen wird, ob sie automatische oder manuelle Failover ist. Dies bietet eine Abstraktion über die Kombination aus einem einzelnen Namen und IP-Adresse wird es der Ausfall nicht maskiert. Eine Anwendung muss die Trennung von irgendeine Funktionalität erkannt und erneute Verbinden mit verarbeiten können.

Allerdings ist die Kombination des DNS-Name und IP-Adresse noch nicht genug, um alle Funktionen bereitzustellen, die ein Listener für einen wsfc-Cluster enthält z. B. das schreibgeschützte routing für ein sekundäres Replikat. Beim Konfigurieren einer Verfügbarkeitsgruppe muss "Listener" noch zu konfigurierenden [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Dies kann im Assistenten als auch die Transact-SQL-Syntax angezeigt werden. Es gibt zwei Möglichkeiten, dies wie auf Windows-Funktion konfiguriert werden kann:

-   Für eine AG mit einem Cluster externer, zugeordnet die IP-Adresse "Listener" im erstellten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] sollte die IP-Adresse der Ressource in Schrittmacher erstellt werden.
-   Verwenden Sie für eine AG mit einem Cluster keine erstellt die IP-Adresse, die das primäre Replikat zugeordnet.

Die Instanz, die die angegebene IP-Adresse zugeordnet sind, dann wird der Koordinator für Angaben wie die schreibgeschützten routing-Anforderungen von Anwendungen.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilität mit Windows-basierten Verfügbarkeitsgruppen und Replikate 

Eine, die mit einem Clustertyp der externen oder einem WSFC AG sind keine Plattformen cross Replikate. Dies ist "true" gibt an, ob die Verfügbarkeitsgruppe [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] oder [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Das bedeutet, dass in einer herkömmlichen AG-Konfiguration mit einem Cluster zugrunde liegen, darf nicht auf einem wsfc- und die andere unter Linux mit Schrittmacher ein Replikat sein.

Eine AG mit einem Cluster keine möglich seiner Replikate OS-hinweg, gelten, damit in der gleichen Verfügbarkeitsgruppe konnte beide Replikate mit Linux und Windows-basierte vorhanden sein. Ein Beispiel ist hier angezeigt, in dem das primäre Replikat ist Windows-basierten, während die sekundäre Datenbank auf einem Linux-Distributionen enthalten ist.

![Hybride None](./media/sql-server-linux-availability-group-overview/image1.png)

Eine verteilte Verfügbarkeitsgruppe kann auch OS Grenzen überqueren. Die zugrunde liegenden Testreihen durch die Regeln gebunden sind, für deren, wie z. B. mit externen wird konfiguriert Konfiguration nur Linux, jedoch die Verfügbarkeitsgruppe, der er angehört könnte mit einem WSFC konfiguriert werden. Betrachten Sie das folgende Beispiel:

![Hybrid Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Nächste Schritte
[Konfigurieren der verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

[Konfigurieren Sie Skalieren von Lesevorgängen verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-rs.md)

[Verfügbarkeitsgruppe-Clusterressource auf RHEL hinzufügen](sql-server-linux-availability-group-cluster-rhel.md)

[Verfügbarkeitsgruppe-Clusterressource auf SLES hinzufügen](sql-server-linux-availability-group-cluster-sles.md)

[Verfügbarkeitsgruppe-Clusterressource auf Ubuntu hinzufügen](sql-server-linux-availability-group-cluster-ubuntu.md)

[Konfigurieren Sie eine verfügbarkeitsgruppe über Plattformen hinweg](sql-server-linux-availability-group-cross-platform.md)

