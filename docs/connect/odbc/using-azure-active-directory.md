---
title: Mithilfe von Azure Active Directory mit dem ODBC-Treiber | Microsoft Docs
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52205f03-ff29-4254-bfa8-07cced155c86
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 801f0ec683811776b7a249e4984030d3496e5a1e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-azure-active-directory-with-the-odbc-driver"></a>Mithilfe von Azure Active Directory mit dem ODBC-Treiber
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="purpose"></a>Zweck

Der ODBC Driver 13.1 for SQL Server ODBC-Anwendungen für die Verbindung mit einer Instanz von SQL Azure ermöglicht es mit einem Identitätsverbund in Azure Active Directory mit Benutzername/Kennwort, ein Zugriffstoken von Azure Active Directory (nur Windows-Treiber) oder integrierte Windows- Authentifizierung (nur Windows-Treiber). Dies wird durch die Verwendung von neuen DSN und Schlüsselwörter für Verbindungszeichenfolgen sowie die Verbindungsattribute erreicht.

## <a name="new-andor-modified-dsn-and-connection-string-keywords"></a>Neue und/oder geänderte DSN und Schlüsselwörter für Verbindungszeichenfolgen

Die `Authentication` -Schlüsselwort kann verwendet werden bei der Verbindung mit einer Zeichenfolge DSN- oder Verbindungszeichenfolge den Authentifizierungsmodus zu steuern. Der Wert in der Verbindungszeichenfolge festgelegt wird, die in der DSN überschrieben, wenn bereitgestellt. Die _vorab-Attributwert_ von der `Authentication` Einstellung wird der Wert aus der Verbindungszeichenfolge und die DSN-Werte berechnet.

|Name|Werte|Standardwert|Description|
|-|-|-|-|
|`Authentication`|(nicht festgelegt), (leere Zeichenfolge), `SqlPassword`, `ActiveDirectoryPassword`,`ActiveDirectoryIntegrated`|(nicht festgelegt)|Steuert den Authentifizierungsmodus an.<table><tr><th>Wert<th>Description<tr><td>(nicht festgelegt)<td>Authentifizierungsmodus bestimmt durch andere Schlüsselwörter (vorhandenen älteren Verbindungsoptionen.)<tr><td>(leere Zeichenfolge)<td>(Verbindungszeichenfolge nur.) Außer Kraft setzen und Festlegung einer `Authentication` festgelegten in DSN angegebene Wert.<tr><td>`SqlPassword`<td>Direkt mit einer SQL Server-Instanz, die mit einem Benutzernamen und Kennwort zu authentifizieren.<tr><td>`ActiveDirectoryPassword`<td>Mit einer Azure Active Directory-Identität mit einem Benutzernamen und Kennwort zu authentifizieren.<tr><td>`ActiveDirectoryIntegrated`<td>_Nur Windows-Treiber_. Mit einer Azure Active Directory-Identität, die mithilfe der integrierten Authentifizierung authentifizieren.</table>|
|`Encrypt`|(nicht festgelegt), `Yes`,`No`|(siehe Beschreibung)|Steuert die Verschlüsselung für eine Verbindung. Wenn das erforderliche Attribut den Wert der `Authentication` Einstellung ist nicht _keine_, der Standardwert ist `Yes`. Andernfalls der Standardwert ist `No`. Der erforderliche Attributwert der Verschlüsselung ist `Yes` , wenn der Wert, um festgelegt ist `Yes` in entweder die DSN-oder Verbindungszeichenfolge.|

## <a name="new-andor-modified-connection-attributes"></a>Neue und/oder geänderte Verbindungsattribute

Die folgenden Verbindung vordefinierten Attribute entweder eingeführt oder geändert wurden zur Unterstützung von Azure Active Directory-Authentifizierung. Wenn ein Verbindungsattribut verfügt über eine entsprechende Verbindungszeichenfolge oder DSN-Schlüsselwort und festgelegt ist, hat das Verbindungsattribut Vorrang vor.

|Attribut|Typ|Werte|Standardwert|Description|
|-|-|-|-|-|
|`SQL_COPT_SS_AUTHENTICATION`|`SQL_IS_INTEGER`|`SQL_AU_NONE`, `SQL_AU_PASSWORD`, `SQL_AU_AD_INTEGRATED`, `SQL_AU_AD_PASSWORD`, `SQL_AU_RESET`|(nicht festgelegt)|Finden Sie in der Beschreibung der `Authentication` Schlüsselwort oben. `SQL_AU_NONE`wird bereitgestellt, um einen Satz explizit überschreiben `Authentication` Wert in der Zeichenfolge DSN und/oder Verbindung während `SQL_AU_RESET` das Attribut, wenn er festgelegt wurde, ermöglicht die DSN- oder Verbindungszeichenfolge Zeichenfolgenwert Vorrang, hebt die Festlegung.|
|`SQL_COPT_SS_ACCESS_TOKEN`|`SQL_IS_POINTER`|Zeiger auf `ACCESSTOKEN` oder NULL|NULL|_Nur Windows-Treiber_. Wenn nicht Null ist, gibt der Azure AD-Zugriffstokens verwenden. Es ist ein Fehler auf, geben Sie ein Zugriffstoken sowie `UID`, `PWD`, `Trusted_Connection`, oder `Authentication` Verbindungszeichenfolgen-Schlüsselwörter oder deren entsprechende Attribute.|
|`SQL_COPT_SS_ENCRYPT`|`SQL_IS_INTEGER`|`SQL_EN_OFF`, `SQL_EN_ON`|(siehe Beschreibung)|Steuert die Verschlüsselung für eine Verbindung. `SQL_EN_OFF`und `SQL_EN_ON` deaktivieren und Aktivieren der Verschlüsselung, bzw. Wenn das erforderliche Attribut den Wert der `Authentication` Einstellung ist nicht _keine_ oder `SQL_COPT_SS_ACCESS_TOKEN` festgelegt ist, und `Encrypt` wurde nicht angegeben entweder die DSN- oder Verbindungszeichenfolge-Zeichenfolge, die Standardeinstellung ist `SQL_EN_ON`. Andernfalls der Standardwert ist `SQL_EN_OFF`. Der tatsächliche Wert der dieses Attribut steuert [ob Verschlüsselung für die Verbindung verwendet wird.](https://docs.microsoft.com/en-us/sql/relational-databases/native-client/features/using-encryption-without-validation)|
|`SQL_COPT_SS_OLDPWD`|\-|\-|\-|Mit Azure Active Directory, unterstützt nicht, da kennwortänderungen AAD Prinzipalen über eine ODBC-Verbindung nicht erreicht werden können. <br><br>Ablauf des Kennworts für die SQL Server-Authentifizierung wurde in SQL Server 2005 eingeführt. Die `SQL_COPT_SS_OLDPWD` -Attribut wurde hinzugefügt, damit der Client sowohl das alte als auch das neue Kennwort für die Verbindung angeben kann. Wenn diese Eigenschaft festgelegt ist, verwendet der Anbieter für die erste Verbindung oder für nachfolgende Verbindungen keinen Verbindungspool, da die Verbindungszeichenfolge das "alte Kennwort" enthält, das inzwischen geändert wurde.|
|`SQL_COPT_SS_INTEGRATED_SECURITY`|`SQL_IS_INTEGER`|`SQL_IS_OFF`,`SQL_IS_ON`|`SQL_IS_OFF`|_Als veraltet markiert_; verwenden Sie `SQL_COPT_SS_AUTHENTICATION` festgelegt `SQL_AU_AD_INTEGRATED` stattdessen. <br><br>Erzwingt, der Windows-Authentifizierung (Kerberos auf Linux- und MacOS) für Access-Überprüfung auf dem Server-Anmeldung verwenden. Wenn Windows-Authentifizierung verwendet wird, ignoriert der Treiber als Teil der bereitgestellten Werte für Benutzer-ID und Kennwort `SQLConnect`, `SQLDriverConnect`, oder `SQLBrowseConnect` verarbeiten.|

## <a name="ui-additions-for-azure-active-directory-windows-driver-only"></a>UI-Ergänzungen für Azure Active Directory (nur Windows-Treiber)

Das DSN-Setup und die Verbindung Benutzeroberflächen des Treibers wurden mit den zusätzlichen Optionen erforderlich für die Verwendung der Authentifizierung mit Azure AD erweitert.

### <a name="creating-and-editing-dsns-in-the-ui"></a>Erstellen und Bearbeiten von DSNs in der Benutzeroberfläche

Es ist möglich, verwenden Sie den neuen Azure AD-Authentifizierungsoptionen beim Erstellen oder Bearbeiten einer vorhandenen DSN mithilfe der Treiber-Setup-Benutzeroberfläche:

`Authentication=ActiveDirectoryIntegrated`für die Azure Active Directory-integrierte Authentifizierung mit SQL Azure

![CreateNewDSN3.png](windows/CreateNewDSN3.png)

`Authentication=ActiveDirectoryPassword`für Azure Active Directory-Benutzername/Kennwort-Authentifizierung in SQL Azure

![CreateNewDSN4.png](windows/CreateNewDSN4.png)

`Authentication=SqlPassword`für die Benutzername/Kennwort-Authentifizierung bei SQL Server (Azure oder anderweitig)

![CreateNewDSN.png](windows/CreateNewDSN.png)

`Trusted_Connection=Yes`für Windows integrierte legacy SSPI-Authentifizierung

![CreateNewDSN2.png](windows/CreateNewDSN2.png)

Die vier Optionen entsprechen `Trusted_Connection=Yes` (vorhandenen älteren Windows integrierte Authentifizierung nur über SSPI) und `Authentication=` `ActiveDirectoryIntegrated`, `SqlPassword`, und `ActiveDirectoryPassword`bzw.

### <a name="sqldriverconnect-prompt-windows-driver-only"></a>SQLDriverConnect-Eingabeaufforderung (nur Windows-Treiber)

Das Dialogfeld "Prompt" von SQLDriverConnect angezeigt wird, wenn diese Informationen erforderlich, um die Verbindung anfordert enthält zwei neue Optionen für Azure AD-Authentifizierung:

![SQLServerLogin.png](windows/SQLServerLogin.png)

Diese Optionen entsprechen den gleichen vier in der DSN-Setup-Benutzeroberfläche, die oben genannten verfügbar.

### <a name="example-connection-strings"></a>Exemplarische Verbindungszeichenfolgen
1. SQL Server-Authentifizierung – legacy-Syntax. Serverzertifikat wird nicht überprüft, und Verschlüsselung verwendet wird, nur dann, wenn der Server sie durchsetzt. Der Benutzername/Kennwort wird in der Verbindungszeichenfolge übergeben.
`server=Server;database=Database;UID=UserName;PWD=Password;`
2. SQL-Authentifizierung – neue Syntax. Fordert der Client-Verschlüsselung (der Standardwert `Encrypt` ist `true`) und das Serverzertifikat überprüft wurden, unabhängig von der verschlüsselungseinstellung (es sei denn, `TrustServerCertificate` festgelegt ist, um `true`). Der Benutzername/Kennwort wird in der Verbindungszeichenfolge übergeben.
 `server=Server;database=Database;UID=UserName;PWD=Password;Authentication=SqlPassword;`
3. Integrierte Windows-Authentifizierung (Kerberos auf Linux- und MacOS) mithilfe der SSPI (auf SQL Server- oder SQL IaaS) – aktuelle-Syntax. Serverzertifikat wird nicht überprüft, es sei denn, die Verschlüsselung verwendet wird. 
`server=Server;database=Database;Trusted_Connection=yes;`
4. (_Nur die Windows-Treiber_.) Integrierte Windows-Authentifizierung unter Verwendung von SSPI (wenn die Zieldatenbank in SQL Server oder SQL IaaS ist) – neue Syntax. Fordert der Client-Verschlüsselung (der Standardwert `Encrypt` ist `true`) und das Serverzertifikat überprüft wurden, unabhängig von der verschlüsselungseinstellung (es sei denn, `TrustServerCertificate` festgelegt ist, um `true`). 
`server=Server;database=Database;Authentication=ActiveDirectoryIntegrated;`
5. AAD Benutzername/Kennwort-Authentifizierung (wenn die Zieldatenbank in Azure SQL-Datenbank ist). Serverzertifikat überprüft Ruft ab, unabhängig von der verschlüsselungseinstellung (es sei denn, `TrustServerCertificate` festgelegt ist, um `true`). Der Benutzername/Kennwort wird in der Verbindungszeichenfolge übergeben. 
`server=Server;database=Database;UID=UserName;PWD=Password;Authentication=ActiveDirectoryPassword;`
6. (_Nur die Windows-Treiber_.) Integrierte Windows-Authentifizierung mit ADAL, der auch die Windows-Kontoanmeldeinformationen für ein AAD-seitig Zugriffstoken einlösen, vorausgesetzt, dass die Zieldatenbank in Azure SQL-Datenbank befindet. Serverzertifikat überprüft Ruft ab, unabhängig von der verschlüsselungseinstellung (es sei denn, `TrustServerCertificate` festgelegt ist, um `true`). 
`server=Server;database=Database; Authentication=ActiveDirectoryIntegrated;`

> [!NOTE] 
>- Wenn Sie die neuen Active Directory-Optionen mit der Windows-ODBC-Treiber verwenden, stellen Sie sicher, dass die [Active Directory-Authentifizierungsbibliothek für SQL Server](http://go.microsoft.com/fwlink/?LinkID=513072) installiert wurde. Die Treiber für Linux und MacOS erfordern keine zusätzlichen Abhängigkeiten für die Authentifizierung bei Azure Active Directory.
>- Um eine Verbindung herzustellen, verwenden einen SQL Server-Benutzernamen und ein Kennwort, können jetzt verwenden Sie die neue `SqlPassword` Option, die speziell für SQL Azure empfohlen wird, da diese Option sicherer Standardwerte für die Verbindung ermöglicht.
>- Beim Verbinden mit einer Azure Active Directory-Benutzernamen und Kennwort angeben `Authentication=ActiveDirectoryPassword` in der Verbindungszeichenfolge und die `UID` und `PWD` Schlüsselwörter, mit dem Benutzernamen und Kennwort bzw.
>- Um die integrierte Windows-Authentifizierung oder Active Directory-integrierte (nur Windows-Treiber) Authentifizierung zu verbinden, geben Sie `Authentication=ActiveDirectoryIntegrated` in der Verbindungszeichenfolge angegeben. Der Treiber wird den richtige Authentifizierungsmodus automatisch auszuwählen. `UID`und `PWD` darf nicht angegeben werden.

## <a name="authenticating-with-an-access-token-windows-driver-only"></a>Bei Authentifizierung über ein Zugriffstoken (nur Windows-Treiber)

Die `SQL_COPT_SS_ACCESS_TOKEN` vorverbindungsattribut ermöglicht die Verwendung eines Zugriffstokens aus Azure Active Directory für die Authentifizierung anstelle von Benutzername und Kennwort abgerufen und die Aushandlung und Abrufen eines Zugriffstokens durch den Treiber auch umgangen. Um ein Zugriffstoken zu verwenden, legen die `SQL_COPT_SS_ACCESS_TOKEN` -Verbindungsattribut auf einen Zeiger auf eine `ACCESSTOKEN` Struktur:

~~~
typedef struct AccessToken
{
    DWORD dataSize;
    BYTE data[];
} ACCESSTOKEN;
~~~

Die `ACCESSTOKEN` ist eine variabler Länge, die Struktur besteht ein 4-Byte- _Länge_ gefolgt von _Länge_ Bytes von nicht transparenten Daten, die das Zugriffstoken zu bilden. Aufgrund von wie SQL Server Zugriffstoken behandelt, eine über abgerufen ein [OAuth 2.0](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios) JSON-Antwort muss erweitert werden, sodass jedes Byte 0 padding Byte, ähnlich wie eine UCS-2-Zeichenfolge, enthält nur ASCII-Zeichen folgt, wird; allerdings das Token ist ein nicht transparenter Wert und die Länge angegeben wird, in Bytes, dürfen keine null-Terminator enthalten. Aufgrund ihrer erheblichen Einschränkungen für Länge und Format dieser Methode der Authentifizierung ist nur verfügbar, programmgesteuert über die `SQL_COPT_SS_ACCESS_TOKEN` Coonnection-Attribut; es gibt keine entsprechenden DSN oder Verbindungszeichenfolgen-Schlüsselwort. Die Verbindungszeichenfolge darf keinen `UID`, `PWD`, `Authentication`, oder `Trusted_Connection` Schlüsselwörter.

## <a name="azure-active-directory-authentication-sample-code"></a>Beispielcode für Azure Active Directory-Authentifizierung

Das folgende Beispiel zeigt den Code für die Verbindung mit SQL Server mithilfe von Azure Active Directory mit Verbindungsschlüsselwörter. Beachten Sie, dass keine Notwendigkeit besteht, den Code der Anwendung zu ändern; die Verbindungszeichenfolge oder DSN, sofern einer verwendet wird, ist die einzige Änderung, die für die Authentifizierung mit AAD erforderlich:
~~~
    ...
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server};UID=myuser;PWD=myPass;Authentication=ActiveDirectoryPassword"
    ...
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);  
    ...
~~~
Das folgende Beispiel zeigt den Code für die Verbindung mit SQL Server mithilfe von Azure Active Directory mit Access token-Authentifizierung. In diesem Fall ist es erforderlich ist, ändern Anwendungscode, um das Zugriffstoken zu verarbeiten, und legen Sie das zugeordnete Verbindungsattribut.
~~~
    SQLCHAR connString[] = "Driver={ODBC Driver 13 for SQL Server};Server={server}"
    SQLCHAR accessToken[] = "eyJ0eXAiOi..."; // In the format extracted from an OAuth JSON response
    ...
    DWORD dataSize = 2 * strlen(accessToken);
    ACCESSTOKEN *pAccToken = malloc(sizeof(ACCESSTOKEN) + dataSize);
    pAccToken->dataSize = dataSize;
    // Expand access token with padding bytes
    for(int i = 0, j = 0; i < dataSize; i += 2, j++) {
        pAccToken->data[i] = accessToken[j];
        pAccToken->data[i+1] = 0;
    }
    ...
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_ACCESS_TOKEN, (SQLPOINTER)pAccToken, SQL_IS_POINTER);
    SQLDriverConnect(hDbc, NULL, connString, SQL_NTS, NULL, 0, NULL, SQL_DRIVER_NOPROMPT);      
    ...
    free(pAccToken);
~~~

## <a name="see-also"></a>Siehe auch
[Token-basierte Authentifizierung-Unterstützung für Azure SQL-Datenbank mithilfe von Azure AD-Authentifizierung](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth)


