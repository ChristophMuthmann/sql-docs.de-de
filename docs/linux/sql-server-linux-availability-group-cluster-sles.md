---
title: "SLES Cluster für SQL Server-Verfügbarkeitsgruppe konfigurieren | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 05/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 50a2633790b9878a8be2a9a3c417fc877a37633d
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>SLES Cluster für SQL Server-Verfügbarkeitsgruppe zu konfigurieren.

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Dieses Handbuch enthält Anweisungen, um einen Cluster mit drei Knoten für SQL Server auf SUSE Linux Enterprise Server 12 SP2 (SLES) zu erstellen. Für hohe Verfügbarkeit, eine verfügbarkeitsgruppe unter Linux erfordert drei Knoten?: Siehe [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md). Die clustering-Ebene basiert auf SUSE [hohe Verfügbarkeit Erweiterung (HAE)](https://www.suse.com/products/highavailability) baut auf [Schrittmacher](http://clusterlabs.org/). 

Weitere Informationen zur Clusterkonfiguration, Ressourcenoptionen-Agent, Management, best Practices und Empfehlungen, finden Sie unter [SUSE Linux Enterprise hohe Verfügbarkeit Erweiterung 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>SQL Server Integration in Schrittmacher unter Linux ist an diesem Punkt nicht als gekoppelten als mit WSFC unter Windows. SQL Server-Dienst unter Linux ist nicht clusterfähig. Schrittmacher steuert alle Clusterressourcen, die verfügbarkeitsgruppenressource einschließlich Orchestrierung. Unter Linux sollten Sie nicht immer auf Verfügbarkeit Gruppe dynamische Verwaltungssichten (DMVs) abhängig, die Clusterinformationen z. B. sys. dm_hadr_cluster bereitstellen. Außerdem virtuellen Netzwerknamen bezieht sich auf WSFC, es gibt keine Entsprechung in Schrittmacher identisch. Sie können einen Listener für die Verwendung für transparente wiederverbindung nach einem Failover weiterhin erstellen, jedoch müssen Sie manuell den verfügbarkeitsgruppenlistener-Namen in der DNS-Server für die IP-Adresse verwendet, um die virtuelle IP-Adressressource erstellen (wie nachstehend beschrieben) registrieren.


## <a name="roadmap"></a>Roadmap für die

Die Schritte zum Erstellen einer verfügbarkeitsgruppe auf Linux-Servern zwecks hoher Verfügbarkeit unterscheiden sich von den Schritten in einem Windows Server-Failovercluster. Die folgende Liste beschreibt auf hoher Ebene die Schritte aus: 

1. [Konfigurieren von SQL Server auf den Clusterknoten](sql-server-linux-setup.md).

2. [Erstellen der verfügbarkeitsgruppe](sql-server-linux-availability-group-failover-ha.md). 

3. Konfigurieren eines Cluster-Ressourcen-Managers wie Schrittmacher an. Diese Anweisungen sind in diesem Dokument.
   
   Die Möglichkeit zum Konfigurieren eines Cluster-Ressourcen-Managers, hängt von der bestimmten Linux-Distribution ab. 

   >[!IMPORTANT]
   >Produktionsumgebungen sind einen Fencing-Agent, wie STONITH für hohe Verfügbarkeit erforderlich. Die Demos in dieser Dokumentation verwenden Zäune-Agents. Die Demos sind für das Testen und nur die Überprüfung. 
   
   >Ein Cluster Schrittmacher werden mit Fencing Cluster in einen bekannten Zustand zurückgegeben. Die Methode zum Konfigurieren von Fencing hängt davon ab, die Verteilung und der Umgebung. Zu diesem Zeitpunkt ist die Fencing nicht in einige Cloud-Umgebungen verfügbar. Finden Sie unter [SUSE Linux Enterprise hohe Verfügbarkeit Erweiterung](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Fügen Sie die verfügbarkeitsgruppe als Ressource im Cluster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Erforderliche Komponenten

Zum Abschließen der End-to-End-Szenarios unten benötigen Sie drei Computer zum Bereitstellen des Clusters drei Knoten. Die folgenden Schritte zeigen diese Server zu konfigurieren.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Richten Sie ein und konfigurieren Sie des Betriebssystems auf allen Clusterknoten 

Der erste Schritt ist so konfigurieren Sie das Betriebssystem auf den Clusterknoten. Verwenden Sie für diese Gang durch SLES 12 SP2 mit einem gültigen Abonnement für das Add-on für hohe Verfügbarkeit.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Installieren und Konfigurieren von SQL Server-Dienst auf jedem Clusterknoten

1. Installieren und Einrichten von SQL Server-Dienst auf allen Knoten. Ausführliche Anweisungen finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).

1. Legen Sie einen Knoten als primären und anderen Knoten als sekundäre Replikate. Verwenden Sie diese Begriffe in diesem Leitfaden.

1. Stellen Sie sicher, dass der Knoten, die Teil des Clusters sein werden, die miteinander kommunizieren können.

   Das folgende Beispiel zeigt `/etc/hosts` mit Ergänzungen für drei Knoten mit dem Namen SLES1, SLES2 und SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Alle Clusterknoten müssen über SSH, aufeinander zugreifen können. Tools wie `hb_report` oder `crm_report` (zwecks Problembehandlung) und Hawk Verlauf Explorer passwordless SSH-Zugriff zwischen Knoten erfordern, andernfalls können sie nur Daten sammeln, aus dem aktuellen Knoten. Für den Fall, dass Sie einen nicht standardmäßigen SSH-Port verwenden, verwenden Sie die Option-X (siehe `man` Seite "). Angenommen, Ihre SSH-Port 3479 ist, rufen Sie eine `crm_report` mit:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Weitere Informationen finden Sie unter der [SLES Administratorhandbuch - sonstige Abschnitt](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Erstellen Sie eine SQL Server-Anmeldung für Schrittmacher

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Konfigurieren einer Always On-Verfügbarkeitsgruppe

Konfigurieren der verfügbarkeitsgruppe, und konfigurieren Sie die Clusterressourcen, auf Linux-Servern. Um die verfügbarkeitsgruppe zu konfigurieren, finden Sie unter [Konfigurieren von Always On-Verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher

1. Installieren Sie die Erweiterung für hohe Verfügbarkeit

   Weitere Informationen finden Sie [Installieren von SUSE Linux Enterprise Server und die hohe Verfügbarkeit-Erweiterung](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Installieren Sie SQL Server-Agent ressourcenpaket auf beiden Knoten.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Richten Sie den ersten Knoten

   Verweisen auf [SLES installationsanweisungen](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Melden Sie sich als `root` auf dem physischen oder virtuellen Computer, die Sie als Clusterknoten verwenden möchten.
2. Starten Sie das bootstrap-Skript, durch das ausführen:
   ```bash
   sudo ha-cluster-init
   ```

   Wenn NTP nicht beim Systemstart starten konfiguriert wurde, wird eine Meldung angezeigt. 

   Wenn Sie trotzdem fortfahren möchten, das Skript automatisch generieren von Schlüsseln für den SSH-Zugriff und die für das verzeichnissynchronisierungstool Csync2 und starten Sie die Dienste für beide benötigt. 

3. So konfigurieren Sie die clusterkommunikationsebene (Corosync): 

   A. Geben Sie eine Netzwerkadresse zum Binden an. Standardmäßig wird das Skript die Netzwerkadresse des eth0 vorzuschlagen. Alternativ geben Sie eine andere Netzwerkadresse, z. B. die Adresse des bond0 ein. 

   B. Geben Sie eine Multicastadresse. Das Skript schlägt eine zufällige Adresse, die als Standard verwendet werden können. 

   c. Geben Sie einen multicast-Port. Das Skript schlägt 5405 als Standard. 

   d. So konfigurieren Sie `SBD ()`, eingeben ein persistenten Pfads für die Partition des Geräts blockieren, die Sie für SBD verwenden möchten. Der Pfad muss in allen Knoten im Cluster konsistent sein. 
   Schließlich wird das Skript starten Sie den Dienst Schrittmacher zum Onlineschalten des Clusters einem Knoten und zum Aktivieren der Webverwaltungsoberfläche Hawk2. Die URL für Hawk2 wird auf dem Bildschirm angezeigt. 

4. Überprüfen Sie alle Details des Setupvorgangs `/var/log/sleha-bootstrap.log`. Sie verfügen jetzt über einen laufenden Einzelknotencluster. Überprüfen Sie das Cluster den Status mit dem Crm-Status:

   ```bash
   sudo crm status
   ```

   Sie sehen auch Clusterkonfiguration mit `crm configure show xml` oder `crm configure show`.

5. Das bootstrapverfahren erstellt einen Linux-Benutzer mit dem Namen Hacluster mit dem Kennwort Linux. Ersetzen Sie das Standardkennwort durch eine sichere so bald wie möglich: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Hinzufügen von Knoten zum vorhandenen cluster

Wenn Sie einen Cluster mit einem oder mehreren Knoten ausgeführt haben, fügen Sie weitere Clusterknoten mit dem bootstrap-ha-Cluster-Join-Skript hinzu. Das Skript wird nur benötigt Zugriff auf einen vorhandenen Clusterknoten und der grundlegenden Setup auf dem aktuellen Computer wird automatisch abgeschlossen. Führen Sie die folgenden Schritte aus:

Wenn Sie die vorhandenen Clusterknoten mit konfiguriert haben die `YaST` cluster-Modul, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind, vor dem Ausführen `ha-cluster-join`:
- Der Root-Benutzer auf den vorhandenen Knoten hat SSH-Schlüssel für passwordless Anmeldung eingerichtet. 
- `Csync2`wird auf den vorhandenen Knoten konfiguriert. Weitere Informationen finden Sie in konfigurieren Csync2 mit YaST. 

1. Melden Sie sich als Root auf dem physischen oder virtuellen Computer, die dem Cluster beitreten soll. 
2. Starten Sie das bootstrap-Skript, durch das ausführen: 

   ```bash
   sudo ha-cluster-join
   ```

   Wenn NTP nicht beim Systemstart starten konfiguriert wurde, wird eine Meldung angezeigt. 

3. Wenn Sie trotzdem fortfahren möchten, werden Sie aufgefordert, die IP-Adresse von einem vorhandenen Knoten anzugeben. Geben Sie die IP-Adresse ein. 

4. Wenn Sie eine passwordless SSH-Zugriffs zwischen den beiden Computern nicht bereits konfiguriert haben, werden Sie auch für das Stammkennwort für den vorhandenen Knoten aufgefordert. 

   Das Skript wird nach der Anmeldung mit dem angegebenen Knoten kopieren Sie die Konfiguration Corosync, konfigurieren Sie SSH und `Csync2`, und den aktuellen Computer online als neuen Clusterknoten wird angezeigt. Abgesehen von, dass wird für Hawk erforderliche gestartet. Wenn Sie mit freigegebenen Speicher konfiguriert haben `OCFS2`, erstellt jedoch auch automatisch das Bereitstellungspunkt-Verzeichnis für die `OCFS2` Dateisystem. 

5. Wiederholen Sie die oben genannten Schritte für alle Computer, die Sie dem Cluster hinzufügen möchten. 

6. Überprüfen Sie die Details des Prozesses `/var/log/ha-cluster-bootstrap.log`. 

1. Überprüfen Sie den Clusterstatus `sudo crm status`. Wenn Sie einen zweiten Knoten erfolgreich hinzugefügt haben, sieht die Ausgabe ähnlich der folgenden aus:

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr`ist die virtuelle IP-Clusterressource, die während des Setups der anfänglichen Einzelknotencluster konfiguriert ist.

Überprüfen Sie nachdem alle Knoten hinzugefügt wurde, ob Sie keine-Quorum-Richtlinie in der globalen Clusteroptionen anpassen müssen. Dies ist besonders wichtig für Cluster mit zwei Knoten. Weitere Informationen finden Sie im Abschnitt 4.1.2 Option ohne-Quorum-Richtlinie. 

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Festlegen Sie Clustereigenschaft auf "false" Start-Fehler-ist--Schwerwiegender

`Start-failure-is-fatal`Gibt an, ob ein Fehler beim Starten einer Ressource auf einem Knoten weiter Start Versuche auf diesem Knoten verhindert. Bei Festlegung auf `false`, der Cluster wird entscheiden Sie, ob auf demselben Knoten erneut basierend auf der Ressource aktuelle Anzahl und Migration Fehlerschwellenwert starten. Daher nach dem Failover unternimmt Schrittmacher starten die verfügbarkeitsgruppenressource auf dem ehemaligen primären SQL-Instanz verfügbar ist. Schrittmacher übernimmt die Herabstufung des sekundäre Replikats, und es wird automatisch die verfügbarkeitsgruppe erneut. Auch wenn `start-failure-is-fatal` festgelegt ist, um `false`, des Clusters wird ein Fallback auf die konfigurierten Failcount Grenzwerte, die mit der Migration Schwellenwert konfiguriert werden, daher müssen Sie Sie sicher, dass der standardanwendung für die Migration Schwellenwert entsprechend aktualisiert wird.

So aktualisieren Sie den Wert der Eigenschaft auf "false" ausführen:
```bash
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
Wenn die Eigenschaft den Standardwert hat `true`, wenn beim ersten Versuch zum Starten der Ressource nicht erfolgreich war, ein Eingreifen des Benutzers erforderlich, nach der ein automatisches Failover an den Bereinigungstasks, die Anzahl der Ressourcen-Fehler ist und der Konfiguration verwendet zurücksetzen: `sudo crm resource cleanup <resourceName>` Befehl.

Weitere Informationen zur Schrittmacher Clustereigenschaften finden Sie [Clusterressourcen konfigurieren](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

# <a name="configure-fencing-stonith"></a>Konfigurieren von Fencing (STONITH)
Schrittmacher Cluster Lieferanten erfordern STONITH aktiviert werden und ein Fencing Gerät für ein unterstütztes Clustersetup konfiguriert. Wenn der Cluster-Ressourcen-Manager den Status eines Knotens oder einer Ressource auf einem Knoten nicht ermitteln kann, wird Fencing verwendet, auf den Cluster erneut in einen bekannten Zustand zu versetzen.
Ressource Ebene Zäune hauptsächlich wird sichergestellt, dass es keine beschädigte Daten bei einem Ausfall durch Konfigurieren einer Ressource. Können Sie Ressourcen Ebene Zäune, z. B. mit DRBD (Distributed repliziert Blockgerät), um den Datenträger auf einem Knoten, wie wenn veraltet zu markieren der kommunikationsverbindung ausfällt.
Knoten Ebene Zäune wird sichergestellt, dass alle Ressourcen von ein Knoten nicht ausgeführt werden kann. Dies erfolgt durch das Zurücksetzen des Knotens, und die Implementierung Schrittmacher davon STONITH (Dies steht für "den andere Knoten im Kopf Schießen") aufgerufen. Schrittmacher unterstützt eine große Anzahl von Fencing Geräte, z. B. eine unterbrechungsfreie Stromversorgung oder Management Netzwerkschnittstellenkarten für Server.
Weitere Informationen finden Sie unter [Schrittmacher Clustern von Grund auf Neu](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html), [Fencing und Stonith](http://clusterlabs.org/doc/crm_fencing.html) und [SUSE-HA-Dokumentation: Fencing und STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html).

Während der Initialisierung des Clusters ist die STONITH deaktiviert, wenn keine Konfiguration erkannt wird. Sie kann später durch Ausführen nachfolgenden Befehl aktiviert werden

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>Deaktivieren von STONITH ist nur für Testzwecke verwenden. Wenn Sie Schrittmacher in einer produktiven Umgebung verwenden möchten, sollten Sie eine Implementierung STONITH je nach Umgebung planen und bewahren Sie ihn der aktiviert. Beachten Sie, dass SUSE keine Fencing-Agents für alle Cloud-Umgebungen (einschließlich Azure) oder Hyper-V bietet. Die Cluster-Hersteller bietet Unterstützung für die Ausführung von produktionsclustern in diesen Umgebungen, nicht. Wir arbeiten an einer Lösung für diese Lücke, die in zukünftigen Versionen verfügbar sein wird.


## <a name="configure-the-cluster-resources-for-sql-server"></a>Konfigurieren Sie die Clusterressourcen für SQL Server

Verweisen auf [SLES Verwaltung Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

### <a name="create-availability-group-resource"></a>Erstellen Sie die Verfügbarkeit der Ressource "Group"

Der folgende Befehl erstellt und konfiguriert die verfügbarkeitsgruppenressource für 3 Replikate der verfügbarkeitsgruppe [ag1]. Das Überwachen von Vorgängen und Timeouts in SLES explizit angegeben werden, beruht auf der Tatsache, dass Timeouts äußerst arbeitsauslastung abhängig sind und müssen für jede Bereitstellung sorgfältig angepasst werden müssen.
Führen Sie den Befehl auf einem der Knoten im Cluster:

1. Führen Sie `crm configure` auf die Crm-Eingabeaufforderung öffnen:

   ```bash
   sudo crm configure 
   ```

1. Führen Sie den folgenden Befehl ein, so konfigurieren Sie die Ressourceneigenschaften in der Eingabeaufforderung Crm.

   ```bash
primitive ag_cluster \
   ocf:mssql:ag \
   params ag_name="ag1" \
   op start timeout=60s \
   op stop timeout=60s \
   op promote timeout=60s \
   op demote timeout=10s \
   op monitor timeout=60s interval=10s \
   op monitor timeout=60s interval=11s role="Master" \
   op monitor timeout=60s interval=12s role="Slave" \
   op notify timeout=60s
ms ms-ag_cluster ag_cluster \
   meta master-max="1" master-node-max="1" clone-max="3" \
  clone-node-max="1" notify="true" \
commit
   ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>Erstellen der virtuellen IP-Adressressource

Wenn Sie nicht die virtuelle IP-Adressressource erstellt haben, bei der Ausführung `ha-cluster-init` diese Ressource kann nun erstellt. Der folgende Befehl erstellt eine virtuelle IP-Adressressource. Ersetzen Sie `<**0.0.0.0**>` mit einer verfügbaren Adresse aus dem Netzwerk und `<**24**>` mit der Anzahl von Bits in der CIDR-Subnetzmaske. Führen Sie auf einem Knoten.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Zusammenstellung-Einschränkung hinzufügen
Fast jeder Entscheidung in einem Cluster Schrittmacher ähnelt dem auswählen, in dem eine Ressource ausgeführt werden soll, erfolgt durch Vergleichen der Ergebnisse. Ergebnisse pro Ressource berechnet werden und der Clusterressourcen-Manager wählt die Knoten mit der höchsten Bewertung für eine bestimmte Ressource. (Wenn ein Knoten ein negatives Ergebnis für eine Ressource besitzt, kann nicht die Ressource auf diesem Knoten ausgeführt.) Wir können die Entscheidungen, die den Cluster mit Einschränkungen bearbeiten. Eine Bewertung eine Beschränkung vorliegt. Wenn eine Einschränkung, ein Ergebnis kleiner als UNENDLICH ist, ist es nur eine Empfehlung. Eine Bewertung von UNENDLICH bedeutet, dass es ein muss. Wir möchten sicherstellen, dass primäre der verfügbarkeitsgruppe und die virtuelle IP-Ressource werden ausgeführt auf demselben Host, sodass definieren wir eine Zusammenstellung-Einschränkung mit einem Faktor von UNENDLICH. 

Um Zusammenstellung-Einschränkung für die virtuelle IP-Adresse zur Ausführung auf demselben Knoten wie Master festzulegen, führen Sie den folgenden Befehl auf einem Knoten aus:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Sortierung-Einschränkung hinzufügen
Die Zusammenstellung-Einschränkung verfügt über eine implizite Reihenfolge Einschränkung. Er verschiebt die virtuelle IP-Adressressource, bevor sie die verfügbarkeitsgruppenressource verschoben wird. Standardmäßig lautet die Abfolge von Ereignissen. 

1. Probleme-Ressource "User", mit dem Availability Group-Master von Knoten1 auf Knoten2 migrieren.
2. Die virtuelle IP-Adressressource wird auf Knoten 1 beendet.
3. Die virtuelle IP-Adressressource, die auf Knoten 2 wird gestartet. An diesem Punkt die IP-Adresse vorübergehend verweist auf Knoten 2 während Knoten 2 noch ein Pre-Failover ist sekundären. 
4. Der Verfügbarkeit Master auf Knoten 1 wird herabgestuft, um slave.
5. Die Verfügbarkeit Gruppe Slave auf Knoten 2 höher gestuft wird Master. 

Um zu verhindern, dass die IP-Adresse vorübergehend auf den Knoten mit der vor dem Failover sekundären Datenbank verweist, fügen Sie eine Sortierung Einschränkung hinzu. Um eine Sortierung Einschränkung hinzuzufügen, führen Sie den folgenden Befehl auf einem Knoten aus: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Nachdem Sie den Cluster konfigurieren und als Clusterressource der verfügbarkeitsgruppe hinzufügen, können nicht Sie Transact-SQL verwenden, um die verfügbarkeitsgruppenressourcen Failover. SQL Server-Cluster-Ressourcen unter Linux werden mit dem Betriebssystem nicht als eng verbunden, da es sich auf einem Windows Server Failover Cluster (WSFC) handelt. SQL Server-Dienst ist nicht über das Vorhandensein des Clusters. Alle Orchestrierung erfolgt über die Verwaltungstools. Verwenden Sie SLES `crm`. 

Ausführen des manuellen Failovers der verfügbarkeitsgruppe mit `crm`. Failover mit Transact-SQL nicht initialisiert werden. Anweisungen hierzu finden Sie unter [Failover](sql-server-linux-availability-group-failover-ha.md#failover).


Weitere Informationen finden Sie unter:
- [Verwalten von Clusterressourcen](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [Virtuelle Maschinen mit hoher Konzepte](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Kurzübersicht Schrittmacher](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Nächste Schritte

[Betreiben HA-verfügbarkeitsgruppe](sql-server-linux-availability-group-failover-ha.md)
