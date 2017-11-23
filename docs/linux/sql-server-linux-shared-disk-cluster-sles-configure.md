---
title: "SLES freigegebene Datenträgercluster für SQL Server konfigurieren | Microsoft Docs"
description: "SUSE Linux Enterprise Server (SLES) freigegebene Datenträgercluster für SQL Server konfigurieren, um hohe Verfügbarkeit zu implementieren."
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
ms.assetid: e5ad1bdd-c054-4999-a5aa-00e74770b481
ms.workload: Inactive
ms.openlocfilehash: f5c51b405d3c3eaca081abfddd1b770e4b9a8559
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="configure-sles-shared-disk-cluster-for-sql-server"></a>SLES freigegebene Datenträgercluster für SQL Server konfigurieren

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Dieses Handbuch enthält Anweisungen, um eine freigegebene Datenträgercluster zwei Knoten für SQL Server auf SUSE Linux Enterprise Server (SLES) zu erstellen. Die clustering-Ebene basiert auf SUSE [hohe Verfügbarkeit Erweiterung (HAE)](https://www.suse.com/products/highavailability) baut auf [Schrittmacher](http://clusterlabs.org/). 

Weitere Informationen zur Clusterkonfiguration, Ressourcenoptionen-Agent, Management, best Practices und Empfehlungen, finden Sie unter [SUSE Linux Enterprise hohe Verfügbarkeit Erweiterung 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

## <a name="prerequisites"></a>Erforderliche Komponenten

Zum Abschließen der End-to-End-Szenarios unten benötigen Sie zwei Computer zum Bereitstellen der zwei Knoten-Cluster und einem anderen Server so konfigurieren Sie die NFS-Freigabe. Unten aufgeführten Schritten dargestellt, wie diesen Servern konfiguriert werden kann.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Richten Sie ein und konfigurieren Sie des Betriebssystems auf allen Clusterknoten

Der erste Schritt ist so konfigurieren Sie das Betriebssystem auf den Clusterknoten. Verwenden Sie für diese Gang durch SLES mit einem gültigen Abonnement für das Add-on für hohe Verfügbarkeit.

## <a name="install-and-configure-sql-server-on-each-cluster-node"></a>Installieren und Konfigurieren von SQL Server auf jedem Clusterknoten

1. Installieren und Einrichten von SQL Server auf beiden Knoten. Ausführliche Anweisungen finden Sie unter [Installieren von SQL Server on Linux](sql-server-linux-setup.md).
2. Festlegen Sie ein Knoten als primärer und der andere als sekundärer, zum Zweck der Konfiguration. Verwenden Sie diese Begriffe für die folgenden dieses Handbuchs. 
3. Beenden und Deaktivieren von SQL Server, auf dem sekundären Knoten. Im folgenden Beispiel wird beendet und deaktiviert SQL Server:

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl disable mssql-server
    ```

    > [!NOTE]
    > Beim Setup eine Server-Hauptschlüssel für die SQL Server-Instanz generiert und an platziert `/var/opt/mssql/secrets/machine-key`. Unter Linux wird SQL Server immer ausgeführt, als ein lokales Konto Mssql aufgerufen werden. Da es sich um ein lokales Konto handelt, wird nicht seine Identität Knoten gemeinsam verwendet. Aus diesem Grund müssen Sie den Verschlüsselungsschlüssel primären Knoten für jeden sekundären Knoten kopieren, damit jedes lokale Mssql-Konto, um den Server-Hauptschlüssel entschlüsseln zugreifen kann.
4. Klicken Sie auf dem primären Knoten, erstellen Sie eine SQL Server-Anmeldung für Schrittmacher, und erteilen Sie die Login-Berechtigung zum Ausführen `sp_server_diagnostics`. Schrittmacher wird dieses Konto verwendet, um zu überprüfen, welcher Knoten auf SQL Server ausgeführt wird.

    ```bash
    sudo systemctl start mssql-server
    ```
    Herstellen einer Verbindung mit der master-Datenbank von SQL Server mit dem Konto'sa', und führen Sie Folgendes aus:

    ```tsql
    USE [master]
    GO
    CREATE LOGIN [<loginName>] with PASSWORD= N'<loginPassword>'
    GRANT VIEW SERVER STATE TO <loginName>
    ```
5. Beenden und Deaktivieren von SQL Server, auf dem primären Knoten.
6. Befolgen Sie die Anweisungen [in der Dokumentation für die SUSE](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) konfigurieren und die Hosts-Datei für jeden Clusterknoten zu aktualisieren. Die Datei 'Hosts' muss die IP-Adresse und die Namen aller Clusterknoten enthalten.

    So überprüfen Sie die IP-Adresse des aktuellen Knotens ausführen

    ```bash
    sudo ip addr show
    ```

    Legen Sie den Computernamen auf jedem Knoten ein. Geben Sie jeden Knoten einen eindeutigen Namen, der 15 Zeichen oder weniger. Legen Sie die Computernamen durch Hinzufügen zu `/etc/hostname` mit [Yast](https://www.suse.com/documentation/sles11/book_sle_admin/data/sec_basicnet_yast.html) oder [manuell](https://www.suse.com/documentation/sled11/book_sle_admin/data/sec_basicnet_manconf.html).

    Das folgende Beispiel zeigt `/etc/hosts` mit Ergänzungen für zwei Knoten mit dem Namen `SLES1` und `SLES2`.

    ```
    127.0.0.1   localhost
    10.128.18.128 SLES1
    10.128.16.77 SLES2
    ```

    > [!NOTE]
    > Alle Clusterknoten müssen über SSH, aufeinander zugreifen können. Tools wie „hb_report“ oder „crm_report“ (zur Problembehandlung) und Hawk's History Explorer erfordern kennwortlosen SSH-Zugriff zwischen den Knoten, andernfalls können sie nur Daten vom aktuellen Knoten sammeln. Für den Fall, dass Sie einen nicht standardmäßigen SSH-Port verwenden, verwenden Sie die Option-X ([finden Sie unter Seite Man](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)). Wenn der SSH-Port 3479 ist, rufen Sie z. B. eine Crm_report mit:
    >
    >```bash
    >crm_report -X "-p 3479" [...]
    >```
    >Weitere Informationen finden Sie unter [Administratorhandbuch]. (https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc)

Im nächsten Abschnitt Konfigurieren freigegebenen Speicher und die Datenbankdateien an, dass Speicher verschieben.  

## <a name="configure-shared-storage-and-move-database-files"></a>Konfigurieren von freigegebenen Speicher und Verschieben von Datenbankdateien

Es gibt eine Vielzahl von Lösungen für das Bereitstellen von freigegebenen Speichers. Diese exemplarische Vorgehensweise wird das Konfigurieren von freigegebenen Speicher mit NFS. Es wird empfohlen, bewährte Methoden befolgen und Kerberos verwenden, um NFS zu schützen: 

- [Freigeben von Dateisystemen für NFS](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.nfs)

Wenn Sie nicht in dieser Anleitung befolgen, werden Personen Zugriff auf Ihr Netzwerk und die IP-Adresse eines SQL-Knotens zu spoofen können auf die Datendateien zugreifen. Wie immer, stellen Sie sicher, dass Sie Bedrohungsmodells für Ihr System vor der Verwendung in der Produktion. 

Eine andere Speicheroption ist die Verwendung von SMB-Dateifreigabe:

- [Samba-Abschnitt der Dokumentation zu SUSE](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#cha.samba)

### <a name="configure-an-nfs-server"></a>Konfigurieren von einem NFS-server

Um einem NFS-Server zu konfigurieren, finden Sie in die folgenden Schritte aus, in der Dokumentation für die SUSE: [Konfigurieren von NFS-Server](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-server).

### <a name="configure-all-cluster-nodes-to-connect-to-the-nfs-shared-storage"></a>Konfigurieren Sie alle Knoten des Clusters für die Verbindung mit dem freigegebenen NFS-Speicher

Vor dem Konfigurieren des Clients NFS zum Bereitstellen von Dateien Pfad des SQL Server-Datenbank, zeigen Sie auf den freigegebenen Speicherort, stellen Sie sicher, dass Sie die Datenbankdateien an einem temporären Speicherort, damit diese später auf die Freigabe kopieren werden speichern:

1. **Auf dem primären Knoten nur**, die Datenbankdateien an einem temporären Speicherort speichern. Das folgende Skript erstellt ein neues temporäres Verzeichnis, die Datenbankdateien in das neue Verzeichnis kopiert und die alten Datenbankdateien entfernt. Wie SQL Server als lokaler Benutzer Mssql ausgeführt wird, müssen Sie sicherstellen, dass nach der Datenübertragung an den bereitgestellten Freigabe lokaler Benutzer Lese-/ Schreibzugriff auf die Freigabe verfügt. 

    ```bash
    su mssql
    mkdir /var/opt/mssql/tmp
    cp /var/opt/mssql/data/* /var/opt/mssql/tmp
    rm /var/opt/mssql/data/*
    exit
    ```

    Konfigurieren des NFS-Clients auf allen Knoten im Cluster:

    - [Konfigurieren von Clients](https://www.suse.com/documentation/sles-12/singlehtml/book_sle_admin/book_sle_admin.html#sec.nfs.configuring-nfs-clients)

    > [!NOTE]
    > Es wird empfohlen, führen die SUSE best Practices und Empfehlungen bezüglich der hoch verfügbare NFS-Speicher: [hoch verfügbarer NFS-Speicher mit DRBD und Schrittmacher](https://www.suse.com/documentation/sle-ha-12/book_sleha_techguides/data/art_ha_quick_nfs.html).

2. Überprüfen Sie, dass SQL Server erfolgreich mit dem neuen Dateipfad gestartet wird. Hierzu auf jedem Knoten. An diesem Punkt sollte nur ein Knoten SQL Server zu einem Zeitpunkt ausführen. Sie können nicht beide zur gleichen Zeit ausgeführt werden, da sie beide versucht, Zugriff auf die Datendateien gleichzeitig (aus, um zu vermeiden, versehentlich Starten von SQL Server auf beiden Knoten, eine Dateisystem-Clusterressource verwenden, um sicherzustellen, dass die Freigabe nicht zweimal von der verschiedenen Knoten bereitgestellt ist). Die folgenden Befehle Starten von SQL Server, überprüfen Sie den Status und beenden Sie SQL Server.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    sudo systemctl stop mssql-server
    ```

Zu diesem Zeitpunkt sind beide SQL Server-Instanzen mit Datenbankdateien auf den freigegebenen Speicher Ausführung konfiguriert. Der nächste Schritt ist so konfigurieren Sie SQL Server für Schrittmacher. 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Installieren Sie und konfigurieren Sie auf jedem Clusterknoten Schrittmacher

1. **Erstellen Sie auf beiden Clusterknoten eine Datei zum Speichern von Benutzername und Kennwort für SQL Server für die Pacemaker-Anmeldung**. Der folgende Code erstellt und füllt diese Tabelle:

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **Alle Clusterknoten müssen in der Lage sein, über SSH aufeinander zugreifen**. Tools wie „hb_report“ oder „crm_report“ (zur Problembehandlung) und Hawk's History Explorer erfordern kennwortlosen SSH-Zugriff zwischen den Knoten, andernfalls können sie nur Daten vom aktuellen Knoten sammeln. Falls Sie keinen nicht-standardmäßigen SSH-Port verwenden, nutzen Sie die Option „-X“ (siehe Hauptseite). Wenn Ihr SSH-Port z.B. 3479 ist, rufen Sie hb_report mit Folgendem auf:

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    Weitere Informationen finden Sie unter [System Requirements and Recommendations in the SUSE documentation (Systemanforderungen und Empfehlungen in der SUSE-Dokumentation)](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html).

3. **Installieren Sie die Erweiterung für hohe Verfügbarkeit**. Um die Erweiterung zu installieren, befolgen Sie die Schritte im folgenden SUSE-Thema:
    
    [Installation and Setup Quick Start (Installation und Setup – Schnellstart)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **Installieren Sie den FCI-Ressourcenagent für SQL Server**. Führen Sie die folgenden Befehle auf beiden Knoten aus:

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **Richten Sie den ersten Knoten automatisch ein**. Im nächsten Schritt wird ein ausgeführter Cluster mit einem Noten durch Konfigurieren des ersten Knotens, SLES1, eingerichtet. Befolgen Sie den Anweisungen im SUSE-Thema [Setting Up the First Node (Einrichten des ersten Knotens)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node).

    Abschließend überprüfen Sie den Status des Clusters mit `crm status`:
    ```bash
    crm status
    ```

    Es sollte angezeigt werden, dass ein Knoten, SLES1, konfiguriert wurde.

6. **Hinzufügen von Knoten zu einem vorhandenen Cluster**. Als Nächstes fügen Sie den SLES2-Knoten dem Cluster hinzu. Befolgen Sie den Anweisungen im SUSE-Thema [Adding the Second Node (Hinzufügen des zweiten Knotens)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node).
    
    Abschließend überprüfen Sie den Status des Clusters mit **crm status**. Wenn Sie einen zweiten Knoten erfolgreich hinzugefügt haben, sieht die Ausgabe ähnlich der folgenden aus:
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** ist die virtuelle IP-Clusterressource, die während der anfänglichen Einrichtung des Clusters mit einem Knoten konfiguriert wird.

7.  **Vorgehensweisen zum Entfernen**. Wenn Sie einen Knoten aus dem Cluster entfernen möchten, verwenden Sie das Bootstrap-Skript **ha-cluster-remove**. Weitere Informationen finden Sie unter [Overview of the Bootstrap Scripts (Übersicht über die Bootstrap-Skripts)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap).  

## <a name="configure-the-cluster-resources-for-sql-server"></a>Konfigurieren Sie die Clusterressourcen für SQL Server

Die folgenden Schritte erläutern, wie die Clusterressource für SQL Server zu konfigurieren. Es gibt zwei Einstellungen, die Sie anpassen möchten.

- **SQL Server-Ressourcenname**: einen Namen für die SQL Server-Clusterressource. 
- **Timeoutwert**: Wert für das Timeout ist die Zeitspanne, die der Cluster wartet, während eine Ressource online geschaltet wird. Für SQL Server, ist dies die Zeit, die Sie erwarten, SQL Server dass auszuführenden schalten Sie die `master` -Datenbank online geschaltet. 

Aktualisieren Sie die Werte aus dem Skript unten für Ihre Umgebung. Führen Sie auf einem Knoten zu konfigurieren und starten Sie den Clusterdienst.

```bash
sudo crm configure
primitive <sqlServerResourceName> ocf:mssql:fci op start timeout=<timeout_in_seconds>
colocation <constraintName> inf: <virtualIPResourceName> <sqlServerResourceName>
show
commit
exit
```

Das folgende Skript erstellt z. B. eine gruppierten SQL Server-Ressource, die mit dem Namen Mssqlha. 

```bash
sudo crm configure
primitive mssqlha ocf:mssql:fci op start timeout=60s
colocation admin_addr_mssqlha inf: admin_addr mssqlha
show
commit
exit
```

Nach die Konfiguration ein Commit ausgeführt wurde, wird SQL Server auf demselben Knoten wie die virtuelle IP-Adressressource gestartet. 

Weitere Informationen finden Sie unter [konfigurieren und Verwalten von Clusterressourcen (Befehlszeile)](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config). 

### <a name="verify-that-sql-server-is-started"></a>Stellen Sie sicher, dass SQL Server gestartet wurde. 

Um sicherzustellen, dass SQL Server gestartet wird, führen Sie die **Crm Status** Befehl:

```bash
crm status
```

In den folgenden Beispielen werden die Ergebnisse auf, wenn Schrittmacher als geclusterte Ressource erfolgreich gestartet wurde. 
```
2 nodes configured
2 resources configured

Online: [ SLES1 SLES2 ]

Full list of resources:

 admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
 mssqlha        (ocf::mssql:fci):       Started SLES1
```

## <a name="managing-cluster-resources"></a>Verwalten von Clusterressourcen

Um Ihre Clusterressourcen zu verwalten, finden Sie unter folgendem Thema SUSE: [Clusterressourcen verwalten](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm )

### <a name="manual-failover"></a>Manuelles Failover

Obwohl Ressourcen konfiguriert sind automatisch ein Failover (oder migrieren), auf andere Knoten des Clusters im Fall eines Hardware- oder Software, können Sie auch manuell eine Ressource auf einen anderen Knoten im Cluster unter Verwendung der GUI Schrittmacher oder der Befehlszeile verschieben. 

Verwenden des Befehls zum Migrieren für diese Aufgabe. Beispielsweise Informationen zum Migrieren der SQL-Ressource auf einem Cluster Knotennamen SLES2 ausführen: 

```bash
crm resource
migrate mssqlha SLES2
```

## <a name="additional-resources"></a>Weitere Ressourcen

[SUSE Linux Enterprise hohe Verfügbarkeit Erweiterung – Administratorhandbuch](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html) 
