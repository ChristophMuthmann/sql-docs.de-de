---
title: Konfigurieren Sie SQLServer Always On-Verfügbarkeitsgruppe unter Windows und Linux | Microsoft Docs
description: Konfigurieren Sie SQL Server Availability Group, mit Replikaten unter Windows und Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/31/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: fc9460e9454c2ef4559e6b45f0d8f7bb85f91031
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Configure SQL Server AlwaysOn-Verfügbarkeitsgruppe unter Windows und Linux (Cross-Platform)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Dieser Artikel beschreibt die Schritte zum Erstellen einer immer auf Verfügbarkeit Gruppe (AG) mit einem Replikat auf einem WindowsServer und das andere Replikat auf einem Linux-Server. Diese Konfiguration ist plattformübergreifende, da die Replikate befinden sich unter verschiedenen Betriebssystemen. Verwenden Sie diese Konfiguration für die Migration von einer Plattform, die andere oder Wiederherstellung im Notfall (DR). Diese Konfiguration unterstützt keine hohe Verfügbarkeit, da es keine Clusterlösung zum Verwalten der Konfiguration einer plattformübergreifenden gibt. 

![Hybride None](./media/sql-server-linux-availability-group-overview/image1.png)

Bevor Sie fortfahren, sollten Sie mit der Installation und Konfiguration für SQL Server-Instanzen unter Windows und Linux vertraut sein. 

## <a name="scenario"></a>Szenario

In diesem Szenario sind zwei Server unter verschiedenen Betriebssystemen. Windows Server 2016 mit dem Namen `WinSQLInstance` das primäre Replikat hostet. Ein Linux-Beispielserver namens `LinuxSQLInstance` das sekundäre Replikat hosten.

## <a name="configure-the-ag"></a>Konfigurieren der Verfügbarkeitsgruppe 

Die Schritte zum Erstellen der Verfügbarkeitsgruppe sind die Schritte zum Erstellen einer Verfügbarkeitsgruppe für das Skalieren von Lesevorgängen Arbeitslasten identisch. Der Clustertyp AG ist keine ",", da es kein Cluster-Manager ist. 

   >[!NOTE]
   >Für die Skripts in diesem Artikel spitze Klammern `<` und `>` identifizieren Werte, die Sie für Ihre Umgebung ersetzen müssen. Die spitzen Klammern selbst sind nicht erforderlich, für die Skripts. 

1. Installieren Sie 2017 von SQL Server unter Windows Server 2016, aktivieren Sie AlwaysOn-Verfügbarkeitsgruppen von SQL Server-Konfigurations-Manager und legen Sie die Authentifizierung im gemischten Modus. 

   >[!TIP]
   >Wenn Sie diese Lösung in Azure überprüfen, platzieren Sie beide Server in derselben verfügbarkeitsgruppe, um sicherzustellen, dass sie im Datencenter getrennt werden. 

   **Aktivieren von Verfügbarkeitsgruppen**

   Anweisungen hierzu finden Sie unter [aktivieren und Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).

   ![Aktivieren von Verfügbarkeitsgruppen](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   SQL Server-Konfigurations-Manager fest, dass es sich bei der Computer kein Knoten in einem Failovercluster ist. 

   Starten Sie SQL Server neu, nachdem Sie Verfügbarkeitsgruppen zu aktivieren.

   **Festlegen der Authentifizierung im gemischten Modus**

   Anweisungen hierzu finden Sie unter [Ändern des Serverauthentifizierungsmodus](../database-engine/configure-windows/change-server-authentication-mode.md#SSMSProcedure).

1. Installieren von SQLServer 2017 unter Linux. Anweisungen hierzu finden Sie unter [installieren SQL Sever](sql-server-linux-setup.md). Aktivieren Sie `hadr` über Mssql-conf

   So aktivieren Sie `hadr` über Mssql-Conf in einer Shell-Eingabeaufforderung den folgenden Befehl ausgeben:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   Nach der Aktivierung `hadr`, die SQL Server-Instanz neu.  

   Die folgende Abbildung zeigt dieses Schritts.

   ![Verfügbarkeit Gruppen Linux aktivieren](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. Konfigurieren Sie Hosts-Datei auf beiden Servern, oder registrieren Sie den Servernamen mit DNS.

1. Öffnen von Firewallports für TPC 1433 und 5022 auf Windows- und Linux.

1. Erstellen Sie auf dem primären Replikat einen Datenbank-Anmeldenamen und ein Kennwort ein.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. Klicken Sie auf dem primären Replikat erstellen Sie ein Hauptschlüssel und ein Zertifikat zu, und Sichern Sie das Zertifikat mit einem privaten Schlüssel.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. Kopieren Sie das Zertifikat und den privaten Schlüssel mit dem Linux-Server (sekundären Replikat entspricht) am `/var/opt/mssql/data`. Sie können `pscp` auf die Dateien auf dem Linux-Server kopieren. 

1. Legen Sie die Gruppe und den Besitz des privaten Schlüssels und das Zertifikat an `mssql:mssql`.

   Im folgenden Skript wird die Gruppe und den Besitz von Dateien. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   Im folgenden Diagramm werden Objektbesitz und Gruppe für das Zertifikat und Schlüssel ordnungsgemäß festgelegt.

   ![Verfügbarkeit Gruppen Linux aktivieren](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. Erstellen Sie einen Datenbank-Anmeldenamen und ein Kennwort und erstellen Sie einen Hauptschlüssel, auf dem sekundären Replikat.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. Auf dem sekundären Replikat Wiederherstellen des Zertifikats, die Sie kopiert, um haben `/var/opt/mssql/data`. 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. Erstellen Sie einen Endpunkt, auf dem primären Replikat.

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >Die Firewall muss für den Listener TCP-Port geöffnet sein. Im Skript ist der Port 5022. Verwenden Sie einen beliebigen verfügbaren TCP-Port. 

1. Erstellen Sie den Endpunkt, auf dem sekundären Replikat. Wiederholen Sie dieses Skript auf dem sekundären Replikat einen Endpunkt erstellen. 

1. Erstellen Sie auf dem primären Replikat die Verfügbarkeitsgruppe mit `CLUSTER_TYPE = NONE`. Das Beispielskript verwendet `SEEDING_MODE = AUTOMATIC` zum Erstellen der Verfügbarkeitsgruppe. 

   >[!NOTE]
   >Wenn verwendet die Windows-Instanz von SQL Server unterschiedliche Pfade für Daten- und Protokolldateien, automatisches seeding ein Fehler auftritt, mit der Linux-Instanz von SQL Server, da diese Pfade nicht auf dem sekundären Replikat vorhanden sind. Um das folgende Skript für eine plattformübergreifende AG verwenden zu können, muss die Datenbank im gleichen Pfad für die Daten und Protokolldateien auf dem WindowsServer. Alternativ können Sie das Skript festzulegende aktualisieren `SEEDING_MODE = MANUAL` sichern und Wiederherstellen der Datenbank mit `NORECOVERY` auf das Seeding der Datenbank. 
   >
   >Dieses Verhalten gilt für Azure Marketplace-Images. 
   >
   >Weitere Informationen zu automatischen seeding, finden Sie unter [automatischem Seeding - Datenträgerlayout](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout). 

   Bevor Sie das Skript ausführen, aktualisieren Sie die Werte für Ihre Testreihen.

      * Ersetzen Sie `<WinSQLInstance>` mit den Namen des SQL Server-Instanz das primäre Replikat.

      * Ersetzen Sie `<LinuxSQLInstance>` mit den Namen des SQL Server-Instanz das sekundäre Replikat. 

   Um die Verfügbarkeitsgruppe zu erstellen, aktualisieren Sie die Werte, und führen Sie das Skript auf dem primären Replikat.  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   Weitere Informationen finden Sie unter [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md).

1. Verknüpfen Sie auf dem sekundären Replikat der Verfügbarkeitsgruppe.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. Erstellen Sie eine Datenbank für die Verfügbarkeitsgruppe an. Die Beispielschritte verwenden Sie eine Datenbank namens `<TestDB>`. Wenn Sie das automatische seeding verwenden, legen Sie den gleichen Pfad für die Daten und Protokolldateien. 

   Bevor Sie das Skript ausführen, aktualisieren Sie die Werte für Ihre Datenbank.

      * Ersetzen Sie `<TestDB>` durch den Namen der Datenbank.

      * Ersetzen Sie `<F:\Path>` durch den Pfad für Ihre Datenbank und Protokolldateien. Verwenden Sie denselben Pfad für die Datenbank und Protokolldateien an. 

      Sie können auch die Standardpfaden verwenden. 

    Führen Sie das Skript, um Ihre Datenbank zu erstellen. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. Nehmen Sie eine vollständige Sicherung der Datenbank. 

1. Wenn Sie das automatische seeding nicht verwenden, wird wiederherstellen Sie die Datenbank auf dem sekundären (Linux)-Replikatserver. [Migration von einer SQL Server-Datenbank von Windows, Linux mit Sicherung und Wiederherstellung](sql-server-linux-migrate-restore-database.md). Wiederherstellen der Datenbank `WITH NORECOVERY` auf dem sekundären Replikat. 

1. Die Datenbank der Verfügbarkeitsgruppe hinzufügen. Aktualisieren Sie das Beispielskript. Ersetzen Sie `<TestDB>` durch den Namen der Datenbank. Führen Sie die SQL-Abfrage, um die Datenbank der Verfügbarkeitsgruppe hinzuzufügen, auf dem primären Replikat.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. Stellen Sie sicher, dass die Datenbank auf dem sekundären Replikat aufgefüllt erhalten wird. 

## <a name="fail-over-the-primary-replica"></a>Führen Sie ein Failover des primären Replikats

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

In diesem Artikel überprüft die Schritte zum Erstellen einer plattformübergreifenden AG zur Migration oder Skalieren von Lesevorgängen arbeitsauslastungen zu unterstützen. Es kann für die manuelle Wiederherstellung verwendet werden. Es wird erläutert, wie für ein Failover der Verfügbarkeitsgruppe wird. Eine plattformübergreifende AG verwendet Clustertyp `NONE` und hohen Verfügbarkeit, da es kein Cluster Tool auf-Plattformen ist nicht unterstützt. 

## <a name="next-steps"></a>Nächste Schritte

[Übersicht über Always On-Verfügbarkeitsgruppen](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Grundlagen der SQL Server-Verfügbarkeit für Linux-Bereitstellungen](sql-server-linux-ha-basics.md)
