---
title: Ubuntu-Cluster für SQL Server-Verfügbarkeitsgruppe konfigurieren | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 37008fbf209bbdc8a610e5a21bbd599e9783c423
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Ubuntu-Cluster und die Verfügbarkeitsgruppenressource konfigurieren

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Dokument erläutert, wie Sie einen Cluster mit drei Knoten auf Ubuntu erstellen, und fügen eine zuvor erstellte verfügbarkeitsgruppe als Ressource im Cluster. Für hohe Verfügbarkeit, eine verfügbarkeitsgruppe unter Linux erfordert drei Knoten?: Siehe [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> SQL Server Integration in Schrittmacher unter Linux ist an diesem Punkt nicht als gekoppelten als mit WSFC unter Windows. Von SQL, besteht keine Kenntnisse über das Vorhandensein des Clusters, alle Orchestrierung befindet sich im außerhalb und der Dienst wird als eigenständige Instanz von Schrittmacher gesteuert. Außerdem virtuellen Netzwerknamen bezieht sich auf WSFC, es gibt keine Entsprechung in Schrittmacher identisch. Always On-dynamische Verwaltungssichten, die Clusterinformationen Abfragen werden leere Zeilen zurückgegeben. Sie können einen Listener für die Verwendung für transparente wiederverbindung nach einem Failover weiterhin erstellen, jedoch müssen Sie manuell den verfügbarkeitsgruppenlistener-Namen in der DNS-Server für die IP-Adresse verwendet, um die virtuelle IP-Adressressource erstellen (wie in den folgenden Abschnitten erläutert) registrieren.

In den folgenden Abschnitten exemplarisch die Schritte zum Einrichten einer Lösung mit Failovercluster. 

## <a name="roadmap"></a>Roadmap für die

Die Schritte zum Erstellen einer verfügbarkeitsgruppe auf Linux-Servern zwecks hoher Verfügbarkeit unterscheiden sich von den Schritten in einem Windows Server-Failovercluster. Die folgende Liste beschreibt die allgemeinen Schritte: 

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
>Enable Schrittmacher Befehl möglicherweise mit Fehler abgeschlossen "Schrittmacher Standard Boot-enthält keine Ausführungsstufe, wird abgebrochen." Dies harmlos ist, kann die Clusterkonfiguration weiter. 

## <a name="create-the-cluster"></a>Erstellen des Clusters

1. Entfernen Sie alle vorhandenen Clusterkonfiguration von allen Knoten. 

   Ausgeführten "" sudo "apt-Get Install-Pcs" Schrittmacher, Corosync und Pcs zur selben Zeit installiert und alle 3 der Dienste ausgeführt wird.  Corosync starten eine Vorlage generiert "/ etc/cluster/corosync.conf" Datei.  Nächste Schritte erfolgreich ausgeführt werden, kann diese Datei haben sollten nicht vorhanden – die problemumgehung besteht darin Schrittmacher beenden / Corosync und Löschen von "/ etc/cluster/corosync.conf", und klicken Sie dann weitere Schritte erfolgreich abgeschlossen. "Entfernen von Pcs Clusters" bewirkt dasselbe, und können Sie sie als Zeitschritt anfängliche Cluster-Setup.
   
   Der folgende Befehl entfernt alle vorhandenen Cluster-Konfigurationsdateien und beendet alle Clusterdienste. Dies zerstört dauerhaft Cluster. Führen Sie sie als ersten Schritt in einer vorproduktionsumgebung aus. Hinweis Schrittmacher-Dienst und muss erneut aktiviert werden, dass "Pcs Cluster zerstört" deaktiviert. Führen Sie den folgenden Befehl auf allen Knoten aus.
   
   >[!WARNING]
   >Der Befehl löscht alle vorhandenen Clusterressourcen.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Erstellen des Clusters an. 

   >[!WARNING]
   >Cluster ("Pcs Cluster Start") tritt aufgrund eines bekannten Problems, die Hersteller des clustering untersuchen, beginnend folgende Fehler. Dies ist die Protokolldatei in /etc/corosync/corosync.conf der wird erstellt, wenn die Cluster-Setup-Befehlsoption wird ausgeführt, ist falsch konfiguriert. Um dieses Problem zu umgehen, ändern Sie die Protokolldatei: /var/log/corosync/corosync.log. Alternativ können Sie die /var/log/cluster/corosync.log-Datei erstellen.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
Der folgende Befehl erstellt einen Cluster mit drei Knoten. Bevor Sie das Skript ausführen, ersetzen Sie die Werte zwischen `< ... >`. Führen Sie den folgenden Befehl auf dem primären Knoten. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2…> <node3>
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Wenn Sie vorher einen Cluster auf denselben Knoten konfiguriert haben, müssen Sie die Option „--force“ verwenden, wenn Sie „pcs cluster setup“ ausführen. Beachten Sie, dass dies der Ausführung von „pcs cluster destroy“ entspricht, und der Peacemaker-Dienst muss erneut mithilfe von „sudo systemctl enable pacemaker“ aktiviert werden.


## <a name="configure-fencing-stonith"></a>Konfigurieren von Fencing (STONITH)

Schrittmacher Cluster Lieferanten erfordern STONITH aktiviert werden und ein Fencing Gerät für ein unterstütztes Clustersetup konfiguriert. Wenn der Cluster-Ressourcen-Manager den Status eines Knotens oder einer Ressource auf einem Knoten nicht ermitteln kann, wird Fencing verwendet, auf den Cluster erneut in einen bekannten Zustand zu versetzen. Ressource Ebene Zäune hauptsächlich wird sichergestellt, dass es keine beschädigte Daten bei einem Ausfall durch Konfigurieren einer Ressource. Können Sie Ressourcen Ebene Zäune, z. B. mit DRBD (Distributed repliziert Blockgerät), um den Datenträger auf einem Knoten, wie wenn veraltet zu markieren der kommunikationsverbindung ausfällt. Knoten Ebene Zäune wird sichergestellt, dass alle Ressourcen von ein Knoten nicht ausgeführt werden kann. Dies erfolgt durch das Zurücksetzen des Knotens, und die Implementierung Schrittmacher davon STONITH (Dies steht für "den andere Knoten im Kopf Schießen") aufgerufen. Schrittmacher unterstützt eine große Anzahl von Fencing Geräte, z. B. eine unterbrechungsfreie Stromversorgung oder Management Netzwerkschnittstellenkarten für Server. Weitere Informationen finden Sie unter [Schrittmacher Clustern von Grund auf Neu](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) und [Fencing und Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

Da Knotenebene Zauns Konfiguration stark von der Umgebung abhängig ist, deaktivieren wir für dieses Lernprogramm (es kann zu einem späteren Zeitpunkt konfiguriert). Führen Sie das folgende Skript auf dem primären Knoten aus: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Deaktivieren von STONITH ist nur für Testzwecke verwenden. Wenn Sie Schrittmacher in einer produktiven Umgebung verwenden möchten, sollten Sie eine Implementierung STONITH je nach Umgebung planen und bewahren Sie ihn der aktiviert. Beachten Sie, dass an diesem Punkt gibt es keine Fencing-Agents für alle Cloud-Umgebungen (einschließlich Azure) oder Hyper-V. Die Cluster-Hersteller bietet Unterstützung für die Ausführung von produktionsclustern in diesen Umgebungen, nicht. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Legen Sie Cluster Eigenschaft Cluster-erneut prüfen-Intervall

`cluster-recheck-interval` Gibt an, das Abrufintervall für Änderungen in der Ressourcenparameter, Einschränkungen oder andere Clusteroptionen in dem Cluster abfragt. Wenn ein Replikat ausfällt, versucht der Cluster, das Replikat in einem Intervall neu zu starten, die durch gebunden ist die `failure-timeout` Wert und die `cluster-recheck-interval` Wert. Z. B. wenn `failure-timeout` auf 60 Sekunden festgelegt ist und `cluster-recheck-interval` festgelegt ist auf 120 Sekunden wird versucht, der Neustart in einem Intervall, das größer als 60 Sekunden, aber weniger als 120 Sekunden ist. Es wird empfohlen, dass Sie Fehler-Timeout auf 60 s und Cluster erneut prüfen Wiederherstellungsintervall auf einen Wert, der größer als 60 Sekunden festgelegt. Cluster-erneut prüfen-Intervall auf einen niedrigen Wert festlegen, wird nicht empfohlen.

Aktualisieren Sie den Eigenschaftswert an `2 minutes` ausführen:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Wenn Sie bereits eine verfügbarkeitsgruppenressource, die von einem Cluster Schrittmacher verwaltet haben, beachten Sie, dass alle Verteilungen, die die neuesten verfügbaren Schrittmacher Paket 1.1.18-11.el7 verwenden eine verhaltensänderung für den Start-Fehler-ist--Schwerwiegender-Einstellung, wenn Cluster einführen seiner Wert ist "false". Diese Änderung wirkt sich auf den Failover-Workflow. Wenn ein primäres Replikat ein Ausfall auftritt, muss der Cluster Failover auf eines der sekundären Replikate verfügbar. Stattdessen werden Benutzer feststellen, dass der Cluster immer wieder versucht, um das primäre Replikat mit fehlgeschlagenem zu starten. Wenn dieser primären nie (aufgrund einer dauerhaften Ausfall) online geschaltet wird, ein Cluster nie Failover an ein anderes verfügbares sekundäres Replikat. Aufgrund dieser Änderung eine zuvor empfohlene Konfiguration festzulegende Start Fehler-ist-schwerwiegend ist nicht mehr gültig und die Einstellung muss auf den Standardwert zurückgesetzt werden `true`. Darüber hinaus muss die AG-Ressource auf Einbeziehung aktualisiert werden die `failover-timeout` Eigenschaft. 
>
>Aktualisieren Sie den Eigenschaftswert an `true` ausführen:
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>Aktualisieren Ihrer vorhandenen AG Ressourceneigenschaft `failure-timeout` auf `60s` ausführen (ersetzen Sie `ag1` durch den Namen des Ihre verfügbarkeitsgruppenressource):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

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
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Erstellen der virtuellen IP-Adressressource

Führen Sie den folgenden Befehl auf einem Knoten, um die virtuelle IP-Adressressource zu erstellen. Verwenden Sie eine verfügbare statische IP-Adresse aus dem Netzwerk. Bevor Sie das Skript ausführen, ersetzen Sie die Werte zwischen `< ... >` mit einer gültigen IP-Adresse.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Es ist keine virtuellen Servernamen Schrittmacher äquivalent. Verwenden eine Verbindungszeichenfolge, die auf einen Servernamen Zeichenfolge verweist und nicht die IP-Adresse, die Adresse der IP-Ressource und die gewünschten virtuellen Servernamen in DNS registrieren. Registrieren Sie für die DR-Konfigurationen den gewünschten virtuellen Servernamen und die IP-Adresse mit DNS-Server sowohl primäre als auch DR-Standort.

## <a name="add-colocation-constraint"></a>Zusammenstellung-Einschränkung hinzufügen

Fast jeder Entscheidung in einem Cluster Schrittmacher ähnelt dem auswählen, in dem eine Ressource ausgeführt werden soll, erfolgt durch Vergleichen der Ergebnisse. Ergebnisse pro Ressource berechnet werden und der Clusterressourcen-Manager wählt die Knoten mit der höchsten Bewertung für eine bestimmte Ressource. (Wenn ein Knoten ein negatives Ergebnis für eine Ressource besitzt, kann nicht die Ressource auf diesem Knoten ausgeführt.) Verwenden Sie Einschränkungen, um die Entscheidungen, die im Cluster konfigurieren. Eine Bewertung eine Beschränkung vorliegt. Wenn eine Einschränkung, ein Ergebnis kleiner als UNENDLICH ist, ist es nur eine Empfehlung. Ein Ergebnis von UNENDLICH bedeutet, dass es erforderlich ist. Um sicherzustellen, dass das primäre Replikat und die virtuelle Ip-Adressressource auf demselben Host sind, definieren Sie eine Zusammenstellung-Einschränkung mit einem Faktor von UNENDLICH. Führen Sie den folgenden Befehl zum Hinzufügen der Einschränkung durch die Zusammenstellung auf einem Knoten. 

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

