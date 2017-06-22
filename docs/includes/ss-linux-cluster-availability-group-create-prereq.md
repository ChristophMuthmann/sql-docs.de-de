## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie die verfügbarkeitsgruppe erstellen, müssen Sie:

- Festlegen Sie Ihrer Umgebung, sodass alle Server, die verfügbarkeitsreplikate hosten kommunizieren kann
- Installieren von SQLServer

>[!NOTE]
>Unter Linux müssen Sie eine verfügbarkeitsgruppe erstellen, bevor es als Clusterressource für die Verwaltung mit dem Cluster hinzugefügt wird. Dieses Dokument enthält ein Beispiel, das die verfügbarkeitsgruppe erstellt. Für die Verteilung spezifische Anweisungen zum Erstellen des Clusters, und fügen der verfügbarkeitsgruppe als Clusterressource, finden Sie unter den Links unter [nächste Schritte](#next-steps).

1. **Aktualisieren Sie den Computernamen für jeden host**

   Jeder SQL Server-Name muss sein:
   
   - 15 Zeichen oder weniger
   - Eindeutig innerhalb des Netzwerks
   
   Bearbeiten Sie zum Festlegen der Computername `/etc/hostname`. Das folgende Skript können Sie bearbeiten `/etc/hostname` mit `vi`.

   ```bash
   sudo vi /etc/hostname
   ```

1. **Konfigurieren Sie die Hosts-Datei**

>[!NOTE]
>Wenn Hostnamen mit ihrer IP-Adresse in der DNS-Server registriert sind, ist es nicht erforderlich, führen Sie die folgenden Schritte aus. Überprüfen Sie, dass alle Knoten, die Teil der Konfiguration der verfügbarkeitsgruppe werden sollen (pingen, mit der entsprechenden IP-Adresse der Hostnamen Antworten sollten) miteinander kommunizieren können. Stellen Sie außerdem sicher, dass diese Datei/etc/Hosts keinen Datensatz enthält, der "localhost" IP-Adresse 127.0.0.1 mit dem Hostnamen des Knotens zugeordnet.


   Die Hostdatei auf jedem Server enthält die IP-Adressen und Namen von allen Servern, die in der verfügbarkeitsgruppe einbezogen werden. 

   Der folgende Befehl gibt die IP-Adresse des aktuellen Servers:

   ```bash
   sudo ip addr show
   ```

   Update `/etc/hosts`. Das folgende Skript können Sie bearbeiten `/etc/hosts` mit `vi`.

   ```bash
   sudo vi /etc/hosts
   ```

   Das folgende Beispiel zeigt `/etc/hosts` auf **node1** mit Ergänzungen für **node1** und **node2**. In diesem Dokument **node1** bezieht sich auf dem primären SQL Server-Replikat. **Node2** bezieht sich auf den sekundären SQL-Server.;


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 node1
   10.128.16.77 node2
   ```

### <a name="install-sql-server"></a>Installieren von SQLServer

Installieren von SqlServer. Die folgenden Links weisen auf SQL Server-installationsanweisungen für verschiedene Verteilungen. 

- [Red Hat Enterprise Linux](..\linux\sql-server-linux-setup-red-hat.md)

- [SUSE Linux Enterprise Server](..\linux\sql-server-linux-setup-suse-linux-enterprise-server.md)

- [Ubuntu](..\linux\sql-server-linux-setup-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Always On-Verfügbarkeitsgruppen aktivieren und starten Sie SQL Server neu.

Aktivieren Sie Always On-Verfügbarkeitsgruppen auf jedem Knoten, der SQL Server-Dienst hostet, und dann neu `mssql-server`.  Führen Sie folgendes Skript aus:

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-alwaysonhealth-event-session"></a>AlwaysOn_health ereignissitzung aktivieren 

Sie können Optionaly Enable AlwaysOn-Verfügbarkeitsgruppen bestimmte erweiterte Ereignisse bei der Diagnose Ursache helfen bei der Problembehebung für einer verfügbarkeitsgruppe.

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Weitere Informationen zu dieser Sitzung XE, finden Sie unter [immer auf erweiterte Ereignisse](http://msdn.microsoft.com/library/dn135324.aspx).

## <a name="create-db-mirroring-endpoint-user"></a>Erstellen Sie Db datenbankspiegelungs Endpunktbenutzer

Die folgende Transact-SQL-Skript erstellt eine Anmeldung mit dem Namen `dbm_login`, und einen Benutzer namens `dbm_user`. Aktualisieren Sie das Skript durch ein sicheres Kennwort ein. Führen Sie den folgenden Befehl für alle SQL Server die datenbankspiegelungs-Endpunktbenutzer erstellen.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>Erstellen Sie ein Zertifikat

SQL Server-Dienst unter Linux verwendet Zertifikate zum Authentifizieren von Kommunikation zwischen der Endpunkte für die datenbankspiegelung. 

Die folgende Transact-SQL-Skript erstellt ein Hauptschlüssel und ein Zertifikat. Klicken Sie dann das Zertifikat sichert, und sichert die Datei mit einem privaten Schlüssel. Aktualisieren Sie das Skript mit sicheren Kennwörtern. Herstellen einer Verbindung mit dem primären SQL Server, und führen Sie die folgende Transact-SQL, um das Zertifikat zu erstellen:

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

Zu diesem Zeitpunkt das primäre Replikat für die SQL Server hat ein Zertifikat unter `/var/opt/mssql/data/dbm_certificate.cer` und einen privaten Schlüssel at `var/opt/mssql/data/dbm_certificate.pvk`. Kopieren Sie diese beiden Dateien am gleichen Speicherort auf allen Servern, die verfügbarkeitsreplikate hosten. Verwenden Sie den Mssql-Benutzer, oder erteilen Sie Berechtigungen Mssql-Benutzer auf diese Dateien zugreifen. 

Auf dem Quellserver kopiert der folgende Befehl z. B. die Dateien auf dem Zielcomputer. Ersetzen Sie die  **<node2>**  Werte mit den Namen der SQL Server-Instanzen, die die Replikate hosten. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

Erteilen Sie Berechtigungen auf dem Zielserver Mssql-Benutzer auf das Zertifikat zugreifen.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>Erstellen Sie das Zertifikat auf dem sekundären Server

Die folgende Transact-SQL-Skript erstellt ein Hauptschlüssel und ein Zertifikat aus der Sicherung, die Sie auf dem primären SQL Server-Replikat erstellt. Der Befehl autorisiert auch die Benutzer auf das Zertifikat zugreifen. Aktualisieren Sie das Skript mit sicheren Kennwörtern. Das Entschlüsselungskennwort ist das gleiche Kennwort, mit denen Sie die PVK-Datei in einem vorherigen Schritt erstellt. Führen Sie das folgende Skript auf allen sekundären Servern zum Erstellen des Zertifikats an.

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

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>Erstellen Sie die datenbankspiegelungs-Endpunkte auf allen Replikaten

Datenbank-Spiegelungsendpunkte senden und empfangen Meldungen zwischen den Serverinstanzen beim Teilnehmen an Datenbankspiegelungssitzungen über TCP (Transmission Control Protocol) oder beim Hosten verfügbarer Replikate. Der Datenbank-Spiegelungsendpunkt lauscht an einer eindeutigen TCP-Portnummer. 

Die folgende Transact-SQL-Anweisung erstellt einen überwachenden Endpunkt mit dem Namen `Hadr_endpoint` für die verfügbarkeitsgruppe dienen. Den Endpunkt gestartet, und bietet connect-Berechtigung für den Benutzer, den Sie erstellt haben. Bevor Sie das Skript ausführen, ersetzen Sie die Werte zwischen `**< ... >**`.


>[!NOTE]
>Verwenden Sie eine andere IP-Adresse nicht für die Listener-IP-Adresse, um für diese Version. Wir arbeiten an der Behebung dieses Problems, aber vorläufig der einzige zulässige Wert ist "0.0.0.0".

Aktualisieren Sie die folgende Transact-SQL für Ihre Umgebung für alle SQL Server-Instanzen: 

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

Ausführliche Informationen finden Sie unter [der Datenbankspiegelungs-Endpunkt (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx).
