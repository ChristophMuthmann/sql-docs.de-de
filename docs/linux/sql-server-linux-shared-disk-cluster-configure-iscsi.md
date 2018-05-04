---
title: Konfigurieren von Failover Cluster Instanz Speicher iSCSI - SQL Server on Linux | Microsoft Docs
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
ms.openlocfilehash: d3b1fa90c6112247c88b9e148bc65c0cef7be0b0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-failover-cluster-instance---iscsi---sql-server-on-linux"></a>Konfigurieren der Failover-Clusterinstanz - iSCSI - SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Artikel erläutert, wie iSCSI-Speicher für eine Failoverclusterinstanz (FCI) unter Linux konfigurieren. 

## <a name="configure-iscsi"></a>Konfigurieren von iSCSI 
iSCSI verwendet Netzwerk zur Darstellung von Datenträger von einem Server als Ziel zu Servern bekannt. Herstellen einer Verbindung mit dem iSCSI-Ziel Server erfordern, dass ein iSCSI-Initiator konfiguriert ist. Die Datenträger auf dem Ziel werden explizite Berechtigungen erteilt, also nur die Initiatoren, die darauf zugreifen können soll dies tun können. Das Ziel selbst sollte hochverfügbar und zuverlässig sein.

### <a name="important-iscsi-target-information"></a>Informationen zum wichtig iSCSI-Ziel
Obwohl in diesem Abschnitt nicht wird einem iSCSI-Ziel zu konfigurieren abgedeckt wird, da sie speziell für den Typ der Quelle darstellt, das Sie verwenden, stellen Sie sicher, dass die Sicherheit für den Datenträger, die von den Clusterknoten verwendet wird, konfiguriert ist.  

Das Ziel sollte nie auf keinem der FCI Knoten konfiguriert werden, wenn ein Linux-basierte iSCSI-Ziel zu verwenden. ISCSI-Netzwerke sollten von von regulären Netzwerkdatenverkehr für die Quell- und die Clientserver verwendeten getrennt sein, für die Leistung und Verfügbarkeit. Verwendet für den iSCSI-Netzwerke sollte schnell ausgeführt werden. Denken Sie daran, das Netzwerk weist einige Prozessorbandbreite verbrauchen Sie daher entsprechend planen, wenn einen regulären Server verwenden.
Um sicherzustellen, dass die wichtigste ist abgeschlossen auf dem Ziel, dass die Datenträger, die erstellt werden die richtigen Berechtigungen zugewiesen werden, damit nur die Einbeziehung in die FCI Server Zugriff darauf haben. Ein Beispiel ist unten dargestellt, aus dem Microsoft iSCSI-Ziel, wobei linuxnodes1 den Namen erstellt und in diesem Fall sind die IP-Adressen der Knoten zugeordnet, sodass NewFCIDisk1.vhdx erscheint.

![Initiator][1]

### <a name="instructions"></a>Instructions

In diesem Abschnitt wird beschrieben, wie einen iSCSI-Initiator auf den Servern zu konfigurieren, das als Knoten für die FCI fungieren soll. Auf RHEL und Ubuntu ausgeführt wird, sollte die Anweisungen funktionieren.

Weitere Informationen zu iSCSI-Initiator zu den unterstützten-Verteilungen finden Sie in den folgenden Links:
- [Red Hat](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/iscsi-api.html)
- [SUSE](http://www.suse.com/documentation/sles11/stor_admin/data/sec_inst_system_iscsi_initiator.html) 
- [Ubuntu](https://help.ubuntu.com/lts/serverguide/iscsi-initiator.html)

1.  Wählen Sie einen der Server, die einbezogen werden in der FCI-Konfiguration aus. Welche spielt es keine Rolle. iSCSI muss auf ein dediziertes Netzwerk so iSCSI zum Erkennen und verwenden dieses Netzwerk konfigurieren. Führen Sie `sudo iscsiadm -m iface -I <iSCSIIfaceName> -o new` , in dem `<iSCSIIfaceName>` ist der eindeutige oder benutzerfreundliche Namen für das Netzwerk. Im folgenden Beispiel wird `iSCSINIC`:
   
    ```bash
    sudo iscsiadm -m iface -I iSCSINIC -o new
    ```
    ![7-setiscsinetwork][6]
 
2.  Bearbeiten Sie `/var/lib/iscsi/ifaces/iSCSIIfaceName`. Stellen Sie sicher, dass sie die folgenden Werte, die vollständig ausgefüllt hat:

    - iface.net_ifacename ist der Name der Netzwerkkarte, wie in der das Betriebssystem dargestellt.
    - iface.hwaddress ist die MAC-Adresse, der den eindeutigen Namen, der für diese Schnittstelle, die unten erstellt werden soll.
    - iface.IPAddress
    - iface.subnet_Mask 

    Sehen Sie sich folgendes Beispiel an:

    ![iSCSITargetSettings][2]

3.  Suchen Sie das iSCSI-Ziel.

    ```bash
    sudo iscsiadm -m discovery -t sendtargets -I <iSCSINetName> -p <TargetIPAddress>:<TargetPort>
    ```

     \<iSCSINetName > ist der eindeutige/Anzeigenamen für das Netzwerk \<TargetIPAddress > die IP-Adresse des iSCSI-Ziels und \<TargetPort > ist der Port des iSCSI-Ziels. 

    ![iSCSITargetResults][3]

 
4.  Melden Sie sich bei dem Ziel

    ```bash
    sudo iscsiadm -m node -I <iSCSIIfaceName> -p TargetIPAddress -l
    ```

    \<iSCSIIfaceName > ist der eindeutige/Anzeigenamen für das Netzwerk und \<TargetIPAddress > die IP-Adresse des iSCSI-Ziels.

    ![iSCSITargetLogin][4]

5.  Überprüfen Sie, ergibt sich eine Verbindung mit dem iSCSI-Ziel.

    ```bash
    sudo iscsiadm -m session
    ```

    ![iSCSIVerify][5]

 
6.  Überprüfen Sie die angefügte iSCSI-Datenträger

    ```bash
    sudo grep “Attached SCSI” /var/log/messages
    ```
    ![30-iSCSIattachedDisks][7]

7.  Erstellen Sie einen physischen Datenträger, auf dem iSCSI-Datenträger.

    ```bash
    sudo pvcreate /dev/<devicename>
    ```

    \<DeviceName > ist der Name des Geräts aus dem vorherigen Schritt. 

 
8.  Erstellen Sie eine Volumegruppe, auf dem iSCSI-Datenträger. Eine einzelne Volumegruppe zugewiesenen Datenträger sind als ein Pool oder eine Auflistung zu sehen. 

    ```bash
    sudo vgcreate <VolumeGroupName> /dev/devicename
    ```

    \<VolumeGroupName > ist der Name der Volumegruppe und \<Devicename > ist der Name des Geräts aus Schritt 6. 
 
9.  Erstellen Sie und überprüfen Sie der logische Datenträger für den Datenträger.

    ```bash
    sudo lvcreate -Lsize -n <LogicalVolumeName> <VolumeGroupName>
    ```
    
    \<Größe > ist die Größe des Volumes zu erstellen, und kann angegeben werden, mit G (GB), T (Terabytes) usw.,\<LogicalVolumeName > ist der Name des logischen Datenträgers und \<VolumeGroupName > ist der Name der Volumegruppe aus der vorherigen Schritt. 

    Das folgende Beispiel erstellt ein Volume 25GB an.
 
    ![Create25GBVol][10]

10. Führen Sie `sudo lvs` dem LVM anzeigen, die erstellt wurde.
 
11. Der logische Datenträger mit einem unterstützten Dateisystem zu formatieren. Verwenden Sie für EXT4 das folgende Beispiel:

    ```bash
    sudo mkfs.ext4 /dev/<VolumeGroupName>/<LogicalVolumeName>
    ```

    \<VolumeGroupName > ist der Name der Volumegruppe aus dem vorherigen Schritt. \<LogicalVolumeName > ist der Name des logischen Datenträgers aus dem vorherigen Schritt.  

12. Für Systemdatenbanken oder alle Daten in den Standardspeicherort der Daten gespeichert werden die folgenden Schritte aus. Andernfalls fahren Sie mit Schritt 13.

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

    \<"TempDir" > der Name des Ordners. Das folgende Beispiel erstellt einen Ordner namens /var/opt/mssql/TempDir.

    ```bash
    mkdir /var/opt/mssql/TempDir
    ```
    
   *    Kopieren Sie die SQL Server-Daten und Protokolldateien-Dateien in das temporäre Verzeichnis. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    cp /var/opt/mssql/data/* <TempDir>
    ```

    \<"TempDir" > der Name des Ordners aus dem vorherigen Schritt.
    
   *    Stellen Sie sicher, dass die Dateien im Verzeichnis sind.

    ```bash
    ls \<TempDir>
    ```
    \<"TempDir" > der Name des Ordners aus Schritt d fort.

   *    Löschen Sie die Dateien aus dem vorhandenen SQL Server-Datenverzeichnis. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    rm – f /var/opt/mssql/data/*
    ```

   *    Stellen Sie sicher, dass die Dateien gelöscht wurden. Die folgende Abbildung zeigt ein Beispiel für die gesamte Sequenz von c bis h.

    ```bash
    ls /var/opt/mssql/data
    ```

    ![45 CopyMove][8]
 
   *    Typ `exit` So wechseln Sie zurück an den Root-Benutzer.

   *    Stellen Sie das logische iSCSI-Volume in der SQL Server-Datenordner bereit. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> /var/opt/mssql/data
    ``` 

    \<VolumeGroupName > ist der Name der Volumegruppe und \<LogicalVolumeName > ist der Name des logischen Volumes, die erstellt wurde. Die folgende Beispielsyntax entspricht der Volumegruppe und logische Datenträger aus dem vorherigen Befehl.

    ```bash
    mount /dev/FCIDataVG1/FCIDataLV1 /var/opt/mssql/data
    ``` 

   *    Ändern Sie den Besitzer der Bereitstellung in Mssql. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    chown mssql /var/opt/mssql/data
    ```

   *    Ändern Sie den Besitz der Gruppe aus der Bereitstellung in Mssql. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    chgrp mssql /var/opt/mssql/data
    ``` 

   *    Wechseln Sie zu der Mssql-Benutzer. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    su mssql
    ``` 

   *    Kopieren Sie die Dateien aus dem temporären Verzeichnis /var/opt/mssql/data. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    cp /var/opt/mssql/TempDir/* /var/opt/mssql/data
    ``` 

   *    Stellen Sie sicher, dass die Dateien vorhanden sind.

    ```bash
    ls /var/opt/mssql/data
    ``` 
 
   *    Geben Sie `exit` nicht Mssql sein.
    
   *    Geben Sie `exit` kein Stammverzeichnis sein.

   *    Starten Sie SqlServer. Wenn alles ordnungsgemäß kopiert wurde und angewendeten Sicherheitsfunktionen ordnungsgemäß, SQL Server sollte als gestartet.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ``` 
 
   *    Beenden von SQL Server, und stellen Sie sicher, dass er heruntergefahren ist.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ``` 

13. Für Elemente, die als Systemdatenbanken, z. B. Benutzerdatenbanken oder Sicherungen die folgenden Schritte aus. Wenn Sie nur den Standardspeicherort zu verwenden, fahren Sie mit Schritt 14.

   *    Wechseln Sie zu der Superuser sein. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    sudo -i
    ```

   *    Erstellen Sie einen Ordner, der von SQL Server verwendet wird. 

    ```bash
    mkdir <FolderName>
    ```

    \<Ordnername > ist der Name des Ordners. Vollständigen Ordnerpfad muss angegeben werden, sofern Sie nicht den richtigen Speicherort. Das folgende Beispiel erstellt einen Ordner namens /var/opt/mssql/userdata.

    ```bash
    mkdir /var/opt/mssql/userdata
    ```

   *    Laden Sie das logische iSCSI-Volume in den Ordner, der im vorherigen Schritt erstellt wurde. Sie erhalten Bestätigung nicht im Erfolgsfall.
    
    ```bash
    mount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > ist der Name der Volumegruppe, \<LogicalVolumeName > ist der Name des logischen Volumes, die erstellt wurde, und \<FolderName > ist der Name des Ordners. Beispielsyntax ist unten dargestellt.

    ```bash
    mount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

   *    Ändern Sie den Besitz des Ordners zu Mssql erstellt. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    chown mssql <FolderName>
    ```

    \<Ordnername > ist der Name des Ordners, der erstellt wurde. Das folgende Beispiel soll dies erläutern:

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```
  
   *    Ändern Sie die Gruppe des Ordners zu Mssql erstellt. Sie erhalten Bestätigung nicht im Erfolgsfall.

    ```bash
    chown mssql <FolderName>
    ```

    \<Ordnername > ist der Name des Ordners, der erstellt wurde. Das folgende Beispiel soll dies erläutern:

    ```bash
    chown mssql /var/opt/mssql/userdata
    ```

   *    Typ `exit` nicht mehr der Superuser sein.

   *    Um zu testen, erstellen Sie eine Datenbank in diesem Ordner. Im Beispiel unten verwendet Sqlcmd, erstellen Sie eine Datenbank, den Kontext zu wechseln, vergewissern Sie sich die Dateien vorhanden sind, auf der Betriebssystemebene und löscht dann das temporäre Verzeichnis. Sie können SSMS verwenden.
  
    ![50-ExampleCreateSSMS][9]

   *    Heben Sie die Bereitstellung der Freigabe 

    ```bash
    sudo umount /dev/<VolumeGroupName>/<LogicalVolumeName> <FolderName>
    ```

    \<VolumeGroupName > ist der Name der Volumegruppe, \<LogicalVolumeName > ist der Name des logischen Volumes, die erstellt wurde, und \<FolderName > ist der Name des Ordners. Beispielsyntax ist unten dargestellt.

    ```bash
    sudo umount /dev/FCIDataVG2/FCIDataLV2 /var/opt/mssql/userdata 
    ```

14. Konfigurieren Sie den Server aus, damit diese nur Schrittmacher die Volumegruppe aktiviert werden kann.

    ```bash
    sudo lvmconf --enable-halvm --services –startstopservices
    ```
 
15. Generieren Sie eine Liste der Volumegruppen auf dem Server. Elemente aufgeführt, die nicht den iSCSI-Datenträger wird vom System, z. B. für den Betriebssystem-Datenträger verwendet.

    ```bash
    sudo vgs
    ```

16. Ändern Sie den Aktivierung Konfigurationsabschnitt der Datei /etc/lvm/lvm.conf. Konfigurieren Sie die folgende Zeile:

    ```bash
    volume_list = [ <ListOfVGsNotUsedByPacemaker> ]
    ```

    \<ListOfVGsNotUsedByPacemaker > ist die Liste der Volumegruppen aus der Ausgabe von Schritt 20, die nicht von der FCI verwendet werden. Fügen Sie jeweils in Anführungszeichen eingeschlossen und getrennt durch ein Komma. Das folgende Beispiel soll dies erläutern:

    ![55-ListOfVGs][11]
 
 
17. Wenn Sie Linux gestartet wird, wird er im Dateisystem einlegen. Um sicherzustellen, dass nur Schrittmacher des iSCSI-Datenträgers einbinden kann, erstellen Sie das Stamm-Filesystem-Abbild neu. 

    Führen Sie den folgenden Befehl an der Zeit in Anspruch nehmen kann. Sie werden keine Nachricht wieder im Erfolgsfall zurückkehren.

    ```bash
    sudo dracut -H -f /boot/initramfs-$(uname -r).img $(uname -r)
    ```

18. Starten Sie den Server an.

19. Führen Sie auf einem anderen Server, die in der FCI einbezogen werden, die Schritte 1 – 6. Dies stellt das iSCSI-Ziel mit dem SQL Server bereit. 
 
20. Generieren Sie eine Liste der Volumegruppen auf dem Server. Sie sollten die Volumegruppe, die zuvor erstellte anzeigen. 

    ```bash
    sudo vgs
    ``` 
23. Starten Sie SQL Server, und stellen Sie sicher, dass er auf diesem Server gestartet werden kann.

    ```bash
    sudo systemctl start mssql-server
    sudo systemctl status mssql-server
    ```

24. Beenden von SQL Server, und stellen Sie sicher, dass er heruntergefahren wird.

    ```bash
    sudo systemctl stop mssql-server
    sudo systemctl status mssql-server
    ```
25. Wiederholen Sie die Schritte 1 bis 6 auf andere Server, die in der FCI einbezogen werden.

Sie können nun die FCI konfigurieren.

|Distribution |Thema 
|----- |-----
|**Red Hat Enterprise Linux mit HA-Add-On** |[Konfigurieren](sql-server-linux-shared-disk-cluster-configure.md)<br/>[Operate (Ausführen)](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server mit HA-Add-On** |[Konfigurieren](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren Sie Failoverclusterinstanz – SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/05-initiator.png
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/10-iscsiTargetSettings.png
[3]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/15-iSCSITargetResults.png
[4]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/20-iSCSITargetLogin.png
[5]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/25-iSCSIVerify.png
[6]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/7-setiscsinetwork.png
[7]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/30-iSCSIattachedDisks.png
[8]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/45-CopyMove.png
[9]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/50-ExampleCreateSSMS.png
[10]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/40-Create25GBVol.png
[11]: ./media/sql-server-linux-shared-disk-cluster-configure-iscsi/55-ListOfVGs.png
