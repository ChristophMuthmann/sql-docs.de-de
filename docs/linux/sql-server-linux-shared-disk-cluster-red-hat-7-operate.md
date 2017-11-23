---
title: "Betreiben von Red Hat Enterprise Linux freigegebenen Clusterdatenträger für SQL Server | Microsoft Docs"
description: "Red Hat Enterprise Linux freigegebene Datenträgercluster für SQL Server konfigurieren, um hohe Verfügbarkeit zu implementieren."
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
ms.assetid: 075ab7d8-8b68-43f3-9303-bbdf00b54db1
ms.workload: Inactive
ms.openlocfilehash: ed87490e0aedfd0953c8c77715ddc7e843aefd2c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="operate-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Betreiben von Red Hat Enterprise Linux freigegebene Datenträgercluster für SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Dieses Dokument beschreibt, wie die folgenden Aufgaben für SQL Server auf einem freigegebenen Datenträger-Failovercluster mit Red Hat Enterprise Linux ausgeführt werden.

- Ein manuelles Failover cluster
- Überwachen Sie ein Failoverclusters in einem SQL Server-Dienst
- Hinzufügen eines Clusterknotens
- Entfernen eines Clusterknotens
- Ändern Sie die SQL Server-Ressource, die Überwachung der Häufigkeit

## <a name="architecture-description"></a>Beschreibung von Architektur

Die clustering-Ebene basiert auf Red Hat Enterprise Linux (RHEL) [HA-Add-On](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) baut auf [Schrittmacher](http://clusterlabs.org/). Corosync und Schrittmacher Clusterkommunikation und ressourcenverwaltung zu koordinieren. SQL Server-Instanz ist auf einem "Node" oder anderen aktiv.

Das folgende Diagramm veranschaulicht die Komponenten in einem Linux-Cluster mit SQL Server. 

![Red Hat Enterprise Linux 7 freigegebene Datenträgercluster für SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Weitere Informationen zur Clusterkonfiguration, Agents Ressourcenoptionen und Verwaltung, finden Sie auf [RHEL Referenzdokumentation](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

## <a name = "failManual"></a>Failovercluster manuell

Die `resource move` Befehl erstellt eine Einschränkung erzwingen die Ressource, auf dem Zielknoten zu starten.  Nach der Ausführung der `move` Befehl, eine Ressource ausgeführt, `clear` wird die Einschränkung entfernt, daher ist es möglich, verschieben Sie die Ressource erneut, oder die Ressource automatisch ein Failover ausgeführt haben. 

```bash
sudo pcs resource move <sqlResourceName> <targetNodeName>  
sudo pcs resource clear <sqlResourceName> 
```

Im folgenden Beispiel wird die **Mssqlha** Ressource auf einen Knoten mit dem Namen **sqlfcivm2**, und klicken Sie dann die Einschränkung entfernt, sodass die Ressource später auf einen anderen Knoten verschoben werden kann.  

```bash
sudo pcs resource move mssqlha sqlfcivm2 
sudo pcs resource clear mssqlha 
```

## <a name="monitor-a-failover-cluster-sql-server-service"></a>Überwachen Sie ein Failoverclusters in einem SQL Server-Dienst

Zeigen Sie den aktuellen Clusterstatus an:

```bash
sudo pcs status  
```

Live Status der Cluster und Ressourcen anzeigen:

```bash
sudo crm_mon 
```

Die Ressource-Agent-Protokolle im anzeigen`/var/log/cluster/corosync.log`

## <a name="add-a-node-to-a-cluster"></a>Hinzufügen eines Knotens zu einem cluster

1. Überprüfen Sie die IP-Adresse für jeden Knoten. Das folgende Skript zeigt die IP-Adresse von Ihrem aktuellen Knoten. 

   ```bash
   ip addr show
   ```

3. Der neue Knoten benötigt einen eindeutigen Namen, der 15 Zeichen oder weniger. In Red Hat Linux standardmäßig der Name des Computers ist `localhost.localdomain`. Dieser Standardname möglicherweise nicht eindeutig sein und ist zu lang. Legen Sie den Computernamen des neuen Knotens. Legen Sie die Computernamen durch Hinzufügen zu `/etc/hosts`. Mithilfe des folgenden Skripts können Sie `/etc/hosts` mit `vi` bearbeiten. 

   ```bash
   sudo vi /etc/hosts
   ```

   Das folgende Beispiel zeigt `/etc/hosts` mit Ergänzungen für drei Knoten mit dem Namen `sqlfcivm1`, `sqlfcivm2`, und`sqlfcivm3`.

   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1         localhost localhost6 localhost6.localdomain6
   10.128.18.128 fcivm1
   10.128.16.77 fcivm2
   10.128.14.26 fcivm3
    ```
    
   Die Datei sollte auf allen Knoten identisch sein. 

1. Beenden Sie den SQL Server-Dienst auf dem neuen Knoten an.

1. Führen Sie die Anweisungen, um das datenbankdateiverzeichnis auf den freigegebenen Speicherort bereitstellen:

   Von den NFS-Server installieren`nfs-utils`

   ```bash
   sudo yum -y install nfs-utils 
   ``` 

   Öffnen Sie die Firewall auf Clients und Server für NFS 

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

   Bearbeiten von/etc/fstab-Datei, um die Mount-Befehl einschließen: 

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr
   ```

   Führen Sie `mount -a` für die Änderungen wirksam werden.
   
1. Erstellen Sie eine Datei zum Speichern von SQL Server-Benutzername und Kennwort für die Anmeldung Schrittmacher, auf dem neuen Knoten. Der folgende Code erstellt und füllt diese Tabelle:

   ```bash
   sudo touch /var/opt/mssql/passwd
   sudo echo "<loginName>" >> /var/opt/mssql/secrets/passwd
   sudo echo "<loginPassword>" >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/passwd
   sudo chmod 600 /var/opt/mssql/passwd
   ```

3. Öffnen Sie auf den neuen Knoten Schrittmacher Firewall-Ports. Führen Sie zum Öffnen dieser Ports mit `firewalld` folgenden Befehl aus:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > [!NOTE]
   > Wenn Sie eine andere Firewall verwenden, in die keine Konfiguration mit hoher Verfügbarkeit integriert ist, müssen die folgenden Ports geöffnet werden, damit Pacemaker mit anderen Knoten im Cluster kommunizieren kann:
   >
   > * TCP: Ports 2224, 3121, 21064
   > * UDP: Port 5405

1. Installieren Sie Schrittmacher Pakete auf dem neuen Knoten an.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```
 
2. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie das gleiche Kennwort wie die vorhandenen Knoten an. 

   ```bash
   sudo passwd hacluster
   ```
 
3. Aktivieren und starten Sie den `pcsd`-Dienst und Pacemaker. Dadurch können den neuen Knoten den Cluster nach dem Neustart erneut beitreten. Führen Sie den folgenden Befehl auf dem neuen Knoten an.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Installieren Sie den FCI-Ressourcenagent für SQL Server. Führen Sie die folgenden Befehle auf dem neuen Knoten an. 

   ```bash
   sudo yum install mssql-server-ha
   ```

1. Authentifizieren Sie auf einen vorhandenen Knoten aus dem Cluster den neuen Knoten, und fügen Sie es dem Cluster hinzu:

    ```bash
    sudo pcs    cluster auth <nodeName3> -u hacluster 
    sudo pcs    cluster node add <nodeName3> 
    ```

    Das folgende Beispiel Ads ein Knoten mit dem Namen **vm3** für den Cluster.

    ```bash
    sudo pcs    cluster auth  
    sudo pcs    cluster start 
    ```

## <a name="remove-nodes-from-a-cluster"></a>Entfernen von Knoten aus einem cluster

Zum Entfernen eines Knotens aus einem Cluster, führen Sie den folgenden Befehl:

```bash
sudo pcs    cluster node remove <nodeName>  
```

## <a name="change-the-frequency-of-sqlservr-resource-monitoring-interval"></a>Ändern Sie die Häufigkeit der Überwachungszeitraum Sqlservr-Ressource

```bash
sudo pcs    resource op monitor interval=<interval>s <sqlResourceName> 
```

Im folgenden Beispiel wird das Überwachungsintervall auf 2 Sekunden für die Mssql-Ressource:

```bash
sudo pcs    resource op monitor interval=2s mssqlha 
```
## <a name="troubleshoot-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Problembehandlung für Red Hat Enterprise Linux freigegebene Datenträgercluster für SQL Server

Bei der Problembehandlung des Clusters kann es hilfreich sein, um zu verstehen, wie die drei Daemons zusammenarbeiten, um Cluster-Ressourcen zu verwalten. 

| Daemon | Description 
| ----- | -----
| Corosync | Bietet Quorum Mitgliedschaft und messaging zwischen Clusterknoten.
| Schrittmacher | Zusätzlich zu Corosync befindet, und stellt die Zustandsautomaten für Ressourcen bereit. 
| PCSD | Verwaltet Schrittmacher und Corosync über die `pcs` Tools

PCSD muss ausgeführt werden, damit verwenden `pcs` Tools. 

### <a name="current-cluster-status"></a>Aktueller Clusterstatus 

`sudo pcs status`grundlegende Informationen zu den Cluster, Quorum-Knoten, Ressourcen und Daemon-Status für jeden Knoten zurückgegeben. 

Ein Beispiel für eine fehlerfreie Schrittmacher Quorum Ausgabe würde folgendermaßen lauten:

```
Cluster name: MyAppSQL 
Last updated: Wed Oct 31 12:00:00 2016  Last change: Wed Oct 31 11:00:00 2016 by root via crm_resource on sqlvmnode1 
Stack: corosync 
Current DC: sqlvmnode1  (version 1.1.13-10.el7_2.4-44eb2dd) - partition with quorum 
3 nodes and 1 resource configured 

Online: [ sqlvmnode1 sqlvmnode2 sqlvmnode3] 

Full list of resources: 

mssqlha (ocf::sql:fci): Started sqlvmnode1 

PCSD Status: 
sqlvmnode1: Online 
sqlvmnode2: Online 
sqlvmnode3: Online 

Daemon Status: 
corosync: active/disabled 
pacemaker: active/enabled 
```

Im Beispiel `partition with quorum` bedeutet, dass die meisten Quorums der Knoten online ist. Wenn der Cluster die Mehrheit Quorums der Knoten, verliert `pcs status` zurück `partition WITHOUT quorum` und alle Ressourcen beendet. 

`online: [sqlvmnode1 sqlvmnode2 sqlvmnode3]`Gibt den Namen aller Knoten, die derzeit Teil des Clusters zurück. Wenn keine Knoten beteiligt sind, `pcs status` gibt `OFFLINE: [<nodename>]`.

`PCSD Status`Zeigt das Cluster den Status für jeden Knoten an.

### <a name="reasons-why-a-node-may-be-offline"></a>Gründe, warum ein Knoten offline geschaltet werden kann

Suchen Sie die folgenden Elemente aus, wenn ein Knoten offline ist.

- **Firewall**

    Die folgenden Ports müssen auf allen Knoten für Schrittmacher kommunizieren können geöffnet sein.
    
    - ** TCP: 2224, 3121, 21064

- **Schrittmacher oder Corosync Services ausgeführt wird**

- **Kommunikation von Knoten**

- **Namenszuordnungen Knoten**

## <a name="additional-resources"></a>Weitere Ressourcen

* [Clustern von Grund auf Neu](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Leitfaden für Schrittmacher

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Red Hat Enterprise Linux freigegebene Datenträgercluster für SQL Server](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)

