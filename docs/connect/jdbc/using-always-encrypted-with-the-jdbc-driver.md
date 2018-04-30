---
title: Always Encrypted mit dem JDBC-Treiber verwenden | Microsoft Docs
ms.custom: ''
ms.date: 3/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 02a0be7375eafcd3ba54dbdf83f3e55e73b13a91
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Always Encrypted verwenden mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Diese Seite enthält Informationen zum Entwickeln von Java-Anwendungen mit [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) und Microsoft JDBC Driver 6.0 (oder höher) für SQL Server.

Immer kann verschlüsselte Clients zum Verschlüsseln von sensiblen Daten und niemals weiterzugeben, die Daten oder die Verschlüsselungsschlüssel in SQL Server oder Azure SQL-Datenbank. Ein Always Encrypted-Treiber, wie z. B. Microsoft JDBC Driver 6.0 (oder höher) für SQL Server aktiviert ist, erreicht dies durch die transparente Ver- und Entschlüsselung von sensiblen Daten in der Clientanwendung. Der Treiber ermittelt automatisch, welche Abfrage Parameter entsprechen den Datenbankspalten Always Encrypted und die Werte dieser Parameter verschlüsselt, bevor sie an SQL Server oder Azure SQL-Datenbank gesendet. Auf ähnliche Weise entschlüsselt der Treiber die Daten transparent, die von verschlüsselten Datenbankspalten in Abfrageergebnissen empfangen werden. Weitere Informationen finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) und [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

## <a name="prerequisites"></a>Erforderliche Komponenten
- Stellen Sie sicher, dass Microsoft JDBC Driver 6.0 (oder höher) für SQL Server auf dem Entwicklungscomputer installiert ist. 
- Laden Sie die Richtliniendateien Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction herunter und installieren Sie sie.  Achten Sie darauf, dass die Zip-Datei für die installationsanweisungen und relevante Details auf der möglichen Export-/importproblemen-Infodatei zu lesen.  

    - Falls der Mssql-Jdbc-X.X.X.jre7.jar oder "sqljdbc41.jar" verwenden, können die Richtliniendateien von heruntergeladen werden [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Richtliniendateien 7 herunterladen](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - Falls der Mssql-Jdbc-X.X.X.jre8.jar oder "sqljdbc42.jar" verwenden, können die Richtliniendateien von heruntergeladen werden [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Richtliniendateien 8 herunterladen](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - Wenn der Mssql-Jdbc-X.X.X.jre9.jar verwenden zu können, muss keine Richtliniendatei heruntergeladen werden. Die Richtlinie für die Zuständigkeit in Java 9 standardmäßig unbegrenzt Verschlüsselung.

## <a name="working-with-column-master-key-stores"></a>Arbeiten mit Hauptschlüssel spaltenspeicher
Zum Ver- und Entschlüsseln von Daten aus verschlüsselten Spalten, behält SQL Server spaltenverschlüsselungsschlüssel. Spaltenverschlüsselungsschlüssel werden in verschlüsselter Form in den Datenbankmetadaten gespeichert. Jeder spaltenverschlüsselungsschlüssel verfügt über einen entsprechenden spaltenhauptschlüssel, der zum Verschlüsseln des Verschlüsselungsschlüssels für die Spalte verwendet wird. Die Datenbank-Metadaten enthält keine spaltenhauptschlüssel. Diese Schlüssel werden nur vom Client aufrechterhalten. Allerdings die Datenbank-Metadaten enthalten Informationen zum Speicherort der spaltenhauptschlüssel relativ zu dem Client. Kann die Datenbank-Metadaten, die wie folgt lauten Keystore hält ein spaltenhauptschlüssel ist die Windows-Zertifikatspeicher, und das bestimmte zum Verschlüsseln und Entschlüsseln verwendete Zertifikat befindet sich in einem bestimmten Pfad innerhalb der Windows-Zertifikatspeicher. Wenn der Client den Zugriff auf dieses Zertifikat in Windows-Zertifikatspeicher verfügt, können sie das Zertifikat abrufen. Das Zertifikat kann dann verwendet werden, die spaltenverschlüsselungsschlüssel zu entschlüsseln. Dann, dass der Verschlüsselungsschlüssel zum Entschlüsseln oder Verschlüsseln von Daten für verschlüsselte Spalten, die diese spaltenverschlüsselungsschlüssel verwenden verwendet werden kann.

Microsoft JDBC Driver für SQL Server kommuniziert mit einer ein Hauptschlüssel Speicheranbieter, der eine Instanz einer Klasse ist von abgeleitet Schlüsselspeicher using **SQLServerColumnEncryptionKeyStoreProvider**.

### <a name="using-built-in-column-master-key-store-providers"></a>Verwenden integrierter Spaltenhauptschlüssel-Speicheranbieter
Im Lieferumfang von Microsoft JDBC Driver für SQL Server sind die folgenden integrierten Hauptschlüssel Speicheranbieter. Einige dieser Anbieter vorab mit den bestimmten Anbieternamen (wird verwendet, um den Anbieter zu suchen) registriert sind, und einige zusätzliche Anmeldeinformationen oder explizite Registrierung erforderlich.

| Klasse | Description | Anbietername (Suche) |Ist bereits registriert?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Ein Anbieter für einen Schlüsselspeicher für den Azure Key Vault.| AZURE_KEY_VAULT|nein|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Ein Anbieter für den Windows-Zertifikatspeicher.|MSSQL_CERTIFICATE_STORE|ja
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Für die Java-Schlüsselspeicher-Anbieter|MSSQL_JAVA_KEYSTORE|ja|

Für die zuvor registrierten-Schlüsselspeicher-Anbieter müssen keine Änderungen am Anwendungscode verwenden diese Anbieter, aber beachten Folgendes vornehmen:

- Sie (oder Ihrem DBA) müssen sicherstellen, dass der in den Metadaten des spaltenhauptschlüssels konfigurierte Anbietername richtig ist und der Pfad des Hauptschlüssels Spalte entspricht, mit dem Schlüsselpfad-Format, das für einen angegebenen Anbieter gültig ist. Es wird empfohlen, die die Schlüssel mithilfe von Tools, z. B. SQL Server Management Studio, der die gültigen Anbieternamen und Schlüsselpfade automatisch generiert, wenn die Anweisung CREATE COLUMN MASTER KEY (Transact-SQL) ausgeben zu konfigurieren.
- Stellen Sie sicher, dass die Anwendung den Schlüssel im Schlüsselspeicher zugreifen können. Diese Aufgabe kann zur Folge haben, gewähren Ihrer Anwendungszugriff auf den Schlüssel und/oder Schlüsselspeicher, je nach den Schlüsselspeicher oder andere Keystore-spezifische Konfigurationsschritte ausführen. Beispielsweise müssen für die Verwendung der SQLServerColumnEncryptionJavaKeyStoreProvider, geben Sie den Speicherort und das Kennwort für den Schlüsselspeicher in den Verbindungseigenschaften. 

Alle diese Schlüsselspeicher-Anbieter sind in den Abschnitten ausführlicher beschrieben. Sie müssen nur einen Schlüsselspeicheranbieter Verwendung von Always Encrypted zu implementieren.

### <a name="using-azure-key-vault-provider"></a>Verwenden des Azure Key Vault-Anbieters
Azure Key Vault ist eine praktische Möglichkeit zum Speichern und Verwalten von spaltenhauptschlüsseln für Always Encrypted (insbesondere, wenn die Anwendung in Azure gehostet wird). Microsoft JDBC Driver für SQL Server enthält einen integrierten Anbieter SQLServerColumnEncryptionAzureKeyVaultProvider, für Anwendungen, die in Azure Key Vault gespeicherte Schlüsseln haben. Der Name des Anbieters ist AZURE_KEY_VAULT. Damit den Azure Key Vault-Speicheranbieter verwenden zu können, muss ein Anwendungsentwickler dem Tresor und die Schlüssel in Azure Key Vault zu erstellen, und erstellen Sie eine App-Registrierung in Azure Active Directory. Die registrierte Anwendung muss erteilt, entschlüsseln, verschlüsseln, Unwrap-Schlüssel, Key Wrap und überprüfen Sie, ob Berechtigungen in der für den schlüsseltresor für die Verwendung mit Always Encrypted erstellt definierten Zugriffsrichtlinien zu erhalten. Weitere Informationen zum schlüsseltresor einrichten, und erstellen einen spaltenhauptschlüssel finden Sie unter [Azure Key Vault – Schritt-für-Schritt](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) und [Erstellen von Spaltenhauptschlüsseln in Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

Für die Beispiele auf dieser Seite, wenn Sie ein Azure-Schlüsseltresor erstellt haben, spaltenhauptschlüssel und spaltenverschlüsselungsschlüssel mithilfe von SQL Server Management Studio basieren, das T-SQL-Skript erneut erstellen kann Ähnlichkeit mit diesem Beispiel durch eigene spezielle **KEY_ Pfad** und **ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

Um Azure-Schlüsseltresor zu verwenden, müssen Clientanwendungen die SQLServerColumnEncryptionAzureKeyVaultProvider instanziieren und registrieren Sie ihn mit dem Treiber.

Hier ist ein Beispiel der SQLServerColumnEncryptionAzureKeyVaultProvider initialisieren:  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**ClientID** ist die ID einer App-Registrierung in einer Azure Active Directory-Instanz. **ClientKey** ist ein Kennwort für den Schlüssel unter der API-Zugriff auf Azure Key Vault ermöglicht der Anwendung registriert.

Nachdem die Anwendung eine Instanz von SQLServerColumnEncryptionAzureKeyVaultProvider erstellt wurde, muss die Anwendung die Instanz mit dem Treiber mithilfe der sqlserverconnection.registercolumnencryptionkeystoreproviders()-Methode registrieren. Es wird dringend empfohlen, dass die Instanz registriert ist, mit dem Standardnamen des Suche, AZURE_KEY_VAULT, die durch Aufrufen der API SQLServerColumnEncryptionAzureKeyVaultProvider.getName() abgerufen werden kann. Mithilfe des Standardnamens können Sie Tools wie SQL Server Management Studio oder PowerShell zur Bereitstellung und Verwaltung von Always Encrypted-Schlüssel (die Tools verwenden den Standardnamen zum Generieren des Metadatenobjekts, um spaltenhauptschlüssel) verwenden. Das folgende Beispiel zeigt die Registrierung des Azure Key Vault-Anbieters. Weitere Informationen zu der sqlserverconnection.registercolumnencryptionkeystoreproviders()-Methode, finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  Wenn Sie den Azure Key Vault-Schlüsselspeicher-Anbieter verwenden, hat Azure Key Vault Implementierung des JDBC-Treibers Abhängigkeiten von diesen Bibliotheken (von GitHub), die in der Anwendung enthalten sein müssen:
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [Azure-Active Directory-Bibliothek-für-Java-Bibliotheken](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> Ein Beispiel dafür, wie diese Abhängigkeiten in einem Projekt Maven eingeschlossen werden sollen, finden Sie unter [herunterladen ADAL4J und AKV Abhängigkeiten mit Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>Mithilfe der Windows-Zertifikatspeicher-Anbieter
Die SQLServerColumnEncryptionCertificateStoreProvider kann verwendet werden, zum Speichern von spaltenhauptschlüsseln im Windows-Zertifikatspeicher. Verwenden Sie SQL Server Management Studio (SSMS) Always Encrypted-Assistenten oder andere unterstützte Tools, um die spaltenhauptschlüssel und die spaltenverschlüsselung Definitionen in der Datenbank erstellen. Des gleiche Assistenten kann verwendet werden, um ein selbst signiertes Zertifikat in Windows-Zertifikatspeicher zu generieren, das als spaltenhauptschlüssel für die immer verschlüsselten Daten verwendet werden kann. Weitere Informationen zu spaltenhauptschlüssel und Column Encryption Key T-SQL-Syntax, finden Sie unter [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) und [CREATE COLUMN Encryption KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) bzw.

Der Name des der SQLServerColumnEncryptionCertificateStoreProvider MSSQL_CERTIFICATE_STORE ist und die getName()-API des Objekts Anbieter abgefragt werden kann. Es wird automatisch vom Treiber registriert und kann ohne Änderung Anwendung nahtlos verwendet werden.

Für die Beispiele auf dieser Seite, wenn Sie eine Windows-Zertifikatspeicher erstellt haben, spaltenhauptschlüssel und spaltenverschlüsselungsschlüssel mithilfe von SQL Server Management Studio basieren, das T-SQL-Skript erneut erstellen kann Ähnlichkeit mit diesem Beispiel durch eigene spezielle **KEY_PATH** und **ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> Während die andere Schlüsselspeicher-Anbieter in diesem Artikel auf allen Plattformen, die vom Treiber unterstützten verfügbar sind, ist die SQLServerColumnEncryptionCertificateStoreProvider-Implementierung des JDBC-Treibers auf Windows-Betriebssystemen verfügbar. Es besteht eine Abhängigkeit "sqljdbc_auth.dll", die im Treiberpaket enthaltenen verfügbar ist. Kopieren Sie die Datei "sqljdbc_auth.dll" zur Verwendung dieses Anbieters in ein Verzeichnis auf dem Windows-Systempfad auf dem Computer, auf dem der JDBC-Treiber installiert ist. Alternativ können Sie mit der java.libary.path-Systemeigenschaft das Verzeichnis von „sqljdbc_auth.dll“ angeben. Wenn Sie eine 32-Bit-JVM (Java Virtual Machine) ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x86“, auch wenn es sich bei dem Betriebssystem um die x64-Version handelt. Wenn Sie eine 64-Bit-JVM mit einem x64-Prozessor ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x64“. Beispielsweise können, wenn Sie die 32-Bit-JVM und der JDBC-Treiber wird im Standardverzeichnis installiert, Sie geben Sie den Speicherort der DLL mit dem folgenden Argument für den virtuellen Computer (VM) beim Start der Java-Anwendung: `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>Mithilfe von Java-Schlüsselspeicher-Anbieter
Der JDBC-Treiber ist mit einer integrierten Schlüsselspeicher-Anbieter-Implementierung für die Java-Schlüsselspeicher. Wenn die **KeyStoreAuthentication** Verbindungszeichenfolgen-Eigenschaft in der Verbindungszeichenfolge vorhanden ist und "JavaKeyStorePassword" festgelegt ist, der Treiber automatisch instanziiert und registriert den Java-Schlüsselspeicher-Anbieter. Der Name von der Java-Schlüsselspeicher-Anbieter ist MSSQL_JAVA_KEYSTORE. Dieser Name kann auch mithilfe der SQLServerColumnEncryptionJavaKeyStoreProvider.getName()-API abgefragt werden. 

Es gibt drei Verbindungszeichenfolgen-Eigenschaften, die eine Clientanwendung die Anmeldeinformationen angeben, die der Treiber benötigt Java-Schlüsselspeicher zu authentifizieren. Der Treiber initialisiert den Anbieter anhand der Werte für diese drei Eigenschaften in der Verbindungszeichenfolge angegeben.

**KeyStoreAuthentication:** identifiziert die Java-Schlüsselspeicher verwenden. Mit Microsoft JDBC Driver 6.0 und höher für SQL Server können Sie auf der Java-Schlüsselspeicher über diese Eigenschaft nur authentifizieren. Der Wert für diese Eigenschaft muss für die Java-Schlüsselspeicher `JavaKeyStorePassword`.

**KeyStoreLocation:** den Pfad zur Java-Schlüsselspeicher-Datei, in der die spaltenhauptschlüssel gespeichert. Der Pfad enthält den Dateinamen des Keystore.

**KeyStoreSecret:** das Kennwort für den geheimen/für den Schlüsselspeicher als auch für den Schlüssel verwendet. Für die Verwendung von Java-Schlüsselspeicher, müssen Keystore und das Kennwort für den Schlüssel identisch sein.

Hier ist ein Beispiel für diese Anmeldeinformationen in der Verbindungszeichenfolge angeben:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

Sie können auch abrufen oder legen Sie diese Einstellungen mithilfe der SQLServerDataSource-Objekts. Weitere Informationen finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).

Der JDBC-Treiber instanziiert die SQLServerColumnEncryptionJavaKeyStoreProvider automatisch, wenn diese Anmeldeinformationen in den Verbindungseigenschaften vorhanden sind.

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Erstellen einen spaltenhauptschlüssel für die Java-Schlüsselspeicher
Die SQLServerColumnEncryptionJavaKeyStoreProvider kann mit JKS oder PKCS12-Schlüsselspeicher-Typen verwendet werden. Erstellen oder importieren ein Schlüssels für die Verwendung mit diesem Anbieter verwenden, die Java [Keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) Hilfsprogramm. Der Schlüssel muss dasselbe Kennwort wie Keystore selbst aufweisen. Hier ist ein Beispiel zum Erstellen eines öffentlichen Schlüssels und dazugehörigen privaten Schlüssel mit dem Hilfsprogramm Keytool:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

Dieser Befehl erstellt einen öffentlichen Schlüssel und umschließt ihn in ein x. 509 selbstsigniertes Zertifikat, das im Schlüsselspeicher "keystore.jks" zusammen mit dem zugehörigen privaten Schlüssel gespeichert ist. Dieser Eintrag im Schlüsselspeicher wird durch den Alias "AlwaysEncryptedKey" identifiziert.

Hier ist ein Beispiel für die gleiche mit einem PKCS12-Speichertyp aus:

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

Wenn Keystore PKCS12-Typ aufweist, das Hilfsprogramm Keytool fordert nicht für ein Kennwort für den Schlüssel und Kennwort für der Schlüssel muss mit der Option - Keypass bereitgestellt werden, wie die SQLServerColumnEncryptionJavaKeyStoreProvider erfordert, dass die gleichen Keystore und den Schlüssel verfügen das Kennwort.

Sie können auch ein Zertifikat aus dem Windows-Zertifikatspeicher im PFX-Format exportieren und verwenden, die mit der SQLServerColumnEncryptionJavaKeyStoreProvider. Das exportierte Zertifikat kann auch auf die Java-Schlüsselspeicher als JKS Keystore Typ importiert werden.

Erstellen Sie nach dem Erstellen des Keytool-Eintrags, der spaltenhauptschlüssel-Metadaten in die Datenbank, die den Anbieternamen Keystore und dem Schlüsselpfad erforderlich ist. Weitere Informationen zum Erstellen von Hauptschlüssel-Spaltenmetadaten finden Sie unter [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Für SQLServerColumnEncryptionJavaKeyStoreProvider Schlüsselpfad ist nur der Alias des Schlüssels und der Name der SQLServerColumnEncryptionJavaKeyStoreProvider ist "MSSQL_JAVA_KEYSTORE". Sie können auch diesen Namen, die mit der öffentlichen getName()-API der Klasse SQLServerColumnEncryptionJavaKeyStoreProvider Abfragen. 

Die T-SQL-Syntax zum Erstellen des spaltenhauptschlüssels ist:

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

Die "AlwaysEncryptedKey" oben erstellten wäre der Spalten-hauptschlüsseldefinition:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> Die integrierte SQL Server Management Studio-Funktionalität kann nicht Hauptschlüssel Spaltendefinitionen für die Java-Schlüsselspeicher zu erstellen. T-SQL-Befehle müssen programmgesteuert verwendet werden.

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Erstellen eines spaltenverschlüsselungsschlüssels für die Java-Schlüsselspeicher
Der SQL Server Management Studio oder einem anderen Tool kann nicht verwendet werden, um Spalte Verschlüsselungsschlüssel mit der Hauptschlüssel für Spalten in der Java-Schlüsselspeicher zu erstellen. Die Clientanwendung muss den spaltenverschlüsselungsschlüssel, der programmgesteuert mithilfe der SQLServerColumnEncryptionJavaKeyStoreProvider-Klasse erstellen. Weitere Informationen finden Sie unter [Speicheranbieter Hauptschlüssel für die programmgesteuerte schlüsselbereitstellung mit](#using-column-master-key-store-providers-for-programmatic-key-provisioning).

### <a name="implementing-a-custom-column-master-key-store-provider"></a>Implementieren eines benutzerdefinierten Speicheranbieters für den Spaltenhauptschlüssel
Wenn Sie möchten zum Speichern von spaltenhauptschlüsseln in einem Schlüsselspeicher, die nicht von einem vorhandenen Anbieter unterstützt wird, können Sie einen benutzerdefinierten Anbieter implementieren, indem erweitern die SQLServerColumnEncryptionKeyStoreProvider-Klasse und registrieren den Anbieter mithilfe der Sqlserverconnection.registercolumnencryptionkeystoreproviders()-Methode.

```
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

Registrieren Sie den Anbieter:

```
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>Verwenden von Spaltenhauptschlüssel-Speicheranbietern für die programmgesteuerte Schlüsselbereitstellung
Wenn für den Zugriff auf verschlüsselte Spalten sucht nach Microsoft JDBC Driver für SQL Server transparent und ruft die rechte Spalte Speicheranbieter für spaltenhauptschlüssel um spaltenverschlüsselungsschlüssel zu entschlüsseln. In der Regel ruft der normale Anwendungscode die Speicheranbieter für Spaltenhauptschlüssel nicht direkt auf. Sie können jedoch instanziieren und rufen einen Anbieter programmgesteuert bereitstellen und Verwalten von Always Encrypted-Schlüssel. Dieser Schritt kann zum Generieren eines verschlüsselten spaltenverschlüsselungsschlüssels und Entschlüsseln eines spaltenverschlüsselungsschlüssels als Rotation der spaltenhauptschlüssel Teil, z. B. ausgeführt werden. Weitere Informationen finden Sie unter [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Übersicht über die Schlüsselverwaltung für Always Encrypted).

Wenn Sie einen benutzerdefinierten Schlüsselspeicheranbieter verwenden, kann die Implementierung eigener schlüsselverwaltungstools erforderlich sein. Bei Verwendung in Windows-Zertifikatspeicher oder Azure Key Vault gespeicherte Schlüsseln können Sie vorhandene Tools, z. B. SQL Server Management Studio oder PowerShell verwenden, verwalten und Bereitstellen von Schlüsseln zu verwenden. Wenn Sie Schlüssel gespeichert sind, in der Java-Schlüsselspeicher verwenden zu können, müssen Sie Schlüssel programmgesteuert bereitzustellen. Das folgende Beispiel veranschaulicht das Verwenden der SQLServerColumnEncryptionJavaKeyStoreProvider-Klasse zum Verschlüsseln des Schlüssels mit einem Schlüssel in der Java-Schlüsselspeicher gespeichert.

```
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider =
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key
                 * For more details on the syntax, see:
                 * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = "
                        + columnMasterKeyName
                        + " , ALGORITHM =  '"
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x"
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {
        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation :
         *      Path where keystore is located, including the keystore file name.
         * 2) keyStoreSecret :
         *      Password of the keystore and the key.
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>Aktivieren von Always Encrypted für Anwendungsabfragen
Die einfachste Möglichkeit zum Aktivieren der Verschlüsselung von Parametern und die Entschlüsselung der Abfrageergebnisse, die auf verschlüsselte Spalten ausgerichtet ist, durch Festlegen des Werts, der die **ColumnEncryptionSetting** Schlüsselwort für Verbindungszeichenfolgen zu **aktiviert** .

Die folgende Verbindungszeichenfolge ist ein Beispiel für die Aktivierung von Always Encrypted in der JDBC-Treiber:

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

Der folgende Code ist ein gleichwertiges Beispiel SQLServerDataSource-Objekts:

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

Always Encrypted kann auch für einzelne Abfragen aktiviert werden. Weitere Informationen finden Sie unter [Steuern der leistungsauswirkungen von Always Encrypted](#controlling-the-performance-impact-of-always-encrypted). Aktivieren von Always Encrypted reicht nicht aus, für die Verschlüsselung oder Entschlüsselung erfolgreich ausgeführt werden kann. Sie müssen auch Folgendes sicherstellen:
- Die Anwendung verfügt über die Datenbankberechtigungen *VIEW ANY COLUMN MASTER KEY DEFINITION* und *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , die für den Zugriff auf die Metadaten in der Datenbank über Always Encrypted-Schlüssel erforderlich sind. Weitere Informationen finden Sie unter [Berechtigungen in Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- Die Anwendung kann den spaltenhauptschlüssel zugreifen, der die spaltenverschlüsselungsschlüssel schützt die abgefragten Datenbankspalten verschlüsselt. Um den Java-Schlüsselspeicher-Anbieter verwenden, müssen Sie zusätzliche Anmeldeinformationen in der Verbindungszeichenfolge angeben. Weitere Informationen finden Sie unter [mit Java-Schlüsselspeicher-Anbieter](#using-java-key-store-provider).

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Konfigurieren, wie java.sql.Time-Werte an den Server gesendet werden
Die **SendTimeAsDatetime** Verbindungseigenschaft dient zum Konfigurieren, wie der java.sql.Time-Wert an den Server gesendet wird. Auf "false" festgelegt, wird der Zeitwert als Time-Typ SQL Server gesendet. Wenn festgelegt, die Zeit "true", die als Datentyp "DateTime"-Wert gesendet wird. Wenn eine Time-Spalte verschlüsselt wird, die **SendTimeAsDatetime** -Eigenschaft muss "false" sein, wie Sie verschlüsselte Spalten nicht die Konvertierung von Zeit in "DateTime" unterstützen. Beachten Sie außerdem, dass diese Eigenschaft von der Standardeinstellung "true", damit bei Verwendung von verschlüsselten Spalten Sie sie auf "false" festgelegt müssen. Andernfalls wird der Treiber eine Ausnahme ausgelöst. Ab Version 6.0 des Treibers, die SQLServerConnection-Klasse verfügt über zwei Methoden, um den Wert dieser Eigenschaft programmgesteuert zu konfigurieren:
 
* Öffentliche void SetSendTimeAsDatetime (boolesche SendTimeAsDateTimeValue)
* öffentlicher boolescher Wert getSendTimeAsDatetime()

Weitere Informationen zu dieser Eigenschaft finden Sie unter [konfigurieren wie java.sql.Time-Werte werden an den Server gesendet](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Konfigurieren, wie die Zeichenfolgenwerte an den Server gesendet werden
Die **SendStringParametersAsUnicode** Connection-Eigenschaft wird verwendet, um zu konfigurieren, die Zeichenfolgenwerte auf SQL Server gesendet werden. Wenn auf "true", String-Parameter im Unicode-Format an den Server gesendet werden. Wenn auf "false", String-Parameter festgelegt ist, die in nicht-Unicode-Format, z. B. ASCII oder MBCS, sondern gesendet werden. Der Standardwert für diese Eigenschaft ist "true". Wenn Always Encrypted aktiviert ist und eine char/varchar/varchar(max)-Spalte wird verschlüsselt, wird der Wert der **SendStringParametersAsUnicode** muss auf "false" festgelegt werden. Wenn diese Eigenschaft festgelegt ist, auf "true", der Treiber löst eine Ausnahme bei der Entschlüsselung von Daten aus einer verschlüsselten char/varchar/varchar(max)-Spalte, die Unicode-Zeichen aufweist. Weitere Informationen zu dieser Eigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md).
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Abrufen und Ändern von Daten in verschlüsselten Spalten
Nachdem Sie Always Encrypted für Anwendungsabfragen aktiviert, können Sie den JDBC-standard-APIs verwenden, abrufen und Ändern von Daten in verschlüsselten Datenbankspalten. Wenn die Anwendung die erforderlichen Datenbankberechtigungen verfügt und den spaltenhauptschlüssel zugreifen kann, wird der Treiber alle Abfrageparameter verschlüsseln, die verschlüsselte Spalten anvisieren und entschlüsselt die Daten, die aus verschlüsselten Spalten abgerufen werden.

Wenn Always Encrypted nicht aktiviert ist, tritt bei Abfragen mit Parametern, die auf verschlüsselte Spalten ausgerichtet sind, ein Fehler auf. Abfragen können weiterhin Daten aus verschlüsselten Spalten abrufen, solange die Abfrage keine Parameter für verschlüsselte Spalten enthält. Allerdings versucht der Treiber nicht auf die von verschlüsselten Spalten abgerufenen Werte zu entschlüsseln und erhält die Anwendung binäre verschlüsselte Daten (als Bytearrays).

Die folgende Tabelle fasst das Verhalten von Abfragen, je nachdem, ob Always Encrypted oder nicht aktiviert ist:

|Abfragemerkmal | Always Encrypted ist aktiviert und die Anwendung kann auf die Schlüssel und Schlüsselmetadaten zugreifen.|Always Encrypted ist aktiviert und die Anwendung kann nicht auf die Schlüssel oder Schlüsselmetadaten zugreifen. | Always Encrypted ist deaktiviert|
|:---|:---|:---|:---|
| Abfragen mit Parametern, die auf verschlüsselte Spalten ausgerichtet sind. | Parameterwerte werden transparent verschlüsselt. | Fehler | Fehler|
| Abfragen, die Abrufen von Daten aus verschlüsselten Spalten ohne Parameter für verschlüsselte Spalten.| Ergebnisse von verschlüsselten Spalten werden transparent entschlüsselt. Die Anwendung erhält klartextwerte der JDBC-Datentypen, die für die SQL Server-Datentypen, die für den verschlüsselten Spalten konfiguriert. | Fehler | Ergebnisse von verschlüsselten Spalten werden nicht entschlüsselt. Die Anwendung erhält verschlüsselte Werte als Bytearrays (byte[]).

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Einfügen und Abrufen von verschlüsselten Daten-Beispiele 
Die folgenden Beispiele veranschaulichen das Abrufen und Ändern von Daten in verschlüsselten Spalten. Die Beispiele gehen von der Zieltabelle mit dem folgenden Schema und den verschlüsselten Spalten von "ssn" und "BirthDate". Wenn Sie konfiguriert haben, als Spaltenhauptschlüssel mit dem Namen "MyCMK" und einen Verschlüsselungsschlüssel für die Spalte mit dem Namen "MyCEK" (wie in den vorangehenden Abschnitten von Schlüsselspeicher-Anbieter beschrieben), können Sie die Tabelle anhand des folgenden Skripts erstellen:

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

Für jedes Beispiel Java-Code müssen Sie zum Einfügen von Schlüsselspeicher-spezifischen Code am Speicherort notiert haben.

Wenn Sie einen Azure Key Vault-Schlüsselspeicher-Anbieter verwenden:

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Wenn Sie einen Windows-Zertifikatspeicher-Schlüsselspeicher-Anbieter verwenden:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

Wenn Sie einen Java-Schlüsselspeicher-Schlüsselspeicher-Anbieter verwenden:

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>Beispiel zum Einfügen von Daten
In diesem Beispiel wird eine Zeile in die Tabelle „Patients“ eingefügt. Beachten Sie die folgenden Elemente:
- Es erfolgt keine spezielle Verschlüsselung im Beispielcode. Microsoft JDBC Driver für SQL Server wird automatisch erkannt und verschlüsselt die Parameter, die verschlüsselte Spalten ausgerichtet. Dieses Verhalten wird Verschlüsselung für die Anwendung transparent.
- Die Werte, die in Datenbankspalten, einschließlich der verschlüsselten Spalten eingefügt werden als Parameter, die mithilfe der sqlserverpreparedstatement-Klasse übergeben. Beim Verwenden von Parametern optional ist, wenn Werte nicht verschlüsselten Spalten gesendet werden (obwohl es wird dringend empfohlen, da sie verhindert, dass SQL-Injection), es ist erforderlich, damit die Werte, die verschlüsselte Spalten ausgerichtet. Wenn die in den verschlüsselten Spalten eingefügten Werte als Literale in der abfrageanweisung eingebettet übergeben wurden, würde die Abfrage fehl, da der Treiber wären nicht in der Lage, zur Bestimmung der Werte in den verschlüsselten Zielspalten und würden sie die Werte nicht verschlüsselt. Daher würde der Server sie zurückweisen, da sie mit den verschlüsselten Spalten inkompatibel sind.
- Alle Werte, die vom Programm gedruckt wird als nur-Text wie Microsoft JDBC Driver für SQL Server die aus den verschlüsselten Spalten abgerufenen Daten transparent entschlüsselt werden.
- Wenn Sie auf diese Weise sind einer Suche mit einer WHERE-Klausel den Wert in die WHERE-Klausel muss verwendet werden, um als Parameter übergeben werden, damit der Treiber transparent vor dem Senden an die Datenbank verschlüsseln kann. Im folgenden Beispiel wird die "ssn" als Parameter übergeben, jedoch das LastName als Literal übergeben wird, wie LastName nicht verschlüsselt ist.
- Der Setter-Methode, die für den Parameter für die Spalte "ssn" verwendete ist setString(), die von SQL Server-Datentyp Char/Varchar zugeordnet wird. Wenn für diesen Parameter der Setter-Methode verwendet setNString(), die Nchar/Nvarchar zugeordnet wird wurde, würde die Abfrage fehl, da Always Encrypted keine Konvertierungen von verschlüsselten Nchar/Nvarchar-Werte in verschlüsselten Char/Varchar-Werte unterstützt.

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))
        {
            insertStatement.setString(1, "795-73-9838");
            insertStatement.setString(2, "Catherine");
            insertStatement.setString(3, "Abel");
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));
            insertStatement.executeUpdate();
            System.out.println("1 record inserted.\n");
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>Abrufen eines Datenbeispiels nur-Text
Im folgende Beispiel wird veranschaulicht, Filtern von Daten basierend auf verschlüsselten Werten und Abrufen von Klartextdaten aus verschlüsselten Spalten. Beachten Sie die folgenden Elemente:
- Der Wert in die WHERE-Klausel auf die Spalte "ssn" Filtern muss verwendet werden, um als Parameter übergeben werden, damit der Microsoft JDBC-Treiber für SQL Server transparent vor dem Senden an die Datenbank verschlüsseln können.
- Alle Werte, die vom Programm gedruckt wird als nur-Text wie Microsoft JDBC Driver für SQL Server aus den Spalten "ssn" und "BirthDate" abgerufenen Daten transparent entschlüsselt werden.

> [!NOTE]
> Wenn Spalten mittels deterministischer Verschlüsselung verschlüsselt sind, können Abfragen Übereinstimmungsvergleiche darauf ausführen. Weitere Informationen finden Sie unter [Auswählen der deterministischen oder zufälligen Verschlüsselung in Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";
    
        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "795-73-9838");
            ResultSet rs = selectStatement.executeQuery();
            while(rs.next())
            {
                System.out.println("SSN: " +rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName")+
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>Abrufen von verschlüsselten Daten, Beispiel
Wenn Always Encrypted nicht aktiviert ist, können Abfragen weiterhin Daten aus verschlüsselten Spalten abrufen, so lange die Abfrage keine Parameter für verschlüsselte Spalten enthält.

Das folgende Beispiel veranschaulicht das Abrufen von Binär verschlüsselten Daten aus verschlüsselten Spalten. Beachten Sie die folgenden Elemente:
- Da Always Encrypted in der Verbindungszeichenfolge nicht aktiviert ist, wird die Abfrage verschlüsselte Werte von "ssn" und "BirthDate" als Bytearrays zurück, die (das Programm die Werte in Zeichenfolgen konvertiert).
- Eine Abfrage, die Daten aus verschlüsselten Spalten mit deaktiviertem Always Encrypted abruft, kann Parameter aufweisen, so lange keiner der Parameter auf eine verschlüsselte Spalte ausgerichtet ist. Die folgenden Abfragefilter von LastName, die nicht in der Datenbank verschlüsselt ist. Wenn die Abfrage nach „SSN“ oder „BirthDate“ filtert, würde ein Fehler auftreten.

```
try
{
    String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;";

        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "Abel");
            ResultSet rs = selectStatement.executeQuery();
            while (rs.next())
            {
                System.out.println("SSN: " + rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName") +
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Vermeiden allgemeiner Probleme beim Abfragen von verschlüsselten Spalten
Dieser Abschnitt beschreibt allgemeine Kategorien von Fehlern beim Abfragen verschlüsselter Spalten aus Java-Anwendungen und einige Grundsätze zum vermeiden.

### <a name="unsupported-data-type-conversion-errors"></a>Konvertierungsfehler durch nicht unterstützte Datentypen
Always Encrypted unterstützt einige Konvertierungen für verschlüsselte Datentypen. Finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) für eine ausführliche Liste der unterstützten typkonvertierungen. Hier ist, was Sie tun können, um Fehler bei der datentypkonvertierung zu vermeiden. Stellen Sie Folgendes sicher:

- Verwenden Sie die entsprechenden Setter-Methoden, wenn die Übergabe der Werte für Parameter, die auf Spalten verschlüsselt. Stellen Sie sicher, dass der SQL Server-Datentyp des Parameters identisch mit dem Typ der Zielspalte ist oder eine Konvertierung von der SQL Server-Datentyp des Parameters in den Zieltyp der Spalte unterstützt wird. API-Methoden wurden für die SQLServerResultSet, SQLServerPreparedStatement und SQLServerCallableStatement-Klassen zum Übergeben von Parametern, die für bestimmte SQL Server-Datentypen hinzugefügt. Wenn eine Spalte nicht verschlüsselt ist z. B. können Sie die setTimestamp()-Methode einen Parameter oder eine Datetime-Spalte einen datetime2 übergeben. Aber wenn eine Spalte verschlüsselt wird, haben, verwenden Sie die genaue Methode, die den Typ der Spalte in der Datenbank darstellt. Verwenden Sie z. B. setTimestamp() Werte übergeben, um eine verschlüsselte datetime2-Spalte und setDateTime() zum Übergeben von Werten in einer verschlüsselten "DateTime"-Spalte verwenden. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) für eine vollständige Liste der neuen APIs.
- Die Genauigkeit und Dezimalstellenanzahl von Parametern, die auf Spalten der SQL Server-Datentypen „decimal“ und „numeric“ ausgerichtet sind, ist mit der für die Zielspalte konfigurierten Genauigkeit und Dezimalstellenanzahl identisch. API-Methoden wurden hinzugefügt, auf die SQLServerResultSet, SQLServerPreparedStatement und SQLServerCallableStatement-Klassen zum Akzeptieren von Genauigkeit und Dezimalstellenanzahl zusammen mit den Datenwerten für Parameter oder Spalten, die Datentypen decimal und numeric darstellt. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) für eine vollständige Liste der APIs neue/überladen.  
- die Sekundenbruchteile Genauigkeit/Skalierung der Parameter für Spalten von datetime2, Datetimeoffset oder Time SQL Server-Datentypen ist nicht größer als die Sekundenbruchteile-Precision/Dezimalstellen für die Zielspalte in Abfragen, die Werte der Zielspalte ändern . API-Methoden wurden für die SQLServerResultSet, SQLServerPreparedStatement und SQLServerCallableStatement-Klassen Sekundenbruchteile Genauigkeit/Skalierung zusammen mit den Datenwerten für Parameter, die diese Datentypen darstellen akzeptieren hinzugefügt. Eine vollständige Liste der neuen/überladen-APIs finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).   

### <a name="errors-due-to-incorrect-connection-properties"></a>Fehler aufgrund von falschen Verbindungseigenschaften
In diesem Abschnitt wird beschrieben, wie so konfigurieren Sie die Verbindungseinstellungen ordnungsgemäß um immer verschlüsselte Daten verwendet wird. Da Unterstützung für verschlüsselte Datentypen beschränkt Konvertierungen, die **SendTimeAsDatetime** und **SendStringParametersAsUnicode** Verbindungseinstellungen benötigen geeignete Konfiguration aus, wenn verschlüsselte Spalten zu verwenden. Stellen Sie Folgendes sicher: 
- [SendTimeAsDatetime](setting-the-connection-properties.md) verbindungseinstellung auf "false" festgelegt ist, beim Einfügen von Daten in Spalten verschlüsselt. Weitere Informationen finden Sie unter [konfigurieren, wie java.sql.Time-Werte an den Server gesendet werden](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- [SendStringParametersAsUnicode](setting-the-connection-properties.md) verbindungseinstellung auf festgelegt ist "true" (oder bleibt die Standardeinstellung) beim Einfügen von Daten in verschlüsselte char/varchar/varchar(max) Spalten umfassen.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Fehler aufgrund der Übergabe von Klartext anstelle von verschlüsselten Werten
Jeder Wert, der auf eine verschlüsselte Spalte ausgerichtet ist, muss in der Anwendung verschlüsselt werden. Ein Versuch einzufügen bzw. zu ändern oder nach einem Klartextwert für eine verschlüsselte Spalte zu filtern, führt zu einem Fehler, die etwa so aus:

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Stellen Sie Folgendes sicher, um solche Fehler zu vermeiden:
- immer ist Encrypted für Anwendungsabfragen für verschlüsselte Spalten (für die Verbindungszeichenfolge oder für eine bestimmte Abfrage) aktiviert.
- Verwendung von vorbereiteten Anweisungen und Parameter zum Senden von Daten auf verschlüsselte Spalten. Das folgende Beispiel zeigt eine Abfrage, die falsch nach einem Literal bzw. einer Konstante einer verschlüsselten Spalte (SSN) filtert, anstatt das Literal als Parameter übergeben. Diese Abfrage schlägt fehl:

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>Erzwingen der Verschlüsselung auf Eingabeparametern
Die Verschlüsselung erzwingen-Funktion erzwingt die Verschlüsselung eines Parameters bei Verwendung von Always Encrypted. Wenn Verschlüsselung erzwingen verwendet wird, und SQL Server den Treiber, den der Parameter nicht informiert verschlüsselt werden muss, wird die Abfrage, die mithilfe des Parameters fehl. Diese Eigenschaft bietet zusätzlichen Schutz vor Angriffen, bei denen ein kompromittierter SQL Server falsche Verschlüsselungsmetadaten für den Client bereitstellt, was zur Offenlegung von Daten führen kann. Die Methoden Satz * in die Sqlserverpreparedstatement- und SQLServerCallableStatement-Klassen und das Update\* Methoden in der SQLServerResultSet-Klasse sind überladen, sodass ein boolesches Argument, um anzugeben, die verschlüsselungseinstellung Force akzeptieren. Wenn der Wert dieses Arguments auf "false" festgelegt ist, wird der Treiber keine Verschlüsselung auf Parameter erzwungen. Wenn die Verschlüsselung erzwingen festgelegt ist auf "true", die Abfrage Parameter nur gesendet, wenn die Zielspalte verschlüsselt und Always Encrypted aktiviert ist, für die Verbindung oder bei der Anweisung an. Verwenden diese Eigenschaft bietet eine zusätzliche Sicherheitsebene, die sicherstellen, dass der Treiber keine versehentlich gesendet werden Daten mit SQL Server als nur-Text, wenn davon ausgegangen wird, verschlüsselt werden.

Weitere Informationen zu den Sqlserverpreparedstatement- und SQLServerCallableStatement-Methoden, die überladen werden mit der Force-verschlüsselungseinstellung finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Steuern der leistungsauswirkungen von Always Encrypted
Da Always Encrypted eine clientseitige verschlüsselungstechnologie ist, werden die meisten Beeinträchtigung der Systemleistung auf der Clientseite, nicht in der Datenbank festgestellt. Sind nicht nur die Kosten für verschlüsselungs-und Entschlüsselungsvorgänge können andere Quellen für Leistungseinbußen auf der Clientseite:
- Zusätzliche Roundtrips zur Datenbank zum Abrufen von Metadaten für Abfrageparameter.
- Aufrufe an einen Spaltenhauptschlüsselspeicher für den Zugriff auf einen Spaltenhauptschlüssel.

Dieser Abschnitt beschreibt die integrierten leistungsoptimierungen im Microsoft JDBC-Treiber für SQL Server und wie Sie die Auswirkungen der beiden oben genannten Faktoren auf die Leistung steuern können.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Kontrollieren von Roundtrips zum Abrufen von Metadaten für Abfrageparameter
Wenn Always Encrypted für eine Verbindung aktiviert ist, in der Standardeinstellung ruft der Treiber [Sys. sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) für jede parametrisierte Abfrage übergeben Sie die abfrageanweisung (ohne Parameterwerte) an SQL Server. [Sys. sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analysiert die Query-Anweisung, um herauszufinden, wenn alle Parameter müssen verschlüsselt werden, und wenn Ja, für jede eine It die verschlüsselungsbezogenen Informationen zurück, die den Treiber zum Verschlüsseln von Parameterwerten ermöglichen. Dieses Verhalten wird sichergestellt, dass ein hohes Maß an Transparenz für die Clientanwendung. Solange die Anwendung Parameter verwendet, um Werte zu übergeben, die an den Treiber verschlüsselte Spalten ausgerichtet, muss die Anwendung (und der Anwendungsentwickler) nicht wissen, welche Abfragen Zugriff auf verschlüsselte Spalten.

### <a name="setting-always-encrypted-at-the-query-level"></a>Festlegen von Always Encrypted auf Abfrageebene
Um die Beeinträchtigung der Leistung beim Abrufen von verschlüsselungsmetadaten für parametrisierte Abfragen zu steuern, können Sie die Always Encrypted für einzelne Abfragen anstelle der Einstellung für die Verbindung aktivieren. Auf diese Weise können Sie sicherstellen, diese Sys. sp_describe_parameter_encryption wird nur für Abfragen aufgerufen, die Sie kennen die Parameter für verschlüsselte Spalten haben. Beachten Sie jedoch, dass Sie die Transparenz der Verschlüsselung reduzieren, da Sie dadurch: Wenn Sie die Verschlüsselungseigenschaften der Datenbankspalten ändern, müssen Sie möglicherweise so ändern Sie den Code der Anwendung, um es mit den schemaänderungen auszurichten.

Um das Verhalten Always Encrypted für einzelne Abfragen zu steuern, müssen Sie so konfigurieren Sie einzelne Statement-Objekte durch Übergeben einer Enumeration SQLServerStatementColumnEncryptionSetting, der angibt, wie Daten gesendet und empfangen, beim Lesen und Schreiben verschlüsselte Spalten für bestimmte betreffende Anweisung ausführt. Hier sind einige nützliche Richtlinien:
- Wenn die meisten Abfragen, die eine Clientanwendung über eine datenbankverbindung greift auf verschlüsselte Spalten zugreifen, verwenden Sie diese Richtlinien:
    - Legen Sie die **ColumnEncryptionSetting** Schlüsselwort für Verbindungszeichenfolgen zu **aktiviert**.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.Disabled für einzelne Abfragen, die kein verschlüsselten Spalten zugreifen. Diese Einstellung wird sowohl aufrufenden Sys. sp_describe_parameter_encryption als auch beim Entschlüsseln der Werte im Resultset deaktiviert.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.ResultSet für einzelne Abfragen, die keine Parameter, die eine Verschlüsselung erforderlich ist, jedoch Daten aus verschlüsselten Spalten abrufen. Mit dieser Einstellung werden aufrufende Sys. sp_describe_parameter_encryption und die parameterverschlüsselung deaktiviert. Die Abfrage ist in der Lage, die Ergebnisse von Spaltenverschlüsselungen zu entschlüsseln.
- Wenn die meisten Abfragen, die eine Clientanwendung über eine datenbankverbindung greift nicht verschlüsselte Spalten zugreifen müssen, verwenden Sie diese Richtlinien:
    - Legen Sie die **ColumnEncryptionSetting** Schlüsselwort für Verbindungszeichenfolgen zu **deaktiviert**.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.Enabled für einzelne Abfragen, die Parameter aufweisen, die verschlüsselt werden müssen. Diese Einstellung wird sowohl aufrufenden Sys. sp_describe_parameter_encryption als auch die Entschlüsselung der Abfrageergebnisse von verschlüsselten Spalten abgerufenen aktivieren.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.ResultSet für Abfragen, die keine Parameter, die eine Verschlüsselung erforderlich ist, jedoch Daten aus verschlüsselten Spalten abrufen. Mit dieser Einstellung werden aufrufende Sys. sp_describe_parameter_encryption und die parameterverschlüsselung deaktiviert. Die Abfrage ist in der Lage, die Ergebnisse von Spaltenverschlüsselungen zu entschlüsseln.

Die SQLServerStatementColumnEncryptionSetting-Einstellungen können nicht verwendet werden, um Verschlüsselung zu umgehen und Zugriff auf Klartextdaten zu erhalten. Weitere Informationen zum Konfigurieren der spaltenverschlüsselung in einer Anweisung finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

Im folgenden Beispiel ist Always Encrypted für die datenbankverbindung deaktiviert. Die Abfrage von der Anwendung ausgestellte weist einen Parameter, der die LastName-Spalte ausgerichtet ist, die nicht verschlüsselt ist. Die Abfrage ruft Daten aus den Spalten „SSN“ und „BirthDate“ ab, die beide verschlüsselt sind. In diesem Fall ist der Aufruf von „sys.sp_describe_parameter_encryption“ nicht erforderlich, um Verschlüsselungsmetadaten abzurufen. Die Entschlüsselung der Abfrageergebnisse muss jedoch aktiviert werden, sodass die Anwendung klartextwerte aus den beiden verschlüsselten Spalten erhalten. Die SQLServerStatementColumnEncryptionSetting.ResultSet-Einstellung wird verwendet, um sicherzustellen, dass.

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord,
        ResultSet.TYPE_FORWARD_ONLY,
        ResultSet.CONCUR_READ_ONLY,
        connection.getHoldability(),
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");
ResultSet rs = selectStatement.executeQuery();
while(rs.next()) {
    System.out.println("First name: " + rs.getString("FirstName"));
    System.out.println("Last name: " + rs.getString("LastName"));
    System.out.println("SSN: " + rs.getString("SSN"));
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
}
rs.close();
selectStatement.close();
connection.close();
```

### <a name="column-encryption-key-caching"></a>Zwischenspeicherung von Spaltenverschlüsselungsschlüsseln
Um die Anzahl der Aufrufe an einen spaltenhauptschlüsselspeicher spaltenhauptschlüsselspeicher zu verringern, werden von Microsoft JDBC Driver für SQL Server die Klartext-spaltenverschlüsselungsschlüssel im Arbeitsspeicher zwischengespeichert. Nach dem Empfang der verschlüsselte spaltenverschlüsselungsschlüssel-Wert aus den Datenbankmetadaten, versucht der Treiber zunächst mithilfe der Softwareoption die Klartext-Verschlüsselungsschlüssel, der dem verschlüsselten Schlüsselwert entspricht. Der Treiber Ruft den Schlüsselspeicher, der den spaltenhauptschlüssel enthält, nur dann, wenn er den verschlüsselten spaltenverschlüsselungsschlüssel-Wert im Cache finden kann.

Sie können einen Time-to-live-Wert für die Spalte Verschlüsselung Schlüsseleinträge im Cache mithilfe der API setColumnEncryptionKeyCacheTtl(), in der SQLServerConnection-Klasse konfigurieren. Time-to-live-Wert für die Spalte Schlüsseleinträge Verschlüsselung im Cache beträgt zwei Stunden. Verwenden Sie zum Deaktivieren des Zwischenspeichern der Wert 0 ein. Um alle Time-to-live-Wert festzulegen, verwenden Sie die folgende API:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

Beispielsweise um eine Time-to-live-Wert von 10 Minuten festzulegen, verwenden Sie:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Tage, Stunden, Minuten oder Sekunden werden als die Zeiteinheit unterstützt.  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Kopieren die verschlüsselte Daten mithilfe von "sqlserverbulkcopy"
Mit "sqlserverbulkcopy" können Sie Daten kopieren, die bereits verschlüsselt und in einer Tabelle zu einer anderen Tabelle gespeichert werden, ohne die Daten zu entschlüsseln. Gehen Sie dazu wie folgt vor:

- Stellen Sie sicher, dass die Verschlüsselungskonfiguration der Zieltabelle mit der Konfiguration der Quelltabelle identisch ist. Insbesondere beide Tabellen müssen dieselben Spalten verschlüsselt, und die Spalten mithilfe derselben Verschlüsselungstypen und denselben Verschlüsselungsschlüsseln verschlüsselt werden müssen. Wenn eine Zielspalte anders als die entsprechende Quellspalte verschlüsselt ist, werden Sie nicht zum Entschlüsseln der Daten in der Zieltabelle nach dem Kopiervorgang sein. Die Daten werden beschädigt.
- Konfigurieren Sie beide Datenbankverbindungen, um die Quelltabelle und die Zieltabelle, ohne Always Encrypted aktiviert.
- Legen Sie die Option "allowencryptedvaluemodifications". Weitere Informationen finden Sie unter [Verwenden von Massenkopieren mit dem JDBC-Treiber](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Gehen Sie vorsichtig vor, wenn Sie "allowencryptedvaluemodifications" angeben, da diese Option führen möglicherweise zur Beschädigung der Datenbank, da der Microsoft JDBC-Treiber für SQL Server nicht überprüft, wenn die Daten tatsächlich verschlüsselt oder ordnungsgemäß mit der gleichen Verschlüsselung verschlüsselt wurden Typ, Algorithmus und Schlüssel wie die Zielspalte.

## <a name="see-also"></a>Siehe auch
[Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
