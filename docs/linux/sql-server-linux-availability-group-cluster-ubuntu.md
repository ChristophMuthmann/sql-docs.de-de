---
title: "Ubuntu-Cluster für SQL Server-Verfügbarkeitsgruppe konfigurieren | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.workload: Inactive
ms.openlocfilehash: cc6eee565499d696c4f634d6eedc562547bc8253
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Ubuntu-Cluster und die Verfügbarkeitsgruppenressource konfigurieren

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Dieses Dokument erläutert, wie Sie einen Cluster mit drei Knoten auf Ubuntu erstellen, und fügen eine zuvor erstellte verfügbarkeitsgruppe als Ressource im Cluster. Für hohe Verfügbarkeit, eine verfügbarkeitsgruppe unter Linux erfordert drei Knoten?: Siehe [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> SQL Server Integration in Schrittmacher unter Linux ist an diesem Punkt nicht als gekoppelten als mit WSFC unter Windows. Aus SQL, besteht keine Kenntnisse über das Vorhandensein des Clusters, alle Orchestrierung befindet sich im außerhalb und der Dienst wird als eigenständige Instanz von Schrittmacher gesteuert. Außerdem virtuellen Netzwerknamen bezieht sich auf WSFC, es gibt keine Entsprechung in Schrittmacher identisch. Always On-dynamische Verwaltungssichten, die Clusterinformationen Abfragen gibt leere Zeilen zurück. Sie können einen Listener für die Verwendung für transparente wiederverbindung nach einem Failover weiterhin erstellen, jedoch müssen Sie manuell den verfügbarkeitsgruppenlistener-Namen in der DNS-Server für die IP-Adresse verwendet, um die virtuelle IP-Adressressource erstellen (wie nachstehend beschrieben) registrieren.

In den folgenden Abschnitten exemplarisch die Schritte zum Einrichten einer Lösung mit Failovercluster. 

## <a name="roadmap"></a>Roadmap für die

Die Schritte zum Erstellen einer verfügbarkeitsgruppe auf Linux-Servern zwecks hoher Verfügbarkeit unterscheiden sich von den Schritten in einem Windows Server-Failovercluster. Die folgende Liste beschreibt auf hoher Ebene die Schritte aus: 

1. [Konfigurieren von SQL Server auf den Clusterknoten](sql-server-linux-setup.md).

2. [Erstellen der verfügbarkeitsgruppe](sql-server-linux-availability-group-configure-ha.md). 

3. Konfigurieren eines Cluster-Ressourcen-Managers wie Schrittmacher an. Diese Anweisungen sind in diesem Dokument.
   
   Die Möglichkeit zum Konfigurieren eines Cluster-Ressourcen-Managers, hängt von der bestimmten Linux-Distribution ab. 

   >[!IMPORTANT]
   >Produktionsumgebungen sind einen Fencing-Agent, wie STONITH für hohe Verfügbarkeit erforderlich. Die Demos in dieser Dokumentation verwenden Zäune-Agents. Die Demos sind für das Testen und nur die Überprüfung. 
   
   >Ein Linux-Cluster verwendet Fencing, um den Cluster in einen bekannten Zustand zurückzugeben. Die Methode zum Konfigurieren von Fencing hängt davon ab, die Verteilung und der Umgebung. Zu diesem Zeitpunkt ist die Fencing nicht in einige Cloud-Umgebungen verfügbar. Finden Sie unter [Richtlinien zur Unterstützung für RHEL hohe Verfügbarkeit Cluster - Virtualisierungsplattformen](https://access.redhat.com/articles/29440) für Weitere Informationen.

5.  [Fügen Sie die verfügbarkeitsgruppe als Ressource im Cluster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher

1. Öffnen Sie auf allen Knoten der Firewallports. Öffnen Sie den Port für den Schrittmacher Hochverfügbarkeits-Dienst, SQL Server-Instanz und den Endpunkt der verfügbarkeitsgruppe. Der TCP-Standardport für SQL Server ausgeführt wird, ist 1433.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   Alternativ können Sie nur die Firewall deaktivieren:
        
   ```bash
   sudo ufw disable
   ```

1. Installieren Sie Schrittmacher Pakete. Führen Sie auf allen Knoten die folgenden Befehle ein:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie auf allen Knoten dasselbe Kennwort. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Aktivieren Sie und starten Sie Pcsd-Dienst und Schrittmacher

Der folgende Befehl aktiviert und startet Pcsd Service und Schrittmacher. Auf allen Knoten ausführen. Dadurch werden die Knoten des Clusters nach dem Neustart erneut beitreten. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Enable Schrittmacher Befehl wird mit Fehler abgeschlossen "Schrittmacher Standard Boot-enthält keine Ausführungsstufe, wird abgebrochen." Dies harmlos ist, kann die Clusterkonfiguration weiter. Wir sind mit Lieferanten der Cluster die folgenden sich zum Beheben dieses Problems.

## <a name="create-the-cluster"></a>Erstellen des Clusters

1. Entfernen Sie alle vorhandenen Clusterkonfiguration von allen Knoten. 

   Ausgeführten "" sudo "apt-Get Install-Pcs" Schrittmacher, Corosync und Pcs zur selben Zeit installiert und alle 3 der Dienste ausgeführt wird.  Corosync starten eine Vorlage generiert "/ etc/cluster/corosync.conf" Datei.  Nächste Schritte erfolgreich ausgeführt werden, kann diese Datei haben sollten nicht vorhanden – die problemumgehung besteht darin Schrittmacher beenden / Corosync und löschen "/ etc/cluster/corosync.conf", und klicken Sie dann der nächste Schritte erfolgreich abgeschlossen werden. "Entfernen von Pcs Clusters" bewirkt dasselbe, und können Sie sie als Zeitschritt anfängliche Cluster-Setup.
   
   Der folgende Befehl entfernt alle vorhandenen Cluster-Konfigurationsdateien und beendet alle Clusterdienste. Dies zerstört dauerhaft Cluster. Führen Sie sie als ersten Schritt in einer vorproduktionsumgebung aus. Hinweis Schrittmacher-Dienst und muss erneut aktiviert werden, dass "Pcs Cluster zerstört" deaktiviert. Führen Sie den folgenden Befehl auf allen Knoten aus.
   
   >[!WARNING]
   >Der Befehl werden alle vorhandenen Clusterressourcen gelöscht.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Erstellen des Clusters an. 

   >[!WARNING]
   >Aufgrund eines bekannten Problems, die Hersteller des clustering untersuchen, beginnend schlägt der Cluster ("Pcs Cluster Start") mit folgenden Fehler fehl. Dies ist, da die Protokolldatei im /etc/corosync/corosync.conf konfigurierten falsch ist. Zur Umgehung dieses Problems die Protokolldatei zu ändern: /var/log/corosync/corosync.log. Alternativ können Sie die /var/log/cluster/corosync.log-Datei erstellen.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
Der folgende Befehl erstellt einen Cluster mit drei Knoten. Bevor Sie das Skript ausführen, ersetzen Sie die Werte zwischen `**< ... >**`. Führen Sie den folgenden Befehl auf dem primären Knoten. 

   ```bash
   sudo pcs cluster auth **<node1>** **<node2>** **<node3>** -u hacluster -p **<password for hacluster>**
   sudo pcs cluster setup --name **<clusterName>** **<node1>** **<node2…>** **<node3>**
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Wenn Sie vorher einen Cluster auf denselben Knoten konfiguriert haben, müssen Sie die Option „--force“ verwenden, wenn Sie „pcs cluster setup“ ausführen. Beachten Sie, dass dies der Ausführung von „pcs cluster destroy“ entspricht, und der Peacemaker-Dienst muss erneut mithilfe von „sudo systemctl enable pacemaker“ aktiviert werden.


## <a name="configure-fencing-stonith"></a>Konfigurieren von Fencing (STONITH)

Schrittmacher Cluster Lieferanten erfordern STONITH aktiviert werden und ein Fencing Gerät für ein unterstütztes Clustersetup konfiguriert. Wenn der Cluster-Ressourcen-Manager den Status eines Knotens oder einer Ressource auf einem Knoten nicht ermitteln kann, wird Fencing verwendet, auf den Cluster erneut in einen bekannten Zustand zu versetzen. Ressource Ebene Zäune hauptsächlich wird sichergestellt, dass es keine beschädigte Daten bei einem Ausfall durch Konfigurieren einer Ressource. Können Sie Ressourcen Ebene Zäune, z. B. mit DRBD (Distributed repliziert Blockgerät), um den Datenträger auf einem Knoten, wie wenn veraltet zu markieren der kommunikationsverbindung ausfällt. Knoten Ebene Zäune wird sichergestellt, dass alle Ressourcen von ein Knoten nicht ausgeführt werden kann. Dies erfolgt durch das Zurücksetzen des Knotens, und die Implementierung Schrittmacher davon STONITH (Dies steht für "den andere Knoten im Kopf Schießen") aufgerufen. Schrittmacher unterstützt eine große Anzahl von Fencing Geräte, z. B. eine unterbrechungsfreie Stromversorgung oder Management Netzwerkschnittstellenkarten für Server. Weitere Informationen finden Sie unter [Schrittmacher Clustern von Grund auf Neu](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) und [Fencing und Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

Da Knotenebene Zauns Konfiguration stark von der Umgebung abhängig ist, wird sie für dieses Lernprogramm deaktivieren wir (es kann zu einem späteren Zeitpunkt konfiguriert). Führen Sie das folgende Skript auf dem primären Knoten aus: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Deaktivieren von STONITH ist nur für Testzwecke verwenden. Wenn Sie Schrittmacher in einer produktiven Umgebung verwenden möchten, sollten Sie eine Implementierung STONITH je nach Umgebung planen und bewahren Sie ihn der aktiviert. Beachten Sie, dass an diesem Punkt gibt es keine Fencing-Agents für alle Cloud-Umgebungen (einschließlich Azure) oder Hyper-V. Die Cluster-Hersteller bietet Unterstützung für die Ausführung von produktionsclustern in diesen Umgebungen, nicht. Wir arbeiten an einer Lösung für diese Lücke, die in zukünftigen Versionen verfügbar sein wird.

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Festlegen Sie Clustereigenschaft auf "false" Start-Fehler-ist--Schwerwiegender

`start-failure-is-fatal`Gibt an, ob ein Fehler beim Starten einer Ressource auf einem Knoten weiter Start Versuche auf diesem Knoten verhindert. Bei Festlegung auf `false`, der Cluster wird entscheiden Sie, ob auf demselben Knoten erneut basierend auf der Ressource aktuelle Anzahl und Migration Fehlerschwellenwert starten. Daher nach dem Failover unternimmt Schrittmacher starten die verfügbarkeitsgruppenressource auf dem ehemaligen primären SQL-Instanz verfügbar ist. Schrittmacher wird das Replikat zum sekundären Tieferstufen, und es wird automatisch die verfügbarkeitsgruppe erneut. 

Aktualisieren Sie den Eigenschaftswert an `false` führen Sie das folgende Skript aus:

```bash
sudo pcs property set start-failure-is-fatal=false
```


>[!WARNING]
>Nach der ein automatisches Failover bei `start-failure-is-fatal = true` der Ressourcen-Manager versucht, die Ressource zu starten. Wenn sie beim ersten Versuch fehlschlägt, müssen Sie manuell ausführen, `pcs resource cleanup <resourceName>` Cleanup der Anzahl der Ressourcen-Fehler und Zurücksetzen der Konfiguration.

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Installieren von SQL Server-Agent-Ressource für die Integration mit Schrittmacher

Führen Sie die folgenden Befehle auf allen Knoten aus. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Erstellen Sie eine SQL Server-Anmeldung für Schrittmacher

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Erstellen Sie die Verfügbarkeit der Ressource "Group"

Verwenden Sie zum Erstellen der verfügbarkeitsgruppenressource `pcs resource create` Befehl, und legen Sie die Ressourceneigenschaften. Im folgenden Befehl erstellt eine `ocf:mssql:ag` Master/Slave Typ der Ressource für die verfügbarkeitsgruppe mit dem Namen `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Erstellen der virtuellen IP-Adressressource

Führen Sie den folgenden Befehl auf einem Knoten, um die virtuelle IP-Adressressource zu erstellen. Verwenden Sie eine verfügbare statische IP-Adresse aus dem Netzwerk. Bevor Sie das Skript ausführen, ersetzen Sie die Werte zwischen `**< ... >**` mit einer gültigen IP-Adresse.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

Es ist keine virtuellen Servernamen Schrittmacher äquivalent. Verwenden eine Verbindungszeichenfolge, die auf einen Servernamen Zeichenfolge verweist und nicht die IP-Adresse, die Adresse der IP-Ressource und die gewünschten virtuellen Servernamen in DNS registrieren. Registrieren Sie für die DR-Konfigurationen den gewünschten virtuellen Servernamen und die IP-Adresse mit DNS-Server sowohl primäre als auch DR-Standort.

## <a name="add-colocation-constraint"></a>Zusammenstellung-Einschränkung hinzufügen

Fast jeder Entscheidung in einem Cluster Schrittmacher ähnelt dem auswählen, in dem eine Ressource ausgeführt werden soll, erfolgt durch Vergleichen der Ergebnisse. Ergebnisse pro Ressource berechnet werden und der Clusterressourcen-Manager wählt die Knoten mit der höchsten Bewertung für eine bestimmte Ressource. (Wenn ein Knoten ein negatives Ergebnis für eine Ressource besitzt, kann nicht die Ressource auf diesem Knoten ausgeführt.) Wir können die Entscheidungen, die den Cluster mit Einschränkungen bearbeiten. Eine Bewertung eine Beschränkung vorliegt. Wenn eine Einschränkung, ein Ergebnis kleiner als UNENDLICH ist, ist es nur eine Empfehlung. Eine Bewertung von UNENDLICH bedeutet, dass es ein muss. Wir möchten sicherstellen, dass primäre der verfügbarkeitsgruppe und die virtuelle IP-Ressource werden ausgeführt auf demselben Host, sodass definieren wir eine Zusammenstellung-Einschränkung mit einem Faktor von UNENDLICH. Führen Sie den folgenden Befehl zum Hinzufügen der Einschränkung durch die Zusammenstellung auf einem Knoten. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Sortierung-Einschränkung hinzufügen

Die Zusammenstellung-Einschränkung verfügt über eine implizite Reihenfolge Einschränkung. Er verschiebt die virtuelle IP-Adressressource, bevor sie die verfügbarkeitsgruppenressource verschoben wird. Standardmäßig lautet die Abfolge von Ereignissen.

1. Benutzerprobleme `pcs resource move` auf dem primären verfügbarkeitsgruppenobjekt von Knoten1 auf Knoten2.
1. Die virtuelle IP-Adressressource reagiert auf Node1 her.
1. Die virtuelle IP-Adressressource beginnt auf Node2 her.

   >[!NOTE]
   >An diesem Punkt die IP-Adresse vorübergehend verweist auf node2 während node2 noch ein Pre-Failover ist sekundären. 
   
1. Die verfügbarkeitsgruppe auf node1 primären zum sekundären Replikat tiefer gestuft wird.
1. Auf node2 sekundäre verfügbarkeitsgruppe wird zum primären höher gestuft. 

Um zu verhindern, dass die IP-Adresse vorübergehend auf den Knoten mit der vor dem Failover sekundären Datenbank verweist, fügen Sie eine Sortierung Einschränkung hinzu. 

Um eine Sortierung Einschränkung hinzuzufügen, führen Sie den folgenden Befehl auf einem Knoten aus:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Nachdem Sie den Cluster konfigurieren und als Clusterressource der verfügbarkeitsgruppe hinzufügen, können nicht Sie Transact-SQL verwenden, um die verfügbarkeitsgruppenressourcen Failover. SQL Server-Cluster-Ressourcen unter Linux werden mit dem Betriebssystem nicht als eng verbunden, da es sich auf einem Windows Server Failover Cluster (WSFC) handelt. SQL Server-Dienst ist nicht über das Vorhandensein des Clusters. Alle Orchestrierung erfolgt über die Verwaltungstools. Verwenden Sie in RHEL oder Ubuntu `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Nächste Schritte

[Betreiben HA-verfügbarkeitsgruppe](sql-server-linux-availability-group-failover-ha.md)

