---
title: Herstellen einer Verbindung mit Azure Active Directory-Authentifizierung | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.technology:
- drivers
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8ee49e767d8d0b92b1c8a6548b8870822460fa6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Herstellen einer Verbindung mit Azure Active Directory-Authentifizierung

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Dieser Artikel enthält Informationen zum Entwickeln von Java-Anwendungen, die das Feature der Azure Active Directory-Authentifizierung mit Microsoft JDBC Driver 6.0 (oder höher) für SQL Server verwendet.

Sie können Azure Active Directory (AAD)-Authentifizierung ein Mechanismus ist für das Herstellen einer Verbindung mit Azure SQL-Datenbank v12 mithilfe von Identitäten in Azure Active Directory. Azure Active Directory-Authentifizierung zur zentralen Verwaltung von Identitäten von Datenbankbenutzern und als Alternative zu SQL Server-Authentifizierung verwenden. Der JDBC-Treiber können Sie Ihre Azure Active Directory-Anmeldeinformationen in der JDBC-Verbindungszeichenfolge zur Verbindung mit Azure SQL-Datenbank angeben. Informationen zum Konfigurieren von Azure Active Directory-Authentifizierung finden Sie auf [Herstellen einer Verbindung mit SQL-Datenbank durch Verwenden von Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Zwei neue Verbindungseigenschaften wurden hinzugefügt, um Azure Active Directory-Authentifizierung zu unterstützen:
*   **Authentifizierung**: Verwenden Sie diese Eigenschaft, um anzugeben, welche SQL-Authentifizierungsmethoden für die Verbindung verwenden. Mögliche Werte sind: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword**, und der standardmäßige **"NotSpecified"**.
    * Mit "Authentifizierung ActiveDirectoryIntegrated =" für die Verbindung mit einer SQL-Datenbank mithilfe der integrierten Windows-Authentifizierung. Um diesen Authentifizierungsmodus zu verwenden, müssen Sie die lokalen Active Directory Federation Services (ADFS) mit Azure AD in der Cloud zu verbinden. Nachdem dies sowie ein Kerberos-Ticket haben eingerichtet, können Sie die Azure SQL-Datenbank zugreifen, ohne zum Eingeben von Anmeldeinformationen aufgefordert werden, wenn Sie in einem verknüpften Computer zur Domäne angemeldet sind. 
    * Mit "Authentifizierung ActiveDirectoryPassword =" für die Verbindung mit einer SQL-Datenbank mit einem Azure AD-Prinzipalnamen und dem Kennwort.
    * Verwenden "Authentifizierung SqlPassword =" Verbindung mit einem SQL Server mithilfe von Benutzername/Benutzer und Kennwort-Eigenschaften.
    * Mit "Authentifizierung" NotSpecified "=" oder lassen Sie ihn als Standard, wenn keines dieser zwei Authentifizierungsmethoden benötigt werden.

*   **AccessToken**: Verwenden Sie diese Eigenschaft für die Verbindung mit einer SQL-Datenbank mithilfe eines Zugriffstokens. AccessToken kann nur festgelegt werden, verwenden den Eigenschaftenparameter der getConnection()-Methode in der DriverManager-Klasse. Es kann nicht in der Verbindungs-URL verwendet werden.  

Details finden Sie unter der Authentifizierungseigenschaft auf die [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) Seite.  


## <a name="client-setup-requirements"></a>Client-Setup-Anforderungen
Stellen Sie sicher, dass die folgenden Komponenten auf dem Clientcomputer installiert sind:
* Java 7 oder höher
*   Microsoft JDBC Driver 6.0 (oder höher) für SQL Server
*   Wenn Sie den Zugriffsmodus für die Token-basierte Authentifizierung verwenden, müssen Sie [Azure-Active Directory-Bibliothek-für-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) und seine Abhängigkeiten zum Ausführen der Beispiele in diesem Artikel. Weitere Informationen finden Sie unter **Herstellen einer Verbindung mit Access Token** Abschnitt.
*   Wenn Sie den Authentifizierungsmodus ActiveDirectoryPassword verwenden, müssen Sie [Azure-Active Directory-Bibliothek-für-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) und seine Abhängigkeiten. Weitere Informationen finden Sie unter **Herstellen einer Verbindung mit ActiveDirectoryPassword Authentifizierungsmodus** Abschnitt.
*   Wenn Sie den ActiveDirectoryIntegrated-Modus verwenden, benötigen Sie Azure-Active Directory-Bibliothek-für-Java und seine Abhängigkeiten. Weitere Informationen finden Sie unter **Herstellen einer Verbindung mit ActiveDirectoryIntegrated Authentifizierungsmodus** Abschnitt.
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Herstellen einer Verbindung mit ActiveDirectoryIntegrated-Authentifizierungsmodus
 Mit Version 6.4 fügt Microsoft JDBC Driver Unterstützung für ActiveDirectoryIntegrated-Authentifizierung mit einem Kerberos-Ticket auf mehreren Plattformen (Windows/Linux und Mac).
Finden Sie unter [legen Sie Kerberos-Ticket unter Windows, Linux und Macintosh](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac) Weitere Details. Alternativ können unter Windows, "sqljdbc_auth.dll" auch für die Authentifizierung ActiveDirectoryIntegrated JDBC-Treiber verwendet werden.

> [!NOTE]
>  Wenn Sie eine ältere Version des Treibers verwenden, aktivieren Sie diese Option [Link](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md) für die entsprechenden Abhängigkeiten, die zum Verwenden dieses Authentifizierungsmodus erforderlich sind. 

Das folgende Beispiel zeigt, wie mit "Authentifizierung ActiveDirectoryIntegrated =" Modus. Führen Sie dieses Beispiel aus, auf einem Computer zur Domäne gehört, der mit Azure Active Directory verbunden ist. Die Benutzer einer eigenständigen Datenbank, die Ihrem Azure AD-Prinzipal oder einer der Gruppen darstellt, müssen Sie angehören, müssen in der Datenbank vorhanden sein und die CONNECT-Berechtigung. 

Vor dem Erstellen und das Beispiel ausführen, auf dem Clientcomputer (auf, die zum Ausführen des Beispiels werden sollen), Herunterladen der [Azure-Active Directory-Bibliothek-für-Java-Bibliothek](https://github.com/AzureAD/azure-activedirectory-library-for-java) und ihre Abhängigkeiten, und sie in der Java-Buildpfad einfügen

Ersetzen Sie den Namen des Server-Datenbank mit dem Namen Ihres Server-Datenbank in den folgenden Zeilen, bevor Sie das Beispiel ausführen:

```
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

Im Beispiel ActiveDirectoryIntegrated Authentifizierungsmodus verwenden:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class IntegratedExample {

    public static void main(String[] args) throws Exception {
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
Dieses Beispiel ausführen, auf einem Clientcomputer automatisch die Kerberos-Ticket verwendet und ist kein Kennwort erforderlich. Wenn eine Verbindung hergestellt wird, sollten Sie die folgende Meldung angezeigt:
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>Legen Sie die Kerberos-Ticket für Windows, Linux und Mac

Sie müssen ein Kerberos-Ticket verknüpfen Ihres aktuellen Benutzers in ein Windows-Domänenkonto einrichten. Eine Zusammenfassung der wichtigsten Schritte finden Sie weiter unten.

#### <a name="windows"></a>Windows
Im Lieferumfang von JDK `kinit` mit Schlüsselverteilungscenter (Key Distribution Center) ein TGT entnommen werden in einer Domäne verknüpft Computer, die mit Azure Active Directory verbunden ist.

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>Schritt 1: Ticket Granting Ticket abrufen
- **Führen Sie auf**: Windows
- **Aktion**:
  - Verwenden Sie den Befehl `kinit username@DOMAIN.COMPANY.COM` um ein TGT vom KDC zu erhalten, dann werden Sie aufgefordert für das Domänenkennwort ein.
  - Verwendung `klist` auf die verfügbaren Tickets finden Sie unter. Wenn die Kinit erfolgreich war, sollte ein Ticket aus krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM angezeigt werden.

> [!NOTE]
>  Müssen Sie möglicherweise angeben einer `.ini` -Datei mit `-Djava.security.krb5.conf` für Ihre Anwendung KDC zu suchen.

#### <a name="linux-and-mac"></a>Linux und Mac

##### <a name="requirements"></a>Anforderungen
Zugriff auf eine Windows-Domäne eingebundenen Computer zum Abfragen der Kerberos-Domänencontroller

##### <a name="step-1-find-kerberos-kdc"></a>Schritt 1: Suchen der Kerberos-KDC
- **Führen Sie auf**: Windows-Befehlszeile
- **Aktion**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (wobei "DOMAIN.COMPANY.COM" ordnet in Ihrer Domäne-Namen)
- **Beispielausgabe**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **Informationen zum Extrahieren** der DC-name, in diesem Fall `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>Schritt 2: Konfigurieren der KDC in krb5.conf
- **Führen Sie auf**: Linux/Mac
- **Aktion**: Bearbeiten der /etc/krb5.conf in einem Editor Ihrer Wahl. Konfigurieren Sie die folgenden Schlüssel
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  Speichern Sie die Datei krb5.conf, und beenden

> [!NOTE]
>  Domäne muss in Großbuchstaben.

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>Schritt 3: Testen des Ticket-Granting-Ticket-Abrufs
- **Führen Sie auf**: Linux/Mac
- **Aktion**:
  - Verwenden Sie den Befehl `kinit username@DOMAIN.COMPANY.COM` um ein TGT vom KDC zu erhalten, dann werden Sie aufgefordert für das Domänenkennwort ein.
  - Verwendung `klist` auf die verfügbaren Tickets finden Sie unter. Wenn die Kinit erfolgreich war, sollte ein Ticket aus krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM angezeigt werden.

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>Herstellen einer Verbindung mit ActiveDirectoryPassword-Authentifizierungsmodus
Das folgende Beispiel zeigt, wie mit "Authentifizierung ActiveDirectoryPassword =" Modus.

Vor dem Erstellen und Ausführen des Beispiels:
1.  Auf dem Clientcomputer (auf, die zum Ausführen des Beispiels werden sollen), Herunterladen der [Azure-Active Directory-Bibliothek-für-Java-Bibliothek](https://github.com/AzureAD/azure-activedirectory-library-for-java) und ihre Abhängigkeiten, und sie in der Java-Buildpfad einfügen
2.  Suchen Sie die folgenden Codezeilen, und Ersetzen Sie den Namen des Server-Datenbank durch den Namen des Server-Datenbank.
    ```
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  Suchen Sie die folgenden Codezeilen, und Ersetzen Sie Benutzernamen ein, mit dem Namen des Azure AD-Benutzers, die Sie als eine Verbindung herstellen möchten.
    ```
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

Im Beispiel ActiveDirectoryPassword Authentifizierungsmodus verwenden:
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class UserPasswordExample {
    
    public static void main(String[] args) throws Exception{
        SQLServerDataSource ds = new SQLServerDataSource();
        
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        Connection connection = ds.getConnection();
        
        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
Wenn die Verbindung hergestellt wurde, sollte die folgende Meldung als Ausgabe angezeigt werden:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Ein enthaltener Benutzer-Remotedatenbank muss vorhanden sein und die Benutzer einer eigenständigen Datenbank, die den angegebenen Azure AD-Benutzers oder einer der Gruppen, die angegebene Azure AD-Benutzer angehört, müssen in der Datenbank vorhanden sein und benötigen die CONNECT-Berechtigung (mit Ausnahme von Azure Active Directory Serveradministrator oder Gruppe)


## <a name="connecting-using-access-token"></a>Herstellen einer Verbindung mit Access Token
Anwendungen/Dienste ein Zugriffstoken aus Azure Active Directory abrufen und verwenden, die zur Verbindung mit SQL Azure-Datenbank. Beachten Sie, dass diese AccessToken nur festgelegt werden kann, verwenden den Eigenschaftenparameter der getConnection()-Methode in der DriverManager-Klasse. Es kann nicht in der Verbindungszeichenfolge verwendet werden.
 
Das folgende Beispiel enthält eine einfache Java-Anwendung, die eine Verbindung mit Access Token-basierte Authentifizierung mit Azure SQL-Datenbank herstellt. Führen Sie vor dem Erstellen und Ausführen des Beispiels, die folgenden Schritte aus:
1.  Erstellen Sie ein Anwendungskonto in Azure Active Directory für den Dienst an.
    1. Melden Sie sich beim Azure-Verwaltungsportal
    2. Klicken Sie im linken Navigationsbereich auf Azure Active Directory
    3. Klicken Sie auf der Registerkarte "App-Registrierungen".
    4. Klicken Sie im Bereich auf "Neue anwendungsregistrierung".
    5. Geben Sie einen Anzeigenamen für die Anwendung ein Mytokentest, wählen Sie "Web-App/API".
    6. Anmelde-URL wird nicht erforderlich. Geben Sie nur etwas: "http://mytokentest".
    7. Klicken Sie unten auf "Erstellen".
    9. Klicken Sie noch im Azure-Portal klicken Sie auf der Registerkarte "Einstellungen" der Anwendung, und Öffnen der Registerkarte "Eigenschaften".
    10. Suchen Sie den Wert "Anwendungs-ID" (AKA Client-ID), und kopieren Sie sie zur Seite gedrängt, dies ist erforderlich später beim Konfigurieren Ihrer Anwendung (z. B. 1846943b-ad04-4808-aa13-4702d908b5c1). Sehen Sie die folgenden Momentaufnahme.
    11. Suchen Sie den Wert "App-ID-URL", und kopieren Sie sie zur Seite gedrängt, dies ist die STS-URL.
    12. Erstellen Sie einen Schlüssel im Abschnitt "Schlüssel" die Dauer des Schlüssels auswählen, füllen im Feld "Name" und speichern die Konfiguration (lassen das Feld "Wert" leer). Nach dem Speichern, muss das Feld "Wert" automatisch ausgefüllt, kopieren Sie den generierten Wert. Dies ist der Client geheimen Schlüssel.

    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. Melden Sie sich mit Ihrem Azure SQL-Server-Benutzerdatenbank sowie einen Azure Active Directory-Administrator mithilfe einer T-SQL-Befehl bereitstellen Benutzer einer eigenständigen Datenbank für Ihre Anwendung Prinzipal. Finden Sie unter der [Herstellen einer Verbindung mit SQL-Datenbank oder SQL Data Warehouse durch Verwenden von Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) Weitere ausführliche Informationen zum Erstellen einer Azure Active Directory-Administrator und Benutzer einer eigenständigen Datenbank.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  Auf dem Clientcomputer (auf, die zum Ausführen des Beispiels werden sollen), Herunterladen der [Azure-Active Directory-Bibliothek-für-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) -Bibliothek und ihre Abhängigkeiten, und sie in der Java-Buildpfad einzuschließen. Beachten Sie, dass die Azure-Active Directory-Bibliothek-für-Java nur erforderlich ist, um dieses konkrete Beispiel auszuführen, wie sie die APIs aus dieser Bibliothek verwendet, um das Zugriffstoken aus Azure AD abzurufen. Wenn Sie bereits über ein Zugriffstoken verfügen, können Sie diesen Schritt überspringen. Beachten Sie, dass müssen Sie auch den Abschnitt im Beispiel zu entfernen, das Zugriffstoken abruft.

Ersetzen Sie im folgenden Beispiel STS-URL, Client-ID, den geheimen Clientschlüssel, Server-und Datenbank durch die entsprechenden Werte ein.

```
import java.sql.Connection;
import java.sql.ResultSet;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD. 
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;


public class TokenBasedExample {

    public static void main(String[] args) throws Exception{

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://microsoft.onmicrosoft.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);     
        
        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

Wenn die Verbindung erfolgreich ist, sollte die folgende Meldung als Ausgabe angezeigt werden:
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
