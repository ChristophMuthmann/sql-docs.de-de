---
title: "RHEL Cluster für SQL Server-Verfügbarkeitsgruppe konfigurieren | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.workload: Inactive
ms.openlocfilehash: dd997e9d3f235d841cd5706b9c81b9335360540d
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2018
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>Konfigurieren von Cluster RHEL für SQL Server-Verfügbarkeitsgruppe

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Dokument erläutert das Erstellen eines drei Knoten Availability Group für SQL Server unter Red Hat Enterprise Linux. Für hohe Verfügbarkeit, eine verfügbarkeitsgruppe unter Linux erfordert drei Knoten?: Siehe [hohe Verfügbarkeit und Datenschutz für verfügbarkeitsgruppenkonfigurationen](sql-server-linux-availability-group-ha.md). Die clustering-Ebene basiert auf Red Hat Enterprise Linux (RHEL) [HA-Add-On](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) baut auf [Schrittmacher](http://clusterlabs.org/). 

> [!NOTE] 
> Zugriff auf Red Hat eine vollständige Dokumentation ist kein gültiges Abonnement erforderlich. 

Weitere Informationen zur Clusterkonfiguration, Agents Ressourcenoptionen und Verwaltung, finden Sie auf [RHEL Referenzdokumentation](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

> [!NOTE] 
> SQL Server ist nicht als eng mit Schrittmacher unter Linux integriert, unverändert in Windows Server-Failoverclustering. SQL Server-Instanz ist keine des Clusters bekannt. Schrittmacher stellt Cluster Ressource Orchestrierung bereit. Darüber hinaus Name des virtuellen Netzwerks bezieht sich auf Windows Server Failover clustering - es gibt keine Entsprechung in Schrittmacher. Verfügbarkeit Gruppe dynamische Verwaltungssichten (DMVs), die Clusterinformationen Abfragen geben leere Zeilen auf Schrittmacher Cluster zurück. Um einen Listener für transparente wiederverbindung nach einem Failover zu erstellen, müssen registrieren Sie den Listenernamen manuell in DNS mit der IP-Adresse, die zum Erstellen der virtuellen IP-Adressressource verwendet. 

In den folgenden Abschnitten exemplarisch die Schritte zum Einrichten eines Clusters Schrittmacher und fügen Sie einer verfügbarkeitsgruppe als Ressource im Cluster für hohe Verfügbarkeit.

## <a name="roadmap"></a>Roadmap

Die Schritte zum Erstellen einer verfügbarkeitsgruppe auf Linux-Servern zwecks hoher Verfügbarkeit unterscheiden sich von den Schritten in einem Windows Server-Failovercluster. Die folgende Liste beschreibt die allgemeinen Schritte: 

1. [Konfigurieren von SQL Server auf den Clusterknoten](sql-server-linux-setup.md).

2. [Erstellen der verfügbarkeitsgruppe](sql-server-linux-availability-group-configure-ha.md). 

3. Konfigurieren eines Cluster-Ressourcen-Managers wie Schrittmacher an. Diese Anweisungen sind in diesem Dokument.
   
   Die Möglichkeit zum Konfigurieren eines Cluster-Ressourcen-Managers, hängt von der bestimmten Linux-Distribution ab. 

   >[!IMPORTANT]
   >Produktionsumgebungen sind einen Fencing-Agent, wie STONITH für hohe Verfügbarkeit erforderlich. Die Demos in dieser Dokumentation verwenden Zäune-Agents. Die Demos sind für das Testen und nur die Überprüfung. 
   
   >Ein Linux-Cluster verwendet Fencing, um den Cluster in einen bekannten Zustand zurückzugeben. Die Methode zum Konfigurieren von Fencing hängt davon ab, die Verteilung und der Umgebung. Derzeit ist Fencing nicht in einige Cloudumgebungen verfügbar. Weitere Informationen finden Sie unter [Richtlinien zur Unterstützung für RHEL hohe Verfügbarkeit Cluster - Virtualisierungsplattformen](https://access.redhat.com/articles/29440).

5. [Fügen Sie die verfügbarkeitsgruppe als Ressource im Cluster](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>Konfigurieren Sie hohe Verfügbarkeit für RHEL

Um hohe Verfügbarkeit für RHEL konfigurieren möchten, aktivieren Sie das Abonnement für die hohe Verfügbarkeit, und konfigurieren Sie Schrittmacher.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Aktivieren Sie das Abonnement hohe Verfügbarkeit für RHEL

Jeder Knoten im Cluster muss eine entsprechende Abonnement für RHEL und hohe Verfügbarkeit hinzuzufügen verfügen. Überprüfen Sie die Anforderungen an [wie hohe Verfügbarkeit Cluster Pakete in Red Hat Enterprise Linux installiert](http://access.redhat.com/solutions/45930). Führen Sie diese Schritte aus, um das Abonnement und Repositorys konfigurieren:

1. Registrieren Sie das System ein.

   ```bash
   sudo subscription-manager register
   ```

   Geben Sie Ihren Benutzernamen und Ihr Kennwort ein.   

1. Liste der verfügbaren Pools für die Registrierung.

   ```bash
   sudo subscription-manager list --available
   ```

   Beachten Sie aus der Liste der verfügbaren Pools die Pool-ID für das Abonnement für die hohe Verfügbarkeit aus.

1. Aktualisieren Sie das folgende Skript ein. Ersetzen Sie `<pool id>` durch die Pool-ID für eine hohe Verfügbarkeit aus dem vorhergehenden Schritt. Führen Sie das Skript aus, um das Abonnement anzufügen.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. Aktivieren Sie das Repository.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

Weitere Informationen finden Sie unter [Schrittmacher – der Open Source, hohe Verfügbarkeit Cluster](http://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/). 

Nachdem Sie das Abonnement konfiguriert haben, führen Sie die folgenden Schritte aus, um Schrittmacher zu konfigurieren:

### <a name="configure-pacemaker"></a>Konfigurieren von Schrittmacher

Nachdem Sie das Abonnement registriert haben, führen Sie die folgenden Schritte aus, um Schrittmacher zu konfigurieren:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Nachdem Schrittmacher konfiguriert ist, verwenden Sie `pcs` für die Interaktion mit dem Cluster. Führen Sie alle Befehle für einen Knoten aus dem Cluster an. 

## <a name="configure-fencing-stonith"></a>Konfigurieren von Fencing (STONITH)

Schrittmacher Cluster Lieferanten erfordern STONITH aktiviert werden und ein Fencing Gerät für ein unterstütztes Clustersetup konfiguriert. STONITH steht für "den andere Knoten gehen im Head". Wenn der Cluster-Ressourcen-Manager den Status eines Knotens oder einer Ressource auf einem Knoten nicht ermitteln kann, bringt Zäune Cluster in einen bekannten Zustand erneut.

Ebene Zäune Ressource wird sichergestellt, dass keine datenbeschädigung bei einem Ausfall durch Konfigurieren einer Ressource vorhanden ist. Beispielsweise können Sie Ressource Ebene Zäune, markieren Sie den Datenträger auf einem Knoten, wie wenn veraltete der kommunikationsverbindung ausfällt. 

Knoten Ebene Zäune wird sichergestellt, dass alle Ressourcen von ein Knoten nicht ausgeführt werden kann. Dies erfolgt durch Zurücksetzen des Knotens. Schrittmacher unterstützt eine große Anzahl von Geräten Zauns. Beispiele hierfür sind eine unterbrechungsfreie Stromversorgung oder Management-Netzwerkschnittstellenkarten für Server.

Informationen zu STONITH und Fencing finden Sie unter den folgenden Artikeln:

* [Schrittmacher Clustern von Grund auf neu](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [Fencing und STONITH](http://clusterlabs.org/doc/crm_fencing.html)
* [Red Hat hohe Verfügbarkeit Add-On mit Schrittmacher: Zauns](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

Da Knotenebene Zauns Konfiguration stark von der Umgebung abhängig ist, deaktivieren sie für dieses Lernprogramm (sie kann später konfiguriert werden). Das folgende Skript deaktiviert Ebene Zäune Knoten:

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>Deaktivieren von STONITH ist nur für Testzwecke verwenden. Wenn Sie Schrittmacher in einer produktiven Umgebung verwenden möchten, sollten Sie eine Implementierung STONITH je nach Umgebung planen und bewahren Sie ihn der aktiviert. RHEL bietet keine Fencing-Agents für alle Cloud-Umgebungen (einschließlich Azure) oder Hyper-V. Die Cluster-Hersteller bietet Unterstützung für die Ausführung von produktionsclustern in diesen Umgebungen, nicht. Wir arbeiten an einer Lösung für diese Lücke, die in zukünftigen Versionen verfügbar sein wird.

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Festlegen Sie Clustereigenschaft auf "false" Start-Fehler-ist--Schwerwiegender

`start-failure-is-fatal`Gibt an, ob ein Fehler beim Starten einer Ressource auf einem Knoten weiter Start Versuche auf diesem Knoten verhindert. Bei Festlegung auf `false`, der Cluster entscheidet, ob auf demselben Knoten erneut basierend auf der Ressource aktuelle Anzahl und Migration Fehlerschwellenwert starten. Nach dem Failover gruppieren Schrittmacher Wiederholungen starten die Verfügbarkeit Ressource auf dem primären ehemaligen, sobald die SQL-Instanz verfügbar ist. Schrittmacher stuft das sekundäre Replikat, und automatisch wieder verbunden, der verfügbarkeitsgruppe. 

Aktualisieren Sie den Eigenschaftswert an `false` ausführen:

```bash
sudo pcs property set start-failure-is-fatal=false
```

>[!WARNING]
>Nach der ein automatisches Failover bei `start-failure-is-fatal = true` der Ressourcen-Manager versucht, die Ressource zu starten. Wenn beim ersten Versuch ein Fehler auftritt, führen Sie manuell `pcs resource cleanup <resourceName>` bereinigen Sie die Anzahl der Ressourcen-Fehler, und setzen Sie die Konfiguration zurück.

Informationen zu Schrittmacher Clustereigenschaften finden Sie unter [Schrittmacher Clustern Eigenschaften](http://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html).

## <a name="create-a-sql-server-login-for-pacemaker"></a>Erstellen Sie eine SQL Server-Anmeldung für Schrittmacher

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Erstellen Sie die Verfügbarkeit der Ressource "Group"

Verwenden Sie zum Erstellen der verfügbarkeitsgruppenressource `pcs resource create` Befehl, und legen Sie die Ressourceneigenschaften. Der folgende Befehl erstellt eine `ocf:mssql:ag` Master/Slave Typ der Ressource für die verfügbarkeitsgruppe mit dem Namen `ag1`.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 master notify=true
```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>Erstellen der virtuellen IP-Adressressource

Führen Sie den folgenden Befehl auf einem Knoten, um die virtuelle IP-Adressressource zu erstellen. Verwenden Sie eine verfügbare statische IP-Adresse aus dem Netzwerk. Ersetzen Sie die IP-Adresse zwischen `**<10.128.16.240>**` mit einer gültigen IP-Adresse.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

Es ist keine virtuellen Servernamen Schrittmacher äquivalent. Um eine Verbindungszeichenfolge zu verwenden, die auf einen Servernamen Zeichenfolge anstelle einer IP-Adresse verweist, registrieren Sie die Adresse der virtuellen IP-Ressource und die gewünschten virtuellen Servernamen in DNS. Registrieren Sie für die DR-Konfigurationen den gewünschten virtuellen Servernamen und die IP-Adresse mit DNS-Server sowohl primäre als auch DR-Standort.

## <a name="add-colocation-constraint"></a>Zusammenstellung-Einschränkung hinzufügen

Fast jeder Entscheidung in einem Cluster Schrittmacher ähnelt dem auswählen, in dem eine Ressource ausgeführt werden soll, erfolgt durch Vergleichen der Ergebnisse. Bewertungen werden pro Ressource berechnet. Der Cluster-Ressourcen-Manager wählt die Knoten mit der höchsten Bewertung für eine bestimmte Ressource an. Wenn ein Knoten ein negatives Ergebnis für eine Ressource besitzt, kann nicht der Ressource auf diesem Knoten ausgeführt werden.

In einem Cluster mit Schrittmacher können Sie die Entscheidungen, die den Cluster mit Einschränkungen bearbeiten. Eine Bewertung eine Beschränkung vorliegt. Wenn eine Einschränkung ein niedriger ist als Ergebnis verfügt `INFINITY`, Schrittmacher sieht es als Empfehlung. Eine Bewertung von `INFINITY` ist obligatorisch.

Um sicherzustellen, dass das primäre Replikat und die virtuelle IP-Ressourcen auf dem gleichen Host ausgeführt, definieren Sie eine Zusammenstellung-Einschränkung mit einem Faktor von UNENDLICH. Führen Sie den folgenden Befehl zum Hinzufügen der Einschränkung durch die Zusammenstellung auf einem Knoten.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Sortierung-Einschränkung hinzufügen

Die Zusammenstellung-Einschränkung verfügt über eine implizite Reihenfolge Einschränkung. Er verschiebt die virtuelle IP-Adressressource, bevor sie die verfügbarkeitsgruppenressource verschoben wird. Standardmäßig lautet die Abfolge von Ereignissen.

1. Benutzerprobleme `pcs resource move` auf dem primären verfügbarkeitsgruppenobjekt von Knoten1 auf Knoten2.
1. Die virtuelle IP-Adressressource wird auf Knoten 1 beendet.
1. Die virtuelle IP-Adressressource, die auf Knoten 2 wird gestartet.
  
   >[!NOTE]
   >An diesem Punkt die IP-Adresse vorübergehend verweist auf Knoten 2 während Knoten 2 noch ein Pre-Failover ist sekundären. 
   
1. Die verfügbarkeitsgruppe auf Knoten 1 primären zum sekundären Replikat tiefer gestuft wird.
1. Die verfügbarkeitsgruppe, der sekundären Datenbank auf Knoten 2 wird zum primären höher gestuft. 

Um zu verhindern, dass die IP-Adresse vorübergehend auf den Knoten mit der vor dem Failover sekundären Datenbank verweist, fügen Sie eine Sortierung Einschränkung hinzu. 

Um eine Sortierung Einschränkung hinzuzufügen, führen Sie den folgenden Befehl auf einem Knoten aus:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Nachdem Sie den Cluster konfigurieren und als Clusterressource der verfügbarkeitsgruppe hinzufügen, können nicht Sie Transact-SQL verwenden, um die verfügbarkeitsgruppenressourcen Failover. SQL Server-Cluster-Ressourcen unter Linux werden mit dem Betriebssystem nicht als eng verbunden, da es sich auf einem Windows Server Failover Cluster (WSFC) handelt. SQL Server-Dienst ist nicht über das Vorhandensein des Clusters. Alle Orchestrierung erfolgt über die Verwaltungstools. Verwenden Sie in RHEL oder Ubuntu `pcs` und SLES `crm` Tools. 

Ausführen des manuellen Failovers der verfügbarkeitsgruppe mit `pcs`. Failover mit Transact-SQL nicht initialisiert werden. Anweisungen hierzu finden Sie unter [Failover](sql-server-linux-availability-group-failover-ha.md#failover).

## <a name="next-steps"></a>Nächste Schritte

[Betreiben HA-verfügbarkeitsgruppe](sql-server-linux-availability-group-failover-ha.md)
