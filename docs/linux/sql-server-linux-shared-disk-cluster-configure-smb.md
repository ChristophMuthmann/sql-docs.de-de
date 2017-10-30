---
title: Konfigurieren von Failover Instanz Clusterspeicher SMB - SQL Server on Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: c32c0593df6b40cc76ecafaabc0571090f2907fa
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="configure-failover-cluster-instance---smb---sql-server-on-linux"></a>Konfigurieren der Failover-Clusterinstanz - SMB - SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Artikel erläutert die SMB-Speicher für eine Failoverclusterinstanz (FCI) unter Linux konfigurieren. 
 
In der nicht-Windows-Welt SMB häufig zum Freigeben von als ein Common Internet File System (CIFS) bezeichnet und über Samba implementiert. In der Windows-Welt, den Zugriff auf eine SMB-Freigabe erfolgt auf diese Weise: \\Servername\Freigabename. Für Linux-basierte SQL Server-Installationen muss die SMB-Freigabe als Ordner bereitgestellt werden.

## <a name="important-source-and-server-information"></a>Wichtige Informationen für Quell- und server

Hier sind einige Tipps und Hinweise für die Verwendung von SMB erfolgreich:
- Die SMB-Freigabe kann unter Windows, Linux oder sogar von einer Einheit als lange, wie das SMB 3.0 verwendet wird oder höher sein. Weitere Informationen zu Samba und SMB 3.0, finden Sie unter [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) um festzustellen, ob die Samba-Implementierung mit SMB 3.0 kompatibel ist.
- Die SMB-Freigabe sollte hoch verfügbar sein.
- Sicherheit muss festgelegt werden, ordnungsgemäß auf die SMB-Freigabe. Folgt ein Beispiel von /etc/samba/smb.conf, wobei SQLData1 der Name der Freigabe ist.

![05 smbsource][1]

## <a name="instructions"></a>Instructions

1.  Wählen Sie einen der Server, die einbezogen werden in der FCI-Konfiguration aus. Welche spielt es keine Rolle.

2.  Abrufen von Informationen zu der Mssql-Benutzer.

    ```bash
    sudo id mssql
    ```
    
    Beachten Sie die Uid, Gid und Gruppen. 

3. Führen Sie `sudo smbclient -L //NameOrIP/ShareName -U User`.

    \<NameOrIP > der DNS-Name oder IP-Adresse des Servers mit der SMB-Freigabe.

    \<Freigabename > ist der Name der SMB-Freigabe. 

4. System-Datenbanken oder alle Daten in den Standardspeicherort der Daten gespeichert werden. Gehen Sie folgendermaßen vor. Andernfalls fahren Sie mit Schritt 5 fort. 

   *    Stellen Sie sicher, dass SQL Server auf dem Server beendet wurde, an dem Sie arbeiten.
    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Wechseln Sie vollständig in der Superuser sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    sudo -i
    ```

   *    Wechseln Sie zu der Mssql-Benutzer sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    su mssql
    ```

   *    Erstellen Sie ein temporäres Verzeichnis zum Speichern von SQL Server-Daten und Protokolldateien an. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    mkdir <TempDir>
    ```

    <TempDir>ist der Name des Ordners. Das folgende Beispiel erstellt einen Ordner namens /var/opt/mssql/tmp.

    ```bash
    mkdir /var/opt/mssql/tmp
    ```

   *    Kopieren Sie die SQL Server-Daten und Protokolldateien-Dateien in das temporäre Verzeichnis. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<"TempDir" > der Name des Ordners aus dem vorherigen Schritt.
    
   *    Stellen Sie sicher, dass die Dateien im Verzeichnis sind.

    ```bash
    ls <TempDir>
    ```

    \<"TempDir" > der Name des Ordners aus Schritt d fort.
    
   *    Löschen Sie die Dateien aus dem vorhandenen SQL Server-Datenverzeichnis. Sie erhalten Bestätigung nicht im Erfolgsfall.
 
    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    Stellen Sie sicher, dass die Dateien gelöscht wurden. 

    ```bash
    ls /var/opt/mssql/data
    ```
 
   *    Geben Sie beenden, wechseln Sie zurück an den Root-Benutzer.

   *    Stellen Sie die SMB-Freigabe in der SQL Server-Datenordner bereit. Sie erhalten Bestätigung nicht im Erfolgsfall. Dieses Beispiel zeigt die Syntax für das Herstellen einer Verbindung mit einem Windows Server-basierten SMB 3.0-Freigabe.

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<ServerName > der Name des Servers mit der SMB-Freigabe
    
    \<Freigabename > ist der Name der Freigabe

    \<Benutzername > ist der Name des Benutzers, der auf die Freigabe zugreifen

    \<Kennwort > ist das Kennwort für den Benutzer

    \<Domäne > ist der Name des Active Directory

    \<MssqlUID > ist die UID der Mssql-Benutzer 
 
    \<MssqlGID > ist die GID des Benutzers Mssql
 
   *    Überprüfen Sie feststellen, ob die Bereitstellung erfolgreich war, durch das Ausgeben von Mount ohne Schalter.

    ```bash
    mount
    ```
 
   *    Wechseln Sie zu der Mssql-Benutzer. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    su mssql
    ```

   *    Kopieren Sie die Dateien aus dem temporären Verzeichnis /var/opt/mssql/data. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    cp /var/opt/mssql/tmp/* /var/opt/mssql/data
    ```

   *    Stellen Sie sicher, dass die Dateien vorhanden sind.

    ```bash
    ls /var/opt/mssql/data
    ```

   *    Geben Sie beenden, um nicht mssql 

   *    Geben Sie beenden, um den Stamm nicht sein.

   *    Starten Sie SqlServer. Wenn alles ordnungsgemäß kopiert wurde und angewendeten Sicherheitsfunktionen ordnungsgemäß, SQL Server sollte als gestartet.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```
 
   *    Um weitere zu testen, erstellen Sie eine Datenbank, um sicherzustellen, dass die Berechtigungen Ordnung sind. Das folgende Beispiel verwendet Transact-SQL. Sie können SSMS verwenden.

    ![10_testcreatedb][2] 
  
   *    Beenden von SQL Server, und stellen Sie sicher, dass er heruntergefahren ist. Wenn Sie zum Hinzufügen oder anderen Datenträgern testen möchten, führen Sie nicht heruntergefahren Sie SQL Server, bis die hinzugefügt und getestet werden.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```

   *    Nur, wenn Sie fertig sind, hängen Sie die Freigabe ein. Wenn dies nicht der Fall ist, Aufheben der Bereitstellung nach Abschluss der Tests / weitere Datenträger hinzugefügt.

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
    ```

    \<IPAddressOrServerName > ist die IP-Adresse oder den Namen des SMB-Hosts

    \<Freigabename > ist der Name der Freigabe
    
    \<FolderMountedIn > ist der Name des Ordners, von dem SMB bereitgestellt wird,

5.  Für Elemente, die als Systemdatenbanken, z. B. Benutzerdatenbanken oder Sicherungen die folgenden Schritte aus. Wenn Sie nur den Standardspeicherort zu verwenden, fahren Sie mit Schritt 14.
    
   *    Wechseln Sie zu der Superuser sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    sudo -i
    ```
    
   *    Erstellen Sie einen Ordner, der von SQL Server verwendet wird. 

    ```bash
    mkdir <FolderName>
    ```

    \<Ordnername > ist der Name des Ordners. Vollständiger Pfad des Ordners müssen angegeben werden, sofern Sie nicht den richtigen Speicherort. Das folgende Beispiel erstellt einen Ordner namens /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Stellen Sie die SMB-Freigabe in der SQL Server-Datenordner bereit. Sie erhalten Bestätigung nicht im Erfolgsfall. Dieses Beispiel zeigt die Syntax für das Herstellen einer Verbindung mit einem Samba-basierte SMB 3.0-Freigabe.

    ```bash
    Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
    ```

    \<ServerName > der Name des Servers mit der SMB-Freigabe

    \<Freigabename > ist der Name der Freigabe

    \<Ordnername > ist der Name des im letzten Schritt erstellten Ordners  

    \<Benutzername > ist der Name des Benutzers, der auf die Freigabe zugreifen

    \<Kennwort > ist das Kennwort für den Benutzer

    \<MssqlUID > ist die UID der Mssql-Benutzer

    \<MssqlGID > ist die GID des Benutzers Mssql.
 
   * Überprüfen Sie feststellen, ob die Bereitstellung erfolgreich war, durch das Ausgeben von Mount ohne Schalter.
 
   * Geben Sie Exit nicht mehr der Superuser sein.

   * Um zu testen, erstellen Sie eine Datenbank in diesem Ordner. Im Beispiel unten verwendet Sqlcmd, erstellen Sie eine Datenbank, den Kontext zu wechseln, vergewissern Sie sich die Dateien vorhanden sind, auf der Betriebssystemebene und löscht dann das temporäre Verzeichnis. Sie können SSMS verwenden.
 
   * Heben Sie die Bereitstellung der Freigabe 

    ```bash
    sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
    ```
    
    \<IPAddressOrServerName > ist die IP-Adresse oder den Namen des SMB-Hosts
 
    \<Freigabename > ist der Name der Freigabe
 
    \<FolderMountedIn > ist der Name des Ordners, von dem SMB bereitgestellt wird.
 
6.  Wiederholen Sie die Schritte für die anderen Knoten aus.

Sie können nun die FCI konfigurieren.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Failoverclusterinstanz – SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 

