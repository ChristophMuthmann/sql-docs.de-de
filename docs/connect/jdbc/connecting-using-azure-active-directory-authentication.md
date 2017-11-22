---
title: Herstellen einer Verbindung mit Azure Active Directory-Authentifizierung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.technology: drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3dde204d199935b25f492ed23fadb3c2d4e70a99
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-using-azure-active-directory-authentication"></a>Herstellen einer Verbindung mit Azure Active Directory-Authentifizierung
Dieser Artikel enthält Informationen zum Entwickeln von Java-Anwendungen, die das Feature der Azure Active Directory-Authentifizierung mit Microsoft JDBC Driver 6.0 (oder höher) für SQL Server verwendet.

Ab Microsoft JDBC Driver 6.0 für SQL Server, können Sie Azure Active Direcoty (AAD)-Authentifizierung einen Mechanismus dar, der Herstellen einer Verbindung mit Azure SQL-Datenbank v12 wird mithilfe von Identitäten in Azure Active Directory. Azure Active Directory-Authentifizierung zur zentralen Verwaltung von Identitäten von Datenbankbenutzern und als Alternative zu SQL Server-Authentifizierung verwenden. Der JDBC-Treiber 6.0 (oder höher) können Sie Ihre Azure Active Directory-Anmeldeinformationen in der JDBC-Verbindungszeichenfolge zur Verbindung mit Azure SQL-Datenbank angeben. Informationen zum Konfigurieren von Azure Active Directory-Authentifizierung finden Sie auf [Herstellen einer Verbindung mit SQL-Datenbank durch Verwenden von Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/). 

Zwei neue Verbindungseigenschaften wurden hinzugefügt, um Azure Active Directory-Authentifizierung zu unterstützen:
*   **Authentifizierung**: Verwenden Sie diese Eigenschaft, um anzugeben, welche SQL-Authentifizierungsmethoden für die Verbindung verwenden. Mögliche Werte sind: **ActiveDirectoryIntegrated**, **ActiveDirectoryPassword**, **SqlPassword** und der standardmäßige **"NotSpecified"** .
    * Mit "Authentifizierung ActiveDirectoryIntegrated =" für die Verbindung mit einer SQL-Datenbank mithilfe der integrierten Windows-Authentifizierung. Zum Verwenden dieses Authentifizierungsmodus müssen Sie die lokalen Active Directory Federation Services (ADFS) mit Azure AD in der Cloud zu verbinden. Sobald dies eingerichtet ist, können Sie die Azure SQL-Datenbank zugreifen, ohne die Nachfrage nach Ceredentials, wenn Sie in einem verknüpften Computer zur Domäne angemeldet sind. 
    * Mit "Authentifizierung ActiveDirectoryPassword =" für die Verbindung mit einer SQL-Datenbank mit einem Azure AD-Prinzipalnamen und dem Kennwort.
    * Verwenden "Authentifizierung SqlPassword =" Verbindung mit einem SQL Server mithilfe von Benutzername/Benutzer und Kennwort-Eigenschaften.
    * Mit "Authentifizierung" NotSpecified "=" oder lassen Sie ihn als Standard, wenn keines dieser zwei Authentifizierungsmethoden erforderlich ist.

*   **AccessToken**: Verwenden Sie diese Eigenschaft für die Verbindung mit einer SQL-Datenbank mithilfe eines Zugriffstokens. AccessToken kann nur festgelegt werden, verwenden den Eigenschaftenparameter der getConnection()-Methode in der DriverManager-Klasse. Es kann nicht in der Verbindungs-URL verwendet werden.  

Details finden Sie unter der Authentifizierungseigenschaft auf die [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md) Seite.  


## <a name="client-setup-requirements"></a>Client-Setup-Anforderungen
Stellen Sie sicher, dass die folgenden Komponenten auf dem Clientcomputer installiert sind:
* Java 7 oder höher
*   Microsoft JDBC Driver 6.2 (oder höher) für SQL Server
*   Wenn Sie den Zugriffsmodus für die token-basierte Authentifizierung verwenden, müssen Sie [Azure-Active Directory-Bibliothek-für-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) und seine Abhängigkeiten zum Ausführen der Beispiele in diesem Artikel. Finden Sie unter **Herstellen einer Verbindung mit Access Token** Abschnitt, um weitere Details.
*   Wenn Sie den Authentifizierungsmodus ActiveDirectoryPassword verwenden müssen Sie [Azure-Active Directory-Bibliothek-für-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) und seine Abhängigkeiten. Finden Sie unter **Herstellen einer Verbindung mit ActiveDirectoryPassword Authentifizierungsmodus** Abschnitt, um weitere Details.
*   Wenn Sie den ActiveDirectoryIntegrated-Modus verwenden, müssen Sie installieren die Active Directory-Authentifizierungsbibliothek für SQL Server (ADALSQL. (DLL) und "sqljdbc_auth.dll".
    * ADALSQL. DLL kann Anwendungen mit Microsoft Azure SQL-Datenbank mithilfe von Azure Active Directory authentifizieren. Die DLL aus dem Download [Microsoft Active Directory-Authentifizierungsbibliothek für Microsoft SQL Server](http://www.microsoft.com/en-us/download/details.aspx?id=48742)
    * Für ADALSQL. Es sind zwei binären Versionen für die DLL X86- und X64 zum Herunterladen verfügbar. Wenn die falsche binäre Version installiert ist oder wenn die DLL nicht vorhanden ist, der Treiber die folgende Fehlermeldung löst wird: "kann nicht geladen adalsql.dll (Authentication =...). Fehlercode: 0 x 2. ". Herunterladen Sie in diesem Fall die richtige Version von ADALSQL DLL. 
    * "sqljdbc_auth.dll" ist im Treiberpaket enthaltenen verfügbar. Kopieren Sie die Datei "sqljdbc_auth.dll" in ein Verzeichnis auf dem Windows-Systempfad auf dem Computer, auf dem der JDBC-Treiber installiert ist. Alternativ können Sie mit der java.libary.path-Systemeigenschaft das Verzeichnis von „sqljdbc_auth.dll“ angeben. 
    * Wenn Sie eine 64-Bit-JVM mit einem x64-Prozessor ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x64“. 
    * Wenn Sie eine 32-Bit-JVM (Java Virtual Machine) ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x86“, auch wenn es sich bei dem Betriebssystem um die x64-Version handelt. 
    * Beispielsweise können, wenn Sie die 32-Bit-JVM und der JDBC-Treiber wird im Standardverzeichnis installiert, Sie geben Sie den Speicherort der DLL mit dem folgenden Argument für den virtuellen Computer (VM) beim Start der Java-Anwendung:  
        ```
        -Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86
        ```
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>Herstellen einer Verbindung mit ActiveDirectoryIntegrated-Authentifizierungsmodus
Das folgende Beispiel zeigt, wie mit "Authentifizierung ActiveDirectoryIntegrated =" Modus. Führen Sie dieses Beispiel aus, auf einem Computer zur Domäne gehört, der mit Azure Active Directory verbunden ist. Die Benutzer einer eigenständigen Datenbank, die Ihrem Azure AD-Prinzipal oder einer der Gruppen darstellt, müssen Sie angehören, müssen in der Datenbank vorhanden sein und die CONNECT-Berechtigung. 
    
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
In diesem Beispiel auf einem Computer, der Mitglied einer Domäne, die einen Verbund mit Azure Active Directory wird ausgeführt, wird automatisch Windows-Anmeldeinformationen verwenden, und kein Kennwort erforderlich ist. Wenn die Verbindung hergestellt wurde, wird die folgende Meldung angezeigt:
```
You have successfully logged on as: <your domain user name>
```

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
Wenn die Verbindung hergestellt wurde, wird die folgende Meldung als Ausgabe angezeigt:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> Ein enthaltener Benutzer-Remotedatenbank muss vorhanden sein und die Benutzer einer eigenständigen Datenbank, die den angegebenen Azure AD-Benutzers oder einer der Gruppen, die angegebene Azure AD-Benutzer gehört, muss in der Datenbank vorhanden sein und muss die CONNECT-Berechtigung (mit Ausnahme von Azure Active Directory Serveradministrator oder Gruppe)


## <a name="connecting-using-access-token"></a>Herstellen einer Verbindung mit Access Token
Anwendungen/Dienste ein Zugriffstoken aus Azure Active Directory abrufen und verwenden, die zur Verbindung mit SQL Azure-Datenbank. Beachten Sie, dass diese AccessToken nur festgelegt werden kann, verwenden den Eigenschaftenparameter der getConnection()-Methode in der DriverManager-Klasse. Es kann nicht in der Verbindungszeichenfolge verwendet werden.
 
Das folgende Beispiel enthält eine einfache Java-Anwendung, die eine Verbindung mit Access token-basierte Authentifizierung mit Azure SQL-Datenbank herstellt. Führen Sie vor dem Erstellen und Ausführen des Beispiels, die folgenden Schritte aus:
1.  Erstellen Sie ein Anwendungskonto in Azure Active Directory für den Dienst an.
    1. Melden Sie sich beim Azure-Verwaltungsportal
    2. Klicken Sie im linken Navigationsbereich auf Azure Active Directory
    3. Klicken Sie auf den verzeichnismandanten, wo die beispielanwendung registriert werden sollen. Dies muss im selben Verzeichnis, das Ihre Datenbank (der Server, auf dem Ihre Datenbank gehostet wird) zugeordnet ist.
    4. Klicken Sie auf der Registerkarte "Anwendungen".
    5. Klicken Sie auf "hinzufügen", in dem Bereich.
    6. Klicken Sie auf "Eine von meinem Unternehmen entwickelte Anwendung hinzufügen".
    7. Geben Sie einen Anzeigenamen für die Anwendung ein Mytokentest, wählen Sie "Webanwendung/oder Web-API", und klicken Sie auf Weiter.
    8. Vorausgesetzt, dass diese Anwendung ein daemondienst und nicht für eine Webanwendung ist, nicht es ein Anmeldeseite-URL oder app-ID-URI verfügen. Geben Sie für diese zwei Felder http://mytokentest
    9. Klicken Sie noch im Azure-Portal auf der Registerkarte "konfigurieren" der Anwendung
    10. Suchen Sie den Client-ID-Wert, und kopieren Sie sie zur Seite gedrängt, diesen benötigen Sie später beim Konfigurieren der Anwendungsstatus (d. h.  a4bbfe26-dbaa-4fec-8ef5-223d229f647d). Finden Sie in der Momentaufnahme, die weiter unten.
    11. Abschnitt "Schlüssel" Wählen Sie die Dauer des Schlüssels, speichern Sie die Konfiguration zu, und kopieren Sie den Schlüssel für die spätere Verwendung. Dies ist der Client geheimen Schlüssel.
    12. Klicken Sie im unteren Bereich klicken Sie auf "Anzeigen von Endpunkten", und kopieren Sie die URL unter "OAUTH 2.0-AUTORISIERUNGSENDPUNKT" für die spätere Verwendung. Dies ist der STS-URL.


![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)


2. Melden Sie sich mit Ihrem Azure SQL-Server-Benutzerdatenbank sowie einen Azure Active Directory-Administrator mithilfe einer T-SQL-Befehl bereitstellen Benutzer einer eigenständigen Datenbank für Ihre Anwendungsprinzipal. Finden Sie unter der [Herstellen einer Verbindung mit SQL-Datenbank oder SQL Data Warehouse durch Verwenden von Azure Active Directory-Authentifizierung](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/) Weitere ausführliche Informationen zum Erstellen einer Azure Active Directory-Administrator und Benutzer einer eigenständigen Datenbank.

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  Auf dem Clientcomputer (auf, die zum Ausführen des Beispiels werden sollen), Herunterladen der [Azure-Active Directory-Bibliothek-für-Java](https://github.com/AzureAD/azure-activedirectory-library-for-java) -Bibliothek und ihre Abhängigkeiten, und sie in der Java-Buildpfad einzuschließen. Beachten Sie, dass die Azure-Active Directory-Bibliothek-für-Java nur erforderlich ist, um dieses konkrete Beispiel auszuführen, wie sie die APIs aus dieser Bibliothek verwendet, um das Zugriffstoken aus Azure AD abzurufen. Wenn Sie bereits über ein Zugriffstoken verfügen, können Sie diesen Schritt überspringen. Beachten Sie, dass müssen Sie auch im Abschnitt im Beispiel zu entfernen, das Zugriffstoken abruft.

Ersetzen Sie im folgenden Beispiel wird die STS-URL, Client-ID, den geheimen Clientschlüssel, Server und Datenbanknamen mit Ihren Werten ein.

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
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "a4bbfe26-dbaa-4fec-8ef5-223d229f647d"; // Replace with your client ID.
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

Wenn die Verbindung erfolgreich ist, wird die folgende Meldung als Ausgabe angezeigt:
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
