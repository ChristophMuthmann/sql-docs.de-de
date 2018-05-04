---
title: Always Encrypted-API-Referenz für den JDBC-Treiber | Microsoft Docs
ms.custom: ''
ms.date: 1/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09c72dbbfaa9863d63575f91eee2bbc2bb50ddb8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>Always Encrypted-API-Referenz für den JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  „Immer verschlüsselt“ ermöglicht es Clients, sensible Daten in Clientanwendungen zu verschlüsseln und die Verschlüsselungsschlüssel niemals an SQL Server weiterzugeben. Ein auf dem Clientcomputer installierter Treiber, bei dem „Immer verschlüsselt“ aktiviert ist, erreicht dies durch die automatische Ver- und Entschlüsselung von sensiblen Daten in der SQL Server-Clientanwendung. Der Treiber verschlüsselt die Daten in vertraulichen Spalten, bevor er sie an SQL Server weitergibt, und schreibt Abfragen automatisch neu, sodass die Semantik der Anwendung beibehalten wird. Auf ähnliche Weise entschlüsselt der Treiber transparent Daten in verschlüsselten Datenbankspalten, die in Abfrageergebnissen enthalten sind. Weitere Informationen finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) und [Using Always Encrypted mit dem JDBC-Treiber](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!NOTE]  
>  AE ist nur von Microsoft JDBC Driver 6.0 unterstützt oder höher für SQL Server mit SQL Server 2016.  
  
 ## <a name="always-encrypted-api-references"></a>Always Encrypted API-Referenzen
 
 Für Clientanwendungen, die „Immer verschlüsselt“ verwenden, sind mehrere neue Erweiterungen und Änderungen der JDBC-Treiber-API verfügbar.  
  
 **SQLServerConnection-Klasse**  
  
|Name|Description|  
|----------|-----------------|  
|Neues Verbindungszeichenfolgen-Schlüsselwort:<br /><br /> columnEncryptionSetting|ColumnEncryptionSetting = Enabled ermöglicht Always Encrypted-Funktion für die Verbindung und ColumnEncryptionSetting = Disabled Deaktiviert sie. Zulässige Werte sind „Enabled“/„Disabled“. Der Standardwert ist „Disabled“.|  
|Neue Methoden:<br /><br /> Öffentliche statische "void" SetColumnEncryptionTrustedMasterKeyPaths (Map < String, Liste\<Zeichenfolge >> TrustedKeyPaths)<br /><br /> Öffentliche statische "void" UpdateColumnEncryptionTrustedMasterKeyPaths (String-Server, Liste\<Zeichenfolge > TrustedKeyPaths)<br /><br /> Öffentliche statische "void" RemoveColumnEncryptionTrustedMasterKeyPaths (String-Server)|Ermöglicht das Festlegen/aktualisieren/entfernen wird eine Liste von vertrauenswürdigen schlüsselpfaden für einen Datenbankserver. Wenn der Treiber während der Verarbeitung eine Anwendungsabfrage einen Schlüsselpfad erhält, der nicht in der Liste enthalten ist, schlägt die Abfrage fehl. Diese Eigenschaft bietet zusätzlichen Schutz vor Angriffen, bei denen ein kompromittierter SQL Server gefälschte Schlüsselpfade bereitstellt, was zu Verlusten von Schlüsselspeicher-Anmeldeinformationen führen kann.|  
|Neue Methode:<br /><br /> Öffentliche statische Zuordnung < String, Liste\<Zeichenfolge >> getColumnEncryptionTrustedMasterKeyPaths()|Gibt eine Liste von vertrauenswürdigen Schlüsselpfaden für einen Datenbankserver zurück.|  
|Neue Methode:<br /><br /> Öffentliche statische "void" RegisterColumnEncryptionKeyStoreProviders (Zuordnung\<String, SQLServerColumnEncryptionKeyStoreProvider > ClientKeyStoreProviders)|Ermöglicht Ihnen, benutzerdefinierte Schlüsselspeicheranbieter zu registrieren. Dies ist ein Wörterbuch, das Anbieternamen von Schlüsselspeichern Implementierungen von Schlüsselspeicheranbietern zuordnet.<br /><br /> Um JVM Key Store zu verwenden, müssen Sie ein JSQLServerColumnEncryptionJVMKeyStoreProvider-Objekt mit Anmeldeinformationen von JVM Key Store instanziieren und beim Treiber registrieren. Der Name für diesen Anbieter muss "MSSQL_JVM_KEYSTORE" sein.<br /><br /> Um den Azure Key Vault-Speicher zu verwenden, müssen Sie zum Instanziieren eines Objekts SQLServerColumnEncryptionAzureKeyStoreProvider und registrieren Sie ihn mit dem Treiber. Der Name für diesen Anbieter muss 'AZURE_KEY_VAULT' sein.|
|Öffentlicher endgültigen boolescher Wert getSendTimeAsDatetime()|Gibt die Einstellung der-Verbindungseigenschaft SendTimeAsDatetime zurück.|
|Öffentliche void SetSendTimeAsDatetime (boolesche SendTimeAsDateTimeValue)|Ändert die Einstellung der-Verbindungseigenschaft SendTimeAsDatetime.|

 **SQLServerConnectionPoolProxy-Klasse**
|Name|Description|  
|----------|-----------------|  
|Öffentlicher endgültigen boolescher Wert getSendTimeAsDatetime()|Gibt die Einstellung der-Verbindungseigenschaft SendTimeAsDatetime zurück.|
|Öffentliche void SetSendTimeAsDatetime (boolesche SendTimeAsDateTimeValue)|Ändert die Einstellung der-Verbindungseigenschaft SendTimeAsDatetime.|
     
  
 **SQLServerDataSource-Klasse**  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche void SetColumnEncryptionSetting (ColumnEncryptionSetting Zeichenfolge)|Aktiviert/deaktiviert die „Immer verschlüsselt“-Funktionalität für das Datenquellenobjekt.<br /><br /> Der Standardwert ist „Disabled“.|  
|Öffentliche Zeichenfolge getColumnEncryptionSetting()|Ruft die „Immer verschlüsselt“-Funktionalitätseinstellung für das Datenquellenobjekt ab.|
|Öffentliche void SetKeyStoreAuthentication (KeyStoreAuthentication Zeichenfolge)|Legt den Namen, der einen Schlüsselspeicher identifiziert. Nur unterstützte Wert ist "JavaKeyStorePassword" für Java-Schlüsselspeicher-Identifiying.<br/><br/>Der Standardwert ist null.|
|Öffentliche Zeichenfolge getKeyStoreAuthentication()|Ruft den Wert der KeyStoreAuthentication-Einstellung für das Datenquellenobjekt ab.|
|Öffentliche void SetKeyStoreSecret (KeyStoreSecret Zeichenfolge)|Legt das Kennwort für die Java-Schlüsselspeicher. Beachten Sie, dass für Java-Schlüsselspeicher-Anbieter das Kennwort für den Schlüsselspeicher und die Schlüssel identisch sein muss. Beachten Sie, dass KeyStoreAuthentication muss mit "JavaKeyStorePassword" festgelegt werden.|
|Öffentliche void SetKeyStoreLocation (KeyStoreLocation Zeichenfolge)|Legt den Speicherort an, einschließlich des Dateinamens für die Java-Schlüsselspeicher fest. Beachten Sie, dass KeyStoreAuthentication muss mit "JavaKeyStorePassword" festgelegt werden.|
|Öffentliche Zeichenfolge getKeyStoreLocation()|Ruft die KeyStoreLocation für die Java-Schlüsselspeicher ab.|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider Class**  
  
 Die Implementierung des Schlüsselspeicheranbieters für Java-Schlüsselspeicher. Diese Klasse ermöglicht die Verwendung von Zertifikaten, die in der Java-Schlüsselspeicher gespeichert werden, als spaltenhauptschlüssel.  
  
 Konstruktoren  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche SQLServerColumnEncryptionJavaKeyStoreProvider (KeyStoreLocation String, Char [] KeyStoreSecret)|Schlüsselspeicheranbieter für die Java-Schlüsselspeicher.|  
  
 Methoden  
  
|Name|Description|  
|----------|-----------------|  
|public Byte [] DecryptColumnEncryptionKey (String MasterKeyPath, String EncryptionAlgorithm, Byte [] EncryptedColumnEncryptionKey)|Entschlüsselt den angegebenen verschlüsselten Wert eines CEK. Der verschlüsselte Wert muss verschlüsselte mithilfe des Zertifikats mit dem angegebenen Schlüsselpfad und angegebenen Algorithmus sein.<br /><br /> **Das Format des Schlüsselpfads sollte eines der folgenden sein:**<br /><br /> Fingerabdruck: <certificate_thumbprint><br /><br /> Alias:<certificate_alias><br /><br /> (Überschreibt SQLServerColumnEncryptionKeyStoreProvider. DecryptColumnEncryptionKey (String, String, Byte[]).)|  
|public Byte [] Decryptcolumnencryptionkey (String MasterKeyPath, String EncryptionAlgorithm, Byte [] Encryptedcolumnencryptionkey)|Verschlüsselt einen CEK, indem das Zertifikat mit dem angegebenen Schlüsselpfad und der angegebene Algorithmus verwendet wird.<br /><br /> **Das Format des Schlüsselpfads sollte eines der folgenden sein:**<br /><br /> Fingerabdruck: <certificate_thumbprint><br /><br /> Alias:<certificate_alias><br /><br /> (Überschreibt SQLServerColumnEncryptionKeyStoreProvider. Decryptcolumnencryptionkey (String, String, Byte[]).)|  
|Öffentliche void SetName (Zeichenfolgennamen)|Legt den Namen des Anbieters Schlüsselspeicher.|
|Öffentliche Zeichenfolge GetName)|Ruft den Namen dieser Schlüsselspeicheranbieter ab.|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider Class**  
  
 Die Implementierung des Schlüsselspeicheranbieters für Azure Key Vault. Diese Klasse ermöglicht die Schlüssel im Azure-Schlüsseltresor gespeichert sind, als spaltenhauptschlüssel verwenden.  
  
 Konstruktoren  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche SQLServerColumnEncryptionAzureKeyVaultProvider (ClientId Zeichenfolge, Zeichenfolge ClientKey)|Schlüsselspeicheranbieter für Azure Key Vault.  Sie müssen die ID und den Schlüssel der anfordernde Client das Token zur Authentifizierung beim Azure-Schlüsseltresor bereitstellen.|  
  
 Methoden  
  
|Name|Description|  
|----------|-----------------|  
|public Byte [] DecryptColumnEncryptionKey (String MasterKeyPath, String EncryptionAlgorithm, Byte [] EncryptedColumnEncryptionKey)|Entschlüsselt den angegebenen verschlüsselten Wert eines CEK. Der verschlüsselte Wert mit der angegebenen Spalte Schlüssel IDmaster Schlüssel und mit dem angegebenen Algorithmus verschlüsselt werden muss. <br />(Überschreibt SQLServerColumnEncryptionKeyStoreProvider. DecryptColumnEncryptionKey (String, String, Byte[]).)|  
|public Byte [] Decryptcolumnencryptionkey (String MasterKeyPath, String EncryptionAlgorithm, Byte [] ColumnEncryptionKey)|Verschlüsselt einen spaltenverschlüsselungsschlüssel mithilfe der angegebenen spaltenhauptschlüssel und mit dem angegebenen Algorithmus. <br />(Überschreibt SQLServerColumnEncryptionKeyStoreProvider. Decryptcolumnencryptionkey (String, String, Byte[]).)|  
|Öffentliche void SetName (Zeichenfolgennamen)|Legt den Namen des Anbieters Schlüsselspeicher.|
|Öffentliche Zeichenfolge GetName)|Ruft den Namen dieser Schlüsselspeicheranbieter ab.|  
  
  
 **SQLServerKeyVaultAuthenticationCallback-Schnittstelle**  
  
 Diese Schnittstelle enthält eine Methode für die Azure Key Vault-Authentifizierung vom Benutzer implementiert werden.  
  
 Methoden  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche Zeichenfolge GetAccessToken (Autorität für die Zeichenfolge, Zeichenfolgenressource, Zeichenfolge Bereich)|Die Methode muss überschrieben werden. Die Methode wird verwendet, um auf Azure Key Vault Zugriffstoken zu erhalten.|  
  
 **SQLServerColumnEncryptionKeyStoreProvider-Klasse**  
  
 Erweitern Sie diese Klasse, um einen benutzerdefinierten Schlüsselspeicheranbieter zu implementieren.  
  
|Name|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|Basisklasse für alle Schlüsselspeicheranbieter. Ein benutzerdefinierter Anbieter muss von dieser Klasse abgeleitet werden und deren Memberfunktionen überschreiben und registrieren ihn mit der SQLServerConnection. registerColumnEncryptionKeyStoreProviders().|  
  
 Methoden  
  
|Name|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|Basisklassenmethode, um den angegebenen verschlüsselten Wert eines CEK zu entschlüsseln. Es wird erwartet, dass der verschlüsselte Wert verschlüsselt wird, indem das Zertifikat mit dem angegebenen Schlüsselpfad sowie der angegebene Algorithmus verwendet wird.|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|Basisklassenmethode, um einen CEK mithilfe eines CMK mit dem angegebenen Schlüsselpfad und mithilfe des angegebenen Algorithmus zu verschlüsseln.|
|öffentliche abstrakte "void" SetName (Zeichenfolgennamen)|Legt den Namen des Anbieters Schlüsselspeicher.|
|öffentliche abstrakte Zeichenfolge getName()|Ruft den Namen dieser Schlüsselspeicheranbieter ab.|  
  
 Neue oder überladene Methoden in **SQLServerPreparedStatement** Klasse  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche void SetBigDecimal (Int ParameterIndex, BigDecimal x Int mit einfacher Genauigkeit, Dezimalstellen Int)<br /><br /> Öffentliche void SetObject (Int ParameterIndex, Objekt X, Int TargetSqlType, ganze Zahl mit einfacher Genauigkeit, Dezimalstellen Int)<br /><br /> Öffentliche void SetObject (Int ParameterIndex, Objekt X, SQLType TargetSqlType, ganze Zahl mit einfacher Genauigkeit, Skala ganze Zahl)<br /><br /> Öffentliche void SetTime (ParameterIndex Int, java.sql.Time Int Skalierung x)<br /><br /> Öffentliche void SetTimestamp (ParameterIndex Int, java.sql.Timestamp, Int Skalierung x) <br />Öffentliche void SetDateTimeOffset (Int ParameterIndex, microsoft.sql.DateTimeOffset Int Skalierung x)|Diese Methoden werden überladen, mit einer Genauigkeit oder ein Argument für Dezimalstellen Always Encrypted für bestimmte Datentypen unterstützen, benötigen die Genauigkeit und Anzahl der Dezimalstellen.|  
|Öffentliche void SetMoney (Int ParameterIndex, BigDecimal X)<br /><br /> Öffentliche void SetSmallMoney (Int ParameterIndex, BigDecimal X)<br /><br /> Öffentliche void SetUniqueIdentifier (ParameterIndex Int, String-Guid)<br /><br /> Öffentliche void SetDateTime (ParameterIndex Int, java.sql.Timestamp X)<br /><br /> Öffentliche void SetSmallDateTime (ParameterIndex Int, java.sql.Timestamp X)|Diese Methoden werden zur Unterstützung von Always Encrypted für Daten Datentypen Money, Smallmoney, "uniqueidentifier", "DateTime" und Smalldatetime hinzugefügt. <br/><br/>Beachten Sie, dass der vorhandene setTimestamp()-Methode für das Senden von Parameterwerten an die verschlüsselte datetime2-Spalte verwendet wird. Verwenden Sie für verschlüsselte Datetime und Smalldatetime-Spalten die neuen Methoden setDateTime() und setSmallDateTime() ein.|  
|Öffentliche endgültigen "void" SetBigDecimal (Int ParameterIndex, BigDecimal x mit einfacher Genauigkeit Int, Int Skala booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetMoney (Int ParameterIndex, BigDecimal x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetSmallMoney (Int ParameterIndex, BigDecimal x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetBoolean (ParameterIndex Int, boolean X, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetByte (ParameterIndex Int, Byte x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetBytes (ParameterIndex Int, Byte X[], boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetUniqueIdentifier (Int ParameterIndex, Guid der Zeichenfolge, boolescher ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetDouble (ParameterIndex Int, double X, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetFloat (Int ParameterIndex, "float" X, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetInt (ParameterIndex Int, Int-Wert, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetLong (ParameterIndex Int, Long X, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen SetObject (Int ParameterIndex, Objekt X, Int TargetSqlType, ganze Zahl mit einfacher Genauigkeit, Int Skala booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetObject (Int ParameterIndex, Objekt X, SQLType TargetSqlType, ganze Zahl mit einfacher Genauigkeit, ganze Zahl Skala booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetShort (ParameterIndex Int, short X, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetString (Int ParameterIndex, str Zeichenfolge, boolescher ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetNString (Int ParameterIndex, Zeichenfolgenwert, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetTime (Int ParameterIndex, java.sql.Time Int-Skalierung x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetTimestamp (Int ParameterIndex, java.sql.Timestamp, Int-Skalierung x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen void SetDateTimeOffset (Int ParameterIndex, microsoft.sql.DateTimeOffset Int-Skalierung x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetDateTime (ParameterIndex Int, java.sql.Timestamp x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetSmallDateTime (ParameterIndex Int, java.sql.Timestamp x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetDate (Int ParameterIndex, java.sql.Date, java.util.Calendar-cal x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetTime (Int ParameterIndex, java.sql.Time, java.util.Calendar-cal x booleschen ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetTimestamp (Int ParameterIndex, java.sql.Timestamp, java.util.Calendar-cal x booleschen ForceEncrypt)|Legt den angegebenen Parameter auf den angegebenen Java-Wert.<br /><br /> Wenn der boolesche ForceEncrypt festgelegt ist auf "true", die Abfrage Parameter wird nur festgelegt, wenn die Bezeichnung-Spalte verschlüsselt wird und Always Encrypted aktiviert ist, für die Verbindung oder bei der Anweisung an.<br /><br /> Wenn der boolesche ForceEncrypt auf "false" festgelegt ist, wird der Treiber keine Verschlüsselung auf Parameter erzwungen.|  
  
 Neue oder überladene Methoden in **SQLServerCallableStatement** Klasse  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche void RegisterOutParameter (Int ParameterIndex, SqlType Int, Int mit einfacher Genauigkeit, Int Skalierung)<br /><br /> Öffentliche void RegisterOutParameter (Int ParameterIndex, SQLType SqlType, Int Genauigkeit, Skala Int)<br /><br /> Öffentliche void RegisterOutParameter (String ParameterName, SqlType Int, Int Genauigkeit, Int Skalierung)<br /><br /> Öffentliche void RegisterOutParameter (Zeichenfolge ParameterName, SQLType SqlType, Int Genauigkeit, Skala Int)<br />Öffentliche void SetBigDecimal (Zeichenfolge ParameterName, BigDecimal bd, Int Genauigkeit, Skala Int)<br /><br /> Öffentliche void SetTime (String ParameterName, java.sql.Time t, Int Scale)<br /><br /> Öffentliche void SetTimestamp (Zeichenfolge ParameterName, t java.sql.Timestamp, Int Skalierung)<br /><br /> Öffentliche void SetDateTimeOffset (String ParameterName, t "Microsoft.SQL.DateTimeOffset" dar, Int Scale)<br/><br/>Öffentliche endgültigen "void" SetObject (Zeichenfolge sCol, Objekt X, Int TargetSqlType, ganze Zahl mit einfacher Genauigkeit, Dezimalstellen Int)|Diese Methoden werden überladen, mit einer Genauigkeit oder ein Argument für Dezimalstellen Always Encrypted für bestimmte Datentypen unterstützen, benötigen die Genauigkeit und Anzahl der Dezimalstellen.|  
|Öffentliche void SetDateTime (String ParameterName, java.sql.Timestamp X)<br /><br /> Öffentliche void SetSmallDateTime (String ParameterName, java.sql.Timestamp X)<br /><br /> Öffentliche void SetUniqueIdentifier (ParameterName Zeichenfolge, Zeichenfolge Guid)<br /><br /> Öffentliche void SetMoney (String ParameterName, BigDecimal bd)<br /><br /> Öffentliche void SetSmallMoney (String ParameterName, BigDecimal bd)<br/><br/>Öffentliche Timestamp GetDateTime (Int Index)<br/><br/>Öffentliche Timestamp GetDateTime (sCol Zeichenfolge)<br/><br/>Öffentliche Timestamp GetDateTime (Int Index, Kalender cal)<br/><br/>Öffentliche Zeitstempel GetSmallDateTime (Int Index)<br/><br/>Öffentliche Zeitstempel GetSmallDateTime (sCol Zeichenfolge)<br/><br/>Öffentliche Zeitstempel GetSmallDateTime (Int Index, Kalender cal)<br/><br/>Öffentliche Zeitstempel GetSmallDateTime (Zeichenfolgennamen, Kalender cal)<br/><br/>Öffentliche BigDecimal GetMoney (Int Index)<br/><br/>Öffentliche BigDecimal GetMoney (sCol Zeichenfolge)<br/><br/>Öffentliche BigDecimal GetSmallMoney (Int Index)<br/><br/>Öffentliche BigDecimal GetSmallMoney (sCol Zeichenfolge)|Diese Methoden werden zur Unterstützung von Always Encrypted für Daten Datentypen Money, Smallmoney, "uniqueidentifier", "DateTime" und Smalldatetime hinzugefügt. <br/><br/>Beachten Sie, dass der vorhandene setTimestamp()-Methode für das Senden von Parameterwerten an die verschlüsselte datetime2-Spalte verwendet wird. Verwenden Sie für verschlüsselte Datetime und Smalldatetime-Spalten die neuen Methoden setDateTime() und setSmallDateTime() ein.|  
|Öffentliche void SetObject (Zeichenfolge ParameterName, Object o, Int n, m Int, boolean ForceEncrypt)<br /><br /> Öffentliche void SetObject (String ParameterName, Objekt Obj, SQLType JdbcType, Int Skalierung, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetDate (String ParameterName, java.sql.Date x Kalender c, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetTime (String ParameterName, java.sql.Time t, Int Skalierung, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetTime (String ParameterName, java.sql.Time x Kalender c, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetDateTime (String ParameterName, x, boolesche ForceEncrypt java.sql.Timestamp)<br /><br /> Öffentliche void SetDateTimeOffset (Zeichenfolge ParameterName, t "Microsoft.SQL.DateTimeOffset" dar, Skalierung Int, boolean ForceEncrypt)<br /><br /> Öffentliche void SetSmallDateTime (String ParameterName, x, boolesche ForceEncrypt java.sql.Timestamp)<br /><br /> Öffentliche void SetTimestamp (Zeichenfolge ParameterName, t java.sql.Timestamp, Int Skalierung, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetTimestamp (String ParameterName, x, boolesche ForceEncrypt java.sql.Timestamp)<br /><br /> Öffentliche void SetUniqueIdentifier (ParameterName Zeichenfolge, Zeichenfolge-Guid, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetBytes (String ParameterName, Byte [] b, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetByte (ParameterName String, Byte b, booleschen ForceEncrypt)<br /><br /> Öffentliche void SetString (String ParameterName, zeichenfolgenzuordnungsvorgänge, boolesche ForceEncrypt)<br /><br /> Öffentliche endgültigen "void" SetNString (String ParameterName, Zeichenfolgenwert, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetMoney (String ParameterName, BigDecimal bd, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetSmallMoney (String ParameterName, BigDecimal bd, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetBigDecimal (Zeichenfolge ParameterName, BigDecimal bd, Genauigkeit Int, Int Skalierung, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetDouble (String ParameterName, double d, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetFloat (String ParameterName, "float"-f, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetInt (String ParameterName, Int i, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetLong (String ParameterName, lang l, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetShort (String ParameterName, kurze s, boolesche ForceEncrypt)<br /><br /> Öffentliche void SetBoolean (ParameterNames Zeichenfolge, boolescher Wert b, boolesche ForceEncrypt)<br/><br/>Öffentliche void SetTimeStamp (Zeichenfolge sCol, java.sql.Timestamp x Kalender c, boolesche ForceEncrypt)|Legt den angegebenen Parameter auf den angegebenen Java-Wert.<br /><br /> Wenn der boolesche ForceEncrypt festgelegt ist auf "true", die Abfrage Parameter wird nur festgelegt, wenn die Bezeichnung-Spalte verschlüsselt wird und Always Encrypted aktiviert ist, für die Verbindung oder bei der Anweisung an.<br /><br /> Wenn der boolesche ForceEncrypt auf "false" festgelegt ist, wird der Treiber keine Verschlüsselung auf Parameter erzwungen.|
 

 Neue oder überladene Methoden in **SQLServerResultSet** Klasse  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche Zeichenfolge GetUniqueIdentifier (Int ColumnIndex)<br/><br/>Öffentliche Zeichenfolge GetUniqueIdentifier (ColumnLabel Zeichenfolge)<br/><br/>   Öffentliche java.sql.Timestamp GetDateTime (Int ColumnIndex) <br/><br/> Öffentliche java.sql.Timestamp GetDateTime (Zeichenfolge Spaltenname)   <br/><br/> Öffentliche java.sql.Timestamp GetDateTime (Int ColumnIndex, Kalender cal)   <br/><br/>Öffentliche java.sql.Timestamp GetDateTime (Zeichenfolge ColName, Kalender cal)    <br/><br/>Öffentliche java.sql.Timestamp GetSmallDateTime (Int ColumnIndex)    <br/><br/> Öffentliche java.sql.Timestamp GetSmallDateTime (Zeichenfolge Spaltenname)   <br/><br/> Öffentliche java.sql.Timestamp GetSmallDateTime (Int ColumnIndex, Kalender cal)   <br/><br/> Öffentliche java.sql.Timestamp GetSmallDateTime (Zeichenfolge ColName, Kalender cal)   <br/><br/>  Öffentliche BigDecimal GetMoney (Int ColumnIndex)  <br/><br/> Öffentliche BigDecimal GetMoney (Zeichenfolge Spaltenname)   <br/><br/> Öffentliche BigDecimal GetSmallMoney (Int ColumnIndex)   <br/><br/>  Öffentliche BigDecimal GetSmallMoney (Zeichenfolge Spaltenname)  <br/><br/>Öffentliche void UpdateMoney (Zeichenfolge ColumnName BigDecimal X)    <br/><br/>  Öffentliche void UpdateSmallMoney (Zeichenfolge ColumnName BigDecimal X)  <br/><br/>     Öffentliche void UpdateDateTime (Index Int, java.sql.Timestamp X) <br/><br/> Öffentliche void UpdateSmallDateTime (Index Int, java.sql.Timestamp X) |Diese Methoden werden zur Unterstützung von Always Encrypted für Daten Datentypen Money, Smallmoney, "uniqueidentifier", "DateTime" und Smalldatetime hinzugefügt. <br/><br/>Beachten Sie, dass der vorhandene updateTimestamp() Methode zum Aktualisieren von verschlüsselten datetime2-Spalten verwendet wird. Verwenden Sie für verschlüsselte Datetime und Smalldatetime-Spalten die neuen Methoden updateDateTime() und updateSmallDateTime() ein.|
|Öffentliche void UpdateBoolean (Int Index, boolesche X, boolesche ForceEncrypt)  <br/><br/>  Öffentliche void UpdateByte (Index Int, Byte x booleschen ForceEncrypt)  <br/><br/>  Öffentliche void UpdateShort (Int Index, kurze X, boolesche ForceEncrypt)  <br/><br/> Öffentliche void UpdateInt (Index Int, Int x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateLong (Index Int, Long X, booleschen ForceEncrypt)  <br/><br/> Öffentliche void UpdateFloat (Int Index, "float" X, boolesche ForceEncrypt)   <br/><br/> Öffentliche void UpdateDouble (Index Int, double X, boolesche ForceEncrypt)   <br/><br/> Öffentliche void UpdateMoney (Int Index BigDecimal x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateMoney (Zeichenfolge ColumnName BigDecimal x booleschen ForceEncrypt)  <br/><br/> Öffentliche void UpdateSmallMoney (Int Index BigDecimal x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateSmallMoney (Zeichenfolge ColumnName BigDecimal x booleschen ForceEncrypt)  <br/><br/> Öffentliche void UpdateBigDecimal (Int Index BigDecimal x, ganze Zahl mit einfacher Genauigkeit, ganze Zahl Skala booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateString (Int ColumnIndex, StringValue Zeichenfolge, boolescher ForceEncrypt)  <br/><br/>  Öffentliche void UpdateNString (ColumnIndex Int, String nString, boolesche ForceEncrypt)  <br/><br/>  Öffentliche void UpdateNString (ColumnLabel Zeichenfolge, Zeichenfolge nString, boolesche ForceEncrypt)  <br/><br/> Öffentliche void UpdateBytes (Index Int, Byte X[], boolesche ForceEncrypt)   <br/><br/>  Öffentliche void UpdateDate (Index Int, java.sql.Date x booleschen ForceEncrypt)  <br/><br/> Öffentliche "void" UpdateTime (Int Index, java.sql.Time x Skalierung ganze Zahl, boolescher ForceEncrypt)   <br/><br/> Öffentliche void UpdateTimestamp (Index von Int, java.sql.Timestamp, Int-Skalierung x booleschen ForceEncrypt)   <br/><br/> Öffentliche void UpdateDateTime (Int Index, java.sql.Timestamp x Skalierung ganze Zahl, boolescher ForceEncrypt)   <br/><br/> Öffentliche void UpdateSmallDateTime (Int Index, java.sql.Timestamp x Skalierung ganze Zahl, boolescher ForceEncrypt)   <br/><br/>  Öffentliche void UpdateDateTimeOffset (Int Index "Microsoft.SQL.DateTimeOffset" dar, x, ganze Zahl Skala booleschen ForceEncrypt)  <br/><br/> Öffentliche void UpdateUniqueIdentifier (Index Int, String x booleschen ForceEncrypt)    <br/><br/>  Öffentliche void UpdateObject (Int Index, Objekt X, Int mit einfacher Genauigkeit, Int Skala booleschen ForceEncrypt)  <br/><br/>  Öffentliche void UpdateObject (Int Index, Objekt Obj, SQLType TargetSqlType, Int Skalierung, boolesche ForceEncrypt)  <br/><br/> Öffentliche void UpdateBoolean (ColumnName Zeichenfolge, boolescher X, boolesche ForceEncrypt)    <br/><br/>  Öffentliche void UpdateByte (ColumnName String, Byte x booleschen ForceEncrypt)  <br/><br/>  Öffentliche void UpdateShort (Zeichenfolge ColumnName, kurze X, boolesche ForceEncrypt)  <br/><br/> Öffentliche void UpdateInt (ColumnName String, Int x booleschen ForceEncrypt)   <br/><br/>   Öffentliche void UpdateLong (Zeichenfolge ColumnName, lang X, boolesche ForceEncrypt) <br/><br/>  Öffentliche void UpdateFloat (Zeichenfolge ColumnName, "float" X, boolesche ForceEncrypt)  <br/><br/>  Öffentliche void UpdateDouble (Zeichenfolge ColumnName, double X, boolesche ForceEncrypt)  <br/><br/> Öffentliche void UpdateBigDecimal (Zeichenfolge ColumnName BigDecimal x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateBigDecimal (Zeichenfolge ColumnName BigDecimal x, ganze Zahl mit einfacher Genauigkeit, ganze Zahl Skala booleschen ForceEncrypt)  <br/><br/> Öffentliche void UpdateString (Spaltenname Zeichenfolge, Zeichenfolge x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateBytes (ColumnName String, Byte X[], boolesche ForceEncrypt)  <br/><br/> Öffentliche void UpdateDate (Zeichenfolge ColumnName, java.sql.Date x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateTime (Zeichenfolge ColumnName, java.sql.Time Int-Skalierung x booleschen ForceEncrypt)  <br/><br/>  Öffentliche void UpdateTimestamp (Zeichenfolge ColumnName, java.sql.Timestamp, Int-Skalierung x booleschen ForceEncrypt)  <br/><br/> Öffentliche void UpdateDateTime (Zeichenfolge ColumnName, java.sql.Timestamp, Int-Skalierung x booleschen ForceEncrypt)   <br/><br/>  Öffentliche void UpdateSmallDateTime (Zeichenfolge ColumnName, java.sql.Timestamp, Int-Skalierung x booleschen ForceEncrypt)  <br/><br/>  Öffentliche void UpdateDateTimeOffset (Zeichenfolge ColumnName, microsoft.sql.DateTimeOffset Int-Skalierung x booleschen ForceEncrypt)  <br/><br/>  Öffentliche void UpdateUniqueIdentifier (Spaltenname Zeichenfolge, Zeichenfolge x booleschen ForceEncrypt)<br/><br/>Öffentliche void UpdateObject (Zeichenfolge ColumnName Objekt X, Int mit einfacher Genauigkeit, Int Skala booleschen ForceEncrypt)<br/><br/>Öffentliche void UpdateObject (ColumnName Zeichenfolge, Objekt Obj, SQLType TargetSqlType, Int Skalierung, boolesche ForceEncrypt)|Aktualisieren Sie die angegebene Spalte auf den angegebenen Java-Wert.<br/><br/>Wenn der boolesche ForceEncrypt festgelegt ist "true", die Spalte wird nur festgelegt, wenn er verschlüsselt und Always Encrypted aktiviert ist, für die Verbindung oder bei der Anweisung an.<br/><br/>Wenn der boolesche ForceEncrypt auf "false" festgelegt ist, wird der Treiber keine Verschlüsselung auf Parameter erzwungen.|

  
Neue Typen in **microsoft.sql.Types** Klasse
|Name|Description|  
|----------|-----------------|  
|DATETIME, SMALLDATETIME, MONEY, SMALLMONEY, GUID|Verwenden Sie diese Typen wie die Ziel-SQL-Datentypen beim Senden von Parameterwerten an **verschlüsselte** Datetime, Smalldatetime, Money, Smallmoney, Uniqueidentifier-Spalten, die mit setObject()/updateObject() API-Methoden.|  
  
  
 **SQLServerStatementColumnEncryptionSetting-Enumeration**  
  
 Gibt an, wie Daten gesendet und empfangen, beim Lesen und Schreiben von verschlüsselten Spalten. Je nach spezifischer Abfrage kann Leistungseinbußen reduziert werden, durch Umgehung des Always Encrypted-Treibers verarbeitet, wenn nicht verschlüsselte Spalten verwendet werden. Beachten Sie, dass diese Einstellungen verwendet werden können, um Verschlüsselung zu umgehen und Zugriff auf Klartextdaten zu erhalten.  
  
 **Syntax**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **Element**  
  
|Name|Description|  
|----------|-----------------|  
|UseConnectionSetting|Gibt an, dass der Befehl die Einstellung für die Always Encrypted in der Verbindungszeichenfolge angegeben standardmäßig sollte.|  
|Aktiviert|Aktiviert die grundsätzliche Verschlüsselung für die Abfrage.|  
|ResultSetOnly|Gibt an, dass nur die Ergebnisse des Befehls von der Routine Always Encrypted im Treiber verarbeitet werden sollen. Verwenden Sie diesen Wert, wenn der Befehl keine Parameter aufweist, die Verschlüsselung zu erzwingen.|  
|Disabled|Deaktiviert die grundsätzliche Verschlüsselung für die Abfrage.|  
  
 Die Anweisung ebeneneinstellung für AE werden hinzugefügt, um SQLServerConnection-Klasse und die SQLServerConnectionPoolProxy-Klasse. Die folgenden Methoden in dieser Klassen sind mit der neuen Einstellung überladen.  
  
|Name|Description|  
|----------|-----------------|  
|Öffentliche Anweisung CreateStatement (Int %nbenachrichtigungen zu, nConcur Int, Int StatementHoldability, SQLServerStatementColumnEncryptionSetting StmtColEncSetting)|Erstellt ein Statement-Objekt, das ResultSet-Objekte mit der angegebenen Datentyp, Parallelität und Haltbarkeit Spalte verschlüsselungseinstellung generiert wird.|  
|Öffentliche CallableStatement PrepareCall (Zeichenfolge Sql, Int %nbenachrichtigungen zu, nConcur Int, Int StatementHoldability, SQLServerStatementColumnEncryptionSetting StmtColEncSetiing)|Erstellt ein CallableStatement-Objekt mit der angegebenen spaltenverschlüsselungseinstellung, durch die ResultSet-Objekte mit dem angegebenen Typ, Parallelität und Haltbarkeit generiert werden.|  
|Öffentliche PreparedStatement PrepareStatement ("Zeichenfolge Sql", "Int" autogeneratedkeys ":", "SQLServerStatementColumnEncryptionSetting StmtColEncSetting")|Erstellt ein PreparedStatement-Objekt mit der angegebenen spaltenverschlüsselungseinstellung, die die Fähigkeit zum Abrufen automatisch generierter Schlüssel verfügt.|  
|Öffentliche PreparedStatement PrepareStatement (Sql String, String [] "ColumnNames" SQLServerStatementColumnEncryptionSetting StmtColEncSetting)|Erstellt ein PreparedStatement-Objekt mit der angegebenen spaltenverschlüsselungseinstellung, die ResultSet-Objekte mit den angegebenen Spaltennamen generieren.|  
|Öffentliche PreparedStatement PrepareStatement (Sql String, Int [] ColumnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting|Erstellt ein PreparedStatement-Objekt mit der angegebenen spaltenverschlüsselungseinstellung, die ResultSet-Objekte mit den angegebenen Indizes generieren.|  
|Öffentliche PreparedStatement PrepareStatement (Zeichenfolge Sql, Int %nbenachrichtigungen zu, nConcur Int, Int nHold, SQLServerStatementColumnEncryptionSetting StmtColEncSetting)|Erstellt ein PreparedStatement-Objekt mit der angegebenen spaltenverschlüsselungseinstellung, durch die ResultSet-Objekte mit dem angegebenen Typ, Parallelität und Haltbarkeit generiert werden.|  
  
> [!NOTE]  
>  Wenn Always Encrypted für eine Abfrage deaktiviert ist, und die Abfrage enthält Parameter, die verschlüsselte (Parameter) sein, die den verschlüsselten Spalten entsprechen müssen, wird die Abfrage fehl.  
>   
>  Wenn Always Encrypted für eine Abfrage deaktiviert ist, und die Abfrage gibt Ergebnisse aus den verschlüsselten Spalten zurück, gibt die Abfrage verschlüsselte Werte zurück. Die verschlüsselten Werte müssen Varbinary-Datentyp.  
  
 ## <a name="see-also"></a>Siehe auch  
 [Verwenden von „Immer verschlüsselt“ mit dem JDBC-Treiber](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

