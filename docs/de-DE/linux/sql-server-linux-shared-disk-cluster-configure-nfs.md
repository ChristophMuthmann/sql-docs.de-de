---
title: Konfigurieren von Failover Instanz Clusterspeicher NFS - SQL Server on Linux | Microsoft Docs
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
ms.openlocfilehash: ddfc1b8546c97e8883730212300c331ed085b476
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-failover-cluster-instance---nfs---sql-server-on-linux"></a>Konfigurieren Sie Failoverclusterinstanz – NFS - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dieser Artikel beschreibt, wie Sie NFS-Speicher für eine Failoverclusterinstanz (FCI) unter Linux konfigurieren. 

NFS oder NFS, ist eine gängige Methode für die Datenträger in Linux weltweit, aber nicht die Windows eine Freigabe auf. Ähnlich wie iSCSI können NFS auf einem Server oder irgendeine Appliance oder Storage-Einheit konfiguriert werden solange sie die speicheranforderungen für SQL Server erfüllt.

## <a name="important-nfs-server-information"></a>Wichtige Informationen der NFS-server

Die Quelle hosting NFS (einem Linux-Server oder ein anderes Element) muss mithilfe von/kompatibel mit Version 4.2 oder höher sein. Frühere Versionen funktioniert nicht mit SQL Server on Linux.

Wenn Sie die Dateien auf dem NFS-Server freigegeben werden zu konfigurieren, stellen Sie sicher, dass sie diese Richtlinien allgemeine Optionen entsprechen:
- `rw` um sicherzustellen, dass den Ordner können von gelesen und geschrieben werden
- `sync` um sicherzustellen, dass sichergestellt, dass Schreibvorgänge in den Ordner
- Verwenden Sie keine `no_root_squash` optional; gilt ein Sicherheitsrisiko
- Stellen Sie sicher, dass der Ordner Vollzugriff (777) angewendet wurde

Stellen Sie sicher, dass für den Zugriff auf Ihre Sicherheitsstandards erzwungen werden. Wenn Sie den Ordner konfigurieren, stellen Sie sicher, dass nur die Server, die in der FCI Einbeziehung den NFS-Ordner einsehen. Ein Beispiel für eine geänderte/etc/Exports auf einer Linux-basierten NFS-Lösung ist unten, in dem der Ordner auf FCIN1 und FCIN2 beschränkt ist.

![05 nfsacl][1]

## <a name="instructions"></a>Instructions

1. Wählen Sie einen der Server, die einbezogen werden in der FCI-Konfiguration aus. Welche spielt es keine Rolle. 

2. Überprüfen Sie sich, dass der Server die Mount(s) auf dem NFS-Server angezeigt werden.

    ```bash
    sudo showmount -e <IPAddressOfNFSServer>
    ```

    \<IPAddressOfNFSServer > die IP-Adresse des NFS-Servers, die Sie verwenden möchten.

3. Für Systemdatenbanken oder alle Daten in den Standardspeicherort der Daten gespeichert werden die folgenden Schritte aus. Andernfalls fahren Sie mit Schritt 4.
 
   * Stellen Sie sicher, dass SQL Server auf dem Server beendet wurde, an dem Sie arbeiten.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
   * Wechseln Sie vollständig in der Superuser sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    sudo -i
    ```

   * Wechseln Sie zu der Mssql-Benutzer sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    su mssql
    ```

   * Erstellen Sie ein temporäres Verzeichnis zum Speichern von SQL Server-Daten und Protokolldateien an. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    mkdir <TempDir>
    ```

    \<"TempDir" > der Name des Ordners. Das folgende Beispiel erstellt einen Ordner namens /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   * Kopieren Sie die SQL Server-Daten und Protokolldateien-Dateien in das temporäre Verzeichnis. Sie erhalten Bestätigung nicht im Erfolgsfall.
    
    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<"TempDir" > der Name des Ordners aus dem vorherigen Schritt.

   * Stellen Sie sicher, dass die Dateien im Verzeichnis sind.

    ```bash
    ls TempDir
    ```

    \<"TempDir" > der Name des Ordners aus Schritt d fort.

   * Löschen Sie die Dateien aus dem vorhandenen SQL Server-Datenverzeichnis. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   * Stellen Sie sicher, dass die Dateien gelöscht wurden. 

    ```bash
    ls /var/opt/mssql/data
    ```
    
   * Geben Sie beenden, wechseln Sie zurück an den Root-Benutzer.

   * Stellen Sie die NFS-Freigabe in der SQL Server-Datenordner bereit. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > die IP-Adresse des NFS-Servers, die Sie verwenden möchten 

    \<FolderOnNFSServer > ist der Name der NFS-Freigabe. Die folgende Beispielsyntax entspricht die NFS-Informationen aus Schritt2.

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci1 /var/opt/mssql/data -o nfsvers=4.2,timeo=14,intr
    ```

   * Überprüfen Sie feststellen, ob die Bereitstellung erfolgreich war, durch das Ausgeben von Mount ohne Schalter.

    ```bash
    mount
    ```

    ![10 mountnoswitches][2]

   * Wechseln Sie zu der Mssql-Benutzer. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    su mssql
    ```

   * Kopieren Sie die Dateien aus dem temporären Verzeichnis /var/opt/mssql/data. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssqldata
    ```

   * Stellen Sie sicher, dass die Dateien vorhanden sind.

    ```bash
    ls /var/opt/mssql/data
    ```

   * Geben Sie beenden, um nicht mssql 
    
   * Geben Sie beenden, um den Stamm nicht sein.

   * Starten Sie SqlServer. Wenn alles ordnungsgemäß kopiert wurde und angewendeten Sicherheitsfunktionen ordnungsgemäß, SQL Server sollte als gestartet.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
    
   * Erstellen Sie eine Datenbank, um zu testen, ob die Sicherheit ordnungsgemäß eingerichtet ist. Im folgende Beispiel wird gezeigt, die über Transact-SQL ausgeführt wird: Sie können über SSMS erfolgen.
 
    ![CreateTestdatabase][3]

   * Beenden von SQL Server, und stellen Sie sicher, dass er heruntergefahren ist.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   * Wenn Sie keine NFS-Mounts erstellen, heben Sie die Bereitstellung der Freigabe. Wenn Sie sich befinden, nicht aufheben der Bereitstellung.

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > die IP-Adresse des NFS-Servers, die Sie verwenden möchten

    \<FolderOnNFSServer > ist der Name der NFS-Freigabe

    \<FolderMountedIn > ist der Ordner, der im vorherigen Schritt erstellt haben. 

4. Für Elemente, die als Systemdatenbanken, z. B. Benutzerdatenbanken oder Sicherungen die folgenden Schritte aus. Wenn Sie nur den Standardspeicherort zu verwenden, fahren Sie mit Schritt 5 fort.

   * Wechseln Sie zu der Superuser sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    sudo -i
    ```

   * Erstellen Sie einen Ordner, der von SQL Server verwendet wird. 

    ```bash
    mkdir <FolderName>
    ```

    \<Ordnername > ist der Name des Ordners. Vollständigen Ordnerpfad muss angegeben werden, sofern Sie nicht den richtigen Speicherort. Das folgende Beispiel erstellt einen Ordner namens /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   * Laden Sie die NFS-Freigabe, in dem Ordner, der im vorherigen Schritt erstellt wurde. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    Mount -t nfs4 <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn> -o nfsvers=4.2,timeo=14,intr
    ```

    \<IPAddressOfNFSServer > die IP-Adresse des NFS-Servers, die Sie verwenden möchten

    \<FolderOnNFSServer > ist der Name der NFS-Freigabe

    \<FolderToMountIn > ist der Ordner, der im vorherigen Schritt erstellt haben. Im folgenden ist ein Beispiel. 

    ```bash
    mount -t nfs4 200.201.202.63:/var/nfs/fci2 /var/opt/mssql/userdata -o nfsvers=4.2,timeo=14,intr
    ```

   * Überprüfen Sie feststellen, ob die Bereitstellung erfolgreich war, durch das Ausgeben von Mount ohne Schalter.
  
   * Geben Sie Exit nicht mehr der Superuser sein.

   * Um zu testen, erstellen Sie eine Datenbank in diesem Ordner. Im folgenden Beispiel wird Sqlcmd, erstellen Sie eine Datenbank, den Kontext zu wechseln, vergewissern Sie sich die Dateien vorhanden sind, auf der Betriebssystemebene und löscht dann das temporäre Verzeichnis. Sie können SSMS verwenden.

    ![15 createtestdatabase][4]
 
   * Heben Sie die Bereitstellung der Freigabe 

    ```bash
    sudo umount <IPAddressOfNFSServer>:<FolderOnNFSServer> <FolderToMountIn>
    ```

    \<IPAddressOfNFSServer > die IP-Adresse des NFS-Servers, die Sie verwenden möchten
    
    \<FolderOnNFSServer > ist der Name der NFS-Freigabe

    \<FolderMountedIn > ist der Ordner, der im vorherigen Schritt erstellt haben. Im folgenden ist ein Beispiel. 
 
5. Wiederholen Sie die Schritte für die anderen Knoten aus.


## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Failoverclusterinstanz – SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/05-nfsacl.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/10-mountnoswitches.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/20-createtestdatabase.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-nfs/15-createtestdatabase.png
