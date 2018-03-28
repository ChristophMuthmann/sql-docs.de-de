---
title: Using Always Encrypted mit dem PHP-Treiber für SQLServer | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: article
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.workload: Inactive
ms.openlocfilehash: 588a0471866b1b33a3e485b321193edfd0c9187d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>Mit "immer verschlüsselt" mit der PHP-Treibern für SQLServer
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>Gilt für
 -   Microsoft Drivers 5.2 for PHP for SQLServer
 
## <a name="introduction"></a>Einführung

Dieser Artikel enthält Informationen zum Entwickeln von PHP-Anwendungen mit [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) und [PHP-Treiber für SQL Server](../../connect/php/Microsoft-php-driver-for-sql-server.md).

Always Encrypted ermöglicht Clientanwendungen das Verschlüsseln von vertraulichen Daten in einer Weise, dass weder die Daten noch die Verschlüsselungsschlüssel zu irgendeinem Zeitpunkt gegenüber SQL Server oder Azure SQL-Datenbank offengelegt werden. Ein Always Encrypted aktiviert-Treiber verwenden, z. B. den ODBC-Treiber für SQL Server, transparent verschlüsselt und entschlüsselt vertrauliche Daten in der Clientanwendung. Der Treiber ermittelt automatisch, welche Abfrageparameter vertraulichen Datenbankspalten (mit Always Encrypted geschützt) entsprechen. Die Werte dieser Parameter werden dann vor der Übergabe an SQL Server oder Azure SQL-Datenbank verschlüsselt. Auf ähnliche Weise entschlüsselt der Treiber die Daten transparent, die von verschlüsselten Datenbankspalten in Abfrageergebnissen empfangen werden. Weitere Informationen finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md). Die PHP-Treiber für SQL Server nutzen die ODBC-Treiber für SQL Server, um sensible Daten zu verschlüsseln.

## <a name="prerequisites"></a>Erforderliche Komponenten

 -   Konfigurieren Sie Always Encrypted in Ihrer Datenbank. Diese Konfiguration umfasst die Bereitstellung von Always Encrypted-Schlüssel und die Einrichtung der Verschlüsselung für ausgewählte Datenbankspalten. Wenn Sie nicht bereits über eine Datenbank verfügen, für die Always Encrypted konfiguriert ist, befolgen Sie die Anweisungen in [Erste Schritte mit Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). Insbesondere sollten Ihre Datenbank die Metadatendefinitionen für eine Zertifizierungsstelle (Column Master Key, CMK), eine Spalte Encryption Key (CEK) und eine Tabelle mit einer oder mehreren Spalten, die mit diesem CEK verschlüsselten enthalten.
 -   Stellen Sie sicher, dass ODBC-Treiber für SQL Server, Version 17 oder höher auf dem Entwicklungscomputer installiert ist. Weitere Informationen finden Sie unter [ODBC-Treiber für SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

## <a name="enabling-always-encrypted-in-a-php-application"></a>Aktivieren von "immer verschlüsselt" in einer PHP-Anwendung

Die einfachste Möglichkeit zum Aktivieren der Verschlüsselung von Parametern für den verschlüsselten Spalten und die Entschlüsselung der Abfrageergebnisse wird durch Festlegen des Werts, der die `ColumnEncryption` Schlüsselwort für Verbindungszeichenfolgen zu `Enabled`. Es folgen Beispiele für die Aktivierung von Always Encrypted in die SQLSRV- und PDO_SQLSRV-Treiber:

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

Aktivierung von Always Encrypted ist nicht ausreichend, damit die Verschlüsselung oder Entschlüsselung erfolgreich ausgeführt werden kann. Sie müssen auch sicherstellen, dass:
 -   Die Anwendung muss die VIEW ANY COLUMN MASTER KEY DEFINITION und VIEW ANY COLUMN ENCRYPTION KEY DEFINITION Datenbankberechtigungen, Zugriff auf die Metadaten zu Always Encrypted-Schlüssel in der Datenbank erforderlich. Weitere Informationen finden Sie unter [Datenbankberechtigung](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
 -   Die Anwendung kann den CMK zugreifen, die die CEKs für die abgefragten verschlüsselte Spalten schützt. Diese Anforderung ist abhängig von der Schlüsselspeicher-Anbieter, der den CMK speichert. Weitere Informationen finden Sie unter [arbeiten mit Spaltenhauptschlüsselspeichern](#working-with-column-master-key-stores).

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Abrufen und Ändern von Daten in verschlüsselten Spalten

Nachdem Sie Always Encrypted für eine Verbindung zu aktivieren, können Sie standard SQLSRV-APIs (finden Sie unter [SQLSRV-Treiber-API-Referenz](../../connect/php/sqlsrv-driver-api-reference.md)) oder PDO_SQLSRV-APIs (finden Sie unter [-API-Referenz zum Treiber PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)) abrufen und Ändern von Daten in verschlüsselten Datenbankspalten. Wenn Ihre Anwendung die erforderlichen Datenbankberechtigungen verfügt und den spaltenhauptschlüssel zugreifen kann, die der Treiber verschlüsselt alle Abfrageparameter, die verschlüsselte Spalten anvisieren und Entschlüsseln von Daten aus verschlüsselten Spalten, die Ihr Verhalten so transparent abgerufen der Anwendung, als ob die Spalten nicht verschlüsselt wurden.

Wenn Always Encrypted nicht aktiviert ist, nicht Abfragen mit Parametern, die verschlüsselte Spalten ausgerichtet. Daten können weiterhin aus verschlüsselten Spalten abgerufen werden, solange die Abfrage keine Parameter für verschlüsselte Spalten enthält. Allerdings versucht des Treibers Entschlüsselung nicht, und die Anwendung empfängt die verschlüsselten Binärdaten (als Bytearrays).

Die folgende Tabelle fasst das Verhalten von Abfragen, je nachdem, ob Always Encrypted oder nicht aktiviert ist:

| Abfrage-Merkmal | Always Encrypted aktiviert ist und die Anwendung zugreifen kann, die Schlüssel und schlüsselmetadaten | Always Encrypted aktiviert ist und die Anwendung kann nicht zugegriffen werden, den Schlüssel oder schlüsselmetadaten | Always Encrypted ist deaktiviert | | Parameter für verschlüsselte Spalten. | Parameterwerte werden transparent verschlüsselt. | Fehler | Fehler beim | | Abrufen von Daten aus verschlüsselten Spalten ohne Parameter für verschlüsselte Spalten. | Ergebnisse von verschlüsselten Spalten werden transparent entschlüsselt. Die Anwendung erhält klartextwerte der Spalte. | Fehler | Ergebnisse von verschlüsselten Spalten werden nicht entschlüsselt werden. Die Anwendung erhält verschlüsselte Werte als Bytearrays. |
 
Die folgenden Beispiele veranschaulichen das Abrufen und Ändern von Daten in verschlüsselten Spalten. Die Beispiele gehen von einer Tabelle mit dem folgenden Schema. Die Spalten "ssn" und "BirthDate" verschlüsselt sind.
```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>Einfügen von Daten (Beispiel)

Die folgenden Beispiele veranschaulichen, wie die SQLSRV- und PDO_SQLSRV-Treiber verwenden, um eine Zeile in die Patienten-Tabelle einzufügen. Beachten Sie die folgenden Punkte:
 -   Es erfolgt keine spezielle Verschlüsselung im Beispielcode. Der Treiber wird automatisch erkannt und die Werte der Parameter "ssn" und "BirthDate", die verschlüsselte Spalten ausgerichtet verschlüsselt. Dieser Mechanismus wird Verschlüsselung für die Anwendung transparent.
 -   Die Werte, die in Datenbankspalten, einschließlich der verschlüsselten Spalten eingefügt werden als gebundene Parameter übergeben. Beim Verwenden von Parametern ist optional, wenn Werte nicht verschlüsselten Spalten gesendet werden (obwohl es sich um eine wird dringend empfohlen, da sie verhindert, dass SQL-Injection), es ist erforderlich, damit die Werte, die auf verschlüsselte Spalten ausgerichtet sind. Wenn die in den Spalten "ssn" oder "BirthDate" eingefügten Werte als Literale in der abfrageanweisung eingebettet übergeben wurden, würde die Abfrage fehl, da der Treiber nicht versucht, verschlüsseln, oder andernfalls Literale in Abfragen zu verarbeiten. Daher würde der Server sie zurückweisen, da sie mit den verschlüsselten Spalten inkompatibel sind.
 -   Beim Einfügen von Werten, die mithilfe der Bind-Parameter muss ein SQL-Typ, die in den Datentyp der Zielspalte identisch ist oder dessen Konvertierung in den Datentyp der Zielspalte unterstützt wird, an die Datenbank übergeben. Diese Anforderung ist, da einige Typumwandlungen Always Encrypted unterstützt werden (Weitere Informationen finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)). Die zwei PHP-Treiber SQLSRV und PDO_SQLSRV, jede verfügt über einen Mechanismus, um dem Benutzer in der SQL-Typ des Werts zu ermitteln helfen. Aus diesem Grund muss der Benutzer nicht den SQL-Typ explizit angeben.
  -   Für den SQLSRV-Treiber hat der Benutzer zwei Optionen zur Verfügung:
   -   Basieren Sie auf den PHP-Treiber, um zu bestimmen, und legen Sie den richtigen SQL-Typ. In diesem Fall muss die Benutzer verwenden `sqlsrv_prepare` und `sqlsrv_execute` zum Ausführen einer parametrisierten Abfrage.
   -   Festlegen Sie den SQL-Typ explizit.
  -   Für den PDO_SQLSRV-Treiber besitzt der Benutzer nicht die Option aus, um die SQL-Typ, der einen Parameter explizit festlegen. Der PDO_SQLSRV-Treiber automatisch kann der Benutzer mithilfe den SQL-Typ zu bestimmen, wann eine parameterbindung.
 -   Die zum Bestimmen des Typs SQL-Treiber gelten einige Einschränkungen:
  -   SQLSRV-Treiber:
   -   Wenn der Benutzer den Treiber, um zu bestimmen, die SQL-Typen für die verschlüsselte Spalten möchte, muss der Benutzer verwenden `sqlsrv_prepare` und `sqlsrv_execute`.
   -   Wenn `sqlsrv_query` wird bevorzugt, der Benutzer ist verantwortlich für die SQL-Typen für alle Parameter angeben. Der angegebene SQL-Typ muss die Länge einer Zeichenfolge für Zeichenfolgen-Datentypen und die Dezimalstellen und Genauigkeit für Dezimaltypen enthalten.
  -   PDO_SQLSRV Driver:
   -   Das Anweisungsattribut `PDO::SQLSRV_ATTR_DIRECT_QUERY` wird in einer parametrisierten Abfrage nicht unterstützt.
   -   Das Anweisungsattribut `PDO::ATTR_EMULATE_PREPARES` wird in einer parametrisierten Abfrage nicht unterstützt.
   
SQLSRV-Treiber und [Sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

SQLSRV-Treiber und [Sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

PDO_SQLSRV-Treiber und [PDO:: Prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>Beispiel für nur-Text-Daten abrufen

Die folgenden Beispiele veranschaulichen, Filtern von Daten basierend auf verschlüsselten Werten und Abrufen von Klartextdaten aus verschlüsselten Spalten, die die SQLSRV- und PDO_SQLSRV-Treiber verwenden. Beachten Sie die folgenden Punkte:
 -   Der Wert in die WHERE-Klausel auf die Spalte "ssn" Filtern muss verwendet werden, um mithilfe der Bind-Parameter übergeben werden, damit, dass der Treiber transparent vor dem Senden an den Server verschlüsseln kann.
 -   Beim Ausführen der Abfrage mit gebundenen Parametern, die PHP-Treiber automatisch bestimmt den SQL-Typ für den Benutzer, wenn der Benutzer explizit den SQL-Typ gibt an, wenn der SQLSRV-Treiber verwenden.
 -   Alle Werte, die vom Programm gedruckt werden als nur-Text, da der Treiber aus den Spalten "ssn" und "BirthDate" abgerufenen Daten transparent entschlüsselt.
 
Hinweis: Abfragen können Übereinstimmungsvergleiche für verschlüsselte Spalten nur ausführen, wenn die Verschlüsselung deterministisch ist. Weitere Informationen finden Sie unter [Auswählen der deterministischen oder zufälligen Verschlüsselung](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>Beispielhafte Chiffretext abrufen

Wenn Always Encrypted nicht aktiviert ist, können Abfragen weiterhin Daten aus verschlüsselten Spalten abrufen, so lange die Abfrage keine Parameter für verschlüsselte Spalten enthält.

Die folgenden Beispiele veranschaulichen das Abrufen von Binär verschlüsselten Daten aus verschlüsselten Spalten, die die SQLSRV- und PDO_SQLSRV-Treiber verwenden. Beachten Sie die folgenden Punkte:
 -   Always Encrypted in der Verbindungszeichenfolge nicht aktiviert ist, gibt die Abfrage verschlüsselte Werte von "ssn" und "BirthDate" als Bytearrays (die Anwendung die Werte in Zeichenfolgen konvertiert).
 -   Eine Abfrage, die Daten aus verschlüsselten Spalten mit deaktiviertem Always Encrypted abruft, kann Parameter aufweisen, so lange keiner der Parameter auf eine verschlüsselte Spalte ausgerichtet ist. Die folgenden Abfragefilter von LastName, die nicht in der Datenbank verschlüsselt ist. Wenn die Abfrage nach "ssn" oder "BirthDate" filtert, würde die Abfrage fehl.
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Vermeiden allgemeiner Probleme beim Abfragen von verschlüsselter Spalten

Dieser Abschnitt beschreibt allgemeine Kategorien von Fehlern beim Abfragen verschlüsselter Spalten von PHP-Anwendungen und einige Grundsätze zum vermeiden.

#### <a name="unsupported-data-type-conversion-errors"></a>Konvertierungsfehler durch nicht unterstützte Datentypen

Always Encrypted unterstützt einige Konvertierungen für verschlüsselte Datentypen. Finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) für eine ausführliche Liste der unterstützten typkonvertierungen. Gehen Sie wie folgt vor, um Fehler bei Konvertierung des Datentyps zu vermeiden:
 -   Bei Verwendung des SQLSRV-Treibers mit `sqlsrv_prepare` und `sqlsrv_execute` der SQL-Typ, die Größe der Spalte und die Anzahl der Dezimalstellen des Parameters wird automatisch bestimmt.
 -   Wenn Sie den PDO_SQLSRV-Treiber zum Ausführen einer Abfrage verwenden, wird der SQL-Typ mit der Größe der Spalte und die Anzahl der Dezimalstellen des Parameters ebenfalls automatisch bestimmt.
 -   Bei Verwendung des SQLSRV-Treibers mit `sqlsrv_query` zum Ausführen einer Abfrage:
  -   Der SQL-Typ des Parameters ist entweder genau identisch mit dem Typ der entsprechenden Spalte, oder die Konvertierung von der SQL-Typ in den Typ der Spalte wird unterstützt.
  -   Die Genauigkeit und Dezimalstellenanzahl der Parameter, die Spalten von der `decimal` und `numeric` SQL Server-Datentypen ist identisch, die Genauigkeit und Dezimalstellenanzahl für die Zielspalte konfigurieren.
  -   Die Genauigkeit der Parameter für Spalten des `datetime2`, `datetimeoffset`, oder `time` SQL Server-Datentypen ist nicht größer als die Genauigkeit für die Zielspalte in Abfragen, die die Zielspalte zu ändern.
 -   Verwenden Sie keine PDO_SQLSRV Anweisungsattribute `PDO::SQLSRV_ATTR_DIRECT_QUERY` oder `PDO::ATTR_EMULATE_PREPARES` in einer parametrisierten Abfrage
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Fehler aufgrund der Übergabe von Klartext anstelle von verschlüsselten Werten

Jeder Wert, der eine verschlüsselte Spalte ausgerichtet ist, muss vor dem Senden an den Server verschlüsselt werden. Fehler beim Einfügen, ändern oder Filtern nach einem Klartextwert für eine verschlüsselte Spalte führt zu einem Fehler. Um solche Fehler zu vermeiden, stellen Sie sicher, dass:
 -   Always Encrypted ist aktiviert (festgelegt in der Verbindungszeichenfolge die `ColumnEncryption` Schlüsselwort `Enabled`).
 -   Verwenden Sie dazu die Bindungsparameter zum Senden von Daten, die auf verschlüsselte Spalten ausgerichtet sind. Das folgende Beispiel zeigt eine Abfrage, die falsch nach einem Literal bzw. einer Konstante einer verschlüsselten Spalte (SSN) filtert:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>Kontrollieren der Auswirkungen von Always Encrypted auf die Leistung

Da Always Encrypted eine clientseitige verschlüsselungstechnologie ist, werden die meisten Beeinträchtigung der Systemleistung auf der Clientseite, nicht in der Datenbank festgestellt. Sind nicht nur die Kosten für verschlüsselungs-und Entschlüsselungsvorgänge die anderen Quellen der Verwaltungsaufwand für die Clientseite:
 -   Zusätzliche Roundtrips zur Datenbank zum Abrufen von Metadaten für Abfrageparameter.
 -   Aufrufe an einen Spaltenhauptschlüsselspeicher für den Zugriff auf einen Spaltenhauptschlüssel.
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>Roundtrips zum Abrufen von Metadaten für Abfrageparameter

Wenn Always Encrypted für eine Verbindung aktiviert ist, der ODBC-Treiber werden standardmäßig Aufrufen [Sys. sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) für jede parametrisierte Abfrage übergeben Sie die abfrageanweisung (ohne Parameterwerte) an SQL Server . Diese gespeicherte Prozedur analysiert die Query-Anweisung, um herauszufinden, wenn alle Parameter müssen verschlüsselt werden, und wenn dies der Fall ist, gibt die verschlüsselungsbezogenen Informationen für jeden Parameter für den Treiber an sie verschlüsseln kann.

Da die PHP-Treiber den Benutzer zum Binden eines Parameters zulassen Geben Sie eine vorbereitete Anweisung ohne Angabe der SQL, rufen Sie die PHP-Treiber beim Binden eines Parameters in einer Verbindung mit Always Encrypted aktiviert, [SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md) auf die Parameter, um SQL-Typ, Größe und Dezimalstellen abzurufen. Die Metadaten wird dann verwendet, um Aufrufen [SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md). Diese zusätzlichen `SQLDescribeParam` Aufrufe erfordern keinen zusätzlichen Roundtrip zur Datenbank, da der ODBC-Treiber die Informationen bereits auf dem Client gespeichert hat beim `sys.sp_describe_parameter_encryption` aufgerufen wurde.

Die vorherigen Verhalten stellen Sie sicher, ein hohes Maß an Transparenz für die Client-Anwendung (und der Anwendungsentwickler) muss nicht beachten, welche Abfragen Zugriff auf verschlüsselte Spalten sein, solange die Werte, die auf verschlüsselte Spalten ausgerichtet an den Treiber in übergeben werden Parameter.

Im Gegensatz zu den ODBC-Treiber für SQL Server ist die Aktivierung von Always Encrypted auf Anweisungsebene/Abfrage-auf noch nicht bei den PHP-Treibern unterstützt. 

### <a name="column-encryption-key-caching"></a>Column Encryption Key, Zwischenspeichern

Um die Anzahl der Aufrufe zum Entschlüsseln von spaltenverschlüsselungsschlüsseln (CEK) an einen spaltenhauptschlüsselspeicher zu verringern, wird der Treiber den nur-Text-CEKs im Arbeitsspeicher zwischengespeichert. Nach dem Empfang der verschlüsselten CEK (ECEK) aus den Datenbankmetadaten, versucht der ODBC-Treiber zunächst Klartext-CEK entspricht dem verschlüsselten Schlüsselwert im Cache gefunden. Der Treiber Ruft den Schlüsselspeicher CMK nur, wenn die entsprechenden Klartext-CEK im Cache gefunden.

Hinweis: In der ODBC-Treiber für SQL Server, der Einträge im Cache nach einem Timeout von zwei Stunden entfernt werden. Dies bedeutet, dass für einen bestimmten ECEK kontaktiert der Treiber den Schlüsselspeicher nur einmal während der Lebensdauer der Anwendung oder alle zwei Stunden, welcher Wert kleiner ist.

## <a name="working-with-column-master-key-stores"></a>Arbeiten mit Spaltenhauptschlüsselspeichern

Zum Verschlüsseln und Entschlüsseln von Daten, muss der Treiber einen CEK zu erhalten, die für die Zielspalte konfiguriert ist. CEKs werden in verschlüsselter Form (ECEKs) in den Datenbankmetadaten gespeichert. Jede CEK verfügt über einen entsprechenden CMK, die beim Verschlüsseln verwendet wurde. Die [Datenbankmetadaten](../../t-sql/statements/create-column-master-key-transact-sql.md) speichert keine CMK selbst enthält nur den Namen der Schlüsselspeicher und Informationen, die der Schlüsselspeicher verwenden können, um den CMK zu suchen.

Um den nur-Text-Wert, der eine ECEK zu erhalten, erhält des Treibers zunächst die Metadaten über den CEK und ihre entsprechenden CMK, und klicken Sie dann anhand dieser Informationen wenden Sie sich an den Schlüsselspeicher CMK und fordert er zum Entschlüsseln der ECEK. Der Treiber kommuniziert mit einem Schlüsselspeicher, der über einen Schlüsselspeicheranbieter.

Für Microsoft Driver 5.2.0 für PHP für SQL Server wird nur Windows Store Zertifikatanbieter unterstützt. Die beiden anderen Keystore Anbieter von der ODBC-Treiber (Azure Key Vault und benutzerdefinierte Schlüsselspeicheranbieter) unterstützt werden noch nicht unterstützt.

### <a name="using-the-windows-certificate-store-provider"></a>Mithilfe des Windows-Zertifikatspeicher-Anbieters

Der ODBC-Treiber für SQL Server unter Windows umfasst eine integrierte Spalte Speicheranbieter für spaltenhauptschlüssel für den Windows-Zertifikatspeicher, mit dem Namen `MSSQL_CERTIFICATE_STORE`. (Dieser Anbieter ist nicht auf MacOS oder Linux verfügbar.) Mit diesem Anbieter der CMK lokal auf dem Clientcomputer gespeichert und ist keine zusätzliche Konfiguration von der Anwendung für die Verwendung mit dem Treiber erforderlich. Allerdings muss die Anwendung auf das Zertifikat und seinen privaten Schlüssel im Speicher zugreifen. Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>Einschränkungen der PHP-Treiber bei Verwendung von Always Encrypted

SQLSRV und PDO_SQLSRV:
 -   Linux/Mac OS-Unterstützung
  -   Linux/MacOS unterstützen keine Windows Store Zertifikatanbieter und d. h. der einzige Schlüsselspeicheranbieter unterstützt derzeit von PHP-Treibern
 -   Das Erzwingen des parameterverschlüsselung
 -   Aktivieren auf der Anweisungsebene Always Encrypted 
 
SQLSRV:
 -   Mithilfe von `sqlsrv_query` für Bindungsparameter ohne Angabe des SQL-Typs
 -   Mithilfe von `sqlsrv_prepare` zum Binden von Parametern in einem Batch mit SQL-Anweisungen  
 
PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` Anweisungsattribut angegeben, die in einer parametrisierten Abfrage
 -   `PDO::ATTR_EMULATE_PREPARE` Anweisungsattribut angegeben, die in einer parametrisierten Abfrage
 -   Binden von Parametern in einem Batch mit SQL-Anweisungen
 
Die PHP-Treiber erbt auch die Einschränkungen auferlegt werden vom ODBC-Treiber für SQL Server und die Datenbank. Finden Sie unter [Einschränkungen des ODBC-Treibers bei Verwendung von Always Encrypted](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) und [immer verschlüsselt Details zur Funktion](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details).  
  
## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
[API-Referenz für den SQLSRV-Treiber](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV Driver API Reference](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
