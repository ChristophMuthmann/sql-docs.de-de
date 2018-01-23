---
title: "Using Always Encrypted with the Odbcdriver für SQLServer | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
caps.latest.revision: "3"
ms.author: v-chojas
manager: jhubbard
author: MightyPen
ms.workload: On Demand
ms.openlocfilehash: a7e2679b04f55f528de1d90070593f6197160d79
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2018
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>Mit "immer verschlüsselt" mit dem ODBC-Treiber für SQLServer
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>Gilt für

- Odbcdriver 13.1 for SQLServer
- ODBC-Treiber 17 für SQLServer

### <a name="introduction"></a>Einführung

Dieser Artikel enthält Informationen zum Entwickeln von ODBC-Anwendungen mit [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) und [ODBC-Treiber für SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md).

Always Encrypted ermöglicht Clientanwendungen das Verschlüsseln von vertraulichen Daten in einer Weise, dass weder die Daten noch die Verschlüsselungsschlüssel zu irgendeinem Zeitpunkt gegenüber SQL Server oder Azure SQL-Datenbank offengelegt werden. Ein Always Encrypted aktiviert-Treiber verwenden, z. B. den ODBC-Treiber für SQL Server, erreicht dies durch die transparente Ver- und Entschlüsselung von sensiblen Daten in der Clientanwendung. Der Treiber ermittelt automatisch, welche Abfrageparameter vertraulichen Datenbankspalten (mit Always Encrypted geschützt) entsprechen. Die Werte dieser Parameter werden dann vor der Übergabe an SQL Server oder Azure SQL-Datenbank verschlüsselt. Auf ähnliche Weise entschlüsselt der Treiber die Daten transparent, die von verschlüsselten Datenbankspalten in Abfrageergebnissen empfangen werden. Weitere Informationen finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md).

### <a name="prerequisites"></a>Erforderliche Komponenten

Konfigurieren Sie Always Encrypted in Ihrer Datenbank. Dies umfasst die Bereitstellung von Always Encrypted-Schlüsseln und die Einrichtung der Verschlüsselung für ausgewählte Datenbankspalten. Wenn Sie nicht bereits über eine Datenbank verfügen, für die Always Encrypted konfiguriert ist, befolgen Sie die Anweisungen in [Erste Schritte mit Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted). Insbesondere sollten Ihre Datenbank die Metadatendefinitionen für eine Zertifizierungsstelle (Column Master Key, CMK), eine Spalte Encryption Key (CEK) und eine Tabelle mit einer oder mehreren Spalten, die mit diesem CEK verschlüsselten enthalten.

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>Aktivieren von "immer verschlüsselt" in einer ODBC-Anwendung

Die einfachste Möglichkeit, aktivieren Sie die parameterverschlüsselung und Entschlüsselung der Resultset-verschlüsselt-Spalte wird durch Festlegen des Werts von der `ColumnEncryption` Schlüsselwort für Verbindungszeichenfolgen zu **aktiviert**. Im folgenden finden ein Beispiel für eine Verbindungszeichenfolge, die Always Encrypted ermöglicht:

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

Always Encrypted möglicherweise ebenfalls aktiviert werden in der DSN-Konfiguration, die mit dem gleichen Schlüssel und Wert (die überschrieben werden soll, indem Sie die Verbindung Zeichenfolge festlegen, falls vorhanden) oder programmgesteuert mit der `SQL_COPT_SS_COLUMN_ENCRYPTION` vorverbindungsattribut. Auf diese Weise festlegen, überschreibt den Wert in der Verbindungszeichenfolge oder DSN festgelegt:

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

Nachdem für die Verbindung aktiviert ist, kann das Verhalten von Always Encrypted für einzelne Abfragen angepasst werden. Finden Sie unter [steuern die Leistung Auswirkungen von Always Encrypted](#controlling-the-performance-impact-of-always-encrypted) unten für Weitere Informationen.

Beachten Sie, dass die Aktivierung von Always Encrypted nicht ausreichend für die Verschlüsselung oder Entschlüsselung erfolgreich ist. Sie müssen auch sicherstellen, dass:

- Die Anwendung verfügt über die Datenbankberechtigungen *VIEW ANY COLUMN MASTER KEY DEFINITION* und *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , die für den Zugriff auf die Metadaten in der Datenbank über Always Encrypted-Schlüssel erforderlich sind. Weitere Informationen finden Sie unter [Datenbankberechtigungen](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).

- Die Anwendung kann den CMK die CEKs für die abgefragten verschlüsselte Spalten schützt zugreifen. Dies ist abhängig von der Schlüsselspeicheranbieter CMK gespeichert. Finden Sie unter [arbeiten mit Spaltenhauptschlüsselspeichern](#working-with-column-master-key-stores) für Weitere Informationen.

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Abrufen und Ändern von Daten in verschlüsselten Spalten

Nachdem Sie Always Encrypted für eine Verbindung zu aktivieren, können Sie standard-ODBC-APIs (finden Sie unter [ODBC-Beispielcode](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953) oder [ODBC Programmer's Reference](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) abrufen und Ändern von Daten in verschlüsselten Datenbankspalten. Angenommen, Ihre Anwendung verfügt über die erforderlichen Datenbankberechtigungen und den spaltenhauptschlüssel zugreifen können, der Treiber verschlüsselt alle Abfrageparameter, die verschlüsselte Spalten anvisieren und Entschlüsseln von Daten aus verschlüsselten Spalten, um transparent verhält abgerufen der Anwendung, als ob die Spalten nicht verschlüsselt wurden.

Wenn Always Encrypted nicht aktiviert ist, werden Abfragen mit Parametern, die verschlüsselte Spalten ausgerichtet fehl. Daten können weiterhin aus verschlüsselten Spalten abgerufen werden, solange die Abfrage keine Parameter für verschlüsselte Spalten enthält. Allerdings versucht der Treiber keiner Entschlüsselung und die Anwendung, die verschlüsselte Binärdaten (als Bytearrays) empfängt.

In der folgenden Tabelle wird das Verhalten von Abfragen, je nachdem, ob Always Encrypted oder nicht aktiviert ist zusammengefasst:

|Abfragemerkmal | Always Encrypted ist aktiviert und die Anwendung kann auf die Schlüssel und Schlüsselmetadaten zugreifen.|Always Encrypted ist aktiviert und die Anwendung kann nicht auf die Schlüssel oder Schlüsselmetadaten zugreifen. | Always Encrypted ist deaktiviert|
|:---|:---|:---|:---|
| Parameter für verschlüsselte Spalten. | Parameterwerte werden transparent verschlüsselt. | Fehler | Fehler|
| Abrufen von Daten aus verschlüsselten Spalten ohne Parameter für verschlüsselte Spalten ein.| Ergebnisse von verschlüsselten Spalten werden transparent entschlüsselt. Die Anwendung erhält klartextwerte der Spalte. | Fehler | Ergebnisse von verschlüsselten Spalten werden nicht entschlüsselt. Die Anwendung erhält verschlüsselte Werte als Bytearrays.

Die folgenden Beispiele veranschaulichen das Abrufen und Ändern von Daten in verschlüsselten Spalten. Die Beispiele gehen von einer Tabelle mit dem folgenden Schema. Beachten Sie, dass die Spalten „SSN“ und „BirthDate“ verschlüsselt werden.

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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>Einfügen von Daten (Beispiel)

In diesem Beispiel wird eine Zeile in die Tabelle „Patients“ eingefügt. Beachten Sie Folgendes:

- Es erfolgt keine spezielle Verschlüsselung im Beispielcode. Der Treiber wird automatisch erkannt und die Werte der Parameter "ssn" und das Datum, die verschlüsselte Spalten ausgerichtet verschlüsselt. Dadurch wird die Verschlüsselung für die Anwendung transparent.

- Die in Datenbankspalten, einschließlich der verschlüsselten Spalten eingefügten Werte als gebundene Parameter übergeben werden (siehe [SQLBindParameter-Funktion](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)). Beim Verwenden von Parametern ist optional, wenn Werte nicht verschlüsselten Spalten gesendet werden (obwohl es sich um eine wird dringend empfohlen, da sie verhindert, dass SQL-Injection), es ist erforderlich, damit die Werte, die auf verschlüsselte Spalten ausgerichtet sind. Wenn die in den Spalten "ssn" oder "BirthDate" eingefügten Werte als Literale in der abfrageanweisung eingebettet übergeben wurden, würde die Abfrage fehl, da der Treiber nicht versucht, verschlüsseln, oder andernfalls Literale in Abfragen zu verarbeiten. Daher würde der Server sie zurückweisen, da sie mit den verschlüsselten Spalten inkompatibel sind.

- Der SQL-Typ des Parameters in der Spalte "ssn" eingefügt wird festgelegt, um SQL_CHAR, der zugeordnet der **Char** SQL Server-Datentyp (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`). Wenn der Typ des Parameters auf SQL_WCHAR, festgelegt wurde, der den zuordnet **Nchar**, würde die Abfrage fehl, da Always Encrypted serverseitige Konvertierungen von verschlüsselten Nchar-Werte in verschlüsselten Char-Werten nicht unterstützt wird. Finden Sie unter [ODBC Programmer's Reference – Anhang D: Datentypen](https://msdn.microsoft.com/library/ms713607.aspx) Informationen zu den datentypzuordnungen.

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>Beispiel für nur-Text-Daten abrufen

Im folgenden Beispiel wird das Filtern von Daten auf Basis verschlüsselter Werte und das Abrufen von Klartextdaten aus verschlüsselten Spalten veranschaulicht. Beachten Sie Folgendes:

- Der Wert in die WHERE-Klausel auf die Spalte "ssn" Filtern muss verwendet werden, um mithilfe von SQLBindParameter übergeben werden, damit, dass der Treiber transparent vor dem Senden an den Server verschlüsseln kann.

- Alle Werte, die vom Programm gedruckt werden als nur-Text, da der Treiber aus den Spalten "ssn" und "BirthDate" abgerufenen Daten transparent entschlüsselt werden.

> [!NOTE]
> Abfragen können nur dann, wenn die Verschlüsselung deterministisch ist Übereinstimmungsvergleiche für verschlüsselte Spalten ausführen. Weitere Informationen finden Sie unter [Auswählen der deterministischen oder zufälligen Verschlüsselung](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>Beispielhafte Chiffretext abrufen

Wenn Always Encrypted nicht aktiviert ist, können Abfragen weiterhin Daten aus verschlüsselten Spalten abrufen, so lange die Abfrage keine Parameter für verschlüsselte Spalten enthält.

Das folgende Beispiel veranschaulicht das Abrufen von Binär verschlüsselten Daten aus verschlüsselten Spalten. Beachten Sie Folgendes:

- Da Always Encrypted in der Verbindungszeichenfolge nicht aktiviert ist, gibt die Abfrage verschlüsselte Werte von „SSN“ und „BirthDate“ als Bytearrays zurück (das Programm konvertiert die Werte in Zeichenfolgen).
- Eine Abfrage, die Daten aus verschlüsselten Spalten mit deaktiviertem Always Encrypted abruft, kann Parameter aufweisen, so lange keiner der Parameter auf eine verschlüsselte Spalte ausgerichtet ist. Die obige Abfrage filtert nach der Spalte „LastName“, die in der Datenbank nicht verschlüsselt ist. Wenn die Abfrage nach „SSN“ oder „BirthDate“ filtert, würde ein Fehler auftreten.


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Vermeiden allgemeiner Probleme beim Abfragen von verschlüsselter Spalten

Dieser Abschnitt beschreibt allgemeine Kategorien von Fehlern beim Abfragen verschlüsselter Spalten aus der ODBC-Anwendungen und einige Grundsätze zum vermeiden.

##### <a name="unsupported-data-type-conversion-errors"></a>Konvertierungsfehler durch nicht unterstützte Datentypen

Always Encrypted unterstützt einige Konvertierungen für verschlüsselte Datentypen. Finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) für eine ausführliche Liste der unterstützten typkonvertierungen. Um Fehler bei der datentypkonvertierung zu vermeiden, stellen Sie sicher, dass Sie die folgenden Punkte beachten, wenn Sie Parameter für verschlüsselte Spalten SQLBindParameter mit:

- Der SQL-Typ des Parameters ist entweder genau identisch mit dem Typ der entsprechenden Spalte, oder die Konvertierung von der SQL-Typ in den Typ der Spalte wird unterstützt.

- Die Genauigkeit und Dezimalstellenanzahl von Parametern, die für Spalten von der `decimal` und `numeric` SQL Server-Datentypen ist identisch mit der Genauigkeit und Dezimalstellenanzahl, die für die Zielspalte konfiguriert.

- Die Genauigkeit der Parameter für Spalten des `datetime2`, `datetimeoffset`, oder `time` SQL Server-Datentypen ist nicht größer als die Genauigkeit für die Zielspalte in Abfragen, die die Zielspalte zu ändern.  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Fehler aufgrund der Übergabe von Klartext anstelle von verschlüsselten Werten

Jeder Wert, der eine verschlüsselte Spalte ausgerichtet ist, muss vor dem Senden an den Server verschlüsselt werden. Ein Versuch, einzufügen, ändern, oder filtern Sie nach einem Klartextwert für eine verschlüsselte Spalte zu einem Fehler führt. Um solche Fehler zu vermeiden, stellen Sie sicher, dass:

- Always Encrypted aktiviert ist (in der DSN, der die Verbindungszeichenfolge vor dem Herstellen einer Verbindung durch Festlegen der `SQL_COPT_SS_COLUMN_ENCRYPTION` Verbindungsattribut für eine bestimmte Verbindung oder die `SQL_SOPT_SS_COLUMN_ENCRYPTION` Anweisungsattribut für eine bestimmte Anweisung).

- Verwenden Sie SQLBindParameter zum Senden von Daten, die auf verschlüsselte Spalten ausgerichtet sind. Das folgende Beispiel zeigt eine Abfrage, die falsch nach einem Literal bzw. einer Konstante einer verschlüsselten Spalte (SSN) filtert, anstatt das Literal als Argument übergeben, um SQLBindParameter.

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>Vorsichtsmaßnahmen bei Verwendung von SQLSetPos und SQLMoreResults

#### <a name="sqlsetpos"></a>SQLSetPos

Die `SQLSetPos` -API ermöglicht es eine Anwendung beim Aktualisieren von Zeilen in einem Resultset, Puffern, die mit SQLBindCol gebunden wurden und in die Zeile wurde zuvor abgerufene Daten, verwenden. Aufgrund der asymmetrischen Auffüllung Verhalten verschlüsselte Typen mit fester Länge ist es möglich, die Daten dieser Spalten unerwartet ändern, während der Durchführung von Updates auf andere Spalten in der Zeile. Mit AE werden Zeichenwerte fester Länge aufgefüllt werden, wenn der Wert kleiner als die Größe des Puffers ist.

Um dieses Verhalten zu verringern, verwenden die `SQL_COLUMN_IGNORE` Flag Spalten ignorieren, die nicht im Rahmen des aktualisiert werden `SQLBulkOperations` als auch bei `SQLSetPos` für Cursor-basierte Updates.  Alle Spalten, die nicht direkt von der Anwendung geändert werden ignoriert werden sollen, sowohl für Leistung und zur Verkürzung von Spalten zu vermeiden, die auf einen Puffer gebunden sind *kleinere* als ihre Originalgröße (DB). Weitere Informationen finden Sie unter [SQLSetPos Funktionsverweis](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx).

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

Anwendungsprogramme, die möglicherweise Aufrufen [SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx) zurückzugebenden Metadaten zu Spalten in der vorbereiteten Anweisungen.  Wenn Always Encrypted aktiviert ist, Aufrufen `SQLMoreResults` *vor* Aufrufen `SQLDescribeCol` bewirkt, dass [Sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) um aufgerufen werden, die keinen ordnungsgemäß zurückgibt des nur-Text Metadaten für verschlüsselte Spalten. Um dieses Problem zu vermeiden, rufen `SQLDescribeCol` für vorbereitete Anweisungen *vor* Aufrufen `SQLMoreResults`.

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>Steuern der Auswirkungen auf die Leistung von Always Encrypted

Da Always Encrypted eine clientseitige verschlüsselungstechnologie ist, werden die meisten Beeinträchtigung der Systemleistung auf der Clientseite, nicht in der Datenbank festgestellt. Sind nicht nur die Kosten für verschlüsselungs-und Entschlüsselungsvorgänge die anderen Quellen der Verwaltungsaufwand für die Clientseite:

- Zusätzliche Roundtrips zur Datenbank zum Abrufen von Metadaten für Abfrageparameter.

- Aufrufe an einen Spaltenhauptschlüsselspeicher für den Zugriff auf einen Spaltenhauptschlüssel.

Dieser Abschnitt beschreibt die integrierten leistungsoptimierungen im ODBC-Treiber für SQL Server und wie Sie die Auswirkungen der beiden oben genannten Faktoren auf die Leistung steuern können.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Steuern der Roundtrips zum Abrufen von Metadaten für Abfrageparameter

Wenn Always Encrypted für eine Verbindung aktiviert ist, ruft der Treiber, standardmäßig [Sys. sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) für jede parametrisierte Abfrage übergeben Sie die abfrageanweisung (ohne Parameterwerte) an SQL Server. Diese gespeicherte Prozedur analysiert die Query-Anweisung, um herauszufinden, wenn alle Parameter müssen verschlüsselt werden, und wenn dies der Fall ist, gibt die verschlüsselungsbezogenen Informationen für jeden Parameter für den Treiber an sie verschlüsseln kann. Das oben beschriebene Verhalten stellt einen hohen Grad an Transparenz für die Clientanwendung sicher: die Anwendung (und der Anwendungsentwickler) muss nicht beachten, welche Abfragen Zugriff auf verschlüsselte Spalten sein, solange die Werte, die auf verschlüsselte Spalten ausgerichtet sind, übergeben werden der Treiber in den Parametern.

### <a name="per-statement-always-encrypted-behavior"></a>Das Verhalten "immer verschlüsselt" pro-Anweisung

Um die Beeinträchtigung der Leistung beim Abrufen von verschlüsselungsmetadaten für parametrisierte Abfragen zu steuern, können Sie das Verhalten Always Encrypted für einzelne Abfragen zu ändern, wenn es für die Verbindung aktiviert wurde. Auf diese Weise können Sie sicherstellen, die `sys.sp_describe_parameter_encryption` aufgerufen wird, nur für Abfragen, die Sie kennen die Parameter für verschlüsselte Spalten auf. Beachten Sie jedoch, dass auf diese Weise Sie Transparenz der Verschlüsselung reduzieren: Wenn Sie zusätzliche Spalten in der Datenbank zu verschlüsseln, müssen Sie möglicherweise so ändern Sie den Code der Anwendung, um es mit den schemaänderungen auszurichten.

Rufen Sie zum Steuern der Always Encrypted-Verhalten einer Anweisung SQLSetStmtAttr Festlegen der `SQL_SOPT_SS_COLUMN_ENCRYPTION` -Anweisungsattribut auf einen der folgenden Werte:

|Wert|Description|
|-|-|
|`SQL_CE_DISABLED` (0)|Always ist Encrypted für die Anweisung deaktiviert|
|`SQL_CE_RESULTSETONLY` (1)|Entschlüsselung. Entschlüsselt von Resultsets und Rückgabewerte und Parameter werden nicht verschlüsselt.|
|`SQL_CE_ENABLED` (3) | Immer verschlüsselt ist, aktiviert und für Parameter und die Ergebnisse verwendet werden|

Neue Anweisungshandles erstellt, die von einer Verbindung mit Always Encrypted aktiviert standardmäßig die SQL_CE_ENABLED. Aus eine Verbindung mit ihm erstellten SQL_CE_DISABLED standardmäßig deaktiviert (und es ist nicht möglich, um Always Encrypted darauf zu aktivieren.)

Wenn die meisten Abfragen einer Clientanwendung auf verschlüsselte Spalten zugreifen, wird Folgendes empfohlen:

- Legen Sie die `ColumnEncryption` Schlüsselwort für Verbindungszeichenfolgen zu `Enabled`.

- Legen Sie die `SQL_SOPT_SS_COLUMN_ENCRYPTION` -Attribut `SQL_CE_DISABLED` auf Anweisungen, die kein verschlüsselte Spalten zugreifen müssen. Dadurch werden sowohl aufrufen deaktiviert `sys.sp_describe_parameter_encryption` festlegen sowie versucht, die Werte im Resultset zu entschlüsseln.
    
- Legen Sie die `SQL_SOPT_SS_COLUMN_ENCRYPTION` -Attribut `SQL_CE_RESULTSETONLY` auf Anweisungen, die keinen Parameter eine Verschlüsselung erforderlich ist, aber Daten aus verschlüsselten Spalten abrufen. Dadurch werden der Aufruf deaktiviert `sys.sp_describe_parameter_encryption` und die parameterverschlüsselung. Ergebnisse, die mit verschlüsselten Spalten werden fortgesetzt, entschlüsselt werden.

## <a name="always-encrypted-security-settings"></a>Always Encrypted Sicherheitseinstellungen

### <a name="force-column-encryption"></a>Spaltenverschlüsselung

Um die Verschlüsselung eines Parameters zu erzwingen, legen Sie die `SQL_CA_SS_FORCE_ENCRYPT` Implementation Parameter Descriptor, (IPD) Feld durch einen Aufruf an die SQLSetDescField-Funktion. Ein Wert ungleich 0 (null) bewirkt, dass der Treiber einen Fehler zurück, wenn keine verschlüsselungsmetadaten für den zugeordneten Parameter zurückgegeben wird.

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

Wenn SQL Server den Treiber, den der Parameter nicht verschlüsselt werden muss informiert, werden Abfragen, verwenden diesen Parameter fehl. Dieses Kennwort bietet zusätzlichen Schutz vor Sicherheitsangriffen, die denn diese enthalten ein kompromittierter SQL Server falsche verschlüsselungsmetadaten für den Client bereitstellt, was zur Offenlegung von Daten führen kann.

### <a name="column-encryption-key-caching"></a>Column Encryption Key, Zwischenspeichern

Um die Anzahl der Aufrufe an einen spaltenhauptschlüsselspeicher spaltenhauptschlüsselspeicher zu verringern, wird der Treiber den nur-Text-CEKs im Arbeitsspeicher zwischengespeichert. Nach dem Empfang der ECEK von Datenbankmetadaten, versucht der Treiber zunächst Klartext-CEK entspricht dem verschlüsselten Schlüsselwert im Cache gefunden. Der Treiber Ruft den Schlüsselspeicher CMK nur, wenn die entsprechenden Klartext-CEK im Cache gefunden.

> [!NOTE]
> In der ODBC-Treiber für SQL Server werden die Einträge im Cache nach einem Timeout von zwei Stunden entfernt. Dies bedeutet, dass für einen bestimmten ECEK kontaktiert der Treiber den Schlüsselspeicher nur einmal während der Lebensdauer der Anwendung oder alle zwei Stunden, welcher Wert kleiner ist.

## <a name="working-with-column-master-key-stores"></a>Arbeiten mit Spaltenhauptschlüsselspeichern

Zum Verschlüsseln und Entschlüsseln von Daten, muss der Treiber einen CEK zu erhalten, die für die Zielspalte konfiguriert ist. CEKs werden in verschlüsselter Form (ECEKs) in den Datenbankmetadaten gespeichert. Jede CEK verfügt über einen entsprechenden CMK, die beim Verschlüsseln verwendet wurde. Die [Datenbankmetadaten](../../t-sql/statements/create-column-master-key-transact-sql.md) speichert keine CMK selbst enthält nur den Namen des Keystore und Informationen, die der Schlüsselspeicher verwenden kann, um den CMK zu suchen.

Um den nur-Text-Wert, der eine ECEK zu erhalten, erhält des Treibers zunächst die Metadaten über den CEK und ihre entsprechenden CMK, und klicken Sie dann anhand dieser Informationen wenden Sie sich an den Schlüsselspeicher mit dem CMK und fordert er zum Entschlüsseln der ECEK. Der Treiber kommuniziert mit einem Schlüsselspeicher, der mit einem Schlüsselspeicheranbieter.

### <a name="built-in-keystore-providers"></a>Integrierte-Schlüsselspeicher-Anbieter

Der ODBC-Treiber für SQL Server enthält die folgenden integrierten-Schlüsselspeicher-Anbieter:

| Name | Description | Name des Anbieters (Metadaten) |Verfügbarkeit|
|:---|:---|:---|:---|
|Azure-Schlüsseltresor |Speichern von CMKs in ein Azure-Schlüsseltresor | `AZURE_KEY_VAULT` |Windows, macOS, Linux|
|Windows Certificate Store|CMKs lokal speichert, in der Windows-Schlüsselspeicher| `MSSQL_CERTIFICATE_STORE`|Windows|

- Sie (oder Ihrem DBA) müssen sicherstellen, dass die in den Metadaten des spaltenhauptschlüssels, konfigurierte Anbietername richtig ist und der Pfad des Hauptschlüssels Spalte Schlüsselpfad Format für den gegebenen Provider einhält. Es wird empfohlen, dass Sie die Schlüssel mithilfe von Tools wie SQL Server Management Studio konfigurieren, die die gültigen Anbieternamen und Schlüsselpfade automatisch generieren, wenn die Anweisung [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) ausgegeben wird.

- Sie müssen sicherstellen, dass die Anwendung den Schlüssel im Schlüsselspeicher zugreifen können. Dies u. Gewähren von Ihrer Anwendungszugriff auf den Schlüssel und/oder Schlüsselspeicher, je nach den Schlüsselspeicher oder andere Keystore-spezifische Konfigurationsschritte ausführen. Beispielsweise müssen ein Azure-Schlüsseltresor für den Zugriff auf die richtigen Anmeldeinformationen des Keystore.

### <a name="using-the-azure-key-vault-provider"></a>Mithilfe des Azure Key Vault-Anbieters

Azure Key Vault ist eine praktische Möglichkeit zum Speichern von Spaltenhauptschlüsseln für Always Encrypted (insbesondere, wenn Ihre Anwendungen in Azure gehostet werden). Der ODBC-Treiber für SQL Server on Linux, Mac OS und Windows umfasst eine integrierte Spalte Speicheranbieter für spaltenhauptschlüssel für Azure Key Vault. Finden Sie unter [Azure Key Vault - Schritt-für-Schritt](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/), [erste Schritte mit Schlüsseltresor](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), und [Erstellen von Spaltenhauptschlüsseln in Azure Key Vault](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2) für Weitere Informationen zum Konfigurieren eines Azure-Schlüssels Tresor für Always Encrypted.

Der Treiber unterstützt die Authentifizierung mit Azure Key Vault mithilfe der folgenden Typen von Clientanmeldeinformationen:

- Benutzername/Kennwort – sind mit dieser Methode die Anmeldeinformationen der Name des Azure Active Directory-Benutzer und das zugehörige Kennwort.

- Client-ID/geheim – mit dieser Methode sind die Anmeldeinformationen an, eine Client-ID und ein anwendungsgeheimnis.

Damit um den Treiber CMKs in AKV speichern gespeichert werden, für die spaltenverschlüsselung verwenden zu können, verwenden Sie die folgenden Schlüsselwörter für nur für die Verbindung Zeichenfolge:

|Anmeldeinformationen| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|Benutzername/Kennwort| `KeyVaultPassword`|Benutzerprinzipalname|Kennwort|
|Client-ID/geheimer Schlüssel| `KeyVaultClientSecret`|Client-ID|Geheime Schlüssel|

#### <a name="example-connection-strings"></a>Beispiele für Verbindungszeichenfolgen

Die folgenden Verbindungszeichenfolgen zeigen, wie Azure Key Vault mit den beiden Anmeldeinformationstypen zu authentifizieren:

**ClientID/Secret**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**Username/Password**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

Zum AKV CMK-Speicher verwenden, sind keine weiteren-ODBC-anwendungsänderungen erforderlich.

### <a name="using-the-windows-certificate-store-provider"></a>Mithilfe des Windows-Zertifikatspeicher-Anbieters

Der ODBC-Treiber für SQL Server unter Windows umfasst eine integrierte Spalte Speicheranbieter für spaltenhauptschlüssel für den Windows-Zertifikatspeicher, mit dem Namen `MSSQL_CERTIFICATE_STORE`. (Dieser Anbieter ist nicht auf MacOS oder Linux verfügbar.) Mit diesem Anbieter der CMK lokal auf dem Clientcomputer gespeichert und ist keine zusätzliche Konfiguration von der Anwendung für die Verwendung mit dem Treiber erforderlich. Allerdings muss die Anwendung auf das Zertifikat und seinen privaten Schlüssel im Speicher zugreifen. Finden Sie unter [Create and Store Spaltenhauptschlüsseln (Always Encrypted)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted) für Weitere Informationen.

### <a name="using-custom-keystore-providers"></a>Verwenden von benutzerdefinierten-Schlüsselspeicher-Anbieter

Der ODBC-Treiber für SQL Server unterstützt auch benutzerdefinierte Drittanbieter-Schlüsselspeicher-Anbieter, die über die CEKeystoreProvider-Schnittstelle. Dabei kann es sich um eine Anwendung zum Laden, Abfrage, und Konfigurieren von Schlüsselspeicher-Anbieter, sodass sie vom Treiber verwendet werden können, um Zugriff auf verschlüsselte Spalten. Anwendungen können auch direkt interagieren mit einem Schlüsselspeicheranbieter zum Verschlüsseln CEKs, in SQL Server zu speichern und Ausführen von Aufgaben über den Zugriff auf verschlüsselte Spalten mit ODBC; Weitere Informationen finden Sie unter [benutzerdefinierte-Schlüsselspeicher-Anbieter](../../connect/odbc/custom-keystore-providers.md).

Zwei Verbindungsattribute werden für die Interaktion mit benutzerdefinierten-Schlüsselspeicher-Anbieter verwendet. Die Überladungen sind:

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

Die erste wird verwendet, geladen und Auflisten von geladenen Schlüsselspeicher-Anbieter, während Letzteres Anwendung-Anbieter-Kommunikation ermöglicht. Diese Verbindungsattribute können verwendet werden, zu einem beliebigen Zeitpunkt vor oder nach dem Herstellen einer Verbindungs, da Anwendung-Anbieterinteraktion keine Kommunikation mit SQL Server beinhaltet. Jedoch, da der Treiber noch nicht geladen wurde, festlegen und Abrufen dieser Attribute vor dem Herstellen einer Verbindung werden vom Treiber-Manager verarbeitet werden, und nicht zu den erwarteten Ergebnissen führen.

#### <a name="loading-a-keystore-provider"></a>Laden einen Schlüsselspeicher-Anbieter

Festlegen der `SQL_COPT_SS_CEKEYSTOREPROVIDER` Verbindungsattribut ermöglicht es eine Clientanwendung beim Laden einer Anbieterbibliothek, die darin enthaltenen Schlüsselspeicher-Anbieter für die Verwendung zur Verfügung stellen.

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argument | Description |
|:---|:---|
|`ConnectionHandle`|[Eingabe] Verbindungshandle. Muss ein gültiger Verbindungshandle jedoch Anbieter, die über ein Verbindungshandle geladen sind von einer anderen im selben Prozess zugegriffen werden kann.|
|`Attribute`|[Eingabe] Attribut, das festgelegt: die `SQL_COPT_SS_CEKEYSTOREPROVIDER` konstant.|
|`ValuePtr`|[Eingabe] Ein Zeiger auf eine Null-terminierte Zeichenfolge, die den Dateinamen des der Anbieterbibliothek angibt. Für SQLSetConnectAttrA ist dies eine ANSI-Zeichenfolge (multibyte). Für SQLSetConnectAttrW ist dies eine Unicodezeichenfolge (Wchar_t).|
|`StringLength`|[Eingabe] Die Länge der Zeichenfolge ValuePtr oder SQL_NTS.|

Der Treiber versucht, beim Laden der Bibliothek, die durch den mit der Plattform-definierten dynamische Bibliothek laden Mechanismus ValuePtr-Parameter identifizierte (`dlopen()` auf Linux- und MacOS, `LoadLibrary()` unter Windows), und fügt dort zur Liste der definierten Anbietern Anbieter für den Treiber bezeichnet. Die folgenden Fehler können auftreten:

| Fehler | Description |
|:--|:--|
|`CE203`|Die dynamische Bibliothek konnte nicht geladen werden.|
|`CE203`|Das Symbol "CEKeyStoreProvider" exportiert wurde in der Bibliothek nicht gefunden.|
|`CE203`|Mindestens ein Anbieter in der Bibliothek sind bereits geladen.|

`SQLSetConnectAttr`Gibt die üblichen Fehler oder Erfolg Werte und zusätzlichen Informationen steht für alle Fehler, die über ODBC-Diagnose der Standardmechanismus auftraten.

> [!NOTE]
> Der Programmierer muss sicherstellen, dass alle benutzerdefinierten Anbieter geladen werden, bevor jede Abfrage, dass sie über eine Verbindung gesendet wird. Bei unterlassen ergibt sich der Fehler auf:

| Fehler | Description |
|:--|:--|
|`CE200`|Schlüsselspeicheranbieter %1 wurde nicht gefunden. Stellen Sie sicher, dass die entsprechenden Keystore Anbieterbibliothek geladen wurde.|

> [!NOTE]
> In einer Implementierung von Schlüsselspeicher-Anbieter sollten die Verwendung von `MSSQL` den Namen ihrer benutzerdefinierten Anbietern. Dieser Begriff wird ausschließlich für die Verwendung von Microsoft reserviert und möglicherweise Konflikte mit künftigen integrierte Anbieter. Mithilfe dieser Begriff im Namen eines benutzerdefinierten Anbieters, möglicherweise in einer ODBC-Warnung.

#### <a name="getting-the-list-of-loaded-providers"></a>Abrufen der Liste der Anbieter geladen

Erste dieses Verbindungsattribut ermöglicht es eine Clientanwendung, um zu bestimmen, die Schlüsselspeicher-Anbieter, die derzeit geladen, in der Treiber (einschließlich jenen erstellt.) Dies kann nur nach dem Herstellen einer Verbindung ausgeführt werden.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argument | Description |
|:---|:---|
|`ConnectionHandle`|[Eingabe] Verbindungshandle. Muss ein gültiger Verbindungshandle jedoch Anbieter, die über ein Verbindungshandle geladen sind von einer anderen im selben Prozess zugegriffen werden kann.|
|`Attribute`|[Eingabe] Abzurufenden Attributs: die `SQL_COPT_SS_CEKEYSTOREPROVIDER` konstant.|
|`ValuePtr`|[Ausgabe] Ein Zeiger auf Speicher in den Namen des nächsten geladenen Anbieter zurückgegeben werden soll.|
|`BufferLength`|[Eingabe] Die Länge des Puffers ValuePtr.|
|`StringLengthPtr`|[Ausgabe] Ein Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \*ValuePtr. Wenn ValuePtr ein null-Zeiger ist, wird keine Länge zurückgegeben. Wenn der Wert des Attributs ist eine Zeichenfolge, und die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als die Pufferlänge minus der Länge des der Null-Terminierung Zeichen, die Daten in \*ValuePtr auf die Pufferlänge abzüglich der Länge des abgeschnitten der NULL-Abschlusszeichen und wird vom Treiber Null-terminiert.|

Damit wird die gesamte Liste abrufen, alle Get-Vorgang gibt den Namen des Anbieters zurück, und wird zum nächsten Endpunkt einen interne Zähler erhöht. Sobald diese Zähler am Ende der Liste eine leere Zeichenfolge ist ("") zurückgegeben wird, und der Leistungsindikator wird zurückgesetzt; aufeinander folgende Get-Vorgängen fortzufahren vom Anfang der Liste klicken Sie dann erneut.

### <a name="communicating-with-keystore-providers"></a>Bei der Kommunikation mit dem Schlüsselspeicher-Anbieter

Die `SQL_COPT_SS_CEKEYSTOREDATA` Verbindungsattribut es einer Clientanwendung zur Kommunikation mit geladenen Schlüsselspeicher-Anbieter, für die Konfiguration zusätzlicher Parameter Erfassung Material usw. ermöglicht. Die Kommunikation zwischen einer Clientanwendung und eines Anbieters folgt eine einfache Anforderung / Antwort-Protokoll, basierend auf Get und Set fordert mithilfe dieses Verbindungsattribut. Kommunikation ist nur von der Clientanwendung initiiert.

> [!NOTE]
> Aufgrund der Natur der ODBC-ruft CEKeyStoreProvider Antworten (SQLGet/SetConnectAttr), die ODBC-Schnittstelle unterstützt nur das Festlegen von Daten in der Auflösung des den Verbindungskontext.

Die Anwendung kommuniziert mit Schlüsselspeicher-Anbieter über den Treiber über die CEKeystoreData-Struktur:

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| Argument | Description |
|:---|:---|
|`name`|[Eingabe] Bei festgelegt ist, den Namen des Anbieters an die die Daten gesendet werden. Nach Get ignoriert. NULL-terminierte, Breitzeichen-Zeichenfolge.|
|`dataSize`|[Eingabe] Die Größe des Datenarrays der Struktur.|
|`data`|[InOut] Nach der Menge der Daten an den Anbieter gesendet wird. Dies kann beliebige Daten sein. der Treiber unternimmt keinen Versuch zu interpretieren. Bei "Get" Lesen der Puffer zum Empfangen der Daten vom Anbieter aus.|

#### <a name="writing-data-to-a-provider"></a>Schreiben von Daten zu einem Anbieter

Ein `SQLSetConnectAttr` rufen mithilfe der `SQL_COPT_SS_CEKEYSTOREDATA` Attribut schreibt ein "Datenpaket" in der angegebenen Schlüsselspeicheranbieter.
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| Argument | Description |
|:---|:---|
|`ConnectionHandle`| [Eingabe] Verbindungshandle. Muss ein gültiger Verbindungshandle jedoch Anbieter, die über ein Verbindungshandle geladen sind von einer anderen im selben Prozess zugegriffen werden kann.|
|`Attribute`|[Eingabe] Attribut, das festgelegt: die `SQL_COPT_SS_CEKEYSTOREDATA` konstant.|
|`ValuePtr`|[Eingabe] Zeiger auf eine CEKeystoreData-Struktur. Das Namensfeld der Struktur identifiziert den Anbieter für den die Daten vorgesehen ist.|
|`StringLength`|[Eingabe] SQL_IS_POINTER-Konstante|

Zusätzliche detaillierte Fehlerinformationen abgerufen werden kann, über [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

> [!NOTE]
> Der Anbieter können das Verbindungshandle Sie die geschriebenen Daten zu einer bestimmten Verbindung zuordnen, wenn sie dies wünscht. Dies ist hilfreich bei der Implementierung von pro-Verbindungskonfiguration. Außerdem kann den Verbindungskontext ignorieren und behandeln Sie die Daten identisch, unabhängig von der die Verbindung zum Senden von Daten verwendet. Finden Sie unter [Zuordnung Kontext](../../connect/odbc/custom-keystore-providers.md#context-association) für Weitere Informationen.

#### <a name="reading-data-from-a-provider"></a>Lesen von Daten von einem Anbieter

Ein Aufruf von `SQLGetConnectAttr` mithilfe der `SQL_COPT_SS_CEKEYSTOREDATA` Attribut liest ein "Datenpaket" aus *der letzten-geschrieben-to* Anbieter. Wenn es keine ", wurde" tritt ein Sequenzfehler-Funktion. Implementierer von Schlüsselspeicher-Anbieter werden empfohlen, "Dummy schreibt" von 0 Byte als eine Möglichkeit, ohne dass andere Nebeneffekte Anbieter für Lesevorgänge auswählen, wenn dies sinnvoll zu unterstützen.

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| Argument | Description |
|:---|:---|
|`ConnectionHandle`|[Eingabe] Verbindungshandle. Muss ein gültiger Verbindungshandle jedoch Anbieter, die über ein Verbindungshandle geladen sind von einer anderen im selben Prozess zugegriffen werden kann.|
|`Attribute`|[Eingabe] Abzurufenden Attributs: die `SQL_COPT_SS_CEKEYSTOREDATA` konstant.|
|`ValuePtr`|[Ausgabe] Ein Zeiger auf eine CEKeystoreData-Struktur, die in der die Daten lesen, die vom Anbieter platziert werden.|
|`BufferLength`|[Eingabe] SQL_IS_POINTER-Konstante|
|`StringLengthPtr`|[Ausgabe] Ein Zeiger auf einen Puffer, in die Pufferlänge zurückgegeben werden sollen. Wenn * ValuePtr ein null-Zeiger ist, keine Länge zurückgegeben.|

Der Aufrufer muss sicherstellen, dass der Anbieter zum Schreiben in ein Puffer lang genug, befolgen die Struktur CEKEYSTOREDATA zugeordnet werden. Nach der Rückgabe wird der DataSize-Feld mit der tatsächlichen Länge der Daten, die vom Anbieter gelesen aktualisiert. Zusätzliche detaillierte Fehlerinformationen abgerufen werden kann, über [SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx).

Diese Schnittstelle stellt keine zusätzlichen Anforderungen an, auf das Format der Daten zwischen einer Anwendung und einen Schlüsselspeicheranbieter übertragen. Jeder Anbieter kann eigene Protocol/Datenformat, abhängig von der Anforderungen definieren.

Ein Beispiel für einen eigenen Schlüsselspeicheranbieter implementieren, finden Sie unter [benutzerdefinierte-Schlüsselspeicher-Anbieter](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>Einschränkungen des ODBC-Treibers bei Verwendung von Always Encrypted

### <a name="asynchronous-operations"></a>Asynchrone Vorgänge
Während der ODBC-Treiber die Verwendung von ermöglichen [asynchrone Vorgänge](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md) mit Always Encrypted, besteht eine Leistungseinbuße auf den Betrieb Wenn Always Encrypted aktiviert ist. Der Aufruf von `sys.sp_describe_parameter_encryption` verschlüsselungsmetadaten zu bestimmen, für die Anweisung blockiert wird, und dazu, den Treiber für den Server dass führt zurückzugebenden Metadaten vor der Rückgabe warten `SQL_STILL_EXECUTING`.

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>Abrufen von Daten in Teilen mit SQLGetData
Bevor verschlüsselt 17 von ODBC-Treiber für SQL Server können Zeichen und binärer Spalten in Teilen mit SQLGetData abgerufen werden. Nur ein Aufruf von SQLGetData kann vorgenommen werden, mit einem Puffer, der ausreichend lang ist, um die gesamte Spalte Daten enthalten.

### <a name="send-data-in-parts-with-sqlputdata"></a>Senden von Daten mit SQLPutData Teilen
Daten einfügen oder Vergleich können nicht in Teilen mit SQLPutData gesendet werden. Nur ein Aufruf von SQLPutData kann vorgenommen werden, mit einem Puffer, die gesamten Daten enthält. Verwenden Sie zum Einfügen von long-Daten in verschlüsselten Spalten ein, API für das Massenkopieren, mit einer Eingabe-Datendatei im nächsten Abschnitt beschrieben.

### <a name="encrypted-money-and-smallmoney"></a>Verschlüsselte Money und smallmoney
Verschlüsselt **Money** oder **Smallmoney** von Parametern keine Spalten angewendet werden, da es ist keine bestimmte ODBC-Datentyp die Zuordnungen für diese Typen, wodurch Fehler Operand Typ in Konflikt stehen.

## <a name="bulk-copy-of-encrypted-columns"></a>Massenkopieren von verschlüsselten Spalten

Verwenden der [SQL-Massenkopieren Funktionen](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md) und **Bcp** -Hilfsprogramm wird seit 17 der ODBC-Treiber für SQL Server mit Always Encrypted unterstützt. Nur-Text (auf verschlüsselte und entschlüsselte auf) und Chiffretext (wörtlich übertragen) eingefügt werden kann und das Massenkopieren (Bcp_ *) APIs mit abgerufen und die **Bcp** Hilfsprogramm.

- Chiffretext varbinary(max) Format (z. B. für den Massenimport in eine andere Datenbank laden) abgerufen werden, zu verbinden, ohne die `ColumnEncryption` Option (oder legen sie den `Disabled`) und führen Sie einen BCP OUT-Vorgang.

- Zum Einfügen und Abrufen von nur-Text und den Treiber transparent Durchführen von Verschlüsselung und Entschlüsselung als Einstellung für erforderlich ist, können `ColumnEncryption` zu `Enabled` ist ausreichend. Die Funktionalität der BCP-API ist andernfalls nicht geändert.

- Einfügen von verschlüsseltem Text transformiert varbinary(max) Format (z. B. wie oben abgerufen), legen Sie die `BCPMODIFYENCRYPTED` auf "true" aus, und führen Sie einen Vorgang BCP IN. Sicherstellen Sie in der Reihenfolge für die resultierenden Daten zu entschlüsselnden, dass das Ziel Spaltenwerts CEK identisch, von dem der verschlüsselte Text ursprünglich erhalten wurde.

Bei Verwendung der **Bcp** Hilfsprogramm: Steuern der `ColumnEncryption` festlegen, verwenden Sie die Option ' -D ', und geben Sie einen DSN, der den gewünschten Wert enthält. Zum Einfügen von verschlüsseltem Text transformiert, stellen Sie sicher der `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` Einstellung des Benutzers ist aktiviert.

Die folgende Tabelle enthält eine Zusammenfassung der Aktionen, fungierte auf eine verschlüsselte Spalte:

|`ColumnEncryption`|BCP-Richtung|Description|
|----------------|-------------|-----------|
|`Disabled`|OUT (zum Client)|Ruft die Chiffretext ab. Ist der beobachtete Datentyp **varbinary(max)**.|
|`Enabled`|OUT (zum Client)|Ruft nur-Text ab. Der Treiber wird die Spaltendaten zu entschlüsseln.|
|`Disabled`|IN (auf Server)|Fügt ein verschlüsseltem Text transformiert. Dies dient zum Verschieben von verschlüsselten Daten deckend ohne es entschlüsselt werden. Der Vorgang schlägt fehl, wenn die `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` Option für den Benutzer nicht festgelegt ist, oder BCPMODIFYENCRYPTED nicht auf dem Verbindungshandle festgelegt ist. Weitere Informationen finden Sie unten.|
|`Enabled`|IN (auf Server)|Fügt ein nur-Text. Der Treiber verschlüsselt die Daten der Spalte.|

### <a name="the-bcpmodifyencrypted-option"></a>Die BCPMODIFYENCRYPTED-option

Wiederherstellungpunkte mit beschädigten Daten der Server normalerweise lässt keine verschlüsselten Text direkt in eine verschlüsselte Spalte eingefügt, und daher dazu ist nicht möglich; allerdings zum Massenladen von verschlüsselten Daten, die mithilfe der BCP-API, Festlegen der `BCPMODIFYENCRYPTED` [Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) Option auf "true" Chiffretext direkt eingefügt werden können und reduziert das Risiko der Beschädigung von verschlüsselter Daten über die Einstellung der `ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` Option für das Benutzerkonto. Dennoch eine überaus die Schlüssel müssen die Daten übereinstimmen, und es ist eine gute Idee, wenn einige schreibgeschützte überprüft der eingefügten Daten nach der Einfügemarke Bulk und vor der weiteren Verwendung.

Finden Sie unter [migrieren geschützten sensiblen Daten durch Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md) für Weitere Informationen.

## <a name="always-encrypted-api-summary"></a>Always Encrypted-API-Zusammenfassung

### <a name="connection-string-keywords"></a>Schlüsselwörter für Verbindungszeichenfolgen

|Name|Description|  
|----------|-----------------|  
|`ColumnEncryption`|Gültige Werte sind `Enabled` / `Disabled`.<br>`Enabled`--Always Encrypted-Funktionen für die Verbindung ermöglichen.<br>`Disabled`– Deaktivieren von Always Encrypted-Funktionalität für die Verbindung. <br><br>Der Standardwert ist `Disabled`.|  
|`KeyStoreAuthentication` | Gültige Werte: `KeyVaultPassword`,`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | Wenn `KeyStoreAuthentication`  =  `KeyVaultPassword`, legen Sie diesen Wert in einen gültigen Azure Active Directory-Benutzerprinzipalnamen-Namen. <br>Wenn `KeyStoreAuthetication`  =  `KeyVaultClientSecret` legen Sie diesen Wert auf einen gültigen Azure Active Directory Anwendungsclient-ID |
|`KeyStoreSecret` | Wenn `KeyStoreAuthentication`  =  `KeyVaultPassword` legen Sie diesen Wert auf das Kennwort für den entsprechenden Benutzernamen ein. <br>Wenn `KeyStoreAuthentication`  =  `KeyVaultClientSecret` legen Sie diesen Wert auf das Anwendungsgeheimnis an einem gültigen Azure Active Directory Anwendungsclient-ID zugeordnet|

### <a name="connection-attributes"></a>Verbindungsattribute

|Name|Typ|Description|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|Vor dem Verbinden|`SQL_COLUMN_ENCRYPTION_DISABLE`(0) – deaktivieren, die Always Encrypted <br>`SQL_COLUMN_ENCRYPTION_ENABLE`(1) – aktivieren Sie Always Encrypted|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|Nach Herstellen der Verbindung|[Set] Fehler beim Laden der CEKeystoreProvider<br>[Get] Gibt den Namen einer CEKeystoreProvider zurück|
|`SQL_COPT_SS_CEKEYSTOREDATA`|Nach Herstellen der Verbindung|[Set] Schreiben von Daten in CEKeystoreProvider<br>[Get] Lesen von Daten aus CEKeystoreProvider|

### <a name="statement-attributes"></a>Anweisungsattribute

|Name|Description|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED`(0) – always Encrypted ist deaktiviert, für die Anweisung <br>`SQL_CE_RESULTSETONLY`(1) – nur Entschlüsselung. Entschlüsselt von Resultsets und Rückgabewerte und Parameter werden nicht verschlüsselt. <br>`SQL_CE_ENABLED`(3) – always Encrypted aktiviert ist und für Parameter und die Ergebnisse|

### <a name="descriptor-fields"></a>Deskriptorfelder

|IPD-Feld|Größe/Type|Standardwert|Description|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD (2 Bytes)|0|Wenn 0 (Standard): Entscheidung zum Verschlüsseln dieser Parameter richtet sich nach der Verfügbarkeit von verschlüsselungsmetadaten.<br><br>Wenn ungleich NULL ist: Wenn verschlüsselungsmetadaten für diesen Parameter verfügbar ist, wird sie verschlüsselt. Andernfalls die Anforderung schlägt fehl, Fehlercode: [CE300] [Microsoft] [ODBC Driver 13 for SQL Server], obligatorische Verschlüsselung wurde für einen Parameter angegeben, aber keine verschlüsselungsmetadaten wurde vom Server bereitgestellt.|

### <a name="bcpcontrol-options"></a>Bcp_control-Optionen

|Optionsname|Standardwert|Description|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|Bei "true", können varbinary(max) Werte in eine verschlüsselte Spalte eingefügt werden soll. Bei "false", verhindert die Einfügung, wenn richtigen Typ und Verschlüsselung Metadaten angegeben wird.|

## <a name="see-also"></a>Siehe auch

- [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted-Blog](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

