---
title: "SQL Server-Connector – Wartung &amp; Problembehandlung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQL Server Connector, appendix
ms.assetid: 7f5b73fc-e699-49ac-a22d-f4adcfae62b1
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0cce6f70771e67f55f987fe6c307d4713e3f928
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="sql-server-connector-maintenance-amp-troubleshooting"></a>SQL Server-Connector – Wartung &amp; Problembehandlung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält ergänzende Informationen zum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector. Weitere Informationen zum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector finden Sie unter [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md), [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault.](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md) und [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
  
##  <a name="AppendixA"></a> A. Wartungsanweisungen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector  
  
### <a name="key-rollover"></a>Schlüsselrollover  
  
> [!IMPORTANT]  
>  Für den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector ist es erforderlich, dass im Schlüsselnamen nur die Zeichen „a-z“, „A-Z“, „0-9“ und „-“ bei einem Zeichenlimit von 26 Zeichen verwendet werden.   
> Verschiedene Schlüsselversionen unter dem gleichen Schlüsselnamen in Azure Key Vault funktionieren in Verbindung mit dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector nicht. Um die Möglichkeit zur Rotation eines Azure Key Vault-Schlüssels zu bieten, der von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet wird, muss ein neuer Schlüssel mit einem neuen Schlüsselnamen erstellt werden.  
  
 In der Regel müssen asymmetrische Serverschlüssel für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselung alle 1-2 Jahre geändert werden. Es ist wichtig zu beachten, dass der Schlüsseltresor die Änderung von Schlüsseln zwar zulässt, diese Funktion von Kunden jedoch nicht zum Implementieren einer Versionsverwaltung verwendet werden sollte. Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector kann nicht mit Änderungen der Version des Key Vault-Schlüssels umgehen. Zum Implementieren einer Schlüsselversionsverwaltung müssen Kunden einen neuen Schlüssel im Schlüsseltresor erstellen und den Datenverschlüsselungsschlüssel in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]neu verschlüsseln.  
  
 Für TDE wird dies folgendermaßen erreicht:  
  
-   **In PowerShell:** Erstellen Sie im Schlüsseltresor einen neuen asymmetrischen Schlüssel (mit einem anderen Namen als dem Ihres aktuellen asymmetrischen TDE-Schlüssels).  
  
    ```powershell  
    Add-AzureRmKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'Key2' -Destination 'Software'  
    ```  
  
-   **Mithilfe von [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] oder „sqlcmd.exe“:** Verwenden Sie die folgenden Anweisungen, wie in Schritt 3, Abschnitt 3 dargestellt.  
  
     Importieren Sie den neuen asymmetrischen Schlüssel.  
  
    ```sql  
    USE master  
    CREATE ASYMMETRIC KEY [MASTER_KEY2]   
    FROM PROVIDER [EKM]   
    WITH PROVIDER_KEY_NAME = 'Key2',   
    CREATION_DISPOSITION = OPEN_EXISTING   
    GO  
    ```  
  
     Erstellen Sie eine neue Anmeldung, die dem neuen asymmetrischen Schlüssel zugeordnet wird (wie in den TDE-Anweisungen dargestellt).  
  
    ```sql  
    USE master  
    CREATE LOGIN TDE_Login2   
    FROM ASYMMETRIC KEY [MASTER_KEY2]  
    GO  
    ```  
  
     Erstellen Sie neue Anmeldeinformationen zum Zuordnen zur Anmeldung.  
  
    ```sql  
    CREATE CREDENTIAL Azure_EKM_TDE_cred2  
        WITH IDENTITY = 'ContosoDevKeyVault',   
       SECRET = 'EF5C8E094D2A4A769998D93440D8115DAADsecret123456789=’   
    FOR CRYPTOGRAPHIC PROVIDER EKM;  
  
    ALTER LOGIN TDE_Login2  
    ADD CREDENTIAL Azure_EKM_TDE_cred2;  
    GO  
    ```  
  
     Wählen Sie die Datenbank, deren Verschlüsselungsschlüssel sie neu verschlüsseln möchten.  
  
    ```sql  
    USE [database]  
    GO  
    ```  
  
     Verschlüsseln Sie den Datenbank-Verschlüsselungsschlüssel erneut.  
  
    ```sql  
    ALTER DATABASE ENCRYPTION KEY   
    ENCRYPTION BY SERVER ASYMMETRIC KEY [MASTER_KEY2];  
    GO  
    ```  
  
### <a name="upgrade-of-includessnoversionincludesssnoversion-mdmd-connector"></a>Upgrade des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors  

Die Versionen 1.0.0.440 und älter wurden ersetzt und werden nicht länger in Produktionsumgebungen unterstützt. Die Versionen 1.0.1.0 und neuer werden in Produktionsumgebungen unterstützt. Richten Sie sich nach den folgenden Anweisungen, um ein Upgrade auf die neueste im [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45344)verfügbare Version auszuführen.

Wenn Sie aktuell Version 1.0.1.0 oder höher verwenden, führen Sie diese Schritte aus, um auf die neueste Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors zu aktualisieren. Durch diese Anweisungen entfällt der ansonsten erforderliche Neustart der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz.
 
1. Installieren Sie die neueste Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45344). Speichern Sie im Installations-Assistenten die neue DLL-Datei unter einem anderen Dateipfad als dem der ursprünglichen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector-DLL. Als neuer Dateipfad würde sich beispielsweise anbieten: `C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll`
 
2. Führen Sie in der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]den folgenden Transact-SQL-Befehl aus, um Ihre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz auf die neue Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors verweisen zu lassen:

    ``` 
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\<latest version number>\Microsoft.AzureKeyVaultService.EKM.dll'
    GO  
    ```

Wenn Sie aktuell Version 1.0.0.440 oder älter verwenden, führen Sie diese Schritte aus, um auf die neueste Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors zu aktualisieren.
  
1.  Beenden Sie die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  Beenden Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectordienst.  
  
3.  Deinstallieren Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector mithilfe des Windows-Features „Apps &amp; Features“.  
  
     (Alternativ können Sie den Ordner umbenennen, in dem sich die DLL-Datei befindet. Der Standardname des Ordners ist „[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für Microsoft Azure Key Vault“.  
  
4.  Laden Sie die neueste Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors aus dem Microsoft Download Center herunter.  
  
5.  Starten Sie die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]neu.  
  
6.  Führen Sie die folgende Anweisung aus, um den EKM-Anbieter so zu ändern, dass er mithilfe der neuesten Version des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectors gestartet wird. Achten Sie darauf, dass der Dateipfad auf den Speicherort verweist, an dem sich die heruntergeladene neueste Version befindet. (Dieser Schritt kann übersprungen werden, wenn die neue Version an demselben Speicherort wie die ursprüngliche Version installiert wird.) 
  
    ```sql  
    ALTER CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE =   
    'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
7.  Überprüfen Sie, ob auf die Datenbanken, die TDE verwenden, zugegriffen werden kann.  
  
8.  Nachdem Sie bestätigt haben, dass das Update funktioniert, können Sie den alten [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectorordner löschen (wenn Sie sich in Schritt 3 dazu entschlossen haben, ihn umzubenennen statt zu deinstallieren).  
  
### <a name="rolling-the-includessnoversionincludesssnoversion-mdmd-service-principal"></a>Ändern des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstprinzipals  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet in Azure Active Directory erstellte Dienstprinzipale als Anmeldeinformationen zum Zugriff auf den Schlüsseltresor.  Der Dienstprinzipal verfügt über eine Client-ID und einen Authentifizierungsschlüssel.  Für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldenamen werden der **VaultName**, die **Client-ID**und der **Authentifizierungsschlüssel**festgelegt.  Der **Authentifizierungsschlüssel** ist für einen bestimmten Zeitraum (1 oder 2 Jahre) gültig.   Vor Ablauf des Zeitraums muss für den Dienstprinzipal ein neuer Schlüssel in Azure AD generiert werden.  Anschließend müssen die Anmeldeinformationen in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]geändert werden.    [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] verwaltet einen Cache für die Anmeldeinformationen in der aktuellen Sitzung. Wenn also Anmeldeinformationen geändert werden, sollte [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] neu gestartet werden.  
  
### <a name="key-backup-and-recovery"></a>Schlüsselsicherung und -wiederherstellung  
Der Schlüsseltresor sollte regelmäßig gesichert werden. Wenn ein asymmetrischer Schlüssel im Tresor verloren geht, kann er aus der Sicherung wiederhergestellt werden. Der Schlüssel muss mit dem gleichen Namen wie zuvor wiederhergestellt werden, was vom PowerShell-Befehl „Restore“ auch ausgeführt wird (siehe Schritte unten).  
Wenn der Tresor verloren geht, müssen Sie einen Tresor neu erstellen und den asymmetrischen Schlüssel unter Verwendung desselben Namens wie zuvor im Tresor wiederherstellen. Der Name für den Tresor kann vom zuvor verwendeten Namen abweichen (oder diesem entsprechen). Sie müssen für den neuen Tresor auch die Zugriffsberechtigungen festlegen, damit dem SQL Server-Dienstprinzipal der für die SQL Server-Verschlüsselungsszenarien benötigte Zugriff gewährt wird. Anschließend passen Sie die SQL Server-Anmeldeinformationen dahingehend an, dass diese den neuen Tresornamen widerspiegeln.  
Zusammengefasst ergeben sich folgende Schritte:  
  
* Sichern Sie den Tresorschlüssel (mithilfe des PowerShell-Cmdlets „Backup-AzureKeyVaultKey“).  
* Im Fall eines Tresorfehlers erstellen Sie einen neuen Tresor in der gleichen geografischen Region. Der Benutzer, der ihn erstellt, sollte sich im gleichen Standardverzeichnis wie der Dienstprinzipal befinden, der für SQL Server eingerichtet wurde.  
* Stellen Sie den Schlüssel für den neuen Tresor wieder her (mithilfe des PowerShell-Cmdlets „Restore-AzureKeyVaultKey“– dieses stellt den Schlüssel mit dem gleichen Namen wie zuvor wieder her). Wenn bereits ein Schlüssel mit dem gleichen Namen vorhanden ist, tritt ein Fehler bei der Wiederherstellung auf.  
* Erteilen Sie dem SQL Server-Dienstprinzipal Berechtigungen zum Verwenden dieses neuen Tresors.  
* Ändern Sie die vom Datenbankmodul verwendeten SQL Server-Anmeldeinformationen so, dass sie den neuen Tresornamen widerspiegeln (falls erforderlich).  
  
Schlüsselsicherungen können übergreifend über Azure-Regionen wiederhergestellt werden, sofern sie in der gleichen geografischen Region oder nationalen Cloud bleiben: USA, Kanada, Japan, Australien, Indien, APAC, Europa, Brasilien, China, US-Regierung oder Deutschland.  
  
  
##  <a name="AppendixB"></a> B. Häufig gestellte Fragen  
### <a name="on-azure-key-vault"></a>Zum Azure-Schlüsseltresor  
  
**Wie funktionieren Schlüsselvorgänge mit Azure Key Vault?**  
 Der asymmetrische Schlüssel im Schlüsseltresor dient zum Schutz des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselungsschlüssels. Nur der öffentliche Teil des asymmetrischen Schlüssels verlässt jemals den Tresor, der private Teil wird nie vom Tresor exportiert. Alle kryptografischen Vorgänge, die den asymmetrischen Schlüssel verwenden, erfolgen innerhalb des Azure Key Vault-Diensts und werden durch die Sicherheit des Diensts geschützt.  
  
 **Was ist ein Schlüssel-URI?**  
 Jeder Schlüssel im Azure Key Vault weist einen Uniform Resource Identifier (URI) auf, den Sie in Ihrer Anwendung verwenden können, um auf den Schlüssel zu verweisen. Verwenden Sie zum Abrufen der aktuellen Version das Format `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey` und zum Abrufen einer bestimmten Version das Format `https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87` .  
  
### <a name="on-configuring-includessnoversionincludesssnoversion-mdmd"></a>Zur Konfiguration [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  

**Auf welche Endpunkte benötigt der SQL Server-Connector Zugriff?** Der Connector kommuniziert mit zwei Endpunkten, die der Positivliste hinzugefügt werden müssen. Der einzige Port, der für die ausgehende Kommunikation mit diesen anderen Diensten erforderlich ist, lautet 443 für Https:
-  Login.microsoftonline.com/*:443
-  *.Vault.Azure.NET/*:443
  
**Was sind die minimal erforderlichen Berechtigungsstufen, die für die einzelnen Konfigurationsschritte in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]erforderlich sind?**  
 Zwar können Sie alle Konfigurationsschritte als Mitglied der festen Serverrolle „sysadmin“ ausführen, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] legt Ihnen jedoch dringlich nahe, die verwendeten Berechtigungen zu minimieren. Die folgende Liste definiert die minimale Berechtigungsstufe für jede Aktion.  
  
-   Zum Erstellen eines Kryptografieanbieters ist die `CONTROL SERVER` -Berechtigung oder die Mitgliedschaft in der festen Serverrolle **sysadmin** erforderlich.  
  
-   Zum Ändern einer Konfigurationsoption und zum Ausführen der `RECONFIGURE` -Anweisung muss Ihnen die Berechtigung `ALTER SETTINGS` auf Serverebene erteilt worden sein. Die `ALTER SETTINGS` -Berechtigung ist implizit in den festen Serverrollen „sysadmin“ und **serveradmin** enthalten.  
  
-   Zum Erstellen von Anmeldeinformationen wird die `ALTER ANY CREDENTIAL` -Berechtigung benötigt.  
  
-   Zum Hinzufügen von Anmeldeinformationen zu einer Anmeldung wird die `ALTER ANY LOGIN` -Berechtigung benötigt.  
  
-   Zum Erstellen eines asymmetrischen Schlüssels wird die `CREATE ASYMMETRIC KEY` -Berechtigung benötigt.  

**Wie ändere ich mein Standard-Active Directory, sodass mein Schlüsseltresor im gleichen Abonnement und Active Directory erstellt wird wie der Dienstprinzipal, den ich für den [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] -Connector erstellt habe?**

![aad-change-default-directory-helpsteps](../../../relational-databases/security/encryption/media/aad-change-default-directory-helpsteps.png)

1. Gehen Sie zum klassischen Azure-Portal: [https://manage.windowsazure.com](https://manage.windowsazure.com)  
2. Scrollen Sie im Menü auf der linken Seite nach unten, und wählen Sie **Einstellungen**aus.
3. Wählen Sie das Azure-Abonnement aus, das Sie aktuell verwenden, und klicken Sie in den Befehlen am unteren Bildschirmrand auf **Verzeichnis bearbeiten** .
4. Verwenden Sie im Popupfenster die Dropdownliste **Verzeichnis** , um das Active Directory auszuwählen, das Sie verwenden möchten. Dadurch wird es als Standardverzeichnis festgelegt.
5. Vergewissern Sie sich, dass Sie der globale Administrator des neu ausgewählten Active Directorys sind. Wenn Sie nicht der globale Administrator sind, verlieren Sie möglicherweise aufgrund des Verzeichniswechsels Ihre Verwaltungsberechtigungen.
6. Wenn Sie nach dem Schließen des Popupfensters keins Ihrer Abonnements sehen, müssen Sie möglicherweise den Filter **Nach Verzeichnis filtern** im Filter **Abonnements** im oberen rechten Menü des Bildschirms aktualisieren, um Abonnements anzuzeigen, die Ihr neu aktualisiertes Active Directory verwenden.

    > [!NOTE] 
    > Möglicherweise verfügen Sie nicht über die Berechtigung zum Ändern des Standardabonnements für Ihr Azure-Abonnement. Erstellen Sie in diesem Fall den AAD-Dienstprinzipal innerhalb Ihres Standardverzeichnisses, sodass er sich im gleichen Verzeichnis wie der später verwendete Azure Key Vault befindet.

Weitere Informationen zu Active Directory finden Sie unter [Beziehung zwischen Azure-Abonnements und Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-how-subscriptions-associated-directory/)
  
##  <a name="AppendixC"></a> C. Erläuterungen zu Fehlercodes für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector  
 **Anbieterfehlercodes:**  
  
Fehlercode  |Symbol  |Description    
---------|---------|---------  
0 | scp_err_Success | Der Vorgang war erfolgreich.    
1 | scp_err_Failure | Beim Vorgang ist ein Fehler aufgetreten.    
2 | scp_err_InsufficientBuffer | Dieser Fehler weist das Modul an, mehr Arbeitsspeicher für den Puffer zuzuweisen.    
3 | scp_err_NotSupported | Der Vorgang wird nicht unterstützt. Beispielsweise wird der angegebene Schlüsseltyp oder Algorithmus nicht vom EKM-Anbieter unterstützt.    
4 | scp_err_NotFound | Der angegebene Schlüssel oder Algorithmus wurde vom EKM-Anbieter nicht gefunden.    
5 | scp_err_AuthFailure | Authentifizierungsfehler beim EKM-Anbieter.    
6 | scp_err_InvalidArgument | Das angegebene Argument ist ungültig.    
7 | scp_err_ProviderError | Im EKM-Anbieter ist ein nicht angegebener Fehler aufgetreten, der vom SQL-Modul abgefangen wurde.    
2049 | scp_err_KeyNameDoesNotFitThumbprint | Der Schlüsselname ist zu lang, um in den Fingerabdruck des SQL-Moduls zu passen. Der Schlüsselname darf 26 Zeichen nicht überschreiten.    
2050 | scp_err_PasswordTooShort | Die geheime Zeichenfolge, bei der es sich um die Verkettung von AAD-Client-ID und geheimem Schlüssel handelt, ist kürzer als 32 Zeichen.    
2051 | scp_err_OutOfMemory | Das SQL-Modul verfügt nicht über ausreichend Arbeitsspeicher, deshalb ist beim Zuweisen von Arbeitsspeicher für den EKM-Anbieter ein Fehler aufgetreten.    
2052 | scp_err_ConvertKeyNameToThumbprint | Fehler beim Konvertieren des Schlüsselnamens in den Fingerabdruck.    
2053 | scp_err_ConvertThumbprintToKeyName|  Fehler beim Konvertieren des Fingerabdrucks in den Schlüsselnamen.    
3000 | ErrorSuccess | Der AKV-Vorgang war erfolgreich.    
3001 | ErrorUnknown | Unbekannter Fehler beim AKV-Vorgang.    
3002 | ErrorHttpCreateHttpClientOutOfMemory | Es kann kein HttpClient für den AKV-Vorgang aufgrund von unzureichendem Arbeitsspeicher erstellt werden.    
3003 | ErrorHttpOpenSession | Aufgrund eines Netzwerkfehlers kann keine Http-Sitzung geöffnet werden.    
3004 | ErrorHttpConnectSession | Aufgrund eines Netzwerkfehlers kann keine Verbindung mit einer Http-Sitzung hergestellt werden.    
3005 | ErrorHttpAttemptConnect | Aufgrund eines Netzwerkfehlers kann kein Verbindungsversuch ausgeführt werden.    
3006 | ErrorHttpOpenRequest | Aufgrund eines Netzwerkfehlers kann eine Anforderung nicht geöffnet werden.    
3007 | ErrorHttpAddRequestHeader | Ein Anforderungsheader kann nicht hinzugefügt werden.    
3008 | ErrorHttpSendRequest | Aufgrund eines Netzwerkfehlers kann eine Anforderung nicht gesendet werden.    
3009 | ErrorHttpGetResponseCode | Aufgrund eines Netzwerkfehlers kann kein Antwortcode abgerufen werden.    
3010 | ErrorHttpResponseCodeUnauthorized | Der Server hat auf die Anforderung 401 zurückgegeben.    
3011 | ErrorHttpResponseCodeThrottled | Der Server hat die Anforderung gedrosselt.    
3012 | ErrorHttpResponseCodeClientError | Die vom Connector gesendete Anforderung ist ungültig. Dies bedeutet normalerweise, dass der Name des Schlüssels ungültig ist oder ungültige Zeichen enthält.
3013 | ErrorHttpResponseCodeServerError | Der Server hat mit einem Antwortcode zwischen 500 und 600 geantwortet.    
3014 | ErrorHttpQueryHeader | Es kann keine Abfrage auf den Antwortheader ausgeführt werden.    
3015 | ErrorHttpQueryHeaderOutOfMemoryCopyHeader | Der Antwortheader kann aufgrund von unzureichendem Arbeitsspeicher nicht kopiert werden.    
3016 | ErrorHttpQueryHeaderOutOfMemoryReallocBuffer | Der Antwortheader kann bei der Neuzuweisung eines Puffers aufgrund von unzureichendem Arbeitsspeicher nicht abgefragt werden.    
3017 | ErrorHttpQueryHeaderNotFound | Der Abfrageheader wurde in der Antwort nicht gefunden.    
3018 | ErrorHttpQueryHeaderUpdateBufferLength | Beim Abfragen des Antwortheaders kann die Pufferlänge nicht aktualisiert werden.    
3019 | ErrorHttpReadData | Die Antwortdaten können aufgrund eines Netzwerkfehlers nicht gelesen werden. 
3076 | ErrorHttpResourceNotFound | Der Server hat mit 404 geantwortet, da der Schlüsselname nicht gefunden wurde. Überprüfen Sie, ob der Schlüsselname in Ihrem Tresor vorhanden ist.
3077 | ErrorHttpOperationForbidden | Der Server hat mit 403 geantwortet, da der Benutzer keine ordnungsgemäße Berechtigung zum Ausführen der Aktion besitzt. Überprüfen Sie, ob Sie über die Berechtigung für den angegebenen Vorgang verfügen. Der Connector benötigt zur ordnungsgemäßen Funktion mindestens die Berechtigungen „get, list, wrapKey, unwrapKey“.   
  
Wenn Sie Ihren Fehlercode in dieser Tabelle nicht finden, beachten Sie, dass ein Fehler auch noch aus einer Reihe weiterer Gründe auftreten kann:   
  
-   Möglicherweise verfügen Sie nicht über Internetzugriff und können nicht auf den Azure Key Vault zugreifen – überprüfen Sie die Internetverbindung.  
  
-   Der Azure Key Vault-Dienst ist möglicherweise außer Betrieb. Versuchen Sie es ein andermal erneut.  
  
-   Möglicherweise haben Sie den asymmetrischen Schlüssel im Azure Key Vault oder [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gelöscht. Stellen Sie den Schlüssel wieder her.  
  
-   Wenn Sie den Fehler „Die Bibliothek kann nicht geladen werden“ erhalten, überprüfen Sie, ob die für die ausgeführte SQL Server-Version geeignete Version der weitervertreibbaren Visual Studio C++-Komponente installiert ist. In der folgenden Tabelle wird angegeben, welche Version aus dem Microsoft Download Center installiert werden muss.   
  
SQL Server-Version  |Link zum Installieren der weitervertreibbaren Komponente    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Visual C++ Redistributable-Pakete für Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable für Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
 Weitere Informationen über die erweiterbare Schlüsselverwaltung:  
  
-   [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
 SQL-Verschlüsselungen, die EKM unterstützen:  
  
-   [Aktivieren von TDE in SQL Server mithilfe von EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
-   [Verschlüsseln der Sicherung](../../../relational-databases/backup-restore/backup-encryption.md)  
  
-   [Erstellen einer verschlüsselten Sicherung](../../../relational-databases/backup-restore/create-an-encrypted-backup.md)  
  
 Verwandte [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Befehle:  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/create-login-transact-sql.md)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)  
  
 Azure Key Vault-Dokumentation  
  
-   [Was ist Azure Key Vault?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/)  
  
-   [Erste Schritte mit Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)  
  
-   Referenz der PowerShell- [Azure Key Vault-Cmdlets](https://msdn.microsoft.com/library/dn868052.aspx)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterbare Schlüsselverwaltung mithilfe von Azure Key Vault](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
 [EKM provider enabled (Serverkonfigurationsoption)](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)   
 [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault.](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md)  
  
  
