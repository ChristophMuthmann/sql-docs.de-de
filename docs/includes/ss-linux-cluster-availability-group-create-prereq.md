## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie die Verfügbarkeitsgruppe erstellen, müssen Sie:

- Ihre Umgebung so konfigurieren, dass alle Server kommunizieren können, die Verfügbarkeitsreplikate hosten sollen
- SQL Server installieren

>[!NOTE]
>Unter Linux müssen Sie eine Verfügbarkeitsgruppe erstellen, bevor Sie sie als vom Cluster verwaltete Clusterressource hinzufügen. Dieses Dokument enthält ein Beispiel, in dem eine Verfügbarkeitsgruppe erstellt wird. Verteilungsspezifische Anweisungen zum Erstellen des Clusters und Hinzufügen der Verfügbarkeitsgruppe als Clusterressource finden Sie in den Links unter [Nächste Schritte](#next-steps).

1. **Aktualisieren des Computernamens für jeden Host**

   Ein SQL Server-Name muss folgende Anforderungen erfüllen:
   
   - Maximal 15 Zeichen
   - Eindeutig innerhalb des Netzwerks
   
   Um den Computernamen festzulegen, bearbeiten Sie `/etc/hostname`. Mithilfe des folgenden Skripts können Sie `/etc/hostname` mit `vi` bearbeiten.

   ```bash
   sudo vi /etc/hostname
   ```

1. **Konfigurieren der Hostdatei**

>[!NOTE]
>Wenn Hostnamen mit ihrer IP-Adresse auf dem DNS-Server registriert werden, müssen die folgenden Schritte nicht ausgeführt werden. Überprüfen Sie, ob alle Knoten, die Teil der Konfiguration der Verfügbarkeitsgruppe werden, miteinander kommunizieren können (auf das Anpingen des Hostnamens sollte mit der entsprechenden IP-Adresse geantwortet werden). Stellen Sie außerdem sicher, dass diese Datei „/etc/hosts“ keinen Datensatz enthält, der dem Hostnamen des Knotens die localhost-IP-Adresse 127.0.0.1 zugeordnet.


   Die Hostdatei auf jedem Server enthält die IP-Adressen und Namen aller Server, die in die Verfügbarkeitsgruppe einbezogen werden. 

   Der folgende Befehl gibt die IP-Adresse des aktuellen Servers zurück:

   ```bash
   sudo ip addr show
   ```

   Aktualisieren Sie `/etc/hosts`. Mithilfe des folgenden Skripts können Sie `/etc/hosts` mit `vi` bearbeiten.

   ```bash
   sudo vi /etc/hosts
   ```

   In folgendem Beispiel wird `/etc/hosts` auf **node1** mit Ergänzungen für **node1**, **node2** und **node3** veranschaulicht. In diesem Dokument bezieht sich **node1** auf den Server, der das primäre Replikat hostet. **node2** und **node3** beziehen sich auf den Server, der die sekundären Replikate hostet.


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.12 node1
   10.128.16.77 node2
   10.128.15.33 node3
   ```

### <a name="install-sql-server"></a>SQL Server installieren

Installieren Sie SQL Server. Die folgenden Links verweisen auf SQL Server-Installationsanweisungen für verschiedene Verteilungen. 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)

- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)

- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Aktivieren von Always On-Verfügbarkeitsgruppen und Neustarten von sqlserver

Aktivieren Sie Always On-Verfügbarkeitsgruppen auf jedem Knoten, der eine SQL Server-Instanz hostet, und starten Sie `mssql-server` anschließend neu.  Führen Sie folgendes Skript aus:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>Aktivieren der AlwaysOn_health-Ereignissitzung 

Sie können optional erweiterte Ereignisse der Always On-Verfügbarkeitsgruppen aktivieren, die Ihnen bei der Ursachendiagnose helfen, wenn Sie Probleme in einer Verfügbarkeitsgruppe behandeln. Führen Sie den folgenden Befehl auf jeder Instanz des SQL Servers aus. 

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Weitere Informationen zu dieser XE-Sitzung finden Sie unter [Always On erweiterte Ereignisse](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-db-mirroring-endpoint-user"></a>Erstellen eines Datenbankspiegelungs-Endpunktbenuzters

Das folgende Transact-SQL-Skript erstellt eine Anmeldung mit dem Namen `dbm_login` und einen Benutzer mit dem Namen `dbm_user`. Aktualisieren Sie das Skript durch ein sicheres Kennwort. Führen Sie den folgenden Befehl für alle SQL Server-Instanzen aus, um den Endpunktbenutzer für die Datenbankspiegelung zu erstellen.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Erstellen eines Zertifikats

Der SQL Server-Dienst unter Linux verwendet Zertifikate zum Authentifizieren von Kommunikation zwischen den Spiegelungsendpunkten. 

Die folgende Transact-SQL-Skript erstellt ein Hauptschlüssel und ein Zertifikat. Anschließend wird damit das Zertifikat und die Datei mit einem privaten Schlüssel gesichert. Aktualisieren Sie das Skript durch sichere Kennwörter. Stellen Sie eine Verbindung mit der primären SQL Server-Instanz her, und führen Sie die folgende Transact-SQL aus, um das Zertifikat zu erstellen:

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

Zu diesem Zeitpunkt hat das primäre SQL Server-Replikat ein Zertifikat unter `/var/opt/mssql/data/dbm_certificate.cer` und einen privaten Schlüssel unter `var/opt/mssql/data/dbm_certificate.pvk`. Kopieren Sie diese beiden Dateien auf allen Servern, die Verfügbarkeitsreplikate hosten werden, an den gleichen Speicherort. Verwenden Sie den mssql-Benutzer, oder erteilen Sie dem mssql-Benutzer Berechtigungen, um auf diese Dateien zuzugreifen. 

Der folgende Befehl kopiert z.B. auf dem Quellserver die Dateien auf den Zielcomputer. Ersetzen Sie die **<node2>**-Werte durch die Namen der SQL Server-Instanzen, die die Replikate hosten werden. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

Erteilen Sie Berechtigungen auf jedem Zielserver für mssql-Benutzer, damit diese auf das Zertifikat zugreifen können.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Erstellen des Zertifikats auf sekundären Servern

Das folgende Transact-SQL-Skript erstellt ein Hauptschlüssel und ein Zertifikat aus der Sicherung, die Sie auf dem primären SQL Server-Replikat erstellt haben. Der Befehl autorisiert auch den Benutzer, damit er Zugriff auf das Zertifikat hat. Aktualisieren Sie das Skript durch sichere Kennwörter. Das Entschlüsselungskennwort ist das gleiche Kennwort, mit dem Sie die PVK-Datei in einem vorherigen Schritt erstellt haben. Führen Sie das folgende Skript auf allen sekundären Servern zum Erstellen des Zertifikats aus.

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Erstellen des Datenbankspiegelungs-Endpunkte auf allen Replikaten

Datenbank-Spiegelungsendpunkte senden und empfangen Meldungen zwischen den Serverinstanzen beim Teilnehmen an Datenbankspiegelungssitzungen über TCP (Transmission Control Protocol) oder beim Hosten verfügbarer Replikate. Der Datenbank-Spiegelungsendpunkt lauscht an einer eindeutigen TCP-Portnummer. 

Das folgende Transact-SQL erstellt für die Verfügbarkeitsgruppe einen überwachenden Endpunkt mit dem Namen `Hadr_endpoint`. Es startet den Endpunkt, und erteilt Verbindungsberechtigungen an den Benutzer, den Sie erstellt haben. Bevor Sie das Skript ausführen, ersetzen Sie die Werte zwischen `**< ... >**`.

>[!NOTE]
>Verwenden Sie für dieses Release keine andere IP-Adresse für die Listener-IP-Adresse. Wir arbeiten an der Behebung dieses Problems. Vorläufig ist der einzige zulässige Wert jedoch „0.0.0.0“.

Aktualisieren Sie das folgende Transact-SQL für Ihre Umgebung auf allen SQL Server-Instanzen: 

```Transact-SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!IMPORTANT]
>Der TCP-Port in der Firewall muss für den Listenerport geöffnet sein.

>[!IMPORTANT]
>Für die Version SQL Server 2017 ist `CERTIFICATE` die einzige unterstützte Authentifizierungsmethode für den Datenbankspiegelungs-Endpunkt. Die Option `WINDOWS` wird in einer zukünftigen Version aktiviert.

Weitere Informationen finden Sie unter [Der Datenbankspiegelungs-Endpunkt (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
