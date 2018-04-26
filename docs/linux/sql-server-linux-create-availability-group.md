---
title: Erstellen und konfigurieren eine verfügbarkeitsgruppe für SQL Server on Linux | Microsoft Docs
description: Dieses Lernprogramm zeigt, wie zum Erstellen und Konfigurieren von Verfügbarkeitsgruppen für SQL Server on Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: f02ec690caec1c33b4a316707c0011c8be032580
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Erstellen und Konfigurieren einer verfügbarkeitsgruppe für SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

In diesem Lernprogramm wird beschrieben, wie zum Erstellen und Konfigurieren einer verfügbarkeitsgruppe (AG) für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux. Im Gegensatz zu [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] und zuvor auf Windows, Sie können Testreihen mit oder ohne den zugrunde liegenden Schrittmacher Cluster zuerst erstellen. Integration mit dem Cluster bei Bedarf bis zu einem späteren Zeitpunkt erfolgt nicht.

Das Lernprogramm umfasst die folgenden Aufgaben:
 
> [!div class="checklist"]
> * Aktivieren von Verfügbarkeitsgruppen.
> * Erstellen Sie Availability Group-Endpunkten und Zertifikaten.
> * Verwendung [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) oder Transact-SQL zum Erstellen einer verfügbarkeitsgruppe.
> * Erstellen der [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Anmeldung und Berechtigungen für Schrittmacher.
> * Erstellen Sie Gruppenressourcen in einem Cluster Schrittmacher (nur bei externen Typ).

## <a name="prerequisite"></a>Voraussetzung
- Der Cluster mit hoher Verfügbarkeit Schrittmacher bereitstellen, wie in beschrieben [bereitstellen ein Clusters Schrittmacher für SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md).


## <a name="enable-the-availability-groups-feature"></a>Aktivieren Sie die verfügbarkeitsgruppenfunktion

Im Gegensatz zu unter Windows können keine PowerShell oder [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Konfigurations-Manager zum Aktivieren der Verfügbarkeit gruppiert (AG)-Funktion. Sie müssen unter Linux verwenden `mssql-conf` das Feature aktiviert. Es gibt zwei Möglichkeiten, um die verfügbarkeitsgruppenfunktion zu aktivieren: Verwenden der `mssql-conf` -Hilfsprogramm, oder Sie bearbeiten die `mssql.conf` Datei manuell.

> [!IMPORTANT]
> Der AG-Funktion muss für die Konfiguration nur Replikate aktiviert sein, auch auf [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)].

### <a name="use-the-mssql-conf-utility"></a>Verwenden Sie das Dienstprogramm Mssql-conf

Geben Sie an einer Eingabeaufforderung Folgendes ein:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Bearbeiten Sie die Datei mssql.conf

Sie können auch ändern, die `mssql.conf` -Datei unter der `/var/opt/mssql` Netzwerkordner in die folgenden Zeilen hinzufügen:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>neu starten [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Nach der Aktivierung von Verfügbarkeitsgruppen, wie unter Windows neu starten müssen [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Dies kann durch folgenden erfolgen:

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>Erstellen Sie die verfügbarkeitsgruppenendpunkte Verfügbarkeit und Zertifikate

Eine verfügbarkeitsgruppe wird TCP-Endpunkten für die Kommunikation verwendet. Unter Linux werden Endpunkte für eine Verfügbarkeitsgruppe nur unterstützt, wenn Zertifikate für die Authentifizierung verwendet werden. Dies bedeutet, dass das Zertifikat von einer Instanz muss für alle anderen Instanzen wiederhergestellt werden, die Replikate in der gleichen Verfügbarkeitsgruppe einbezogen werden. Des Zertifikats ist auch für ein Replikat nur Konfiguration erforderlich. 

Erstellen von Endpunkten und Zertifikaten wiederherstellen können nur über Transact-SQL erfolgen. Sie können nicht[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-Zertifikate ebenfalls generiert. Sie benötigen auch einen Prozess zum Verwalten und Ersetzen Sie alle Zertifikate, die ablaufen.

> [!IMPORTANT]
> Wenn Sie planen, verwenden Sie die [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] -Assistenten zum Erstellen der Verfügbarkeitsgruppe, Sie noch benötigen, erstellen und Wiederherstellen der Zertifikate mithilfe von Transact-SQL unter Linux.

Wenden Sie für die vollständige Syntax für die verfügbaren Optionen für die verschiedenen Befehle (z. B. die Erhöhung der Sicherheit) sich an:

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [ZERTIFIKAT ERSTELLEN](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> Obwohl Sie eine verfügbarkeitsgruppe erstellen, die der Typ des Endpunkts verwendet *FOR DATABASE_MIRRORING*, da einige Aspekte der zugrunde liegenden einmal für diese Funktion nun veraltete freigegeben wurden.

In diesem Beispiel wird die Zertifikate für eine Konfiguration mit drei Knoten erstellt. Die Instanznamen sind LinAGN1 LinAGN2 und LinAGN3.

1.  Führen Sie die folgende für LinAGN1, um die Hauptschlüssel, Zertifikat und Endpunkt zu erstellen sowie sichern Sie das Zertifikat. In diesem Beispiel wird die typische TCP-Port 5022 für den Endpunkt verwendet.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  Gehen Sie genauso für LinAGN2 vor:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  Führen Sie schließlich die gleiche Sequenz auf LinAGN3:
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  Mithilfe von `scp` oder eine andere-Hilfsprogramm, die Sicherungen des Zertifikats in jedem Knoten zu kopieren, die Teil der Verfügbarkeitsgruppe sein wird.
    
    In diesem Beispiel:
    
    - Kopieren Sie LinAGN1_Cert.cer LinAGN2 und LinAGN3
    - Kopieren Sie LinAGN2_Cert.cer LinAGN1 und LinAGN3.
    - Kopieren Sie LinAGN3_Cert.cer LinAGN1 und LinAGN2.
    
5.  Ändern des Besitzes und die Gruppe der kopierten Zertifikatsdateien zugeordnet `mssql`.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  Erstellen Sie auf Instanzebene Anmeldungen und Benutzer mit LinAGN2 und LinAGN3 auf LinAGN1 verknüpft sind.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  Wiederherstellen von LinAGN2_Cert und LinAGN3_Cert auf LinAGN1. Mit den anderen Replikaten Zertifikate ist ein wichtiger Aspekt der AG-Kommunikation und Sicherheit.
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  Erstellen Sie auf Instanzebene Anmeldungen und Benutzer mit LinAGN1 und LinAGN3 auf LinAGN2 verknüpft sind.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10.  Wiederherstellen von LinAGN1_Cert und LinAGN3_Cert auf LinAGN2. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
11.  Grant the logins associated with LinAG1 and LinAGN3 permission to connect to the endpoint on LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12.  Erstellen Sie auf Instanzebene Anmeldungen und Benutzer mit LinAGN1 und LinAGN2 auf LinAGN3 verknüpft sind.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13.  Wiederherstellen von LinAGN1_Cert und LinAGN2_Cert auf LinAGN3. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
14.  Grant the logins associated with LinAG1 and LinAGN2 permission to connect to the endpoint on LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>Erstellen der verfügbarkeitsgruppe.

In diesem Abschnitt wird beschrieben, wie mit [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) oder Transact-SQL zum Erstellen der verfügbarkeitsgruppe für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>Verwendung von [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]

Dieser Abschnitt zeigt, wie zum Erstellen einer AG mit einem externen Cluster mithilfe von SSMS mit dem Assistenten für neue Verfügbarkeitsgruppen.

1.  Erweitern Sie in SSMS **hohe Verfügbarkeit mit AlwaysOn**, klicken Sie mit der rechten Maustaste auf **Verfügbarkeitsgruppen**, und wählen Sie **Assistenten für neue Verfügbarkeitsgruppen**.

2.  Klicken Sie auf das Dialogfeld "Einführung" auf **Weiter**.

3.  Verfügbarkeitsgruppenoptionen Geben Sie im Dialogfeld Geben Sie einen Namen für die verfügbarkeitsgruppe, und wählen Sie einen Clustertyp des EXTERNEN "oder" NONE in der Dropdownliste. Externe sollte verwendet werden, wenn Schrittmacher bereitgestellt wird. None ist für spezielle Szenarien, z. B. read für horizontales Skalieren. Wählen Sie die Option zur Erkennung der Datenbank-Integrität auf Datenbankebene ist optional. Weitere Informationen zu dieser Option finden Sie unter [Datenbank Zustandsdaten Erkennung Failover verfügbarkeitsgruppenoption](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md). Klicken Sie auf **Weiter**.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  Wählen Sie die Datenbanken, die in der Verfügbarkeitsgruppe einbezogen wird, klicken Sie im Dialogfeld "Datenbanken auswählen". Jede Datenbank muss eine vollständige Sicherung verfügen, bevor sie einer Verfügbarkeitsgruppe hinzugefügt werden kann. Klicken Sie auf **Weiter**.

5.  Klicken Sie im Dialogfeld "Replikate angeben" klicken Sie auf **Hinzufügen von Replikaten**.

6.  Geben Sie im Dialogfeld Verbindung herstellen, den Namen der Instanz von Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] , werden die Anmeldeinformationen für die Verbindung und das sekundäre Replikat. Klicken Sie auf **Verbinden**.

7.  Wiederholen Sie die vorherigen beiden Schritte für die Instanz, die ein Replikat nur Konfiguration oder ein weiteres sekundäres Replikat enthält.

8.  Alle drei Instanzen sollten jetzt auf das Dialogfeld "Replikate angeben" aufgeführt werden. Wenn ein Cluster von externen, bis das sekundäre Replikat verwenden zu können, die eine sekundäre "true" werden, stellen Sie sicher, den Verfügbarkeitsmodus übereinstimmt, der das primäre Replikat und Failovermodus auf externe festgelegt ist. Wählen Sie für das Replikat nur Konfiguration nur ein Verfügbarkeitsmodus der Konfiguration.

    Das folgende Beispiel zeigt eine Verfügbarkeitsgruppe mit zwei Replikaten, ein Cluster von externen und ein Replikat nur Configuration.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    Das folgende Beispiel zeigt eine AG mit zwei Replikaten, ein Cluster None und ein Replikat nur Konfiguration.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  Wenn Sie die sicherungseinstellungen ändern möchten, klicken Sie auf der Registerkarte "Sicherungseinstellungen". Weitere Informationen zu sicherungseinstellungen mit Testreihen, finden Sie unter [Konfigurieren einer Sicherung auf verfügbarkeitsreplikaten](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).

10. Wenn lesbare sekundäre Datenbanken oder Erstellen einer Verfügbarkeitsgruppe mit einem Cluster None für Skalieren von Lesevorgängen eingeben, können Sie einen Listener erstellen, durch Auswählen der Registerkarte "Listener". Ein Listener kann auch später hinzugefügt werden. Um einen Listener zu erstellen, wählen Sie die Option **erstellen ein verfügbarkeitsgruppenlisteners** , und geben Sie einen Namen, einen TCP/IP-Port und angibt, ob eine statische oder automatisch zugewiesene DHCP IP-Adresse verwendet. Denken Sie daran, dass für eine Verfügbarkeitsgruppe mit einem Clustertyp ' None ', die IP-Adresse statisch und festgelegt werden soll, die primäre IP-Adresse.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. Wenn ein Listener für lesbare Szenarien erstellt wird, kann SSMS 17.3 oder höher die Erstellung von schreibgeschütztem routing im Assistenten aus. Sie können auch später über SSMS oder Transact-SQL hinzugefügt werden. So fügen Sie schreibgeschütztes routing jetzt hinzu:

    A.  Wählen Sie die Registerkarte "schreibgeschütztes Routing".

    B.  Geben Sie die URLs für den schreibgeschützten Replikaten aus. Diese URLs sind die Endpunkte ähnlich, außer sie verwenden Sie den Port der Instanz nicht für den Endpunkt.

    c.  Wählen Sie jede URL, und wählen Sie in der unteren die lesbaren Replikaten. Auswählen halten Sie UMSCHALT oder klicken und ziehen.

12. Klicken Sie auf **Weiter**.

13. Wählen Sie, wie die sekundären Replikate initialisiert wird. Die Standardeinstellung ist die Verwendung [automatischem seeding](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), wofür die denselben Pfad auf allen Servern in der Verfügbarkeitsgruppe teilnehmen. Sie können auch veranlassen, den Assistenten führen Sie eine Sicherungskopie, erstellen, und stellen Sie wieder her (die zweite Option;) haben sie die Verknüpfung, wenn Sie manuell gesichert, kopiert und die Datenbank auf dem Replikat wiederhergestellt (dritte option;) oder fügen Sie die Datenbank später (letzte Option). Wie bei der Zertifikate, wenn Sie manuell Sicherungskopien und kopiert werden, muss Berechtigungen für die Sicherungsdateien für die anderen Replikate festgelegt werden. Klicken Sie auf **Weiter**.

14. Klicken Sie im Dialogfeld "Überprüfung" Alles, was nicht wieder als Erfolg stammt, zu untersuchen. Einige Warnungen sind akzeptabel "und" nicht schwerwiegend, z. B. Wenn Sie keinen Listener erstellen. Klicken Sie auf **Weiter**.

15. Klicken Sie auf das Dialogfeld "Zusammenfassung" auf **Fertig stellen**. Der Prozess zum Erstellen der Verfügbarkeitsgruppe wird jetzt gestartet werden.

16. Wenn der AG-Erstellung abgeschlossen ist, klicken Sie auf **schließen** auf den Ergebnissen. Sie sehen nun die AG auf die Replikate in der dynamischen Verwaltungssichten sowie hohe Verfügbarkeit mit AlwaysOn im Ordner in SSMS.

### <a name="use-transact-sql"></a>Verwenden von Transact-SQL

Dieser Abschnitt zeigt Beispiele für das Erstellen einer Verfügbarkeitsgruppe mithilfe von Transact-SQL. Der Listener und schreibgeschütztes routing können konfiguriert werden, nachdem die Verfügbarkeitsgruppe erstellt wurde. Die AG selbst kann geändert werden, mit `ALTER AVAILABILITY GROUP`, aber ändern den Typ des Clusters kann nicht durchgeführt werden, [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Wenn Sie nicht beabsichtigt eine AG mit einem externen Cluster zu erstellen, müssen Sie löschen und neu erstellen, es mit einem Clustertyp ' None '. Weitere Informationen und anderen Optionen finden Sie unter den folgenden Links:

-   [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe (SQLServer)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners (SQLServer)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one--two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>Beispiel 1 – zwei Replikate mit einem Replikat nur Konfiguration (externe Clustertyp)

In diesem Beispiel wird gezeigt, wie eine zwei-Replikat AG erstellen, die ein Replikat nur Konfiguration verwendet wird.

1.  Führen Sie auf den Knoten, die das primäre Replikat, das die vollständig Lese-/Schreibkopie der Datenbank(en) enthält. In diesem Beispiel wird das automatische seeding verwendet.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  Führen Sie in einem Abfrage-Fenster, das an das andere Replikat verbunden ist Folgendes ein, um verknüpfen Sie das Replikat mit der Verfügbarkeitsgruppe und des seedingprozesses vom primären zum sekundären Replikat zu initiieren.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  In einem Abfrage-Fenster, das mit dem Configuration nur Replikat verbunden ist mit der Verfügbarkeitsgruppe verknüpfen.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two--three-replicas-with-read-only-routing-external-cluster-type"></a>Beispiel 2 – 3 Replikate mit schreibgeschütztes routing (externe Clustertyp)

Dieses Beispiel zeigt drei vollständige Sie Replikate und wie schreibgeschütztes routing können im Rahmen der Erstellung der ersten Verfügbarkeitsgruppe konfiguriert werden.

1.  Führen Sie auf den Knoten, die das primäre Replikat, das die vollständig Lese-/Schreibkopie der Datenbank(en) enthält. In diesem Beispiel wird das automatische seeding verwendet.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    Einige Punkte, die über diese Konfiguration zu beachten:
    
    - *%Agname* ist der Name der verfügbarkeitsgruppe.
    - *DBName* ist der Name der Datenbank, die mit der verfügbarkeitsgruppe verwendet wird. Es kann auch eine Liste der Namen, die durch Kommas getrennt sein.
    - *ListenerName* ist ein Name, der sich von den zugrunde liegenden Server/Knoten unterscheidet. Wird registriert, im DNS zusammen mit *IP-Adresse*.
    - *IP-Adresse* eine IP-Adresse, die mit zugeordnetem *ListenerName*. Es ist auch eindeutig und nicht identisch mit den Servern/Knoten. Anwendungen und Endbenutzern verwendet entweder *ListenerName* oder *IP-Adresse* zur Verbindung mit der Verfügbarkeitsgruppe.
    - *Subnetzmaske* ist die Subnetzmaske des *IP-Adresse*, z. B. 255.255.255.0.

2.  Führen Sie in einem Abfrage-Fenster, das an das andere Replikat verbunden ist Folgendes ein, um verknüpfen Sie das Replikat mit der Verfügbarkeitsgruppe und des seedingprozesses vom primären zum sekundären Replikat zu initiieren.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  Wiederholen Sie Schritt2 für das dritte Replikat aus.

#### <a name="example-three--two-replicas-with-read-only-routing-none-cluster-type"></a>Beispiel 3 – zwei Replikate mit schreibgeschütztes routing (keine cluster-Typ)

Dieses Beispiel zeigt die Erstellung eine Konfiguration mit zwei Replikaten mithilfe eines Cluster-Typs ' None '. Es wird für das Szenario lesen Skalierung verwendet, in dem kein Failover erwartet wird. Dies erstellt den Listener, der tatsächlich das primäre Replikat als auch das schreibgeschützte routing ist die Roundrobin-Funktion verwenden.

1.  Führen Sie auf den Knoten, die das primäre Replikat, das die vollständig Lese-/Schreibkopie der Datenbank(en) enthält. In diesem Beispiel wird das automatische seeding verwendet.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    Erläuterungen
    - *%Agname* ist der Name der verfügbarkeitsgruppe.
    - *DBName* ist der Name der Datenbank, die mit der verfügbarkeitsgruppe verwendet wird. Es kann auch eine Liste der Namen, die durch Kommas getrennt sein.
    - *PortOfEndpoint* ist die Portnummer verwendet, die für den Endpunkt erstellt.
    - *PortOfInstance* ist die Portnummer, die von der Instanz der [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].
    - *ListenerName* ist ein Name, die unterscheidet sich keines der zugrunde liegenden Replikate, jedoch wird nicht tatsächlich verwendet werden.
    - *PrimaryReplicaIPAddress* ist die IP-Adresse des primären Replikats.
    - *Subnetzmaske* ist die Subnetzmaske des *IP-Adresse*. Z. B. 255.255.255.0.
    
2.  Verknüpfen Sie das sekundäre Replikat mit der Verfügbarkeitsgruppe, und initiieren Sie die automatische seeding.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>Erstellen der [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Anmeldung und Berechtigungen für Schrittmacher

Ein Schrittmacher Hochverfügbarkeits-Cluster zugrunde liegendes [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux benötigt Zugriff auf die [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Instanz sowie Berechtigungen für die verfügbarkeitsgruppe selbst. Mit diesen Schritten erstellen, die Anmeldung und die zugehörigen Berechtigungen, zusammen mit einer Datei, die Schrittmacher informiert, wie bei anmelden [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

1.  Führen Sie in einem Abfrage-Fenster, das mit dem ersten Replikat verbunden ist die folgenden Schritte aus:

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD '<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  Geben Sie den Befehl, auf Knoten 1 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    Dadurch wird den Emacs-Editor geöffnet.
    
3.  Geben Sie die folgenden zwei Zeilen in den Editor ein:

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Halten Sie die STRG-Taste gedrückt, und drücken Sie dann die X, dann C, um zu beenden, und speichern Sie die Datei.

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    die Datei sperren.

6.  Wiederholen Sie die Schritte 1 bis 5 für die anderen Server, die als Replikate dienen soll.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Erstellen Sie die von Gruppenressourcen im Cluster Schrittmacher (nur extern)

Nach einem verfügbarkeitsgruppenfailover-Gruppe wird erstellt, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], die entsprechenden Ressourcen müssen in Schrittmacher, erstellt werden, wenn ein Cluster von externen angegeben wird. Es gibt zwei Ressourcen, die mit einer Verfügbarkeitsgruppe verknüpft sind: die AG selbst und eine IP-Adresse. Konfigurieren die IP-Adressressource ist optional, wenn Sie die Listener-Funktionalität nicht verwenden, werden jedoch empfohlen.

AG-Ressource, die erstellt wird, ist eine besondere Art von Ressource, die als Klon bezeichnet wird. Die AG-Ressource ist im Wesentlichen Kopien auf jedem Knoten, und es ist eine steuernde Ressource Master aufgerufen. Die Master ist verknüpft mit dem Server, die das primäre Replikat hostet. Die sekundären Replikate (regulären oder nur Metadaten Configuration) gelten als Einzelinstanzen und kann auf heraufgestuft werden in einem Failovercluster master.

1.  Erstellen Sie die AG-Ressource mit der folgenden Syntax aus:

    **Red Hat Enterprise Linux (RHEL) und Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> --master meta notify=true
    ```

    >[!NOTE]
    >Auf RHEL 7.4 können Sie eine Warnung mit der Verwendung des – Master auftreten. Um dies zu vermeiden, verwenden `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> master notify=true`
   
    **SUSE Linux Enterprise Server (SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    wobei *NameForAGResource* ist der eindeutige Name für die Verfügbarkeitsgruppe für diese Clusterressource und *%AGname* ist der Name des der Verfügbarkeitsgruppe, die erstellt wurde.
 
2.  Erstellen Sie die IP-Adressressource für die Verfügbarkeitsgruppe, die die Funktionalität des Listeners zugeordnet werden soll.

    **RHEL und Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    wobei *NameForIPResource* ist der eindeutige Name für die IP-Adressressource und *IP-Adresse* die statische IP-Adresse der Ressource zugeordnet ist. Auf SLES müssen Sie auch die Netzmaske bereitstellen. Beispielsweise müsste 255.255.255.0 einen Wert von 24 für *Netzmaske.*
    
3.  Um sicherzustellen, dass die IP-Adresse und der AG-Ressource auf demselben Knoten ausgeführt werden, muss eine Einschränkung für die Zusammenstellung konfiguriert werden.

    **RHEL und Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    wobei *NameForIPResource* ist der Name für die IP-Adressressource *NameForAGResource* ist der Name für die AG-Ressource, und klicken Sie auf SLES, *NameForConstraint* ist der Name für die Einschränkung.

4.  Erstellen Sie eine Sortierung der Einschränkung, um sicherzustellen, dass die AG-Ressource aktiv ist und ausgeführt wird, bevor Sie die IP-Adresse. Während die Zusammenstellung Einschränkung eine Sortierung Einschränkung impliziert, dadurch werden erzwungen.

    **RHEL und Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    wobei *NameForIPResource* ist der Name für die IP-Adressressource *NameForAGResource* ist der Name für die AG-Ressource, und klicken Sie auf SLES, *NameForConstraint* ist der Name für die Einschränkung.

## <a name="next-steps"></a>Nächste Schritte

In diesem Lernprogramm haben Sie gelernt, wie zum Erstellen und Konfigurieren einer verfügbarkeitsgruppe für [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] unter Linux. Sie haben gelernt, wie auf:
> [!div class="checklist"]
> * Aktivieren von Verfügbarkeitsgruppen.
> * Create AG-Endpunkten und Zertifikaten.
> * Verwendung [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) oder Transact-SQL zum Erstellen einer Verfügbarkeitsgruppe.
> * Erstellen der [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Anmeldung und Berechtigungen für Schrittmacher.
> * Erstellen Sie in einem Cluster Schrittmacher AG-Ressourcen.

Die meisten AG Verwaltungsaufgaben, einschließlich Upgrades und ein Failover finden Sie unter:

> [!div class="nextstepaction"]
> [Betreiben Sie HA-verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-availability-group-failover-ha.md)

