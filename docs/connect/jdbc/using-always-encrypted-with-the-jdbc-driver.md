---
title: Using Always Encrypted mit dem JDBC-Treiber | Microsoft Docs
ms.custom: 
ms.date: 12/30/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: fffb61c4c3dfa58edaf684f103046d1029895e7c
ms.openlocfilehash: cee7f5dbcf66a5357ae68192703d841ae1601a35
ms.contentlocale: de-de
ms.lasthandoff: 10/19/2017

---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>Verwenden von „Immer verschlüsselt“ mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Dieser Artikel enthält Informationen zum Entwickeln von Java-Anwendungen mit [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7) und Microsoft JDBC Driver 6.0 (oder höher) für SQL Server.

Immer kann verschlüsselte Clients zum Verschlüsseln von sensiblen Daten und niemals weiterzugeben, die Daten oder die Verschlüsselungsschlüssel in SQL Server oder Azure SQL-Datenbank. Ein Always Encrypted-Treiber, wie z. B. Microsoft JDBC Driver 6.0 (oder höher) für SQL Server aktiviert ist, erreicht dies durch die transparente Ver- und Entschlüsselung von sensiblen Daten in der Clientanwendung. Der Treiber ermittelt automatisch, welche Abfrage Parameter vertraulichen Datenbankspalten (mit Always Encrypted geschützt) entsprechen, und die Werte dieser Parameter vor der Übergabe der Werte in SQL Server oder Azure SQL-Datenbank verschlüsselt. Auf ähnliche Weise entschlüsselt der Treiber die Daten transparent, die von verschlüsselten Datenbankspalten in Abfrageergebnissen empfangen werden. Weitere Informationen finden Sie auf [Always Encrypted (Datenbankmodul)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7) und [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  


## <a name="prerequisites"></a>Erforderliche Komponenten

- Konfigurieren Sie Always Encrypted in Ihrer Datenbank. Dies umfasst die Bereitstellung von Always Encrypted-Schlüsseln und die Einrichtung der Verschlüsselung für ausgewählte Datenbankspalten. Wenn Sie nicht bereits über eine Datenbank verfügen, für die Always Encrypted konfiguriert ist, befolgen Sie die Anweisungen in [Erste Schritte mit Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_5).
- Stellen Sie sicher, dass Microsoft JDBC Driver 6.0 (oder höher) für SQL Server auf dem Entwicklungscomputer installiert ist. 
-   Laden Sie die Richtliniendateien Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction herunter und installieren Sie sie.  Achten Sie darauf, die in der ZIP-Datei enthaltene Infodatei zu lesen, um Installationsanweisungen und relevante Details zu möglichen Export-/Importproblemen zu erhalten.  
  
    -   Wenn Sie die "sqljdbc41.jar" verwenden, können die Richtliniendateien von heruntergeladen werden [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Richtliniendateien 7 herunterladen](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)  
  
    -   Wenn die Datei sqljdbc42.jar verwenden, können die Richtliniendateien von heruntergeladen werden [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Richtliniendateien 8 herunterladen](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)   
    
## <a name="enabling-always-encrypted-for-application-queries"></a>Aktivieren von Always Encrypted für Anwendungsabfragen  
Die einfachste Möglichkeit zum Aktivieren der Verschlüsselung von Parametern und die Entschlüsselung der Abfrageergebnisse, die für die verschlüsselte Spalten wird durch Festlegen des Werts, der die **ColumnEncryptionSetting** Schlüsselwort für Verbindungszeichenfolgen zu  **Aktiviert**.

Im folgenden finden ein Beispiel für eine Verbindungszeichenfolge, die Always Encrypted in der JDBC-Treiber ermöglicht:
  
```  
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;"; 
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
     
```  
  
Und der folgende Code ist ein gleichwertiges Beispiel SQLServerDataSource-Objekts.  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");  
SQLServerConnection con = (SQLServerConnection) ds.getConnection(); 
```    

Always Encrypted kann auch für einzelne Abfragen aktiviert werden. Finden Sie unter der **steuern Leistung Auswirkungen von Always Encrypted** Abschnitt weiter unten. Beachten Sie, dass die Aktivierung von Always Encrypted für eine erfolgreiche Verschlüsselung und Entschlüsselung nicht ausreichend ist. Sie müssen auch Folgendes sicherstellen:
- Die Anwendung verfügt über die Datenbankberechtigungen *VIEW ANY COLUMN MASTER KEY DEFINITION* und *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* , die für den Zugriff auf die Metadaten in der Datenbank über Always Encrypted-Schlüssel erforderlich sind. Weitere Informationen finden Sie unter [Abschnitt „Berechtigungen“ in Always Encrypted (Datenbankmodul)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7).
- Die Anwendung kann auf den Hauptschlüssel der Spalte zugreifen, der die Spaltenverschlüsselungsschlüssel schützt, mit denen die abgefragten Datenbankspalten verschlüsselt werden. Beachten Sie, um den Java-Schlüsselspeicher-Anbieter verwenden, den Sie zusätzliche Anmeldeinformationen in der Verbindungszeichenfolge angeben müssen. Finden Sie unter **mit Java-Schlüsselspeicher-Anbieter** Abschnitt, um weitere Details.

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Konfigurieren, wie java.sql.Time-Werte an den Server gesendet werden

Die **SendTimeAsDatetime** Verbindungseigenschaft dient zum Konfigurieren, wie der java.sql.Time-Wert an den Server gesendet wird. Wenn SendTimeAsDatetime = "false", die Uhrzeit Wert als Time-Typ von SQL Server gesendet wird und wann SendTimeAsDatetime = "true", die Zeit, der Wert wird als Typ "DateTime" gesendet. Beachten Sie, dass, wenn eine Time-Spalte verschlüsselt wird, die SendTimeAsDatetime-Eigenschaft "false" sein muss als verschlüsselte Spalten nicht die Konvertierung von Zeit in "DateTime" unterstützen. Außerdem Beachten Sie, dass diese Eigenschaft von der Standardeinstellung "true", damit wenn verschlüsselte Spalten zu verwenden, Sie sie auf "false" festgelegt können. Andernfalls wird der Treiber als Ausnahme ausgelöst. SQLServerConnection-Klasse verfügt über zwei Methoden: ab Version 6.0 des Treibers auf den Wert dieser Eigenschaft programmgesteuert zu konfigurieren:
 
* Öffentliche void SetSendTimeAsDatetime (boolesche SendTimeAsDateTimeValue)
* öffentlicher boolescher Wert getSendTimeAsDatetime()

Weitere Informationen zu dieser Eigenschaft finden Sie auf [konfigurieren wie java.sql.Time-Werte werden an den Server gesendet](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx). 

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>Konfigurieren, wie die Zeichenfolgenwerte an den Server gesendet werden

Die **SendStringParametersAsUnicode** Connection-Eigenschaft wird verwendet, um zu konfigurieren, die Zeichenfolgenwerte auf SQL Server gesendet werden. Wenn auf "Wahr", String-Parameter im Unicode-Format an den Server gesendet werden. Wenn auf "false", String-Parameter festgelegt ist, die in nicht-Unicode-Format wie ASCII/MBCS, sondern gesendet werden. Der Standardwert für diese Eigenschaft ist "true". Wenn Always Encrypted aktiviert ist, und eine char/varchar/varchar(max)-Spalte wird verschlüsselt, wird der Wert der **SendStringParametersAsUnicode** muss auf "true" (oder bleiben die Standardeinstellung) festgelegt werden. Microsoft JDBC Driver für SQL Server löst eine Ausnahme aus, wenn Daten in einer verschlüsselten char/varchar/varchar(max)-Spalte einfügen, wenn diese Eigenschaft auf "false" festgelegt ist. Weitere Informationen zu dieser Eigenschaft finden Sie auf [Festlegen der Verbindungseigenschaften](../../connect/jdbc/setting-the-connection-properties.md). 
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>Abrufen und Ändern von Daten in verschlüsselten Spalten

Nachdem Sie Always Encrypted für Anwendungsabfragen aktiviert, können Sie den JDBC-standard-APIs verwenden, abrufen und Ändern von Daten in verschlüsselten Datenbankspalten. Vorausgesetzt, die Anwendung über die erforderlichen Datenbankberechtigungen verfügt und kann den Zugriff des spaltenhauptschlüssels, Microsoft JDBC Driver für SQL Server verschlüsselt alle Abfrageparameter, die verschlüsselte Spalten anvisieren und entschlüsselt die Daten von verschlüsselten Spalten abgerufenen Datentypen zurückgeben klartextwerte der JDBC-Typen für SQL Server für die Spalten im Datenbankschema festgelegt werden.
Wenn Always Encrypted nicht aktiviert ist, tritt bei Abfragen mit Parametern, die auf verschlüsselte Spalten ausgerichtet sind, ein Fehler auf. Abfragen können weiterhin Daten aus verschlüsselten Spalten abrufen, solange die Abfrage keine Parameter für verschlüsselte Spalten enthält. Allerdings Microsoft JDBC Driver für SQL Server nicht versucht, die von verschlüsselten Spalten abgerufenen Werte zu entschlüsseln und erhält die Anwendung binäre verschlüsselte Daten (als Bytearrays).

Die folgende Tabelle fasst das Verhalten von Abfragen in Abhängigkeit davon zusammen, ob Always Encrypted aktiviert ist:

|Abfragemerkmal | Always Encrypted ist aktiviert und die Anwendung kann auf die Schlüssel und Schlüsselmetadaten zugreifen.|Always Encrypted ist aktiviert und die Anwendung kann nicht auf die Schlüssel oder Schlüsselmetadaten zugreifen. | Always Encrypted ist deaktiviert|
|:---|:---|:---|:---|
| Abfragen mit Parametern, die auf verschlüsselte Spalten ausgerichtet sind. | Parameterwerte werden transparent verschlüsselt. | Fehler | Fehler|
| Abfragen, die Daten von verschlüsselten Spalten ohne Parameter abrufen, die auf verschlüsselte Spalten ausgerichtet sind.| Ergebnisse von verschlüsselten Spalten werden transparent entschlüsselt. Die Anwendung erhält klartextwerte der JDBC-Datentypen, die für die SQL Server-Datentypen, die für den verschlüsselten Spalten konfiguriert. | Fehler | Ergebnisse von verschlüsselten Spalten werden nicht entschlüsselt. Die Anwendung erhält verschlüsselte Werte als Bytearrays (byte[]).
      
 
### <a name="inserting-and-retrieving-encrypted-data-examples"></a>Einfügen und Abrufen von verschlüsselten Daten-Beispiele 
Die folgenden Beispiele veranschaulichen das Abrufen und Ändern von Daten in verschlüsselten Spalten. Die Beispiele gehen von der Zieltabelle mit folgendem Schema aus. Beachten Sie, dass die Spalten „SSN“ und „BirthDate“ verschlüsselt werden.

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
 
### <a name="inserting-data-example"></a>Beispiel zum Einfügen von Daten

In diesem Beispiel wird eine Zeile in die Tabelle „Patients“ eingefügt. Beachten Sie Folgendes:
- Es erfolgt keine spezielle Verschlüsselung im Beispielcode. Microsoft JDBC Driver für SQL Server wird automatisch erkannt und verschlüsselt die Parameter, die verschlüsselte Spalten ausgerichtet. Dadurch wird die Verschlüsselung für die Anwendung transparent. 
- Die Werte, die in Datenbankspalten, einschließlich der verschlüsselten Spalten eingefügt werden als Parameter, die mithilfe der sqlserverpreparedstatement-Klasse übergeben. Beim Verwenden von Parametern optional ist, wenn Werte nicht verschlüsselten Spalten gesendet werden (obwohl es wird dringend empfohlen, da sie verhindert, dass SQL-Injection), es ist erforderlich, damit die Werte, die auf verschlüsselte Spalten ausgerichtet sind. Wenn in den verschlüsselten Spalten eingefügten Werte als Literale in der abfrageanweisung eingebettet übergeben wurden, wird die Abfrage fehl, weil es sich bei Microsoft JDBC Driver für SQL Server nicht möglich wäre zu bestimmen, die Werte in den verschlüsselten Zielspalten, dies nicht der Fall wäre Verschlüsseln Sie die Werte ein. Daher würde der Server sie zurückweisen, da sie mit den verschlüsselten Spalten inkompatibel sind.
- Alle Werte, die vom Programm gedruckt wird als nur-Text wie Microsoft JDBC Driver für SQL Server die aus den verschlüsselten Spalten abgerufenen Daten transparent entschlüsselt werden.
- Wenn Sie das Durchführen einer Suche mit wobei-Klausel der Wert in der WHERE-Klausel verwendet als Parameter übergeben werden muss, damit können Microsoft JDBC Driver für SQL Server transparent verschlüsseln Sie ihn vor dem Senden an die Datenbank. Beachten Sie im folgenden Beispiel, dass "ssn" als Parameter übergeben wird, aber die LastName wird als Literal übergeben, wie LastName nicht verschlüsselt ist.
- Der Setter-Methode, die für den Parameter für die Spalte "ssn" verwendete ist setString(), die von SQL Server-Datentyp Char/Varchar zugeordnet wird. Wenn für diesen Parameter der Setter-Methode verwendet setNString(), die Nchar/Nvarchar zugeordnet wird wurde, würde die Abfrage fehl, da Always Encrypted keine Konvertierungen von verschlüsselten Nchar/Nvarchar-Werte in verschlüsselten Char/Varchar-Werte unterstützt.  

```
String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
try  
{           
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

### <a name="retrieving-plaintext-data-example"></a>Beispiel zum Abrufen von Klartextdaten

Im folgenden Beispiel wird das Filtern von Daten auf Basis verschlüsselter Werte und das Abrufen von Klartextdaten aus verschlüsselten Spalten veranschaulicht. Beachten Sie Folgendes:
- Der Wert in die WHERE-Klausel auf die Spalte "ssn" Filtern muss als Parameter übergeben werden verwendet, damit der Microsoft JDBC-Treiber für SQL Server transparent vor dem Senden an die Datenbank verschlüsseln können.
- Alle Werte, die vom Programm gedruckt wird als nur-Text wie Microsoft JDBC Driver für SQL Server aus den Spalten "ssn" und "BirthDate" abgerufenen Daten transparent entschlüsselt werden.

> [!NOTE]  
>  Abfragen können auf Spalten Übereinstimmungsvergleiche ausführen, wenn sie mittels deterministischer Verschlüsselung verschlüsselt sind. Weitere Informationen finden Sie unter der **Auswählen der deterministischen oder zufälligen Verschlüsselung** Teil der [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) Thema.  

```
String connectionString =  "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;" ;
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
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>Beispiel zum Abrufen von verschlüsselten Daten

Wenn Always Encrypted nicht aktiviert ist, können Abfragen weiterhin Daten aus verschlüsselten Spalten abrufen, so lange die Abfrage keine Parameter für verschlüsselte Spalten enthält.

In den folgenden Beispielen wird das Abrufen von binär verschlüsselten Daten aus verschlüsselten Spalten veranschaulicht. Beachten Sie Folgendes:

- Da Always Encrypted in der Verbindungszeichenfolge nicht aktiviert ist, gibt die Abfrage verschlüsselte Werte von „SSN“ und „BirthDate“ als Bytearrays zurück (das Programm konvertiert die Werte in Zeichenfolgen).
- Eine Abfrage, die Daten aus verschlüsselten Spalten mit deaktiviertem Always Encrypted abruft, kann Parameter aufweisen, so lange keiner der Parameter auf eine verschlüsselte Spalte ausgerichtet ist. Die obige Abfrage filtert nach der Spalte „LastName“, die in der Datenbank nicht verschlüsselt ist. Wenn die Abfrage nach „SSN“ oder „BirthDate“ filtert, würde ein Fehler auftreten.

```
String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;"; 
 
try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "Abel");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next())
    {  
        System.out.println("SSN: " + rs.getString("SSN") +
         ", FirstName: " + rs.getString("FirstName") + 
        ", LastName:"+ rs.getString("LastName")+ 
        ", Date of Birth: " + rs.getString("BirthDate"));  
    } 
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>Vermeiden allgemeiner Probleme beim Abfragen von verschlüsselter Spalten

Dieser Abschnitt beschreibt allgemeine Kategorien von Fehlern beim Abfragen verschlüsselter Spalten aus Java-Anwendungen und einige Grundsätze zum vermeiden.

### <a name="unsupported-data-type-conversion-errors"></a>Nicht unterstützte Fehler bei der Datentypkonvertierung

Always Encrypted unterstützt einige Konvertierungen für verschlüsselte Datentypen. Finden Sie unter [Always Encrypted (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) für eine ausführliche Liste der unterstützten typkonvertierungen. Stellen Sie Folgendes sicher, um Fehler bei der Datentypkonvertierung zu vermeiden:

- Wenn Werte für die Parameter für verschlüsselte Spalten übergeben, damit die SQL Server-Datentyp des Parameters ist entweder genau mit dem Typ der Zielspalte oder eine Konvertierung von der SQL Server-Datentyp des Parameters, verwenden die entsprechenden Setter-Methoden an das Ziel ist der Typ der Spalte unterstützt. Beachten Sie, dass die neue API-Methoden SQLServerPreparedStatement und SQLServerCallableStatement mit SQLServerResultSet Klassen zum Übergeben von Parametern, die für bestimmte SQL Server-Datentypen hinzugefügt wurden. Beispielsweise ist eine Spalte unverschlüsselte können setTimestamp()-Methode Sie einen Parameter oder eine Datetime-Spalte einen datetime2 übergeben. Aber wenn eine Spalte verschlüsselt wird, haben, verwenden Sie die genaue Methode, die den Typ der Spalte in der Datenbank darstellt. Verwenden Sie z. B. setTimestamp() Werte übergeben, um eine verschlüsselte datetime2-Spalte und setDateTime() zum Übergeben von Werten in einer verschlüsselten "DateTime"-Spalte verwenden. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) für eine vollständige Liste der neuen APIs. 
- Die Genauigkeit und Dezimalstellenanzahl von Parametern, die auf Spalten der SQL Server-Datentypen „decimal“ und „numeric“ ausgerichtet sind, ist mit der für die Zielspalte konfigurierten Genauigkeit und Dezimalstellenanzahl identisch. Beachten Sie, dass die neue API-Methoden SQLServerPreparedStatement und SQLServerCallableStatement mit SQLServerResultSet-Klassen, die Genauigkeit und Dezimalstellenanzahl zusammen mit den Datenwerten für Parameter oder Spalten, die Datentypen decimal und numeric darstellt akzeptieren hinzugefügt wurden. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) für eine vollständige Liste der APIs neue/überladen.  
- die Sekundenbruchteile Genauigkeit/Skalierung der Parameter für Spalten von datetime2, Datetimeoffset oder Time SQL Server-Datentypen ist nicht größer als der für die Zielspalte in Abfragen, die Werte der Zielspalte zu ändern. Beachten Sie, dass die neue API-Methoden SQLServerPreparedStatement und SQLServerCallableStatement mit SQLServerResultSet Klassen Sekundenbruchteile Genauigkeit/Skalierung zusammen mit den Datenwerten für Parameter, die diese Datentypen darstellen akzeptieren hinzugefügt wurden. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) für eine vollständige Liste der APIs neue/überladen.   

### <a name="errors-due-to-incorrect-connection-properties"></a>Fehler aufgrund von falschen Verbindungseigenschaften
In diesem Abschnitt wird beschrieben, wie so konfigurieren Sie die Verbindungseinstellungen ordnungsgemäß um immer verschlüsselte Daten verwendet wird. Da verschlüsselte Datentypen beschränkt Konvertierungen unterstützen, benötigen die Verbindungseinstellungen "SendTimeAsDatetime" und "SendStringParametersAsUnicode" geeignete Konfiguration aus, wenn mit verschlüsselten Spalten. Stellen Sie Folgendes sicher: 
- [SendTimeAsDatetime](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx) verbindungseinstellung auf "false" festgelegt ist, beim Einfügen von Daten in Spalten verschlüsselt. Weitere Informationen finden Sie im Abschnitt "Konfigurieren, wie java.sql.Time-Werte an den Server gesendet werden".
- [SendStringParametersAsUnicode](../../connect/jdbc/setting-the-connection-properties.md) verbindungseinstellung auf festgelegt ist "true" (oder bleibt die Standardeinstellung) beim Einfügen von Daten in verschlüsselte char/varchar/varchar(max) Spalten umfassen. Weitere Informationen finden Sie im Abschnitt "Konfigurieren, wie die Zeichenfolgenwerte an den Server gesendet werden".

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>Fehler aufgrund der Übergabe von Klartext anstelle von verschlüsselten Werten

Jeder Wert, der auf eine verschlüsselte Spalte ausgerichtet ist, muss in der Anwendung verschlüsselt werden. Ein Versuch, einen Klartextwert einzufügen bzw. zu ändern oder nach einem Klartextwert für eine verschlüsselte Spalte zu filtern, führt zu einem Fehler wie dem Folgenden:


```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

Stellen Sie Folgendes sicher, um solche Fehler zu vermeiden:
- immer ist Encrypted für Anwendungsabfragen für verschlüsselte Spalten (für die Verbindungszeichenfolge oder für eine bestimmte Abfrage) aktiviert.
- Verwendung von vorbereiteten Anweisungen und Parameter zum Senden von Daten auf verschlüsselte Spalten. Das folgende Beispiel zeigt eine Abfrage, die falsch nach einem Literal bzw. einer Konstante einer verschlüsselten Spalte (SSN) filtert, anstatt das literal innere als Parameter übergeben. Diese Abfrage schlägt fehl.

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");  
```

## <a name="working-with-column-master-key-stores"></a>Arbeiten mit Spaltenhauptschlüsselspeichern
Zum Verschlüsseln eines Parameterwerts oder zum Entschlüsseln von Daten in den Abfrageergebnissen, muss Microsoft JDBC Driver für SQL Server einen spaltenverschlüsselungsschlüssel, der so konfiguriert ist, für die Zielspalte zu erhalten. Spaltenverschlüsselungsschlüssel werden in verschlüsselter Form in den Datenbankmetadaten gespeichert. Jeder Spaltenverschlüsselungsschlüssel weist einen entsprechenden Spaltenhauptschlüssel auf, mit dem der Spaltenverschlüsselungsschlüssel verschlüsselt wurde. Die Spaltenhauptschlüssel werden nicht von den Datenbankmetadaten gespeichert. Sie enthalten lediglich die Informationen zu einem Schlüsselspeicher, der einen bestimmten Spaltenhauptschlüssel und die Position des Schlüssels im Schlüsselspeicher enthält.

Um einen Klartextwert eines spaltenverschlüsselungsschlüssels zu erhalten, erhält der Microsoft JDBC-Treiber für SQL Server zunächst die Metadaten über den Verschlüsselungsschlüssel für die Spalte und der entsprechenden spaltenhauptschlüssel, und verwendet die Informationen in den Metadaten, wenden Sie sich an den Schlüssel Speicher, mit dem spaltenhauptschlüssel und den verschlüsselten spaltenverschlüsselungsschlüssel zu entschlüsseln. Microsoft JDBC Driver für SQL Server kommuniziert mit einem Schlüsselspeicher, wobei ein Hauptschlüssel Speicheranbieter – die eine Instanz einer Klasse abgeleitet **SQLServerColumnEncryptionKeyStoreProvider** Klasse.


### <a name="using-built-in-column-master-key-store-providers"></a>Verwenden integrierter Spaltenhauptschlüssel-Speicheranbieter
  
Im Lieferumfang von Microsoft JDBC Driver für SQL Server sind die folgenden integrierten Hauptschlüssel Speicheranbieter. Beachten Sie, dass einige dieser Anbieter mit den bestimmten Anbieternamen sind (wird verwendet, um den Anbieter zu suchen) vorregistrierte und einige zusätzliche Anmeldeinformationen oder explizite Registrierung erforderlich.

| Klasse | Beschreibung | Anbietername (Suche) |Ist bereits registriert?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Ein Anbieter für einen Schlüsselspeicher für den Azure Key Vault.| AZURE_KEY_VAULT|Nein|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Ein Anbieter für den Windows-Zertifikatspeicher.|MSSQL_CERTIFICATE_STORE|ja
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Für die Java-Schlüsselspeicher-Anbieter|MSSQL_JAVA_KEYSTORE|ja|

Für die zuvor registrierten Schlüsselspeicher-Anbieter müssen Sie keine Änderungen am Anwendungscode verwenden diese Anbieter, aber beachten Folgendes vornehmen:

- Sie (oder der Datenbankadministrator) müssen sicherstellen, dass der in den Metadaten des Spaltenhauptschlüssels konfigurierte Anbietername richtig ist und der Pfad des Spaltenhauptschlüssels dem Schlüsselpfadformat entspricht, das für einen angegebenen Anbieter gültig ist. Es wird empfohlen, dass Sie die Schlüssel mithilfe von Tools wie SQL Server Management Studio konfigurieren, die die gültigen Anbieternamen und Schlüsselpfade automatisch generieren, wenn die Anweisung CREATE COLUMN MASTER KEY (Transact-SQL) ausgegeben wird.
- Sie müssen sicherstellen, dass die Anwendung auf den Schlüssel im Schlüsselspeicher zugreifen kann. Dies kann das Gewähren des Zugriffs auf den Schlüssel und/oder Schlüsselspeicher für die Anwendung (abhängig vom Schlüsselspeicher) oder das Ausführen anderer wichtiger speicherspezifischer Konfigurationsschritte einbeziehen. Beispielsweise müssen für die Verwendung der SQLServerColumnEncryptionJavaKeyStoreProvider Geben Sie den Speicherort und das Kennwort für den Schlüsselspeicher in den Verbindungseigenschaften. 

Alle diese Schlüsselspeicher-Anbieter werden im folgenden ausführlicher beschrieben.
  
### <a name="using-azure-key-vault-provider"></a>Verwenden des Azure Key Vault-Anbieters
Azure Key Vault ist eine praktische Möglichkeit zum Speichern von Spaltenhauptschlüsseln für Always Encrypted (insbesondere, wenn Ihre Anwendungen in Azure gehostet werden). Microsoft JDBC Driver für SQL Server enthält einen integrierten Anbieter SQLServerColumnEncryptionAzureKeyVaultProvider, für Anwendungen, die in Azure Key Vault gespeicherte Schlüsseln haben. Der Name des Anbieters ist AZURE_KEY_VAULT. Damit den Azure Key Vault-Speicheranbieter verwenden zu können, muss ein Anwendungsentwickler dem Tresor und die Schlüssel in Azure erstellen und konfigurieren die Anwendung auf die Schlüssel zugreifen. Weitere Informationen zum Einrichten der schlüsseltresor und erstellen spaltenhauptschlüssel finden Sie unter [Azure Key Vault – Schritt für Schritt für Weitere Informationen zum Einrichten der schlüsseltresor](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) und [Erstellen von Spaltenhauptschlüsseln in Azure Key Vault](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2).  
  
Um Azure-Schlüsseltresor zu verwenden, müssen Clientanwendungen die SQLServerColumnEncryptionAzureKeyVaultProvider instanziieren und registrieren Sie ihn mit dem Treiber.

Hier ist ein Beispiel der SQLServerColumnEncryptionAzureKeyVaultProvider initialisieren:  
  
```  
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey); 
```

Nachdem die Anwendung eine Instanz von SQLServerColumnEncryptionAzureKeyVaultProvider erstellt wurde, wird die Anwendung zum Registrieren der Instanz in Microsoft JDBC-Treiber für die Verwendung von SQL Server muss die Sqlserverconnection.registercolumnencryptionkeystoreproviders()-Methode. Es wird dringend empfohlen, die Instanz registriert ist, mithilfe des Standardnamens des Suche, AZURE_KEY_VAULT, die durch Aufrufen der API SQLServerColumnEncryptionAzureKeyVaultProvider.getName() abgerufen werden kann. Mithilfe des Standardnamens können Sie zum Verwenden von Tools, z. B. SQL Server Management Studio oder PowerShell, bereitstellen und Verwalten von Always Encrypted-Schlüssel (die Tools verwenden den Standardnamen zum Generieren des Metadatenobjekts, um spaltenhauptschlüssel). Das folgende Beispiel zeigt die Azure Key Vault-Anbieter wird registriert. Weitere Details zu der sqlserverconnection.registercolumnencryptionkeystoreproviders()-Methode, finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md). 

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();   
keyStoreMap.put(akvProvider.getName(), akvProvider);   
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);   
```
  
> [!IMPORTANT]  
>  Die Azure Key Vault-Implementierung des JDBC-Treibers hat Abhängigkeiten von diesen Bibliotheken (von GitHub):  
>   
>  [Azure Sdk für java](https://github.com/Azure/azure-sdk-for-java)  
>   
>  [Azure-Active Directory-Bibliothek-für-Java-Bibliotheken](https://github.com/AzureAD/azure-activedirectory-library-for-java)  
  
### <a name="using-windows-certificate-store-provider"></a>Mithilfe der Windows-Zertifikatspeicher-Anbieter
Die SQLServerColumnEncryptionCertificateStoreProvider kann verwendet werden, zum Speichern von spaltenhauptschlüsseln im Windows-Zertifikatspeicher. Verwenden Sie SQL Server Management Studio (SSMS) Always Encrypted-Assistenten oder andere unterstützte Tools, um die spaltenhauptschlüssel und die spaltenverschlüsselung Definitionen in der Datenbank erstellen. Des gleiche Assistenten verwendet werden kann, um ein selbstsigniertes Zertifikat in Windows-Zertifikatspeicher zu generieren, die als spaltenhauptschlüssel verwendet wird, für die immer verschlüsselten Daten. Weitere Informationen zu spaltenhauptschlüssel und spaltenverschlüsselung Key T-SQL-Syntax finden Sie auf [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) und [CREATE COLUMN Encryption KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) bzw.

Der Name des der SQLServerColumnEncryptionCertificateStoreProvider "MSSQL_CERTIFICATE_STORE" ist und die getName()-API des Objekts Anbieter abgefragt werden kann. Es wird automatisch vom Treiber registriert und kann ohne Änderung Anwendung nahtlos verwendet werden.

> [!IMPORTANT]  
>  Die SQLServerColumnEncryptionCertificateStoreProvider-Implementierung des JDBC-Treibers ist mit Windows-Betriebssystemen verfügbar und hat eine Abhängigkeit auf "sqljdbc_auth.dll", die im Treiberpaket enthaltenen verfügbar ist.  Kopieren Sie die Datei "sqljdbc_auth.dll" zur Verwendung dieses Anbieters in ein Verzeichnis auf dem Windows-Systempfad auf dem Computer, auf dem der JDBC-Treiber installiert ist. Alternativ können Sie mit der java.libary.path-Systemeigenschaft das Verzeichnis von „sqljdbc_auth.dll“ angeben. Wenn Sie eine 32-Bit-JVM (Java Virtual Machine) ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x86“, auch wenn es sich bei dem Betriebssystem um die x64-Version handelt. Wenn Sie eine 64-Bit-JVM mit einem x64-Prozessor ausführen, verwenden Sie die Datei „sqljdbc_auth.dll“ im Ordner „x64“. Beispielsweise können, wenn Sie die 32-Bit-JVM und der JDBC-Treiber wird im Standardverzeichnis installiert, Sie geben Sie den Speicherort der DLL mit dem folgenden Argument für den virtuellen Computer (VM) beim Start der Java-Anwendung:  
`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`
        
### <a name="using-java-key-store-provider"></a>Mithilfe von Java-Schlüsselspeicher-Anbieter  
Der JDBC-Treiber ist mit einer integrierten Schlüsselspeicheranbieter-Implementierung für die Java-Schlüsselspeicher. Der Treiber automatisch instanziiert und den Anbieter für Java-Schlüsselspeicher, registriert, wenn die **KeyStoreAuthentication** Verbindungszeichenfolgen-Eigenschaft in der Verbindungszeichenfolge vorhanden ist, und klicken Sie auf "JavaKeyStorePassword" festgelegt ist (Sie finden Sie unter Weitere Details unten). Der Name von der Java-Schlüsselspeicher-Anbieter ist MSSQL_JAVA_KEYSTORE. Dieser Name kann auch von der SQLServerColumnEncryptionJavaKeyStoreProvider.getName()-API abgefragt werden. 

Drei neue Schlüsselwörter für Verbindungszeichenfolgen werden eingeführt, damit können eine Client-tasksequenzausführungsmodul deklarativ angeben, die Anmeldeinformationen, die der Treiber benötigt Java-Schlüsselspeicher zu authentifizieren. Der Treiber würde den Anbieter, die anhand der Werte der folgenden drei Eigenschaften der Verbindungszeichenfolge für die bestimmten Verbindungen zu initialisieren. 
  
 **KeyStoreAuthentication:** identifiziert den-Schlüsselspeicher zu verwenden. Mit Microsoft JDBC Driver 6.0 für SQL Server können Sie auf der Java-Schlüsselspeicher über diese Eigenschaft nur authentifizieren. Für die Java-Schlüsselspeicher muss der Wert für diese Eigenschaft "JavaKeyStorePassword" sein.   
  
 **KeyStoreLocation:** den Pfad zur Java Keystore-Datei, in der die spaltenhauptschlüssel gespeichert. Beachten Sie, dass der Pfad den Dateinamen Schlüsselspeicher enthält.  
  
 **KeyStoreSecret:** das Kennwort für den geheimen/für den Schlüsselspeicher als auch für den Schlüssel verwendet. Beachten Sie, dass für die Verwendung von Java-Schlüsselspeicher Keystore und das Kennwort für den Schlüssel identisch sein müssen.  

Hier ist ein Beispiel für diese Anmeldeinformationen in der Verbindungszeichenfolge anzugeben:

    String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
    
Diese Einstellungen können auch mithilfe der SQLServerDataSource-Objekts Set/Get sein. Finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) für Weitere Informationen.     
  
Der JDBC-Treiber instanziiert die SQLServerColumnEncryptionJavaKeyStoreProvider automatisch, wenn diese Anmeldeinformationen in den Verbindungseigenschaften vorhanden sind. 
  
### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Erstellen eines Spaltenhauptschlüssels für die Java-Schlüsselspeicher
Die SQLServerColumnEncryptionJavaKeyStoreProvider kann mit JKS oder PKCS12-Schlüsselspeicher-Typen verwendet werden. Erstellen oder importieren ein Schlüssels für die Verwendung mit diesem Anbieter verwenden, die Java [Keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) Hilfsprogramm. Beachten Sie, dass der Schlüssel dasselbe Kennwort wie Keystore selbst aufweisen muss. Hier ist ein Beispiel zum Erstellen eines öffentlichen Schlüssels und dazugehörigen privaten Schlüssel mit dem Hilfsprogramm Keytool.

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks    

Dieser Befehl erstellt einen öffentlichen Schlüssel und umschließt ihn in einem x. 509 selbstsigniertes Zertifikat diese werden dann im Schlüsselspeicher "keystore.jks" zusammen mit seinem zugehörigen privaten Schlüssel gespeichert ist. Dieser Eintrag im Schlüsselspeicher wird durch den Alias "AlwaysEncryptedKey" identifiziert. 

Hier ist ein Beispiel für die gleiche mit einem PKCS12-Speichertyp aus. 

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword   

Beachten Sie, den Keystore ist der PKCS12 eingeben, und klicken Sie dann das Hilfsprogramm Keytool für das Kennwort für den Schlüssel und Kennwort für den Schlüssel nicht angefordert werden muss mit Keypass - Option bereitgestellt werden, wie die SQLServerColumnEncryptionJavaKeyStoreProvider erfordert, dass der Schlüsselspeicher und den Schlüssel verfügen die dasselbe Kennwort.

Sie können auch ein Zertifikat aus dem Windows-Zertifikatspeicher im PFX-Format exportieren und verwenden, die mit der SQLServerColumnEncryptionJavaKeyStoreProvider. Das exportierte Zertifikat kann auch auf die Java-Schlüsselspeicher als JKS Keystore Typ importiert werden. 

Nach dem Erstellen des Eintrags Keytool müssen Sie die Spaltenmetadaten des Hauptschlüssels in der Datenbank zu erstellen, die von der Name des Schlüsselspeicheranbieters und dem Schlüsselpfad benötigt. Weitere Informationen zum Erstellen von Hauptschlüssel-Spaltenmetadaten finden Sie auf [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). Für SQLServerColumnEncryptionJavaKeyStoreProvider ist die Schlüsselpfad nur den Alias des Schlüssels. Und der Name der SQLServerColumnEncryptionJavaKeyStoreProvider ist "MSSQL_JAVA_KEYSTORE". Sie können auch diesen Namen, die mit der öffentlichen getName()-API der Klasse SQLServerColumnEncryptionJavaKeyStoreProvider Abfragen. 

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
>  Die integrierte in SQL Server Management Studio-Funktionalität kann nicht erstellt Spalte hauptschlüsseldefinitionen für die Java-Schlüsselspeicher Sie für die T-SQL-Befehl verwenden.  
  
### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Erstellen eines Spaltenverschlüsselungsschlüssels für die Java-Schlüsselspeicher
Beachten Sie, dass der SQL Server Management Studio oder einem anderen Tool nicht verwendet werden kann um Spalte Verschlüsselungsschlüssel mit der Hauptschlüssel für Spalten in der Java-Schlüsselspeicher zu erstellen. Die Clientanwendung muss den spaltenverschlüsselungsschlüssel, der programmgesteuert mithilfe der SQLServerColumnEncryptionJavaKeyStoreProvider-Klasse erstellen. Weitere Details finden Sie im Abschnitt "Mithilfe von Master Key-Speicheranbieter für die programmgesteuerte Bereitstellung-Schlüssel". 

  
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

Wenn für den Zugriff auf verschlüsselte Spalten sucht nach Microsoft JDBC Driver für SQL Server transparent und ruft die rechte Spalte Speicheranbieter für spaltenhauptschlüssel um spaltenverschlüsselungsschlüssel zu entschlüsseln. In der Regel ruft der normale Anwendungscode die Speicheranbieter für Spaltenhauptschlüssel nicht direkt auf. Sie können einen Anbieter jedoch explizit instanziieren und aufrufen, um Always Encrypted-Schlüssel programmgesteuert bereitzustellen und zu verwalten: Zum Generieren eines verschlüsselten Spaltenverschlüsselungsschlüssels und Entschlüsseln eines Spaltenverschlüsselungsschlüssels (z. B. im Rahmen einer Spaltenhauptschlüsselrotation) Weitere Informationen finden Sie unter [Übersicht über die Schlüsselverwaltung für Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).
Beachten Sie, dass die Implementierung eigener Schlüsselverwaltungstools möglicherweise nur erforderlich ist, wenn Sie einen benutzerdefinierten Schlüsselspeicheranbieter verwenden. Bei Verwendung in Windows-Zertifikatspeicher oder Azure Key Vault gespeicherte Schlüsseln können Sie vorhandene Tools, z. B. SQL Server Management Studio oder PowerShell verwenden, verwalten und Bereitstellen von Schlüsseln zu verwenden. Wenn Sie Schlüssel gespeichert sind, in der Java-Schlüsselspeicher verwenden zu können, müssen Sie Schlüssel programmgesteuert bereitzustellen. Das folgenden Beispiel veranschaulicht die Verwendung von SQLServerColumnEncryptionJavaKeyStoreProvider-Klasse zum Verschlüsseln des Schlüssels mit einem Schlüssel in der Java-Schlüsselspeicher gespeichert.

```  
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programatically for the Java Key Store.
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
                 * For more details on the syntax refer: 
                 * https://msdn.microsoft.com/library/mt146372.aspx
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
         * Following arguments needed by  SQLServerColumnEncryptionJavaKeyStoreProvider
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
  
## <a name="force-encryption-on-input-parameters"></a>Erzwingen der Verschlüsselung auf Eingabeparametern
  
Die Verschlüsselung erzwingen-Funktion erzwingt die Verschlüsselung eines Parameters bei Verwendung von Always Encrypted. Wenn Verschlüsselung erzwingen verwendet wird, und SQL Server den Treiber, den der Parameter nicht informiert verschlüsselt werden muss, wird die Abfrage, die mithilfe des Parameters fehl. Diese Eigenschaft bietet zusätzlichen Schutz vor Angriffen, bei denen ein kompromittierter SQL Server falsche Verschlüsselungsmetadaten für den Client bereitstellt, was zur Offenlegung von Daten führen kann. Die Methoden Satz * in Sqlserverpreparedstatement- und SQLServerCallableStatement-Klassen und das Update\* Methoden in der SQLServerResultSet-Klasse sind überladen, sodass um ein boolesches Argument zum Angeben des Force-verschlüsselungseinstellung zu akzeptieren. Wenn der Wert dieses Arguments auf "false" festgelegt ist, wird der Treiber keine Verschlüsselung auf Parameter erzwungen. Wenn die Verschlüsselung erzwingen festgelegt ist auf "true", die Abfrage Parameter wird nur gesendet, wenn die Zielspalte verschlüsselt und Always Encrypted aktiviert ist, für die Verbindung oder bei der Anweisung an. Dies ermöglicht eine zusätzliche Sicherheitsebene, die sicherstellen, dass keine Daten versehentlich gesendet werden, auf SQL Server als nur-Text Wenn davon ausgegangen wird, verschlüsselt werden.  
  
 Weitere Informationen zu den Sqlserverpreparedstatement- und SQLServerCallableStatement-Methoden, die überladen werden mit der Force-verschlüsselungseinstellung finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-performance-impact-of-always-encrypted"></a>Kontrollieren der Auswirkungen von Always Encrypted auf die Leistung

Da Always Encrypted eine clientseitige Verschlüsselungstechnologie ist, werden die meisten Leistungseinbußen auf der Clientseite und nicht in der Datenbank beobachtet. Neben den Kosten für Verschlüsselungs- und Entschlüsselungsvorgänge ergeben sich die folgenden anderen Quellen für Leistungseinbußen auf der Clientseite:
- Zusätzliche Roundtrips zur Datenbank zum Abrufen von Metadaten für Abfrageparameter.
- Aufrufe an einen Spaltenhauptschlüsselspeicher für den Zugriff auf einen Spaltenhauptschlüssel.

Dieser Abschnitt beschreibt die integrierten leistungsoptimierungen im Microsoft JDBC Driver für SQL Server und wie Sie die Auswirkungen der beiden oben genannten Faktoren auf die Leistung steuern können.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>Kontrollieren von Roundtrips zum Abrufen von Metadaten für Abfrageparameter

Microsoft JDBC Driver für SQL Server wird aufgerufen, wenn Always Encrypted für eine Verbindung standardmäßig aktiviert ist [Sys. sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396) für jede parametrisierte Abfrage übergeben Sie die abfrageanweisung (ohne Parameterwerte) mit SQL Server. [Sys. sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396) analysiert die Query-Anweisung, um herauszufinden, wenn alle Parameter müssen verschlüsselt werden, und wenn also für jede etwa die verschlüsselungsbezogenen Informationen zurückgegeben, die Microsoft JDBC Driver für SQL Server ermöglichen um Parameterwerte zu verschlüsseln. Das oben beschriebene Verhalten stellt einen hohen Grad an Transparenz für die Clientanwendung sicher. Die Anwendung (und der Anwendungsentwickler) muss nicht beachten, welche Abfragen Zugriff auf verschlüsselte Spalten sein, solange die Werte, die auf verschlüsselte Spalten ausgerichtet an den Microsoft JDBC-Treiber für SQL Server als Parameter übergeben werden.


#### <a name="setting-always-encrypted-at-the-query-level"></a>Festlegen von Always Encrypted auf Abfrageebene

Sie können Always Encrypted für einzelne Abfragen aktivieren, anstatt es für die Verbindung einzurichten, um beim Abrufen von Verschlüsselungsmetadaten für parametrisierte Abfragen die Auswirkung auf die Leistung zu steuern. Auf diese Weise können Sie sicherstellen, dass „sys.sp_describe_parameter_encryption“ nur für Abfragen aufgerufen wird, bei denen Ihnen bekannt ist, dass sie über Parameter verfügen, die auf verschlüsselte Spalten ausgerichtet sind. Beachten Sie jedoch, dass Sie auf diese Weise die Transparenz der Verschlüsselung reduzieren: Wenn Sie die Verschlüsselungseigenschaften der Datenbankspalten ändern, müssen Sie möglicherweise den Code der Anwendung ändern, um ihn mit den Schemaänderungen auszurichten.


Um das Verhalten Always Encrypted für einzelne Abfragen zu steuern, müssen Sie so konfigurieren Sie einzelne Statement-Objekte durch Übergeben einer Enumeration SQLServerStatementColumnEncryptionSetting, der angibt, wie Daten gesendet und empfangen, beim Lesen und Schreiben verschlüsselte Spalten für bestimmte betreffende Anweisung ausführt. Hier sind einige nützliche Richtlinien:
- Für die meisten Abfragen greift eine Clientanwendung über eine Datenbankverbindung auf verschlüsselte Spalten zu:
    - Das Schlüsselwort für Verbindungszeichenfolgen ColumnEncryptionSetting auf Enabled festgelegt.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.Disabled für einzelne Abfragen, die kein verschlüsselten Spalten zugreifen. Dadurch werden sowohl der Aufruf von „sys.sp_describe_parameter_encryption“ als auch der Versuch deaktiviert, Werte im Resultset zu entschlüsseln.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.ResultSet für einzelne Abfragen, die keine Parameter, die eine Verschlüsselung erforderlich ist, jedoch Daten aus verschlüsselten Spalten abrufen. Dadurch werden der Aufruf von „sys.sp_describe_parameter_encryption“ und die Parameterverschlüsselung deaktiviert. Die Abfrage ist in der Lage, die Ergebnisse von Spaltenverschlüsselungen zu entschlüsseln.
- Für die meisten Abfragen greift eine Clientanwendung nicht über eine Datenbankverbindung auf verschlüsselte Spalten zu:
    - Das Schlüsselwort für Verbindungszeichenfolgen ColumnEncryptionSetting auf deaktiviert festgelegt.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.Enabled für einzelne Abfragen, die Parameter aufweisen, die verschlüsselt werden müssen. Dadurch werden sowohl der Aufruf von „sys.sp_describe_parameter_encryption“ als auch die Entschlüsselung von Abfrageergebnissen aktiviert, die aus verschlüsselten Spalten abgerufen werden.
    - Legen Sie SQLServerStatementColumnEncryptionSetting.ResultSet für Abfragen, die keine Parameter, die eine Verschlüsselung erforderlich ist, jedoch Daten aus verschlüsselten Spalten abrufen. Dadurch werden der Aufruf von „sys.sp_describe_parameter_encryption“ und die Parameterverschlüsselung deaktiviert. Die Abfrage ist in der Lage, die Ergebnisse von Spaltenverschlüsselungen zu entschlüsseln.

Beachten Sie, dass die SQLServerStatementColumnEncryptionSetting Einstellungen verwendet werden können, um Verschlüsselung zu umgehen und Zugriff auf Klartextdaten zu erhalten. Weitere Informationen zum Konfigurieren der spaltenverschlüsselung in einer Anweisung finden Sie unter [Always Encrypted-API-Referenz für den JDBC-Treiber](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md).  

In dem folgenden Beispiel ist Always Encrypted für die Datenbankverbindung deaktiviert. Die von der Anwendung ausgestellte Abfrage weist einen Parameter auf, der auf die nicht verschlüsselte Spalte „LastName“ ausgerichtet ist. Die Abfrage ruft Daten aus den Spalten „SSN“ und „BirthDate“ ab, die beide verschlüsselt sind. In diesem Fall ist der Aufruf von „sys.sp_describe_parameter_encryption“ nicht erforderlich, um Verschlüsselungsmetadaten abzurufen. Die Entschlüsselung der Abfrageergebnisse muss jedoch aktiviert sein, damit die Anwendung Klartextwerte aus den beiden verschlüsselten Spalten erhalten kann. SQLServerStatementColumnEncryptionSetting.ResultSet-Einstellung wird verwendet, um sicherzustellen, dass.

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

Um die Anzahl der Aufrufe an einen spaltenhauptschlüsselspeicher spaltenhauptschlüsselspeicher zu verringern, werden von Microsoft JDBC Driver für SQL Server die Klartext-spaltenverschlüsselungsschlüssel im Arbeitsspeicher zwischengespeichert. Nach dem Erhalt des Verschlüsselungsschlüsselwerts für die verschlüsselte Spalte von den Datenbankmetadaten versucht der Treiber zunächst, den Spaltenverschlüsselungsschlüssel im Klartext zu finden, der dem verschlüsselten Schlüsselwert entspricht. Der Treiber ruft den Schlüsselspeicher, der den Spaltenhauptschlüssel enthält, nur dann auf, wenn er den verschlüsselten Spaltenverschlüsselungsschlüssel im Cache nicht finden kann.

Sie können einen Time-to-live-Wert für die Spalte Verschlüsselung Schlüsseleinträge im Cache mithilfe der API setColumnEncryptionKeyCacheTtl(), in der SQLServerConnection-Klasse konfigurieren. Time-to-live-Wert für die Spalte Schlüsseleinträge Verschlüsselung im Cache beträgt 2 Stunden. Deaktivieren der anweisungsvervollständigungsoptionen caching verwenden Sie den Wert 0. Jeder Time-to-live-Wert verwendet die folgende API festlegen:
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
   
Um eine Time-to-live-Wert von 10 Minuten festzulegen, verwenden Sie z. B.
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)

Beachten Sie, dass nur Tage, Stunden, Minuten oder Sekunden als die Zeiteinheit unterstützt werden.  


## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>Kopieren die verschlüsselten Daten mithilfe von "sqlserverbulkcopy"

Mit "sqlserverbulkcopy" können Sie Daten kopieren, die bereits verschlüsselt und in einer Tabelle gespeichert, in eine andere Tabelle, ohne die Daten zu entschlüsseln. Gehen Sie dazu wie folgt vor:

- Stellen Sie sicher, dass die Verschlüsselungskonfiguration der Zieltabelle mit der Konfiguration der Quelltabelle identisch ist. Insbesondere müssen für beide Tabellen dieselben Spalten verschlüsselt sein. Zudem müssen die Spalten mithilfe derselben Verschlüsselungstypen und mit denselben Verschlüsselungsschlüsseln verschlüsselt werden. Hinweis: Wenn eine der Zielspalten anders als die entsprechende Quellspalte verschlüsselt wurde, können Sie die Daten in der Zieltabelle nach dem Kopiervorgang nicht entschlüsseln. Die Daten werden beschädigt.
- Konfigurieren Sie beide Datenbankverbindungen, zur Quelltabelle und zur Zieltabelle, ohne Always Encrypted zu aktivieren. 
- Legen Sie die Option "allowencryptedvaluemodifications". Finden Sie unter [Verwenden von Massenkopieren mit dem JDBC-Treiber](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md) für Weitere Informationen.
 
Hinweis: Seien Sie bei "allowencryptedvaluemodifications" angeben, da dies zur Beschädigung der Datenbank, da der Microsoft JDBC-Treiber für SQL Server nicht überprüft, wenn die Daten tatsächlich verschlüsselt oder ordnungsgemäß mit der gleichen Verschlüsselung verschlüsselt wurden, führen kann Typ, Algorithmus und Schlüssel wie die Zielspalte.

## <a name="see-also"></a>Siehe auch  
 [„Immer verschlüsselt“ (Datenbankmodul)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  

