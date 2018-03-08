---
title: "Red Hat Enterprise Linux freigegebenen Clusterdatenträger für SQL Server konfigurieren | Microsoft Docs"
description: "Red Hat Enterprise Linux freigegebene Datenträgercluster für SQL Server konfigurieren, um hohe Verfügbarkeit zu implementieren."
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: dcc0a8d3-9d25-4208-8507-a5e65d2a9a15
ms.workload: On Demand
ms.openlocfilehash: 5263a40e37388ea9a884cafeffe2302f56f0043e
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="configure-red-hat-enterprise-linux-shared-disk-cluster-for-sql-server"></a>Konfigurieren Sie Red Hat Enterprise Linux freigegebene Datenträgercluster für SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieses Handbuch enthält Anweisungen zum Erstellen eines freigegebenen Datenträgers zwei Knoten-Clusters für SQL Server unter Red Hat Enterprise Linux. Die clustering-Ebene basiert auf Red Hat Enterprise Linux (RHEL) [HA-Add-On](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) baut auf [Schrittmacher](http://clusterlabs.org/). SQL Server-Instanz ist auf einem "Node" oder anderen aktiv.

> [!NOTE] 
> Zugriff auf Red Hat-HA-Add-On und Dokumentation erfordert ein Abonnement. 

Wie das folgende Diagramm zeigt, wird der Speicher auf zwei Servern angezeigt. Komponenten - Corosync "und" Schrittmacher - Kommunikation und ressourcenverwaltung koordiniert werden. Einer der Server hat die aktive Verbindung mit der Speicherressourcen und SQL Server. Wenn Schrittmacher einen Fehler erkennt verwalten die Clusterkomponenten, die Ressourcen auf den anderen Knoten verschoben.  

![Red Hat Enterprise Linux 7 freigegebene Datenträgercluster für SQL](./media/sql-server-linux-shared-disk-cluster-red-hat-7-configure/LinuxCluster.png) 

Weitere Informationen zu Clusterkonfiguration, Optionen für Agents und Management finden Sie auf [RHEL Referenzdokumentation](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).


> [!NOTE] 
> SQL Server Integration in Schrittmacher ist an diesem Punkt nicht als gekoppelten als mit WSFC unter Windows. Aus SQL, besteht keine Kenntnisse über das Vorhandensein des Clusters, alle Orchestrierung befindet sich im außerhalb und der Dienst wird als eigenständige Instanz von Schrittmacher gesteuert. Außerdem ist z. B. Cluster Dmvs Sys. dm_os_cluster_nodes und dm_os_cluster_properties keine Datensätze.
Zum Verwenden einer Verbindungszeichenfolge, die auf einem Zeichenfolgennamen für den Server verweist, und die IP-Adresse verwenden, müssen sie in ihrer DNS-Server die IP-Adresse verwendet, um die virtuelle IP-Adressressource erstellen (wie in den folgenden Abschnitten erläutert wird) mit dem ausgewählten Server registrieren.

In den folgenden Abschnitten exemplarisch die Schritte zum Einrichten einer Lösung mit Failovercluster. 

## <a name="prerequisites"></a>Erforderliche Komponenten

Um das folgende End-to-End-Szenario abzuschließen, benötigen Sie zwei Computer, der zwei Knoten-Cluster und einem anderen Server so konfigurieren Sie die NFS-Server bereitstellen. Unten aufgeführten Schritten dargestellt, wie diesen Servern konfiguriert werden kann.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Richten Sie ein und konfigurieren Sie des Betriebssystems auf allen Clusterknoten

Der erste Schritt ist so konfigurieren Sie das Betriebssystem auf den Clusterknoten. Verwenden Sie für diese Gang durch RHEL mit einem gültigen Abonnement für das Add-on für hohe Verfügbarkeit. 

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Installieren und Konfigurieren von SQL Server auf jedem Clusterknoten

1. Installieren und Einrichten von SQL Server auf beiden Knoten.  Ausführliche Anweisungen finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).

1. Festlegen Sie ein Knoten als primärer und der andere als sekundärer, zum Zweck der Konfiguration. Verwenden Sie diese Begriffe für die folgenden dieses Handbuchs.  

1. Beenden und Deaktivieren von SQL Server, auf dem sekundären Knoten.

   Im folgenden Beispiel wird beendet und deaktiviert SQL Server: 

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl disable mssql-server
   ```
> [!NOTE] 
> Beim Setup eine Server-Hauptschlüssel für die SQL Server-Instanz generiert und an platziert `/var/opt/mssql/secrets/machine-key`. Unter Linux wird SQL Server immer ausgeführt, als ein lokales Konto Mssql aufgerufen werden. Da es sich um ein lokales Konto handelt, wird nicht seine Identität Knoten gemeinsam verwendet. Aus diesem Grund müssen Sie den Verschlüsselungsschlüssel primären Knoten für jeden sekundären Knoten kopieren, damit jedes lokale Mssql-Konto, um den Server-Hauptschlüssel entschlüsseln zugreifen kann. 

1. Klicken Sie auf dem primären Knoten, erstellen Sie eine SQL Server-Anmeldung für Schrittmacher, und erteilen Sie die Login-Berechtigung zum Ausführen `sp_server_diagnostics`. Dieses Konto wird von Schrittmacher verwendet, um zu überprüfen, welcher Knoten auf SQL Server ausgeführt wird. 

   ```bash
   sudo systemctl start mssql-server
   ```

   Herstellen einer Verbindung mit SQL Server `master` Datenbank mit der sa-Konto, und führen Sie Folgendes aus:

   ```bashsql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'

   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```
   Alternativ können Sie die Berechtigungen detaillierter festlegen. Die Anmeldung Schrittmacher benötigt `VIEW SERVER STATE` zum Abfrage-Integritätsstatus mit Sp_server_diagnostics, `setupadmin` und `ALTER ANY LINKED SERVER` den Namen der FCI-Instanz mit dem Ressourcennamen zu aktualisieren, indem Sp_dropserver und Sp_addserver ausführen. 

1. Beenden und Deaktivieren von SQL Server, auf dem primären Knoten. 

1. Konfigurieren Sie die Hosts-Datei für jeden Clusterknoten. Die Hosts-Datei muss die IP-Adresse und die Namen aller Clusterknoten enthalten. 

    Überprüfen Sie die IP-Adresse für jeden Knoten. Das folgende Skript zeigt die IP-Adresse von Ihrem aktuellen Knoten. 

   ```bash
   sudo ip addr show
   ```

   Legen Sie den Computernamen auf jedem Knoten ein. Geben Sie jeden Knoten einen eindeutigen Namen, der 15 Zeichen oder weniger. Legen Sie die Computernamen durch Hinzufügen zu `/etc/hosts`. Mithilfe des folgenden Skripts können Sie `/etc/hosts` mit `vi` bearbeiten. 

   ```bash
   sudo vi /etc/hosts
   ```
   Das folgende Beispiel zeigt `/etc/hosts` mit Ergänzungen für zwei Knoten mit dem Namen `sqlfcivm1` und `sqlfcivm2`.

   ```bash
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 sqlfcivm1
   10.128.16.77 sqlfcivm2
   ```

Im nächsten Abschnitt Konfigurieren freigegebenen Speicher und die Datenbankdateien an, dass Speicher verschieben. 

## <a name="configure-shared-storage-and-move-database-files"></a>Konfigurieren von freigegebenen Speicher und Verschieben von Datenbankdateien 

Es gibt eine Vielzahl von Lösungen für das Bereitstellen von freigegebenen Speichers. Diese exemplarische Vorgehensweise wird das Konfigurieren von freigegebenen Speicher mit NFS. Es wird empfohlen, bewährte Methoden befolgen und Kerberos verwenden, um NFS zu sichern (finden Sie hier ein Beispiel: https://www.certdepot.net/rhel7-use-kerberos-control-access-nfs-network-shares/). 

>[!Warning]
>Wenn Sie NFS nicht sichern, dann werden jeder, der Zugriff auf Ihr Netzwerk und die IP-Adresse eines SQL-Knotens zu spoofen können auf die Datendateien zugreifen. Wie immer, stellen Sie sicher, dass Sie Bedrohungsmodells für Ihr System vor der Verwendung in der Produktion. Eine andere Speicheroption ist die Verwendung von SMB-Dateifreigabe.

### <a name="configure-shared-storage-with-nfs"></a>Konfigurieren von freigegebenen Speicher mit NFS

> [!IMPORTANT] 
> Hosten der Datenbankdateien auf einer NFS-Server mit Version < 4 wird in dieser Version nicht unterstützt. Dazu gehören, verwenden Sie stattdessen NFS für freigegebene Datenträger Failoverclustering sowie Datenbanken für nicht gruppierte Instanzen. Wir arbeiten zur Aktivierung von anderen NFS-Server-Versionen in zukünftigen Releases. 

Führen Sie folgende Schritte aus, auf dem NFS-Server:

1. Installieren `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Aktivieren und starten `rpcbind`

   ```bash
   sudo systemctl enable rpcbind && sudo systemctl start rpcbind
   ```

1. Aktivieren und starten `nfs-server`
 
   ```bash
   sudo systemctl enable nfs-server && sudo systemctl start nfs-server
   ```
 
1.  Bearbeiten Sie `/etc/exports` auf das Verzeichnis exportieren Sie freigeben möchten. Sie benötigen 1 Zeile für jede gewünschte Freigabe. Beispiel: 

   ```bash
   /mnt/nfs  10.8.8.0/24(rw,sync,no_subtree_check,no_root_squash)
   ```

1. Exportieren Sie die Freigaben

   ```bash
   sudo exportfs -rav
   ```

1. Stellen Sie sicher, dass die Pfade/freigegebene exportiert werden, von den NFS-Server ausführen sind

   ```bash
   sudo showmount -e
   ```

1. Ausnahme im SELinux hinzufügen

   ```bash
   sudo setsebool -P nfs_export_all_rw 1
   ```
   
1. Öffnen Sie die Firewall den Server an.

   ```bash 
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Konfigurieren Sie alle Knoten des Clusters für die Verbindung mit dem freigegebenen NFS-Speicher

Führen Sie die folgenden Schritte auf allen Knoten im Cluster.

1.  Installieren `nfs-utils`

   ```bash
   sudo yum -y install nfs-utils
   ```

1. Öffnen Sie die Firewall auf Clients und Server für NFS

   ```bash
   sudo firewall-cmd --permanent --add-service=nfs
   sudo firewall-cmd --permanent --add-service=mountd
   sudo firewall-cmd --permanent --add-service=rpc-bind
   sudo firewall-cmd --reload
   ```

1. Stellen Sie sicher, dass die NFS-Freigaben auf Clientcomputern angezeigt werden können

   ```bash
   sudo showmount -e <IP OF NFS SERVER>
   ```

1. Wiederholen Sie diese Schritte auf allen Clusterknoten.

Weitere Informationen zum Verwenden von NFS finden Sie unter den folgenden Ressourcen:

* [NFS-Servern und Firewalld | Stapel Exchange](http://unix.stackexchange.com/questions/243756/nfs-servers-and-firewalld)
* [Bereitstellen von einem NFS-Volume | Linux-Netzwerkadministratoren geführt.](http://www.tldp.org/LDP/nag2/x-087-2-nfs.mountd.html)
* [NFS-Serverkonfiguration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/3/html/Reference_Guide/s1-nfs-server-export.html)

### <a name="mount-database-files-directory-to-point-to-the-shared-storage"></a>Bereitstellen von Datenbank-Dateiverzeichnis auf dem freigegebenen Speicher

1.  **Auf dem primären Knoten nur**, die Datenbankdateien an einem temporären Speicherort speichern. Das folgende Skript erstellt ein neues temporäres Verzeichnis, die Datenbankdateien in das neue Verzeichnis kopiert und die alten Datenbankdateien entfernt. Wie SQL Server als lokaler Benutzer Mssql ausgeführt wird, müssen Sie sicherstellen, dass nach der Datenübertragung an den bereitgestellten Freigabe lokaler Benutzer Lese-/ Schreibzugriff auf die Freigabe verfügt. 

   ``` 
   $ sudo su mssql
   $ mkdir /var/opt/mssql/tmp
   $ cp /var/opt/mssql/data/* /var/opt/mssql/tmp
   $ rm /var/opt/mssql/data/*
   $ exit
   ``` 

1.  Bearbeiten Sie auf allen Knoten im Cluster `/etc/fstab` Datei Mount-Befehl einschließen.  

   ```bash
   <IP OF NFS SERVER>:<shared_storage_path> <database_files_directory_path> nfs timeo=14,intr 
   ```
   
   Das folgende Skript zeigt ein Beispiel für die Bearbeitung.  

   ``` 
   10.8.8.0:/mnt/nfs /var/opt/mssql/data nfs timeo=14,intr 
   ``` 
> [!NOTE] 
>Wenn eine Datei System (FS) Ressource wie empfohlen hier verwenden, besteht keine Notwendigkeit, den Befehl bereitstellen in/etc/fstab beizubehalten. Schrittmacher übernimmt das Einbinden des Ordners beim Starten der FS gruppierte Ressource. Mithilfe von Fencing wird es sichergestellt, dass das FS nie zweimal bereitgestellt wird. 

1.  Führen Sie `mount -a` Befehl für das System zum Aktualisieren der bereitgestellten Pfade.  

1.  Kopieren der Datenbank und Protokolldateien, die Sie gespeichert `/var/opt/mssql/tmp` auf die neu bereitgestellte Freigabe `/var/opt/mssql/data`. Dies muss nur erfolgen **auf dem primären Knoten**. Stellen Sie sicher, dass Sie schreibgeschützte Schreibberechtigungen "Mssql" Lokale Benutzer zur Verfügung stellen.

   ``` 
   $ sudo chown mssql /var/opt/mssql/data
   $ sudo chgrp mssql /var/opt/mssql/data
   $ sudo su mssql
   $ cp /var/opt/mssql/tmp/* /var/opt/mssql/data/
   $ rm /var/opt/mssql/tmp/*
   $ exit
   ``` 
 
1.  Überprüfen Sie, dass SQL Server erfolgreich mit dem neuen Dateipfad gestartet wird. Hierzu auf jedem Knoten. An diesem Punkt sollte nur ein Knoten SQL Server zu einem Zeitpunkt ausführen. Sie können nicht beide zur gleichen Zeit ausgeführt werden, da sie beide versucht, Zugriff auf die Datendateien gleichzeitig (aus, um zu vermeiden, versehentlich Starten von SQL Server auf beiden Knoten, eine Dateisystem-Clusterressource verwenden, um sicherzustellen, dass die Freigabe nicht zweimal von der verschiedenen Knoten bereitgestellt ist). Die folgenden Befehle Starten von SQL Server, überprüfen Sie den Status und beenden Sie SQL Server.
 
   ```bash
   sudo systemctl start mssql-server
   sudo systemctl status mssql-server
   sudo systemctl stop mssql-server
   ```
 
Zu diesem Zeitpunkt sind beide SQL Server-Instanzen mit Datenbankdateien auf den freigegebenen Speicher Ausführung konfiguriert. Der nächste Schritt ist so konfigurieren Sie SQL Server für Schrittmacher. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher


2. Erstellen Sie auf beiden Clusterknoten eine Datei zum Speichern von Benutzername und Kennwort für SQL Server für die Pacemaker-Anmeldung. Der folgende Befehl erstellt und füllt diese Datei:

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   echo '<loginName>' | sudo tee -a /var/opt/mssql/secrets/passwd
   echo '<loginPassword>' | sudo tee -a /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. Öffnen Sie auf beiden Clusterknoten die Pacemaker-Firewallports. Führen Sie zum Öffnen dieser Ports mit `firewalld` folgenden Befehl aus:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Wenn Sie eine andere Firewall verwenden, in die keine Konfiguration mit hoher Verfügbarkeit integriert ist, müssen die folgenden Ports geöffnet werden, damit Pacemaker mit anderen Knoten im Cluster kommunizieren kann:
   >
   > * TCP: Ports 2224, 3121, 21064
   > * UDP: Port 5405

1. Installieren Sie Pacemaker-Pakete auf jedem Knoten.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie auf beiden Knoten dasselbe Kennwort. 

   ```bash
   sudo passwd hacluster
   ```

   

3. Aktivieren und starten Sie den `pcsd`-Dienst und Pacemaker. So können Knoten dem Cluster nach dem Neustart erneut beitreten. Führen Sie den folgenden Befehl auf beiden Knoten aus.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Installieren Sie den FCI-Ressourcenagent für SQL Server. Führen Sie die folgenden Befehle auf beiden Knoten aus. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="create-the-cluster"></a>Erstellen des Clusters 

1. Erstellen Sie auf einem Knoten des Clusters ein.

   ```bash
   sudo pcs cluster auth <nodeName1 nodeName2 …> -u hacluster
   sudo pcs cluster setup --name <clusterName> <nodeName1 nodeName2 …>
   sudo pcs cluster start --all
   ```

   > RHEL HA-Add-On wurde Zauns Agents für VMWare und KVM. Fencing muss für alle anderen Hypervisoren deaktiviert werden. Deaktivierung Zäune Agents wird in produktionsumgebungen nicht empfohlen. Zum Zeitpunkt der Zeitrahmen befinden sich keine Fencing-Agents, für Hyper-v- oder Cloud-Umgebungen. Wenn Sie eine der folgenden Konfigurationen ausführen, müssen Sie Fencing deaktivieren. \**Dies empfiehlt sich nicht in einem Produktionssystem!**

   Der folgende Befehl deaktiviert die Fencing-Agents.

   ```bash
   sudo pcs property set stonith-enabled=false
   sudo pcs property set start-failure-is-fatal=false
   ```

2. Konfigurieren Sie die Clusterressourcen für SQL Server, Dateisystem und virtuellen IP-Ressourcen, und drücken Sie die Konfiguration für den Cluster. Sie benötigen die folgenden Informationen:

   - **SQL Server-Ressourcenname**: einen Namen für die SQL Server-Clusterressource. 
   - **Floating IP-Ressourcenname**: einen Namen für die virtuelle IP-Adressressource.
   - **IP-Adresse**: die IP-Adresse, den Client für die Verbindung an der gruppierten Instanz von SQL Server verwenden. 
   - **System-Ressource Dateiname**: einen Namen für die Dateisystem-Ressource.
   - **Gerät**: Pfad für die NFS-Freigabe
   - **Gerät**: der lokale Pfad, dass er auf die Freigabe bereitgestellt wurde
   - **FsType**: Freigabe Dateityp (d. h. Nfs)

   Aktualisieren Sie die Werte aus dem folgenden Skript für Ihre Umgebung. Führen Sie auf einem Knoten zu konfigurieren und starten Sie den Clusterdienst.  

   ```bash
   sudo pcs cluster cib cfg 
   sudo pcs -f cfg resource create <sqlServerResourceName> ocf:mssql:fci
   sudo pcs -f cfg resource create <floatingIPResourceName> ocf:heartbeat:IPaddr2 ip=<ip Address>
   sudo pcs -f cfg resource create <fileShareResourceName> Filesystem device=<networkPath> directory=<localPath>         fstype=<fileShareType>
   sudo pcs -f cfg constraint colocation add <virtualIPResourceName> <sqlResourceName>
   sudo pcs -f cfg constraint colocation add <fileShareResourceName> <sqlResourceName> 
   sudo pcs cluster cib-push cfg
   ```

   Das folgende Skript erstellt z. B. eine gruppierten SQL Server-Ressource mit dem Namen `mssqlha`, und eine floating IP-Adressressourcen mit IP-Adresse `10.0.0.99`. Erstellt eine Ressource Filesystem außerdem Einschränkungen hinzugefügt, damit alle Ressourcen auf demselben Knoten wie SQL-Ressource zusammengestellt werden. 

   ```bash
   sudo pcs cluster cib cfg
   sudo pcs -f cfg resource create mssqlha ocf:mssql:fci
   sudo pcs -f cfg resource create virtualip ocf:heartbeat:IPaddr2 ip=10.0.0.99
   sudo pcs -f cfg resource create fs Filesystem device="10.8.8.0:/mnt/nfs" directory="/var/opt/mssql/data" fstype="nfs"
   sudo pcs -f cfg constraint colocation add virtualip mssqlha
   sudo pcs -f cfg constraint colocation add fs mssqlha
   sudo pcs cluster cib-push cfg
   ```

   Nachdem die Konfiguration wird per Push übertragen wird, wird SQL Server auf einem Knoten gestartet. 

3. Stellen Sie sicher, dass SQL Server gestartet wurde. 

   ```bash
   sudo pcs status 
   ```

   Die folgenden Beispiele zeigen, wie die Ergebnisse Schrittmacher erfolgreich wurde gestartet, eine Clusterinstanz von SQL Server. 

   ```
   fs     (ocf::heartbeat:Filesystem):    Started sqlfcivm1
   virtualip     (ocf::heartbeat:IPaddr2):      Started sqlfcivm1
   mssqlha  (ocf::mssql:fci): Started sqlfcivm1
   
   PCSD Status:
    slqfcivm1: Online
    sqlfcivm2: Online
   
   Daemon Status:
    corosync: active/disabled
    pacemaker: active/enabled
    pcsd: active/enabled
   ```

## <a name="additional-resources"></a>Weitere Ressourcen

* [Clustern von Grund auf Neu](http://clusterlabs.org/doc/Cluster_from_Scratch.pdf) Leitfaden für Schrittmacher

## <a name="next-steps"></a>Nächste Schritte

[Arbeiten Sie mit SQL Server freigegebene Datenträgercluster für Red Hat Enterprise Linux](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
