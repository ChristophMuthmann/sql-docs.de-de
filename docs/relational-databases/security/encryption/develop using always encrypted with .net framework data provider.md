---
title: "Entwickeln von Anwendungen unter Verwendung von Always Encrypted mit dem .NET Framework-Datenanbieter f&#252;r SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-security"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 827e509e-3c4f-4820-aa37-cebf0f7bbf80
caps.latest.revision: 11
author: "stevestein"
ms.author: "sstein"
manager: "jhubbard"
---
# Entwickeln von Anwendungen unter Verwendung von Always Encrypted mit dem .NET Framework-Datenanbieter f&#252;r SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Dieser Artikel enthält Informationen zum Entwickeln von .NET-Anwendungen mithilfe von [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) und dem [.NET Framework-Datenanbieter für SQL Server](https://msdn.microsoft.com/library/kb9s9ks0(v=vs.110).aspx).

Always Encrypted ermöglicht Clientanwendungen das Verschlüsseln von vertraulichen Daten in einer Weise, dass weder die Daten noch die Verschlüsselungsschlüssel zu irgendeinem Zeitpunkt gegenüber SQL Server oder Azure SQL-Datenbank offengelegt werden. Ein Treiber, bei dem „Always Encrypted“ aktiviert ist, z. B. der .NET Framework-Datenanbieter für SQL Server, erreicht dies durch die transparente Ver- und Entschlüsselung von sensiblen Daten in der Clientanwendung. Der Treiber ermittelt automatisch, welche Abfrageparameter vertraulichen Datenbankspalten (mit Always Encrypted geschützt) entsprechen. Die Werte dieser Parameter werden dann vor der Übergabe an SQL Server oder Azure SQL-Datenbank verschlüsselt. Auf ähnliche Weise entschlüsselt der Treiber die Daten transparent, die von verschlüsselten Datenbankspalten in Abfrageergebnissen empfangen werden. Weitere Informationen finden Sie unter [Always Encrypted (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).


## Voraussetzungen

- Konfigurieren Sie Always Encrypted in Ihrer Datenbank. Dies umfasst die Bereitstellung von Always Encrypted-Schlüsseln und die Einrichtung der Verschlüsselung für ausgewählte Datenbankspalten. Wenn Sie nicht bereits über eine Datenbank verfügen, für die Always Encrypted konfiguriert ist, befolgen Sie die Anweisungen in [Erste Schritte mit Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_5).
- Stellen Sie sicher, dass .NET Framework, Version 4.6 oder höher, auf dem Entwicklungscomputer installiert ist. Weitere Informationen finden Sie unter [.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2(v=vs.110).aspx). Sie müssen auch sicherstellen, dass .NET Framework, Version 4.6 oder höher, als .NET Framework-Zielversion in der Entwicklungsumgebung konfiguriert ist. Wenn Sie Visual Studio verwenden, finden Sie weitere Informationen unter [Gewusst wie: Ausrichten auf eine .NET Framework-Version](https://msdn.microsoft.com/library/bb398202.aspx). 

> [!NOTE]
> Der Grad der Unterstützung für Always Encrypted in bestimmten Versionen von .NET Framework variiert. Weitere Informationen finden Sie unten im Referenzabschnitt zur Always Encrypted-API. 

## Aktivieren von Always Encrypted für Anwendungsabfragen
Die einfachste Möglichkeit zum Aktivieren der Verschlüsselung von Parametern und der Entschlüsselung von Abfrageergebnissen, die auf verschlüsselte Spalten ausgerichtet sind, besteht im Festlegen des Werts für das Kennwort der Verbindungszeichenfolge der Spaltenverschlüsselungseinstellung auf **Aktiviert**.

Im Folgenden finden Sie ein Beispiel für eine Verbindungszeichenfolge, die „Always Encrypted“ aktiviert:
```
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
SqlConnection connection = new SqlConnection(connectionString);
```

Und im Folgenden finden Sie auch ein gleichwertiges Beispiel, das die SqlConnectionStringBuilder.ColumnEncryptionSetting-Eigenschaft verwendet.

```
SqlConnectionStringBuilder strbldr = new SqlConnectionStringBuilder();
strbldr.DataSource = "server63";
strbldr.InitialCatalog = "Clinic";
strbldr.IntegratedSecurity = true;
strbldr.ColumnEncryptionSetting = SqlConnectionColumnEncryptionSetting.Enabled;
SqlConnection connection = new SqlConnection(strbldr.ConnectionString);
```

Always Encrypted kann auch für einzelne Abfragen aktiviert werden. Weitere Informationen finden Sie unten in **Kontrollieren der Auswirkungen von Always Encrypted auf die Leistung**.
Beachten Sie, dass die Aktivierung von Always Encrypted für eine erfolgreiche Verschlüsselung und Entschlüsselung nicht ausreichend ist. Sie müssen auch Folgendes sicherstellen:
- Die Anwendung verfügt über die Datenbankberechtigungen *VIEW ANY COLUMN MASTER KEY DEFINITION* und *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*, die für den Zugriff auf die Metadaten in der Datenbank über Always Encrypted-Schlüssel erforderlich sind. Weitere Informationen finden Sie unter [Abschnitt „Berechtigungen“ in Always Encrypted (Datenbankmodul)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7).
- Die Anwendung kann auf den Hauptschlüssel der Spalte zugreifen, der die Spaltenverschlüsselungsschlüssel schützt, mit denen die abgefragten Datenbankspalten verschlüsselt werden.

## Abrufen und Ändern von Daten in verschlüsselten Spalten

Nachdem Sie Always Encrypted für Anwendungsabfragen aktiviert haben, können Sie mithilfe der standardmäßigen ADO.NET-APIs (siehe [Abrufen und Ändern von Daten in ADO.NET](https://msdn.microsoft.com/library/ms254937(v=vs.110).aspx)) oder der APIs für [.NET Framework-Datenanbieter für SQL Server](https://msdn.microsoft.com/library/kb9s9ks0(v=vs.110).aspx), die im [System.Data.SqlClient-Namespace](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) definiert sind, die Daten in verschlüsselten Datenbankspalten abrufen oder ändern. Vorausgesetzt, dass Ihre Anwendung über die erforderlichen Datenbankberechtigungen verfügt und auf den Hauptschlüssel für die Spalte zugreifen kann, verschlüsselt der .NET Framework-Datenanbieter für SQL Server alle Abfrageparameter, die auf verschlüsselte Spalten ausgerichtet sind, und entschlüsselt die Daten, die von verschlüsselten Spalten abgerufen wurden, die Klartextwerte von .NET-Typen zurückgeben, die den SQL Server-Datentypen entsprechen, die für die Spalten im Datenbankschema festgelegt wurden.
Wenn Always Encrypted nicht aktiviert ist, tritt bei Abfragen mit Parametern, die auf verschlüsselte Spalten ausgerichtet sind, ein Fehler auf. Abfragen können weiterhin Daten aus verschlüsselten Spalten abrufen, solange die Abfrage keine Parameter für verschlüsselte Spalten enthält. Die .NET Framework-Datenanbieter für SQL Server versuchen jedoch nicht, die aus verschlüsselten Spalten abgerufenen Werte zu entschlüsseln, daher erhält die Anwendung binär verschlüsselte Daten (als Bytearrays).

Die folgende Tabelle fasst das Verhalten von Abfragen in Abhängigkeit davon zusammen, ob Always Encrypted aktiviert ist:

|Abfragemerkmal | Always Encrypted ist aktiviert und die Anwendung kann auf die Schlüssel und Schlüsselmetadaten zugreifen.|Always Encrypted ist aktiviert und die Anwendung kann nicht auf die Schlüssel oder Schlüsselmetadaten zugreifen. | Always Encrypted ist deaktiviert|
|:---|:---|:---|:---|
| Abfragen mit Parametern, die auf verschlüsselte Spalten ausgerichtet sind. | Parameterwerte werden transparent verschlüsselt. | Fehler | Fehler|
| Abfragen, die Daten von verschlüsselten Spalten ohne Parameter abrufen, die auf verschlüsselte Spalten ausgerichtet sind.| Ergebnisse von verschlüsselten Spalten werden transparent entschlüsselt. Die Anwendung erhält Klartextwerte der .NET-Datentypen, die den SQL Server-Datentypen entsprechen, die für die verschlüsselten Spalten konfiguriert wurden. | Fehler | Ergebnisse von verschlüsselten Spalten werden nicht entschlüsselt. Die Anwendung erhält verschlüsselte Werte als Bytearrays (byte[]). 

Die folgenden Beispiele veranschaulichen das Abrufen und Ändern von Daten in verschlüsselten Spalten. Die Beispiele gehen von der Zieltabelle mit folgendem Schema aus. Beachten Sie, dass die Spalten „SSN“ und „BirthDate“ verschlüsselt werden.


```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1), 
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

### Beispiel zum Einfügen von Daten

In diesem Beispiel wird eine Zeile in die Tabelle „Patients“ eingefügt. Beachten Sie Folgendes:
- Es erfolgt keine spezielle Verschlüsselung im Beispielcode. Der .NET Framework-Datenanbieter für SQL Server erkennt und verschlüsselt die Parameter *paramSSN* und *paramBirthdate* automatisch, die auf verschlüsselte Spalten ausgerichtet sind. Dadurch wird die Verschlüsselung für die Anwendung transparent. 
- Die in die Datenbankspalten eingefügten Werte, einschließlich der verschlüsselten Spalten, werden als [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)-Objekte übergeben. Während die Verwendung von **SqlParameter** optional ist, wenn Werte an nicht verschlüsselte Spalten gesendet werden (obwohl es dringend empfohlen wird, da es dabei hilft, eine SQL-Einschleusung zu verhindern), ist sie für Werte erforderlich, die auf verschlüsselte Spalten ausgerichtet sind. Wenn die in die Spalten „SSN“ oder „BirthDate“ eingefügten Werte als Literale übergeben werden, die in die Abfrageanweisung eingebettet sind, würde bei der Abfrage ein Fehler auftreten, da der .NET Framework-Datenanbieter für SQL Server die Werte in den verschlüsselten Zielspalten nicht ermittelt könnte, daher würde er die Werte nicht verschlüsseln. Daher würde der Server sie zurückweisen, da sie mit den verschlüsselten Spalten inkompatibel sind.
- Der auf die Spalte „SSN“ ausgerichtete Datentyp des Parameters wird auf eine ANSI-Zeichenfolge (Nicht-Unicode) festgelegt, der dem SQL Server-Datentyp „char/varchar“ zuordnet wird. Wenn der Typ des Parameters eine Unicode-Zeichenfolge (String) ist, die „nchar/nvarchar“ zugeordnet wird, würde bei der Abfrage ein Fehler auftreten, da Always Encrypted keine Konvertierungen von verschlüsselten „nchar/nvarchar“-Werten in verschlüsselte „char/narchar“-Werte unterstützt. Weitere Informationen zu den Datentypzuordnungen finden Sie unter [SQL Server-Datentypzuordnungen](https://msdn.microsoft.com/library/cc716729.aspx).
- Der Datentyp des in die Spalte „BirthDate“ eingefügten Parameters wird mithilfe der [SqlParameter.SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx)-Eigenschaft explizit auf den SQL Server-Datentyp festgelegt, anstatt auf die implizite Zuordnung von .NET-Typen zu vertrauen, die bei der Verwendung der [SqlParameter.DbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.dbtype.aspx)-Eigenschaft angewendet werden. Standardmäßig wird [DateTime Structure](https://msdn.microsoft.com/library/system.datetime.aspx) dem SQL Server-Datentyp „datetime“ zugeordnet. Da der Datentyp der Spalte „BirthDate“ dem Wert „date“ entspricht und Always Encrypted keine Konvertierung von verschlüsselten „datetime“-Werten in verschlüsselte „date“-Werte unterstützt, würde die Verwendung der Standardzuordnung zu einem Fehler führen. 

```
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
using (SqlConnection connection = new SqlConnection(strbldr.ConnectionString))
{
   using (SqlCommand cmd = connection.CreateCommand())
   {
      cmd.CommandText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

      SqlParameter paramSSN = cmd.CreateParameter();
      paramSSN.ParameterName = @"@SSN";
      paramSSN.DbType = DbType.AnsiStringFixedLength;
      paramSSN.Direction = ParameterDirection.Input;
      paramSSN.Value = "795-73-9838";
      paramSSN.Size = 11;
      cmd.Parameters.Add(paramSSN);

      SqlParameter paramFirstName = cmd.CreateParameter();
      paramFirstName.ParameterName = @"@FirstName";
      paramFirstName.DbType = DbType.String;
      paramFirstName.Direction = ParameterDirection.Input;
      paramFirstName.Value = "Catherine";
      paramFirstName.Size = 50;
      cmd.Parameters.Add(paramFirstName);

      SqlParameter paramLastName = cmd.CreateParameter();
      paramLastName.ParameterName = @"@LastName";
      paramLastName.DbType = DbType.String;
      paramLastName.Direction = ParameterDirection.Input;
      paramLastName.Value = "Abel";
      paramLastName.Size = 50;
      cmd.Parameters.Add(paramLastName);

      SqlParameter paramBirthdate = cmd.CreateParameter();
      paramBirthdate.ParameterName = @"@BirthDate";
      paramBirthdate.SqlDbType = SqlDbType.Date;
      paramBirthdate.Direction = ParameterDirection.Input;
      paramBirthdate.Value = new DateTime(1996, 09, 10);
      cmd.Parameters.Add(paramBirthdate);

      cmd.ExecuteNonQuery();
   } 
}
```

### Beispiel zum Abrufen von Klartextdaten

Im folgenden Beispiel wird das Filtern von Daten auf Basis verschlüsselter Werte und das Abrufen von Klartextdaten aus verschlüsselten Spalten veranschaulicht. Beachten Sie Folgendes:
- Der in der WHERE-Klausel zum Filtern der Spalte „SSN“ verwendete Wert muss mithilfe von „SqlParameter“ übergeben werden, damit ihn der .NET Framework-Datenanbieter für SQL Server vor dem Senden an die Datenbank transparent verschlüsseln kann.
- Alle Werte werden vom Programm als Klartext ausgegeben, da der .NET Framework-Datenanbieter für SQL Server die aus den Spalten „SSN“ und „BirthDate“ abgerufenen Daten transparent entschlüsselt.


> [!NOTE]
> Abfragen können auf Spalten Übereinstimmungsvergleiche ausführen, wenn sie mittels deterministischer Verschlüsselung verschlüsselt sind. Weitere Informationen finden Sie im Abschnitt *Auswählen der deterministischen oder zufälligen Verschlüsselung* des Themas [Always Encrypted (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).

```
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
    
using (SqlConnection connection = new SqlConnection(strbldr.ConnectionString))
 {
    using (SqlCommand cmd = connection.CreateCommand())
 {

 cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN=@SSN";
 SqlParameter paramSSN = cmd.CreateParameter();
 paramSSN.ParameterName = @"@SSN";
 paramSSN.DbType = DbType.AnsiStringFixedLength;
 paramSSN.Direction = ParameterDirection.Input;
 paramSSN.Value = "795-73-9838";
 paramSSN.Size = 11;
 cmd.Parameters.Add(paramSSN);
 using (SqlDataReader reader = cmd.ExecuteReader())
 {
   if (reader.HasRows)
 {
 while (reader.Read())
 {
    Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
 }
```

### Beispiel zum Abrufen von verschlüsselten Daten

Wenn Always Encrypted nicht aktiviert ist, können Abfragen weiterhin Daten aus verschlüsselten Spalten abrufen, so lange die Abfrage keine Parameter für verschlüsselte Spalten enthält.

Im folgenden Beispiel wird das Abrufen von binär verschlüsselten Daten aus verschlüsselten Spalten veranschaulicht. Beachten Sie Folgendes:

- Da Always Encrypted in der Verbindungszeichenfolge nicht aktiviert ist, gibt die Abfrage verschlüsselte Werte von „SSN“ und „BirthDate“ als Bytearrays zurück (das Programm konvertiert die Werte in Zeichenfolgen).
- Eine Abfrage, die Daten aus verschlüsselten Spalten mit deaktiviertem Always Encrypted abruft, kann Parameter aufweisen, so lange keiner der Parameter auf eine verschlüsselte Spalte ausgerichtet ist. Die obige Abfrage filtert nach der Spalte „LastName“, die in der Datenbank nicht verschlüsselt ist. Wenn die Abfrage nach „SSN“ oder „BirthDate“ filtert, würde ein Fehler auftreten.


```
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
                
using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   using (SqlCommand cmd = connection.CreateCommand())
   {
      cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName";
      SqlParameter paramLastName = cmd.CreateParameter();
      paramLastName.ParameterName = @"@LastName";
      paramLastName.DbType = DbType.String;
      paramLastName.Direction = ParameterDirection.Input;
      paramLastName.Value = "Abel";
      paramLastName.Size = 50;
      cmd.Parameters.Add(paramLastName);
      using (SqlDataReader reader = cmd.ExecuteReader())
      {
         if (reader.HasRows)
         {
            while (reader.Read())
         {
         Console.WriteLine(@"{0}, {1}, {2}, {3}", BitConverter.ToString((byte[])reader[0]), reader[1], reader[2], BitConverter.ToString((byte[])reader[3]));
      }
   }
}
```

### Vermeiden allgemeiner Probleme beim Abfragen von verschlüsselten Spalten

Dieser Abschnitt beschreibt die allgemeinen Kategorien von Fehlern bei der Abfrage verschlüsselter Spalten über .NET-Anwendungen sowie einige Grundsätze zum Vermeiden dieser Fehler.

### Konvertierungsfehler durch nicht unterstützte Datentypen

Always Encrypted unterstützt einige Konvertierungen für verschlüsselte Datentypen. Eine ausführliche Liste der unterstützten Typkonvertierungen finden Sie unter [Always Encrypted (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md). Gehen Sie wie folgt vor, um Fehler bei Konvertierung des Datentyps zu vermeiden:

- Legen Sie die Typen der auf die verschlüsselten Spalten ausgerichteten Parameter so fest, dass der SQL Server-Datentyp des Parameters genau dem Typ der Zielspalte entspricht, oder dass eine Konvertierung des SQL Server-Datentyps des Parameters in den Zieltyp der Spalte unterstützt wird. Sie können die gewünschte Zuordnung von .NET-Datentypen zu bestimmten SQL Server-Datentypen mithilfe der „SqlParameter.SqlDbType“-Eigenschaft erzwingen.
- Überprüfen Sie, ob die Genauigkeit und Dezimalstellenanzahl von Parametern, die auf Spalten der SQL Server-Datentypen „decimal“ und „numeric“ ausgerichtet sind, mit der für die Zielspalte konfigurierten Genauigkeit und Dezimalstellenanzahl identisch sind.  
- Überprüfen Sie, ob die Genauigkeit von Parametern, die auf Spalten der SQL Server-Datentypen „datetime2“, „datetimeoffset“ oder „time“ ausgerichtet sind, in Abfragen, in denen Werte der Zielspalte geändert werden, nicht größer als die Genauigkeit für die Zielspalte ist.  

### Fehler aufgrund der Übergabe von Klartext anstelle von verschlüsselten Werten

Jeder Wert, der auf eine verschlüsselte Spalte ausgerichtet ist, muss in der Anwendung verschlüsselt werden. Ein Versuch, einen Klartextwert einzufügen bzw. zu ändern oder nach einem Klartextwert für eine verschlüsselte Spalte zu filtern, führt zu einem Fehler wie dem Folgenden:


```
System.Data.SqlClient.SqlException (0x80131904): Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', column_encryption_key_database_name = 'Clinic') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Stellen Sie Folgendes sicher, um solche Fehler zu vermeiden:
- Always Encrypted ist für Anwendungsabfragen aktiviert, die auf verschlüsselte Spalten ausgerichtet sind (für die Verbindungszeichenfolge oder im [SqlCommand](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)-Objekt für eine bestimmte Abfrage).
- Sie verwenden „SqlParameter“ zum Senden von Daten, die auf verschlüsselte Spalten ausgerichtet sind. Das folgende Beispiel zeigt eine Abfrage, die falsch nach einem Literal bzw. einer Konstante einer verschlüsselten Spalte (SSN) filtert (anstatt das Literal innerhalb eines „SqlParameter“-Objekts zu übergeben). 


```
using (SqlCommand cmd = connection.CreateCommand())
{
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
cmd.ExecuteNonQuery();
}
```

## Arbeiten mit Spaltenhauptschlüsselspeichern

Der .NET Framework-Datenanbieter für SQL Server muss zum Verschlüsseln eines Parameterwerts oder zum Entschlüsseln von Daten in Abfrageergebnissen einen Spaltenverschlüsselungsschlüssel erhalten, der für die Zielspalte konfiguriert ist. Spaltenverschlüsselungsschlüssel werden in der verschlüsselten Form in den Datenbankmetadaten gespeichert. Jeder Spaltenverschlüsselungsschlüssel weist einen entsprechenden Spaltenhauptschlüssel auf, mit dem der Spaltenverschlüsselungsschlüssel verschlüsselt wurde. Die Spaltenhauptschlüssel werden nicht von den Datenbankmetadaten gespeichert. Sie enthalten lediglich die Informationen zu einem Schlüsselspeicher, der einen bestimmten Spaltenhauptschlüssel und die Position des Schlüssels im Schlüsselspeicher enthält.

Um einen Klartextwert eines Spaltenverschlüsselungsschlüssels zu erhalten, ruft der .NET Framework-Datenanbieter für SQL Server zunächst die Metadaten zum Spaltenverschlüsselungsschlüssel und seinen entsprechenden Spaltenhauptschlüssel ab. Dann verwendet er die Informationen in den Metadaten, um den Schlüsselspeicher zu kontaktieren, der den Spaltenhauptschlüssel enthält, und um den verschlüsselten Spaltenverschlüsselungsschlüssel zu entschlüsseln. Der .NET Framework-Datenanbieter für SQL Server kommuniziert mit einem Schlüsselspeicher, wobei ein Spaltenhauptschlüssel-Speicheranbieter verwendet wird, der eine Instanz einer Klasse darstellt, die von der Klasse [SqlColumnEncryptionKeyStoreProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptionkeystoreprovider.aspx) abgeleitet wird.


Vorgang zum Abrufen eines Spaltenverschlüsselungsschlüssels:

1.  Wenn Always Encrypted für eine Abfrage aktiviert ist, ruft der .NET Framework-Datenanbieter für SQL Server transparent **sys.sp_describe_parameter_encryption** auf, um Verschlüsselungsmetadaten für Parameter abzurufen, die verschlüsselte Spalten zum Ziel haben, falls die Abfrage Parameter aufweist. Für verschlüsselte Daten, die in den Ergebnissen einer Abfrage enthalten sind, fügt SQL Server automatisch Verschlüsselungsmetadaten an. Die Informationen über den Spaltenhauptschlüssel umfassen:
    - Den Namen eines Schlüsselspeicheranbieters, in dem ein Schlüsselspeicher verkapselt ist, der den Spaltenhauptschlüssel enthält. 
    - Den Schlüsselpfad, der den Speicherort des Spaltenhauptschlüssels im Schlüsselspeicher angibt.
    
    Die Informationen über den Spaltenverschlüsselungsschlüssel umfassen:

    - Den verschlüsselten Wert eines Spaltenverschlüsselungsschlüssels.
    - Der Name des Algorithmus, der verwendet wurde, um den CEK zu verschlüsseln.
2.  Der .NET Framework-Datenanbieter für SQL Server verwendet den Namen des Spaltenhauptschlüssel-Speicheranbieters, um das Anbieterobjekt (eine Instanz einer von der SqlColumnEncryptionKeyStoreProvider-Klasse abgeleiteten Klasse) in einer internen Datenstruktur nachzuschlagen.
3.  Um den Spaltenverschlüsselungsschlüssel zu entschlüsseln, ruft der.NET Framework-Datenanbieter für SQL Server die Methode SqlColumnEncryptionKeyStoreProvider.DecryptColumnEncryptionKey auf und übergibt den Spaltenhauptschlüsselpfad, den verschlüsselten Wert des Spaltenverschlüsselungsschlüssels und den Namen des Verschlüsselungsalgorithmus, der zum Erstellen des verschlüsselten Spaltenverschlüsselungsschlüssels verwendet wurde.




### Verwenden integrierter Spaltenhauptschlüssel-Speicheranbieter

Der .NET Framework-Datenanbieter für SQL Server enthält die folgenden integrierten Spaltenhauptschlüssel-Speicheranbieter, die mit den bestimmten Anbieternamen vorab registriert wurden (um den Anbieter zu suchen).


| Klasse | Beschreibung | Anbietername (Suche) |
|:---|:---|:---|
|SqlColumnEncryptionCertificateStoreProvider-Klasse| Ein Anbieter für den Windows-Zertifikatspeicher. | MSSQL_CERTIFICATE_STORE |
|[SqlColumnEncryptionCngProvider-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx) <br><br>**Hinweis:** Dieser Anbieter ist in .NET Framework 4.6.1 und höheren Versionen verfügbar. |Ein Anbieter für einen Schlüsselspeicher, der die [Microsoft Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/aa376210.aspx) unterstützt. Üblicherweise handelt es sich bei einem solchen Speicher um ein Hardwaresicherheitsmodul – ein physisches Gerät, das digitale Schlüssel schützt und verwaltet und die kryptografische Verarbeitung bereitstellt.  | MSSQL_CNG_STORE|
| [SqlColumnEncryptionCspProvider-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncspprovider.aspx)<br><br>**Hinweis:** Dieser Anbieter ist in .NET Framework 4.6.1 oder höheren Versionen verfügbar.| Ein Anbieter für einen Schlüsselspeicher, der die [Microsoft Cryptography API (CAPI)](https://msdn.microsoft.com/library/aa266944.aspx) unterstützt. Üblicherweise handelt es sich bei einem solchen Speicher um ein Hardwaresicherheitsmodul – ein physisches Gerät, das digitale Schlüssel schützt und verwaltet und die kryptografische Verarbeitung bereitstellt.| MSSQL_CSP_PROVIDER |
  
Sie müssen keine Änderungen am Anwendungscode vornehmen, um diese Anbieter zu verwenden, aber beachten Sie Folgendes:

- Sie (oder der Datenbankadministrator) müssen sicherstellen, dass der in den Metadaten des Spaltenhauptschlüssels konfigurierte Anbietername richtig ist und der Pfad des Spaltenhauptschlüssels dem Schlüsselpfadformat entspricht, das für einen angegebenen Anbieter gültig ist. Es wird empfohlen, dass Sie die Schlüssel mithilfe von Tools wie SQL Server Management Studio konfigurieren, die die gültigen Anbieternamen und Schlüsselpfade automatisch generieren, wenn die Anweisung [CREATE COLUMN MASTER KEY (Transact-SQL)](https://msdn.microsoft.com/library/mt146393.aspx) ausgegeben wird. Weitere Informationen finden Sie unter [Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md) und [Konfigurieren von Always Encrypted mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).
- Sie müssen sicherstellen, dass die Anwendung auf den Schlüssel im Schlüsselspeicher zugreifen kann. Dies kann das Gewähren des Zugriffs auf den Schlüssel und/oder Schlüsselspeicher für die Anwendung (abhängig vom Schlüsselspeicher) oder das Ausführen anderer wichtiger speicherspezifischer Konfigurationsschritte einbeziehen. Für den Zugriff auf einen Schlüsselspeicher, der eine CNG oder CAPI implementiert (z. B. ein Hardwaresicherheitsmodul), müssen Sie sicherstellen, dass eine Bibliothek auf dem Anwendungscomputer installiert ist, die eine CNG oder CAPI für den Speicher implementiert. Weitere Informationen finden Sie unter [Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

### Verwenden des Azure Key Vault-Anbieters

Azure Key Vault ist eine praktische Möglichkeit zum Speichern von Spaltenhauptschlüsseln für Always Encrypted (insbesondere, wenn Ihre Anwendungen in Azure gehostet werden). Der .NET Framework-Datenanbieter für SQL Server umfasst keinen integrierten Spaltenhauptschlüssel-Speicheranbieter für Azure Key Vault, aber er steht als NuGet-Paket bereit, das Sie problemlos in Ihre Anwendung integrieren können. Weitere Informationen finden Sie unter [Always Encrypted – Schützen vertraulicher Daten in SQL-Datenbank mit Datenverschlüsselung und Speichern von Verschlüsselungsschlüsseln in Azure Key Vault](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/).

### Implementieren eines benutzerdefinierten Speicheranbieters für den Spaltenhauptschlüssel

Wenn Sie Spaltenhauptschlüssel in einem Schlüsselspeicher speichern möchten, der nicht von einem vorhandenen Anbieter unterstützt wird, können Sie einen benutzerdefinierten Anbieter implementieren, indem Sie die [SqlColumnEncryptionCngProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx)-Klasse erweitern und den Anbieter mithilfe der [SqlConnection.RegisterColumnEncryptionKeyStoreProviders](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders.aspx)-Methode registrieren.


```
public class MyCustomKeyStoreProvider : SqlColumnEncryptionKeyStoreProvider
    {
        public override byte[] EncryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] columnEncryptionKey)
        {
            // Logic for encrypting a column encrypted key.
        }
        public override byte[] DecryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] EncryptedColumnEncryptionKey)
        {
            // Logic for decrypting a column encrypted key.
        }
    }  
    class Program
    {
        static void Main(string[] args)
        {
            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
               new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();
            providers.Add("MY_CUSTOM_STORE", customProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
            providers.Add(SqlColumnEncryptionCertificateStoreProvider.ProviderName, customProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers); 
       // ...
        }

    }
```
 
### Verwenden von Spaltenhauptschlüssel-Speicheranbietern für die programmgesteuerte Schlüsselbereitstellung

Beim Zugriff auf verschlüsselte Spalten sucht der .NET Framework-Datenanbieter für SQL Server den richtigen Speicheranbieter für Spaltenhauptschlüssel transparent und ruft ihn anschließend auf, um die Spaltenverschlüsselungsschlüssel zu entschlüsseln. In der Regel ruft der normale Anwendungscode die Speicheranbieter für Spaltenhauptschlüssel nicht direkt auf. Sie können einen Anbieter jedoch explizit instanziieren und aufrufen, um Always Encrypted-Schlüssel programmgesteuert bereitzustellen und zu verwalten: Zum Generieren eines verschlüsselten Spaltenverschlüsselungsschlüssels und Entschlüsseln eines Spaltenverschlüsselungsschlüssels (z. B. im Rahmen einer Spaltenhauptschlüsselrotation) Weitere Informationen finden Sie unter [Übersicht über die Schlüsselverwaltung für Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).
Beachten Sie, dass die Implementierung eigener Schlüsselverwaltungstools möglicherweise nur erforderlich ist, wenn Sie einen benutzerdefinierten Schlüsselspeicheranbieter verwenden. Bei der Verwendung von Schlüsseln, die in Schlüsselspeichern (für die integrierte Anbieter vorhanden sind) und/oder in Azure Key Vault gespeichert werden, können Sie vorhandene Tools wie SQL Server Management Studio oder PowerShell verwenden, um Schlüssel zu verwalten und bereitzustellen.
Im folgenden Beispiel wird das Generieren eines Spaltenverschlüsselungsschlüssels und das Verwenden der [SqlColumnEncryptionCertificateStoreProvider](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider.aspx)-Klasse zum Verschlüsseln des Schlüssels mit einem Zertifikat veranschaulicht.


```
using System.Security.Cryptography;
static void Main(string[] args)
{
    byte[] EncryptedColumnEncryptionKey = GetEncryptedColumnEncryptonKey(); 
    Console.WriteLine("0x" + BitConverter.ToString(EncryptedColumnEncryptionKey).Replace("-", "")); 
    Console.ReadKey();
}

static byte[]  GetEncryptedColumnEncryptonKey()
{
    int cekLength = 32;
    String certificateStoreLocation = "CurrentUser";
    String certificateThumbprint = "698C7F8E21B2158E9AED4978ADB147CF66574180";
    // Generate the plaintext column encryption key.
    byte[] columnEncryptionKey = new byte[cekLength];
    RNGCryptoServiceProvider rngCsp = new RNGCryptoServiceProvider();
    rngCsp.GetBytes(columnEncryptionKey);

    // Encrypt the column encryption key with a certificate.
    string keyPath = String.Format(@"{0}/My/{1}", certificateStoreLocation, certificateThumbprint);
    SqlColumnEncryptionCertificateStoreProvider provider = new SqlColumnEncryptionCertificateStoreProvider();
    return provider.EncryptColumnEncryptionKey(keyPath, @"RSA_OAEP", columnEncryptionKey); 
}
```


## Kontrollieren der Auswirkungen von Always Encrypted auf die Leistung

Da Always Encrypted eine clientseitige Verschlüsselungstechnologie ist, werden die meisten Leistungseinbußen auf der Clientseite und nicht in der Datenbank beobachtet. Neben den Kosten für Verschlüsselungs- und Entschlüsselungsvorgänge ergeben sich die folgenden anderen Quellen für Leistungseinbußen auf der Clientseite:
- Zusätzliche Roundtrips zur Datenbank zum Abrufen von Metadaten für Abfrageparameter.
- Aufrufe an einen Spaltenhauptschlüsselspeicher für den Zugriff auf einen Spaltenhauptschlüssel.

In diesem Abschnitt werden die integrierten Leistungsoptimierungen im .NET Framework-Anbieter für SQL Server und die Steuerung der Auswirkung der beiden oben genannten Faktoren auf die Leistung beschrieben.

### Kontrollieren von Roundtrips zum Abrufen von Metadaten für Abfrageparameter

Wenn Always Encrypted für eine Verbindung aktiviert ist, ruft der .NET Framework-Datenanbieter für SQL Server standardmäßig [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx) für jede parametrisierte Abfrage auf, wobei die Abfrageanweisung (ohne Parameterwerte) an SQL Server übergeben wird. Die Abfrageanweisung wird von **sys.sp_describe_parameter_encryption** analysiert, um zu ermitteln, ob Parameter verschlüsselt werden müssen. In diesem Fall gibt sie die verschlüsselungsbezogenen Informationen zurück, die dem .NET Framework-Datenanbieter für SQL Server das Verschlüsseln von Parameterwerten ermöglichen. Das oben beschriebene Verhalten stellt einen hohen Grad an Transparenz für die Clientanwendung sicher. Die Anwendung (und der Anwendungsentwickler) muss nicht beachten, welche Abfragen Zugriff auf verschlüsselte Spalten haben, so lange die auf verschlüsselte Spalten ausgerichteten Werte in „SqlParameter“-Objekten an den .NET Framework-Datenanbieter für SQL Server übergeben werden.


### Zwischenspeichern von Abfragemetadaten

In .NET Framework 4.6.2 und höher speichert der .NET Framework-Datenanbieter für SQL Server die Ergebnisse von **sys.sp_describe_parameter_encryption** für jede Abfrageanweisung zwischen. Wenn die gleiche Abfrageanweisung mehrfach ausgeführt wird, ruft der Treiber daher **sys.sp_describe_parameter_encryption** nur einmal auf. Die Zwischenspeicherung von Verschlüsselungsmetadaten für Abfrageanweisungen verringert die Leistungskosten beim Abrufen von Metadaten bei der Datenbank erheblich. Die Zwischenspeicherung ist standardmäßig aktiviert. Sie können die Zwischenspeicherung von Parametermetadaten deaktivieren, indem Sie die [SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled.aspx)-Eigenschaft auf FALSCH festlegen, das wird jedoch mit Ausnahme sehr seltener Fälle, wie dem unten beschriebenen, nicht empfohlen:

Betrachten Sie eine Datenbank mit zwei verschiedenen Schemas: s1 und s2. Jedes Schema enthält eine Tabelle mit dem gleichen Namen: t. Die Definitionen der Tabellen s1.t und s2.t sind identisch, mit Ausnahme ihrer verschlüsselungsbezogenen Eigenschaften: Eine Spalte mit dem Namen c ist in s1.t nicht verschlüsselt, wohl aber in s2.t. Die Datenbank weist zwei Benutzer auf, u1 und u2. Das Standardschema für u1-Benutzer ist s1. Das Standardschema für u2 ist s2. Eine .NET-Anwendung öffnet zwei Verbindungen mit der Datenbank, mit der Identität des u1-Benutzers in der einen Verbindung und der des u2-Benutzers in der anderen Verbindung. Die Anwendung sendet eine Abfrage mit einem Parameter, der auf die Spalte c gerichtet ist, über die Verbindung für Benutzer u1 (das Schema wird von der Abfrage nicht angegeben, sodass vom Standardbenutzerschema ausgegangen wird). Anschließend sendet die Anwendung die gleiche Abfrage über die Verbindung für den u2-Benutzer. Wenn die Zwischenspeicherung von Metadaten aktiviert ist, ist der Cache nach der ersten Abfrage mit Metadaten aufgefüllt, die angeben, dass die Spalte c, auf die die Abfrageparameter verweisen, nicht verschlüsselt ist. Da die zweite Abfrage die gleiche Abfrageanweisung aufweist, werden die im Cache gespeicherten Informationen verwendet. Daher sendet der Treiber die Abfrage, ohne den Parameter zu verschlüsseln (was falsch ist, da die Zielspalte s2.t.c verschlüsselt ist), und legt so den Klartextwert des Parameters dem Server gegenüber offen. Der Server wird diese Inkompatibilität erkennen und den Treiber anweisen, den Cache zu aktualisieren, sodass die Anwendung die Abfrage transparent mit ordnungsgemäß verschlüsseltem Parameterwert erneut sendet. In einem solchen Fall sollte die Zwischenspeicherung deaktiviert werden, um die Offenlegung vertraulicher Werte gegenüber dem Server zu verhindern. 




### Festlegen von Always Encrypted auf Abfrageebene

Sie können Always Encrypted für einzelne Abfragen aktivieren, anstatt es für die Verbindung einzurichten, um beim Abrufen von Verschlüsselungsmetadaten für parametrisierte Abfragen die Auswirkung auf die Leistung zu steuern. Auf diese Weise können Sie sicherstellen, dass **sys.sp_describe_parameter_encryption** nur für Abfragen aufgerufen wird, bei denen Ihnen bekannt ist, dass sie über Parameter verfügen, die auf verschlüsselte Spalten ausgerichtet sind. Beachten Sie jedoch, dass Sie auf diese Weise die Transparenz der Verschlüsselung reduzieren: Wenn Sie die Verschlüsselungseigenschaften der Datenbankspalten ändern, müssen Sie möglicherweise den Code der Anwendung ändern, um ihn mit den Schemaänderungen auszurichten.

> [!NOTE]
> Das Festlegen von Always Encrypted auf der Abfrageebene führt in .NET 4.6.2 und späteren Versionen, in denen die Zwischenspeicherung von Metadaten für die Parameterverschlüsselung implementiert ist, zu leichten Leistungsvorteilen.

Sie müssen diesen Konstruktor von  [SqlCommand](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx) und [SqlCommandColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommandcolumnencryptionsetting.aspx) verwenden, um das Verhalten von Always Encrypted für einzelne Abfragen zu steuern. Hier sind einige nützliche Richtlinien:
- Für die meisten Abfragen greift eine Clientanwendung über eine Datenbankverbindung auf verschlüsselte Spalten zu:
    - Legen Sie für das Verbindungszeichenfolgen-Kennwort für **Spaltenverschlüsselungseinstellung** den Wert *Aktiviert* fest.
    - Legen Sie **SqlCommandColumnEncryptionSetting.Disabled** für einzelne Abfragen fest, die nicht auf verschlüsselte Spalten zugreifen müssen. Dadurch werden sowohl der Aufruf von „sys.sp_describe_parameter_encryption“ als auch der Versuch deaktiviert, Werte im Resultset zu entschlüsseln.
    - Legen Sie **SqlCommandColumnEncryptionSetting.ResultSet** für einzelne Abfragen fest, die keine Parameter besitzen, für die eine Verschlüsselung erforderlich ist, die aber Daten aus verschlüsselten Spalten abrufen. Dadurch werden der Aufruf von „sys.sp_describe_parameter_encryption“ und die Parameterverschlüsselung deaktiviert. Die Abfrage ist in der Lage, die Ergebnisse von Spaltenverschlüsselungen zu entschlüsseln.
- Für die meisten Abfragen greift eine Clientanwendung nicht über eine Datenbankverbindung auf verschlüsselte Spalten zu:
    - Legen Sie für das Verbindungszeichenfolgen-Kennwort für **Spaltenverschlüsselungseinstellung** den Wert **Deaktiviert** fest.
    - Legen Sie **SqlCommandColumnEncryptionSetting.Enabled** für einzelne Abfragen mit Parametern fest, die verschlüsselt werden müssen. Dadurch werden sowohl der Aufruf von „sys.sp_describe_parameter_encryption“ als auch die Entschlüsselung von Abfrageergebnissen aktiviert, die aus verschlüsselten Spalten abgerufen werden.
    - Legen Sie **SqlCommandColumnEncryptionSetting.ResultSet** für Abfragen fest, die keine Parameter besitzen, für die eine Verschlüsselung erforderlich ist, aber die Daten aus verschlüsselten Spalten abrufen. Dadurch werden der Aufruf von „sys.sp_describe_parameter_encryption“ und die Parameterverschlüsselung deaktiviert. Die Abfrage ist in der Lage, die Ergebnisse von Spaltenverschlüsselungen zu entschlüsseln.

In dem folgenden Beispiel ist Always Encrypted für die Datenbankverbindung deaktiviert. Die von der Anwendung ausgestellte Abfrage weist einen Parameter auf, der auf die nicht verschlüsselte Spalte „LastName“ ausgerichtet ist. Die Abfrage ruft Daten aus den Spalten „SSN“ und „BirthDate“ ab, die beide verschlüsselt sind. In diesem Fall ist der Aufruf von „sys.sp_describe_parameter_encryption“ nicht erforderlich, um Verschlüsselungsmetadaten abzurufen. Die Entschlüsselung der Abfrageergebnisse muss jedoch aktiviert sein, damit die Anwendung Klartextwerte aus den beiden verschlüsselten Spalten erhalten kann. Um dies sicherzustellen, wird die Einstellung „SqlCommandColumnEncryptionSetting.ResultSet-Einstellung“ verwendet.



```
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
using (SqlConnection connection = new SqlConnection(connectionString))
{
    connection.Open();
    using (SqlCommand cmd = new SqlCommand(@"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName",
connection, null, SqlCommandColumnEncryptionSetting.ResultSetOnly))
    {
        SqlParameter paramLastName = cmd.CreateParameter();
        paramLastName.ParameterName = @"@LastName";
        paramLastName.DbType = DbType.String;
        paramLastName.Direction = ParameterDirection.Input;
        paramLastName.Value = "Abel";
        paramLastName.Size = 50;
        cmd.Parameters.Add(paramLastName);
        using (SqlDataReader reader = cmd.ExecuteReader())
            {
               if (reader.HasRows)
               {
                  while (reader.Read())
                  {
                     Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
                  }
               }
            }
  } 
}
```


### Zwischenspeicherung von Spaltenverschlüsselungsschlüsseln

Der .NET Framework-Datenanbieter für SQL Server speichert die Spaltenverschlüsselungsschlüssel im Klartext im Speicher zwischen, um die Anzahl der Aufrufe an einen Spaltenhauptschlüsselspeicher zu verringern. Nach dem Erhalt des Verschlüsselungsschlüsselwerts für die verschlüsselte Spalte von den Datenbankmetadaten versucht der Treiber zunächst, den Spaltenverschlüsselungsschlüssel im Klartext zu finden, der dem verschlüsselten Schlüsselwert entspricht. Der Treiber ruft den Schlüsselspeicher, der den Spaltenhauptschlüssel enthält, nur dann auf, wenn er den verschlüsselten Spaltenverschlüsselungsschlüssel im Cache nicht finden kann.

> [!NOTE]
> In .NET Framework 4.6 und 4.6.1 werden die Einträge für den Spaltenverschlüsselungsschlüssel niemals aus dem Cache entfernt. Dies bedeutet, dass der Treiber den Schlüsselspeicher für einen gegebenen verschlüsselten Spaltenverschlüsselungsschlüssel während der Lebensdauer der Anwendung nur einmal kontaktiert.

In .NET Framework 4.6.2 und höher werden die Cacheeinträge nach einer konfigurierbaren Gültigkeitsdauer aus Sicherheitsgründen zwangsweise entfernt. Der Standardwert für die Gültigkeitsdauer beträgt 2 Stunden. Wenn Sie strengere Anforderungen an die Dauer der Speicherung von unverschlüsselten Spaltenverschlüsselungsschlüsseln in der Anwendung haben, können Sie den Wert mithilfe der Eigenschaft [SqlConnection.ColumnEncryptionKeyCacheTtl](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionkeycachettl.aspx) ändern. 


## Aktivieren von zusätzlichem Schutz für einen gefährdeten SQL Server

Standardmäßig verlässt sich der *.NET Framework-Datenanbieter für SQL Server* beim Bereitstellen von Metadaten über die in der Datenbank zu verschlüsselnden Spalten und die Art der Verschlüsselung auf das Datenbanksystem (SQL Server oder Azure SQL Database). Die Verschlüsselungsmetadaten ermöglichen dem .NET Framework-Datenanbieter für SQL Server das Verschlüsseln von Abfrageparametern und das Entschlüsseln von Abfrageergebnissen ohne irgendwelche Eingaben von der Anwendung, wodurch sich das Ausmaß der in der Anwendung erforderlichen Änderungen erheblich reduziert. Wenn der SQL Server-Prozess jedoch gefährdet ist und ein Angreifer die Metadaten manipuliert, die von SQL Server an den .NET Framework-Datenanbieter für SQL Server gesendet werden, kann der Angreifer unter Umständen imstande sein, vertrauliche Informationen zu stehlen. In diesem Abschnitt werden APIs beschrieben, die das Bereitstellen einer zusätzlichen Schutzebene gegen diese Art von Angriff unterstützen, um den Preis geringerer Transparenz. 

### Erzwingen von Parameterverschlüsselung 

Bevor der .NET Framework-Datenanbieter für SQL Server eine parametrisierte Abfrage an SQL Server sendet, bittet er SQL Server (durch Aufrufen von [sys.sp_describe_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)), die Abfrageanweisung zu analysieren und Informationen über die in der Abfrage zu verschlüsselnden Parameter bereitzustellen. Eine gefährdete SQL Server-Instanz könnte den .NET Framework-Datenanbieter für SQL Server in die Irre führen, indem er Metadaten sendet, dass ein Parameter auf eine nicht verschlüsselte Spalte gerichtet ist, obwohl die Spalte in der Datenbank verschlüsselt ist. Der .NET Framework-Datenanbieter für SQL Server würde den Parameterwert daher nicht verschlüsseln und ihn im Klartext an die gefährdete SQL Server-Instanz senden.

Um einen derartigen Angriff zu verhindern, kann eine Anwendung die [SqlParameter.ForceColumnEncryption](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.forcecolumnencryption.aspx)-Eigenschaft für den Parameter auf WAHR festlegen. Dadurch löst der .NET Framework-Datenanbieter für SQL Server eine Ausnahme aus, wenn die Metadaten, die er vom Server empfangen hat, angeben, dass der Parameter nicht verschlüsselt werden muss.

Beachten Sie, dass die Eigenschaft **SqlParameter.ForceColumnEncryption** zwar beim Verbessern der Sicherheit hilft, jedoch zugleich die Transparenz der Verschlüsselung für die Clientanwendung verringert. Wenn Sie das Datenbankschema aktualisieren, um die Menge der verschlüsselten Spalten zu ändern, müssen Sie möglicherweise auch an der Anwendung Änderungen vornehmen.

Das folgende Codebeispiel zeigt die Verwendung der **SqlParameter.ForceColumnEncryption**. 



```
SqlCommand cmd = _sqlconn.CreateCommand(); 

// Use parameterized queries to access Always Encrypted data. 
 
cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = @SSN;"; 

SqlParameter paramSSN = cmd.CreateParameter(); 
paramSSN.ParameterName = @"@SSN"; 
paramSSN.DbType = DbType.AnsiStringFixedLength; 
paramSSN.Direction = ParameterDirection.Input; 
paramSSN.Value = ssn; 
paramSSN.Size = 11; 
paramSSN.ForceColumnEncryption = true; 
cmd.Parameters.Add(paramSSN); 

SqlDataReader reader = cmd.ExecuteReader();
```
 

### Konfigurieren von vertrauenswürdigen Spaltenhauptschlüsselpfaden 

Die Verschlüsselungsmetadaten, die SQL Server für Abfrageparameter mit verschlüsselten Spalten als Ziel und für die aus verschlüsselten Spalten abgerufenen Ergebnisse zurückgibt, beinhalten den Schlüsselpfad des Spaltenhauptschlüssels, der den Schlüsselspeicher und den Speicherort des Schlüssels im Schlüsselspeicher angibt. Wenn die SQL Server-Instanz gefährdet ist, könnte sie den Schlüsselpfad, der den .NET Framework-Datenanbieter für SQL Server anweist, an den von einem Angreifer kontrollierten Speicherort senden. Dies kann zur Offenlegung der Anmeldeinformationen des Schlüsselspeichers führen, falls der Schlüsselspeicher die Authentifizierung der Anwendung vorschreibt. 

Um solche Angriffe zu verhindern, kann die Anwendung die Liste der vertrauenswürdigen Schlüsselpfade für einen bestimmten Server mithilfe der Eigenschaft [SqlConnection.ColumnEncryptionTrustedMasterKeyPaths](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths.aspx) festlegen. Wenn der .NET Framework-Datenanbieter für SQL Server einen Schlüsselpfad empfängt, der nicht in der Liste der vertrauenswürdigen Schlüsselpfade aufgeführt ist, löst er eine Ausnahme aus. 

Beachten Sie, dass sich durch das Festlegen vertrauenswürdiger Schlüsselpfade zwar die Sicherheit Ihrer Anwendung verbessert, Sie jedoch am Code und/oder der Konfiguration der Anwendung bei jeder turnusmäßigen Änderung des Spaltenhauptschlüssels Änderungen vornehmen müssen (bei jedem Wechsel des Spaltenhauptschlüsselpfads). 

Das folgende Beispiel zeigt die Konfiguration von vertrauenswürdigen Spaltenhauptschlüsselpfaden:


```
// Configure trusted key paths to protect against fake key paths sent by a compromised SQL Server instance 
// First, create a list of trusted key paths for your server 
List<string> trustedKeyPathList = new List<string>(); 
trustedKeyPathList.Add("CurrentUser/my/425CFBB9DDDD081BB0061534CE6AB06CB5283F5Ea"); 

// Register the trusted key path list for your server 

SqlConnection.ColumnEncryptionTrustedMasterKeyPaths.Add(serverName, trustedKeyPathList);
```
 



## Kopieren von verschlüsselten Daten mithilfe von „SqlBulkCopy“

Mit „SqlBulkCopy“ können Sie Daten, die bereits verschlüsselt sind und in einer Tabelle gespeichert werden, in eine andere Tabelle kopieren, ohne die Daten zu entschlüsseln. Gehen Sie dazu wie folgt vor:

- Stellen Sie sicher, dass die Verschlüsselungskonfiguration der Zieltabelle mit der Konfiguration der Quelltabelle identisch ist. Insbesondere müssen für beide Tabellen dieselben Spalten verschlüsselt sein. Zudem müssen die Spalten mithilfe derselben Verschlüsselungstypen und mit denselben Verschlüsselungsschlüsseln verschlüsselt werden. Hinweis: Wenn eine der Zielspalten anders als die entsprechende Quellspalte verschlüsselt wurde, können Sie die Daten in der Zieltabelle nach dem Kopiervorgang nicht entschlüsseln. Die Daten werden beschädigt.
- Konfigurieren Sie beide Datenbankverbindungen, zur Quelltabelle und zur Zieltabelle, ohne Always Encrypted zu aktivieren. 
- Legen Sie die Option „AllowEncryptedValueModifications“ fest (siehe [SqlBulkCopyOptions](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopyoptions.aspx)). Hinweis: Gehen Sie bei der Angabe von „AllowEncryptedValueModifications“ mit Bedacht vor, da dies zur Beschädigung der Datenbank führen kann, da der .NET Framework-Datenanbieter für SQL Server nicht überprüft, ob die Daten tatsächlich verschlüsselt oder mit demselben Verschlüsselungstyp, Algorithmus und Schlüssel wie die Zielspalte ordnungsgemäß verschlüsselt wurden.

Beachten Sie, dass die Option „AllowEncryptedValueModifications“ in .NET Framework 4.6.1 und höheren Versionen verfügbar ist.

Hier folgt ein Beispiel, in dem Daten aus einer Tabelle in eine andere kopiert werden. Es wird angenommen, dass die Spalten „SSN“ und „BirthDate“ verschlüsselt sind.
        

```
static public void CopyTablesUsingBulk(string sourceTable, string targetTable)
{
   string sourceConnectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
   string targetConnectionString = "Data Source= server64; Initial Catalog=Clinic; Integrated Security=true";
   using (SqlConnection connSource = new SqlConnection(sourceConnectionString))
   {
      connSource.Open();
      using (SqlCommand cmd = new SqlCommand(string.Format("SELECT [PatientID], [SSN], [FirstName], [LastName], [BirthDate] FROM {0}", sourceTable), connSource))
      {
         using (SqlDataReader reader = cmd.ExecuteReader())
         {
            SqlBulkCopy copy = new SqlBulkCopy(targetConnectionString, SqlBulkCopyOptions.KeepIdentity | SqlBulkCopyOptions.AllowEncryptedValueModifications);
            copy.EnableStreaming = true;
            copy.DestinationTableName = targetTable;
            copy.WriteToServer(reader);
         }
      }
}
```


## Always Encrypted – API-Referenz

**Namespace:** [System.Data.SqlClient](https://msdn.microsoft.com/library/system.data.sqlclient.aspx)

**Assembly:** System.Data (in System.Data.dll)




|Name|Beschreibung|In .NET Version eingeführt
|:---|:---|:---
|[SqlColumnEncryptionCertificateStoreProvider-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider.aspx)|Ein Schlüsselspeicheranbieter für den Windows-Zertifikatspeicher.|  4.6
|[SqlColumnEncryptionCngProvider-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncngprovider.aspx)|Eine Schlüsselspeicheranbieter für Microsoft Cryptography API: Next Generation (CNG).|  4.6.1
|[SqlColumnEncryptionCspProvider-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptioncspprovider.aspx)|Eine Schlüsselspeicheranbieter für die auf der Microsoft CAPI basierenden Kryptografiedienstanbieter.|4.6.1  
|[SqlColumnEncryptionKeyStoreProvider-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcolumnencryptionkeystoreprovider.aspx)|Die Basisklasse der Schlüsselspeicheranbieter.|  4.6
|[SqlCommandColumnEncryptionSetting-Enumeration](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommandcolumnencryptionsetting.aspx)|Einstellungen zum Aktivieren der Verschlüsselung und Entschlüsselung für eine Datenbankverbindung.|4.6  
|[SqlConnectionColumnEncryptionSetting-Enumeration](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx)|Einstellungen zum Steuern des Verhaltens von „Always Encrypted“ für einzelne Abfragen.|4.6  
| [SqlConnectionStringBuilder.ColumnEncryptionSetting-Eigenschaft](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx)|Ruft Always Encrypted in der Verbindungszeichenfolge ab und legt es fest.|4.6|
| [SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled-Eigenschaft](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled.aspx) | Aktiviert und deaktiviert das Zwischenspeichern von Verschlüsselungsabfrage-Metadaten. | 4.6.2
| [SqlConnection.ColumnEncryptionKeyCacheTtl-Eigenschaft](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptionkeycachettl.aspx) | Ruft die Gültigkeitsdauer für Einträge im Cache für den Spaltenverschlüsselungsschlüssel ab und legt diese fest. | 4.6.2
|[SqlConnection.ColumnEncryptionTrustedMasterKeyPaths-Eigenschaft](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths.aspx)|Ermöglicht Ihnen, eine Liste von vertrauenswürdigen Schlüsselpfaden für einen Datenbankserver festzulegen. Wenn der Treiber während der Verarbeitung eine Anwendungsabfrage einen Schlüsselpfad erhält, der nicht in der Liste enthalten ist, schlägt die Abfrage fehl. Diese Eigenschaft bietet zusätzlichen Schutz vor Angriffen, bei denen ein kompromittierter SQL Server gefälschte Schlüsselpfade bereitstellt, was zu Verlusten von Schlüsselspeicher-Anmeldeinformationen führen kann.|  4.6
|[SqlConnection.RegisterColumnEncryptionKeyStoreProviders-Methode](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders.aspx)|Ermöglicht Ihnen, benutzerdefinierte Schlüsselspeicheranbieter zu registrieren. Dies ist ein Wörterbuch, das Anbieternamen von Schlüsselspeichern Implementierungen von Schlüsselspeicheranbietern zuordnet.|  4.6
|[SqlCommand-Konstruktor (String, SqlConnection, SqlTransaction, SqlCommandColumnEncryptionSetting)](https://msdn.microsoft.com/library/dn956511\(v=vs.110\).aspx)|Ermöglicht das Steuern des Verhaltens von „Always Encrypted“ für einzelne Abfragen.|  4.6
|[SqlParameter.ForceColumnEncryption-Eigenschaft](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.forcecolumnencryption.aspx)|Erzwingt die Verschlüsselung eines Parameters. Wenn SQL Server den Treiber informiert, dass der Parameter nicht verschlüsselt werden muss, tritt bei der Abfrage, die diesen Parameter verwendet, ein Fehler auf. Diese Eigenschaft bietet zusätzlichen Schutz vor Angriffen, bei denen ein kompromittierter SQL Server falsche Verschlüsselungsmetadaten für den Client bereitstellt, was zur Offenlegung von Daten führen kann.|4.6  
|Neues [Verbindungszeichenfolgen](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)-Schlüsselwort: `Column Encryption Setting=enabled`|Aktiviert oder deaktiviert die „Always Encrypted“-Funktionalität für die Verbindung.| 4.6 
  

## Siehe auch

- [„Immer verschlüsselt“ (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted-Blog](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)
- [Tutorial zur SQL-Datenbank: Schützen vertraulicher Daten mit Always Encrypted](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)
















