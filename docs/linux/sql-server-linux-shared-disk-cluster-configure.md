---
title: Failoverclusterinstanz – SQL Server für Linux (RHEL) konfigurieren | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.workload: Inactive
ms.openlocfilehash: 57f8f5d3881262ed96dcf84295b6c2a21dddc35d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="configure-failover-cluster-instance---sql-server-on-linux-rhel"></a>Konfigurieren Sie Failoverclusterinstanz – SQL Server für Linux (RHEL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Eine Failoverclusterinstanz von SQL Server zwei Knoten freigegebenen Datenträger Redundanz auf Serverebene für hohe Verfügbarkeit. In diesem Lernprogramm erfahren Sie, wie eine zwei-Knoten-Failover-Clusterinstanz von SQL Server unter Linux zu erstellen. Die einzelnen Schritte, die Sie abgeschlossen werden, gehören:

> [!div class="checklist"]
> * Einrichten und Konfigurieren von Linux
> * Installieren und Konfigurieren von SQL Server
> * Konfigurieren Sie die Hosts-Datei
> * Konfigurieren von freigegebenen Speicher und Verschieben von Datenbankdateien
> * Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher
> * Konfigurieren der Failoverclusterinstanz

In diesem Artikel erläutert, wie eine zwei-Knoten freigegebenen Datenträger-Failoverclusterinstanz (FCI) für SQL Server zu erstellen. Der Artikel enthält Anweisungen und Beispiele für Skripts für Red Hat Enterprise Linux (RHEL). Ubuntu-Distributionen sind ähnlich RHEL, damit Skriptbeispiele normalerweise werden auch auf Ubuntu arbeiten. 

Konzeptionelle Informationen finden Sie unter [SQL Server Failoverclusterinstanz (FCI) unter Linux](sql-server-linux-shared-disk-cluster-concepts.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

Um das folgende End-to-End-Szenario abzuschließen, benötigen Sie zwei Computer, der zwei Knoten-Cluster und einem anderen Server für den Speicher bereitstellen. Unten aufgeführten Schritten dargestellt, wie diesen Servern konfiguriert werden kann.

## <a name="set-up-and-configure-linux"></a>Einrichten und Konfigurieren von Linux

Der erste Schritt ist so konfigurieren Sie das Betriebssystem auf den Clusterknoten. Konfigurieren Sie eine Linux-Distribution, auf den einzelnen Knoten im Cluster. Verwenden Sie den Verteilungspunkt und die Version auf beiden Knoten ein. Verwenden Sie eine oder das andere der folgenden Verteilungen:
    
* RHEL mit einem gültigen Abonnement für das Add-on für hohe Verfügbarkeit

## <a name="install-and-configure-sql-server"></a>Installieren und Konfigurieren von SQL Server

1. Installieren und Einrichten von SQL Server auf beiden Knoten.  Ausführliche Anweisungen finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).
1. Festlegen Sie ein Knoten als primärer und der andere als sekundärer, zum Zweck der Konfiguration. Verwenden Sie diese Begriffe für die folgenden dieses Handbuchs.  
1. Beenden und Deaktivieren von SQL Server, auf dem sekundären Knoten.
    Im folgenden Beispiel wird beendet und deaktiviert SQL Server: 
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE] 
    > Satz Betriebszeit, einen Server-Hauptschlüssel für die SQL Server-Instanz generiert und an platziert `var/opt/mssql/secrets/machine-key`. Unter Linux wird SQL Server immer ausgeführt, als ein lokales Konto Mssql aufgerufen werden. Da es sich um ein lokales Konto handelt, wird nicht seine Identität Knoten gemeinsam verwendet. Aus diesem Grund müssen Sie den Verschlüsselungsschlüssel primären Knoten für jeden sekundären Knoten kopieren, damit jedes lokale Mssql-Konto, um den Server-Hauptschlüssel entschlüsseln zugreifen kann. 

1.  Klicken Sie auf dem primären Knoten, erstellen Sie eine SQL Server-Anmeldung für Schrittmacher, und erteilen Sie die Login-Berechtigung zum Ausführen `sp_server_diagnostics`. Dieses Konto wird von Schrittmacher verwendet, um zu überprüfen, welcher Knoten auf SQL Server ausgeführt wird. 

    ```bash
    sudo systemctl start mssql-server
    ```
   
   Herstellen einer Verbindung mit SQL Server `master` Datenbank mit der sa-Konto, und führen Sie Folgendes aus:

   ```sql
   USE [master]
   GO
   CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [<loginName>]
   ```

   Alternativ können Sie die Berechtigungen detaillierter festlegen. Die Anmeldung Schrittmacher benötigt `VIEW SERVER STATE` zum Abfrage-Integritätsstatus mit Sp_server_diagnostics, `setupadmin` und `ALTER ANY LINKED SERVER` den Namen der FCI-Instanz mit dem Ressourcennamen zu aktualisieren, indem Sp_dropserver und Sp_addserver ausführen. 

1. Beenden und Deaktivieren von SQL Server, auf dem primären Knoten. 

## <a name="configure-the-hosts-file"></a>Konfigurieren Sie die Hosts-Datei

Konfigurieren Sie die Hostdatei auf jedem Clusterknoten. Die Hosts-Datei muss die IP-Adresse und die Namen aller Clusterknoten enthalten.

1. Überprüfen Sie die IP-Adresse für jeden Knoten. Das folgende Skript zeigt die IP-Adresse von Ihrem aktuellen Knoten. 

    ```bash
    sudo ip addr show
    ```

1. Legen Sie den Computernamen auf jedem Knoten ein. Geben Sie jeden Knoten einen eindeutigen Namen, der 15 Zeichen oder weniger. Legen Sie die Computernamen durch Hinzufügen zu `/etc/hosts`. Mithilfe des folgenden Skripts können Sie `/etc/hosts` mit `vi` bearbeiten. 

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

## <a name="configure-storage--move-database-files"></a>Konfigurieren des Speichers & Verschieben von Datenbankdateien  

Sie müssen Speicher bereitzustellen, die beide Knoten zugreifen können. Sie können iSCSI, NFS oder SMB verwenden. Konfigurieren Sie des Speichers darstellen Sie des Speichers auf den Clusterknoten, und verschieben Sie die Dateien in den neuen Speicher. Die folgenden Artikel wird erläutert, die Schritte für jede Speicherungsart:

- [Konfigurieren der Failover-Clusterinstanz - iSCSI - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
- [Konfigurieren Sie Failoverclusterinstanz – NFS - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-nfs.md)
- [Konfigurieren der Failover-Clusterinstanz - SMB - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure-smb.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher

1. Erstellen Sie auf beiden Clusterknoten eine Datei zum Speichern von Benutzername und Kennwort für SQL Server für die Pacemaker-Anmeldung. 

    Der folgende Befehl erstellt und füllt diese Datei:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd    
    ```

1. Öffnen Sie auf beiden Clusterknoten die Pacemaker-Firewallports. Führen Sie zum Öffnen dieser Ports mit `firewalld` folgenden Befehl aus:

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
1. Legen Sie das Kennwort für den Standardbenutzer fest, der beim Installieren von Pacemaker und Corosync-Paketen erstellt wird. Verwenden Sie auf beiden Knoten dasselbe Kennwort. 

   ```bash
   sudo passwd hacluster
   ```
1. Aktivieren und starten Sie den `pcsd`-Dienst und Pacemaker. So können Knoten dem Cluster nach dem Neustart erneut beitreten. Führen Sie den folgenden Befehl auf beiden Knoten aus.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

1. Installieren Sie den FCI-Ressourcenagent für SQL Server. Führen Sie die folgenden Befehle auf beiden Knoten aus. 

   ```bash
   sudo yum install mssql-server-ha
   ```

## <a name="configure-the-failover-cluster-instance"></a>Konfigurieren der Failoverclusterinstanz

Die FCI wird in einer Ressourcengruppe erstellt werden. Dies ist etwas einfacher, da die Ressourcengruppe für Einschränkungen nicht werden muss. Fügen Sie jedoch die Ressourcen in der Ressourcengruppe, in der Reihenfolge, die gestartet werden soll. Ist die Reihenfolge, die gestartet werden soll: 

1. Storage-Ressource
2. Netzwerkressource
3. Anwendungsressource

In diesem Beispiel wird eine FCI in der Gruppe "NewLinFCIGrp" erstellt. Der Name der Ressourcengruppe muss eindeutig von anderen Ressourcen im Schrittmacher erstellt sein.

1.  Erstellen der Datenträgerressource. Sie erhalten keine Antwort zurück, wenn es kein Problem ist. Die Möglichkeit zum Erstellen der Datenträgerressource hängt von den Speichertyp ab. Im folgenden ist ein Beispiel für die einzelnen Speicher. Verwenden Sie das Beispiel, das für den Speichertyp für die Clusterspeicher gilt.

    **iSCSI**

    ```bash
    sudo pcs resource create <iSCSIDiskResourceName> Filesystem device="/dev/<VolumeGroupName>/<LogicalVolumeName>" directory="<FolderToMountiSCSIDisk>" fstype="<FileSystemType>" --group RGName
    ```

    \<iSCSIDIskResourceName > ist der Name der Ressource zugeordneten des iSCSI-Datenträgers

    \<VolumeGroupName > ist der Name der Volumegruppe  

    \<LogicalVolumeName > ist der Name des logischen Volumes, die erstellt wurde  

    \<FolderToMountiSCSIDIsk > ist der Ordner auf den Datenträger bereitstellen (für Systemdatenbanken und der Standardspeicherort, er wäre /var/opt/mssql/data)

    \<FileSystemType > wäre EXT4 oder XFS je nachdem wie Dinge formatiert wurden und welche die Verteilung unterstützt. 

    **NFS**

    ```bash
    sudo pcs resource create <NFSDiskResourceName> Filesystem device="<IPAddressOfNFSServer>:<FolderOnNFSServer>" directory="<FolderToMountNFSShare>" fstype=nfs4 options=" nfsvers=4.2,timeo=14,intr" --group RGName
    mount -t nfs4 IPAddressOfNFSServer:FolderOnNFSServer /var/opt/mssql/data -o 
    ```

    \<NFSDIskResourceName > der Name der Ressource, die NFS-Freigabe zugeordnet ist

    \<IPAddressOfNFSServer > die IP-Adresse des NFS-Servers, die Sie verwenden möchten

    \<FolderOnNFSServer > ist der Name der NFS-Freigabe

    \<FolderToMountNFSShare > ist der Ordner auf den Datenträger bereitstellen (für Systemdatenbanken und der Standardspeicherort, er wäre /var/opt/mssql/data)

    Ein Beispiel ist hier gezeigt:

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    **SMB**

    ```bash
    sudo pcs resource create SMBDiskResourceName Filesystem device="//<ServerName>/<ShareName>" directory="<FolderName>" fstype=cifs options="vers=3.0,username=<UserName>,password=<Password>,domain=<ADDomain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777" --group <RGName>
    ```

    \<ServerName > der Name des Servers mit der SMB-Freigabe

    \<Freigabename > ist der Name der Freigabe

    \<Ordnername > ist der Name des im letzten Schritt erstellten Ordners
    
    \<Benutzername > ist der Name des Benutzers, der auf die Freigabe zugreifen

    \<Kennwort > ist das Kennwort für den Benutzer

    \<ADDomain > ist die AD DS-Domäne (falls zutreffend, wenn eine Windows Server-basierten SMB-Freigabe verwendet)

    \<MssqlUID > ist die UID der Mssql-Benutzer

    \<MssqlGID > ist die GID des Benutzers Mssql

    \<%Rgname > ist der Name der Ressourcengruppe
 
2.  Erstellen Sie die IP-Adresse, die von der FCI verwendet werden. Sie erhalten keine Antwort zurück, wenn es kein Problem ist.

    ```bash
    sudo pcs resource create <IPResourceName> ocf:heartbeat:IPaddr2 ip=<IPAddress> nic=<NetworkCard> cidr_netmask=<NetMask> --group <RGName>
    ```

    \<IPResourceName > der Name der Ressource, die IP-Adresse zugeordnet ist

    \<IP-Adresse > ist die IP-Adresse für die FCI

    \<NetworkCard > die Netzwerkkarte, die dem Subnetz (d. h. eth0) zugeordnet ist

    \<Netzmaske > ist die Netzmaske des Subnetzes (d. h. 24)

    \<%Rgname > ist der Name der Ressourcengruppe
 
3.  Erstellen Sie die FCI-Ressource. Sie erhalten keine Antwort zurück, wenn es kein Problem ist.

    ```bash
    sudo pcs resource create FCIResourceName ocf:mssql:fci op defaults timeout=60s --group RGName
    ```

    \<FCIResourceName > ist nicht nur den Namen der Ressource, sondern auch der Anzeigename, der mit der FCI zugewiesen ist. Dies ist, was Benutzer und Anwendungen verwendet werden, eine Verbindung herstellen. 

    \<%Rgname > ist der Name der Ressourcengruppe.
 
4.  Führen Sie den Befehl `sudo pcs resource`. Die FCI muss online sein.
 
5.  Verbinden Sie mit der FCI mit SSMS oder Sqlcmd mithilfe des DNS-Ressourceneinträgen/Namens der FCI.

6.  Geben Sie die Anweisung `SELECT @@SERVERNAME`. Sie sollten den Namen der FCI zurück.

7.  Geben Sie die Anweisung `SELECT SERVERPROPERTY('ComputerNamePhysicalNetBIOS')`. Der Name des Knotens sollte zurückgegeben, die die FCI ausgeführt wird.

8.  Führen Sie die anderen Knoten der FCI manuell ein. Lesen Sie die Anweisungen unter [Operate Failoverclusterinstanz – SQL Server on Linux](sql-server-linux-shared-disk-cluster-operate.md).

9.  Schließlich die FCI wieder auf den ursprünglichen Knoten fehl, und entfernen Sie die Zusammenstellung-Einschränkung.

<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
-->
## <a name="summary"></a>Zusammenfassung

In diesem Lernprogramm Sie die folgenden Aufgaben abgeschlossen.

> [!div class="checklist"]
> * Einrichten und Konfigurieren von Linux
> * Installieren und Konfigurieren von SQL Server
> * Konfigurieren Sie die Hosts-Datei
> * Konfigurieren von freigegebenen Speicher und Verschieben von Datenbankdateien
> * Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher
> * Konfigurieren der Failoverclusterinstanz

## <a name="next-steps"></a>Nächste Schritte

- [Failoverclusterinstanz – SQL Server on Linux Betrieb](sql-server-linux-shared-disk-cluster-operate.md)

<!--Image references-->
