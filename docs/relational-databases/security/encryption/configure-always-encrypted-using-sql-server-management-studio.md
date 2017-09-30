---
title: Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio | Microsoft-Dokumentation
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 097ce7fb331df64de9b293a6af9e05e7d95f1b37
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Dieser Artikel beschreibt die Aufgaben, die bei der Konfiguration von Always Encrypted und der Verwaltung von Datenbanken anfallen, die Always Encrypted mit [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md) verwenden.

Wenn Sie SSMS zur Konfiguration von Always Encrypted verwenden, verwaltet SSMS beide Always Encrypted-Schlüssel und sensible Daten. Beide Schlüssel und die Daten werden daher in SSMS als Klartext angezeigt. Es ist daher wichtig, dass Sie SSMS auf einem sicheren Computer ausführen. Wenn Ihre Datenbank in SQL Server gehostet wird, sollten Sie sicherstellen, dass SSMS auf einem anderen Computer als dem Computer ausgeführt wird, der Ihre SQL Server-Instanz hostet. Der primäre Zweck von Always Encrypted ist, sicherzustellen, dass verschlüsselte sensible Daten sicher sind, selbst wenn das Datenbanksystem kompromittiert wird. Daher kann das Ausführen eines PowerShell-Skripts, das Schlüssel und/oder sensible Daten auf dem SQL Server-Computer verarbeitet, die Vorteile der Funktion einschränken oder zunichte machen. Weitere Empfehlungen finden Sie unter [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)(Überlegungen zur Verwaltung von Schlüsseln).

SSMS unterstützt keine Rollentrennung zwischen Personen, die die Datenbank verwalten (Datenbankadministratoren; DBAs), und denjenigen, die kryptografische Schlüssel verwalten und Zugriff auf Klartextdaten haben (Sicherheitsadministratoren und/oder Anwendungsadministratoren). Wenn Ihre Organisation auf Rollentrennung besteht, sollten Sie PowerShell verwenden, um Always Encrypted zu konfigurieren. Weitere Informationen finden Sie unter [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) (Übersicht über die Schlüsselverwaltung für Always Encrypted) und [Konfigurieren von Always Encrypted mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>Konfigurieren von Always Encrypted mithilfe des Always Encrypted-Assistenten

Der [Always Encrypted-Assistent](../../../relational-databases/security/encryption/always-encrypted-wizard.md) ist ein leistungsstarkes Tool, mit dem Sie die gewünschte Verschlüsselungskonfiguration für ausgewählte Datenbankspalten festlegen können. Der Assistent kann Spalten in Abhängigkeit von der aktuellen Always Encrypted-Konfiguration und der gewünschten Zielkonfiguration verschlüsseln, entschlüsseln (Verschlüsselung entfernen) oder sie erneut verschlüsseln (z.B. mithilfe eines neuen Spaltenverschlüsselungsschlüssels oder eines anderen Verschlüsselungstyps als dem aktuellen, der für die Spalte konfiguriert ist). Während einer einzigen Ausführung des Assistenten können mehrere Spalten konfiguriert werden.

Wenn Sie keinerlei Always Encrypted-Schlüssel bereitgestellt haben, wird der Assistent die Schlüssel automatisch generieren. Sie müssen lediglich einen Schlüsselspeicher für Ihren Spaltenhauptschlüssel auswählen: der Windows-Zertifikatspeicher oder Azure Key Vault. Der Assistent generiert auch die Schlüsselnamen und ihre Metadatenobjekte in der Datenbank automatisch. Wenn Sie mehr Kontrolle über die Bereitstellungsweise der Schlüssel wünschen (und mehr Auswahlmöglichkeiten beim Schlüsselspeicher für den Spaltenhauptschlüssel), können Sie mithilfe der Dialogfelder **Neuer Spaltenhauptschlüssel** und **Neuer Spaltenverschlüsselungsschlüssel** (weiter unten beschrieben) verwenden, um Schlüssel vor dem Start des Assistenten bereitzustellen. Sie können dann im Always Encrypted-Assistenten den vorhandenen Spaltenverschlüsselungsschlüssel auswählen.

Weitere Informationen zur Verwendung des Assistenten finden Sie unter  [Always Encrypted-Assistent](../../../relational-databases/security/encryption/always-encrypted-wizard.md).

## <a name="querying-encrypted-columns"></a>Abfragen von verschlüsselten Spalten

In diesem Abschnitt werden die Vorgehensweisen für folgende Vorgänge erläutert:   
-   Abrufen von in verschlüsselten Spalten gespeicherten Chiffretextwerten   
-   Abrufen von in verschlüsselten Spalten gespeicherten Klartextwerten   
-   Senden von Klartextwerten an verschlüsselte Spalten (z.B. in `INSERT` - oder `UPDATE` -Anweisungen und als Nachschlageparameter von `WHERE` -Klauseln in `SELECT` -Anweisungen)   

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>Abrufen von in verschlüsselten Spalten gespeicherten Chiffretextwerten    

So rufen Sie Werte aus einer verschlüsselten Spalte als Chiffretext ab (ohne die Werte zu entschlüsseln):
1.  Vergewissern Sie sich, dass Always Encrypted für die Datenbankverbindung des Fensters „Abfrage-Editor“ deaktiviert ist, in dem Sie Ihre `SELECT` -Abfrage ausführen. Siehe [Aktivieren und Deaktivieren von Always Encrypted für eine Datenbankverbindung](#en-dis) weiter unten.      
2.  Führen Sie eine `SELECT` -Abfrage aus. Alle aus verschlüsselten Spalten abgerufenen Daten werden als (verschlüsselte) Binärwerte zurückgegeben.   

*Beispiel*   
Sofern `SSN` eine verschlüsselte Spalte in der Tabelle `Patients` ist, ruft die folgende Abfrage die binären Chiffretextwerte ab, wenn Always Encrypted für die Datenbankverbindung deaktiviert ist.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>Abrufen von in verschlüsselten Spalten gespeicherten Klartextwerten    

So rufen Sie Werte aus einer verschlüsselten Spalte als Klartext ab (um die Werte zu entschlüsseln)   
1.  Vergewissern Sie sich, dass Always Encrypted für die Datenbankverbindung des Fensters „Abfrage-Editor“ aktiviert ist, in dem Sie Ihre `SELECT` -Abfrage ausführen. Dadurch wird der (von SSMS verwendete) .NET Framework-Datenanbieter für SQL Server angewiesen, die aus verschlüsselten Spalten abgerufenen Daten zu entschlüsseln. Siehe [Aktivieren und Deaktivieren von Always Encrypted für eine Datenbankverbindung](#en-dis) weiter unten.
2.  Stellen Sie sicher, dass Sie auf alle Spaltenhauptschlüssel zugreifen können, die für verschlüsselte Spalten konfiguriert sind. Wenn beispielsweise Ihr Spaltenhauptschlüssel ein Zertifikat ist, müssen Sie dafür sorgen, dass das Zertifikat auf dem Computer bereitgestellt wird, auf dem SSMS ausgeführt wird. Wenn Ihr Spaltenhauptschlüssel in Azure Key Vault gespeichert ist, müssen Sie sicherstellen, dass Sie über Zugriffsberechtigungen für den Schlüssel verfügen. (Außerdem werden ggf. aufgefordert, sich bei Azure anzumelden.)
3.  Führen Sie eine `SELECT` -Abfrage aus. Aus verschlüsselten Spalten abgerufene Daten werden als Klartext mit Werten der ursprünglichen Datentypen zurückgegeben.   

*Beispiel*   
Wenn SSN eine verschlüsselte Spalte `char(11)` in der Tabelle `Patients` ist, gibt die unten gezeigte Abfrage Klartextwerte zurück, sofern Always Encrypted für die Datenbankverbindung aktiviert ist und Sie Zugriff auf den Spaltenhauptschlüssel haben, der für die Spalte `SSN` konfiguriert ist.   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>Senden von Klartextwerten an verschlüsselte Spalten       

So führen Sie eine Abfrage aus, die einen Wert an eine verschlüsselte Spalte sendet, z.B. eine Abfrage, die einen in einer verschlüsselten Spalte gespeicherten Wert einfügt, aktualisiert oder danach filtert:   
1.  Vergewissern Sie sich, dass Always Encrypted für die Datenbankverbindung des Fensters „Abfrage-Editor“ aktiviert ist, in dem Sie Ihre `SELECT` -Abfrage ausführen. Dadurch wird der (von SSMS verwendete) .NET Framework-Datenanbieter für SQL Server angewiesen, parametrisierte Transact-SQL-Variablen (siehe unten) für verschlüsselte Spalten zu verschlüsseln. Siehe [Aktivieren und Deaktivieren von Always Encrypted für eine Datenbankverbindung](#en-dis) weiter unten.   
2.  Stellen Sie sicher, dass Sie auf alle Spaltenhauptschlüssel zugreifen können, die für verschlüsselte Spalten konfiguriert sind. Wenn beispielsweise Ihr Spaltenhauptschlüssel ein Zertifikat ist, müssen Sie dafür sorgen, dass das Zertifikat auf dem Computer bereitgestellt wird, auf dem SSMS ausgeführt wird. Wenn Ihr Spaltenhauptschlüssel in Azure Key Vault gespeichert ist, müssen Sie sicherstellen, dass Sie über Zugriffsberechtigungen für den Schlüssel verfügen. (Außerdem werden ggf. aufgefordert, sich bei Azure anzumelden.)   
3.  Stellen Sie sicher, dass „Parametrisierung für Always Encrypted“ für das Fenster „Abfrage-Editor“ aktiviert ist. (Erfordert mindestens SSMS Version 17.0) Deklarieren Sie eine Transact-SQL-Variable, und initialisieren Sie sie mit einem Wert, der an die Datenbank gesendet werden soll (Einfügen, Aktualisieren oder Filtern nach). Details finden Sie weiter unten unter [Parametrisierung für Always Encrypted](#param).   
    >   [!NOTE]
    >   Da Always Encrypted nur eine beschränkte Teilmenge von Typumwandlungen unterstützt, ist es in vielen Fällen erforderlich, dass der Datentyp einer Transact-SQL-Variablen dem Typ der Spalte in der Zieldatenbank entspricht.   
4.  Führen Sie die Abfrage aus, um den Wert der Transact-SQL-Variablen an die Datenbank zu senden. SSMS wandelt die Variable in einen Abfrageparameter um und verschlüsselt dessen Wert, ehe er an die Datenbank gesendet wird.   

*Beispiel*   
Wenn `SSN` eine verschlüsselte Spalte `char(11)` in der Tabelle `Patients` ist, versucht das folgende Skript eine Zeile zu finden, die `'795-73-9838'` in der Spalte „SSN“ enthält und den Wert der Spalte `LastName` zurückgibt. Vorausgesetzt wird, dass Always Encrypted für die Datenbankverbindung aktiviert ist, dass „Parametrisierung für Always Encrypted“ für das Fenster „Abfrage-Editor“ aktiviert ist und dass Sie Zugriff auf den Spaltenhauptschlüssel haben, der für die Spalte `SSN` konfiguriert ist.   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)
 
### <a name="en-dis"></a> Aktivieren und Deaktivieren von Always Encrypted für eine Datenbankverbindung   

Durch Aktivieren von Always Encrypted für eine Datenbankverbindung wird der .NET Framework-Datenanbieter für SQL Server, der von SQL Server Management Studio verwendet wird, aufgefordert, die folgenden Aufgaben transparent auszuführen:   
-   Entschlüsseln aller Werte, die aus verschlüsselten Spalten abgerufen und in Abfrageergebnissen zurückgegeben werden   
-   Verschlüsseln der Werte der parametrisierten Transact-SQL-Variablen für verschlüsselte Spalten in der Zieldatenbank   
Geben Sie zum Aktivieren von Always Encrypted für eine Datenbankverbindung `Column Encryption Setting=Enabled` im Dialogfeld **Verbindung mit Server herstellen** auf der Registerkarte **Zusätzliche Eigenschaften** an.    
Geben Sie zum Deaktivieren von Always Encrypted für eine Datenbankverbindung `Column Encryption Setting=Disabled` an, oder entfernen Sie einfach die Einstellung **Spaltenverschlüsselungseinstellung** von der Registerkarte **Zusätzliche Eigenschaften** im Dialogfeld **Verbindung mit Server herstellen** (der Standardwert ist **Deaktiviert**).   

>  [!TIP] 
>  So schalten Sie zwischen dem Aktivieren und Deaktivieren von Always Encrypted für ein vorhandenes Fenster „Abfrage-Editor“ um:   
>  1.   Klicken Sie im Fenster „Abfrage-Editor“ mit der rechten Maustaste auf eine beliebige Stelle.
>  2.   Wählen Sie **Verbindung** > **Verbindung ändern...** aus. 
>  3.   Klicken Sie auf **Optionen** >>.
>  4.   Wählen Sie die Registerkarte **Zusätzliche Eigenschaften** aus, und geben Sie `Column Encryption Setting=Enabled` ein, um Always Encrypted zu aktivieren, oder entfernen Sie die Einstellung, um Always Encrypted zu deaktivieren.   
>  5.   Klicken Sie auf **Verbinden**.   
   
### <a name="param"></a>Parametrisierung für Always Encrypted   
 
„Parametrisierung für Always Encrypted“ ist ein Feature in SQL Server Management Studio, das Transact-SQL-Variablen automatisch in Abfrageparameter (Instanzen der [„SqlParameter“-Klasse](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)) konvertiert. (Erfordert mindestens SSMS Version 17.0) Dies ermöglicht dem zugrunde liegenden .NET Framework-Datenanbieter für SQL Server das Erkennen von Daten für verschlüsselte Spalten und das Verschlüsseln dieser Daten, ehe sie an die Datenbank gesendet werden. 
  
Ohne Parametrisierung übergibt der .NET Framework-Datenanbieter jede Ihrer Anweisungen, die Sie im Abfrage-Editor erstellen, als nicht parametrisierte Abfrage. Wenn die Abfrage Literale oder Transact-SQL-Variablen für verschlüsselte Spalten enthält, kann der .NET Framework-Datenanbieter für SQL Server diese nicht erkennen und verschlüsseln, ehe die Abfrage an die Datenbank gesendet wird. Daher misslingt die Abfrage aufgrund eine Typkonflikts (zwischen dem Literal oder der Transact-SQL-Variablen in Klartext und der verschlüsselten Spalte). Die folgende Abfrage misslingt beispielsweise ohne Parametrisierung, sofern die Spalte `SSN` verschlüsselt ist.   

```tsql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>Aktivieren oder Deaktivieren von „Parametrisierung für Always Encrypted“   


„Parametrisierung für Always Encrypted“ ist standardmäßig deaktiviert.    

So aktivieren Sie „Parametrisierung für Always Encrypted“ für das aktuelle Fenster „Abfrage-Editor“   
1.  Wählen Sie im Hauptmenü **Abfrage** aus.   
2.  Wählen Sie **Abfrageoptionen...**aus.   
3.  Navigieren Sie zu **Ausführung** > **Erweitert**.   
4.  Aktivieren bzw. deaktivieren **Parametrisierung für Always Encrypted**.   
5.  Klicken Sie auf **OK**.   

So aktivieren oder deaktivieren Sie „Parametrisierung für Always Encrypted“ für künftige „Abfrage-Editor“-Fenster   
1.  Wählen Sie im Hauptmenü **Tools** aus.   
2.  Wählen Sie **Optionen...**aus.   
3.  Navigieren Sie zu **Abfrageausführung** > **SQL Server** > **Erweitert**.   
4.  Aktivieren bzw. deaktivieren **Parametrisierung für Always Encrypted**.   
5.  Klicken Sie auf **OK**.   

Bei Ausführung einer Abfrage im Fenster „Abfrage-Editor“, das eine Datenbankverbindung mit aktiviertem Always Encrypted aufweist, ohne dass die Parametrisierung für das Fenster „Abfrage-Editor“ aktiviert ist, werden Sie zur Aktivierung aufgefordert.   
>   [!NOTE]   
>   „Parametrisierung für Always Encrypted“ funktioniert nur in Abfrage-Editor-Fenstern mit Datenbankverbindungen, für die Always Encrypted aktiviert ist (siehe [Aktivieren und Deaktivieren von Always Encrypted für eine Datenbankverbindung](#en-dis)). Transact-SQL-Variablen werden nicht parametrisiert, wenn das Fenster „Abfrage-Editor“ eine Datenbankverbindung ohne aktiviertes Always Encrypted aufweist.   

#### <a name="how-parameterization-for-always-encrypted-works"></a>Funktionsweise von „Parametrisierung für Always Encrypted“   

Wenn sowohl „Parametrisierung für Always Encrypted“ als auch das Always Encrypted-Verhalten für die Datenbankverbindung im Fenster „Abfrage-Editor“ aktiviert sind, versucht SQL Server Management Studio die Parametrisierung von Transact-SQL-Variablen, die die folgenden Bedingungen erfüllen:    
- Sind in der gleichen Anweisung deklariert und initialisiert (Inline-Initialisierung). Variablen, die mit getrennten `SET` -Anweisungen deklariert wurden, werden nicht parametrisiert.   
- Sind mithilfe eines einzelnen Literals initialisiert. Variablen, die mithilfe von Ausdrücken initialisiert wurden, die Operatoren oder Funktionen enthalten, werden nicht parametrisiert.      

Es folgen Beispiele von Variablen, die von SQL Server Management Studio parametrisiert werden.   
```tsql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

Und hier sehen Sie einige Beispiele von Variablen, bei denen SQL Server Management Studio keine Parametrisierung versucht.   
```tsql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';
   
DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal
   
DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
Voraussetzungen für eine erfolgreiche Parametrisierung:   
- Der Typ des Literals, der für die Initialisierung der zu parametrisierenden Variablen verwendet wird, muss dem Typ in der Variablendeklaration entsprechen.   
- Wenn der deklarierte Typ der Variablen ein „date“- oder „time“-Typ ist, muss die Variable mithilfe einer Zeichenfolge in einem der folgenden ISO 8601-kompatiblen Formate initialisiert werden.   

Es folgen Beispiele von Transact-SQL-Variablendeklarationen, die zu Parametrisierungsfehlern führen:   
```tsql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio nutzt Intellisense, um Sie zu informieren, welche Variablen erfolgreich parametrisiert werden können und welche Parametrisierungsversuche misslingen (samt Grund).   

Eine Deklaration einer Variablen, die erfolgreich parametrisiert werden kann, wird im Abfrage-Editor mit einer Warnunterstreichung markiert. Wenn Sie den Mauszeiger über einer Deklarationsanweisung bewegen, die mit einer Warnunterstreichung markiert wurde, sehen Sie die Ergebnisse des Parametrisierungsvorgangs, einschließlich der Werte der Haupteigenschaften des resultierenden [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) -Objekts (dem die Variable zugeordnet ist): [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx). Eine vollständige Liste aller Variablen, die erfolgreich parametrisiert wurden, finden Sie auf der Registerkarte **Warnung** der Ansicht **Fehlerliste** . Zum Öffnen der Ansicht **Fehlerliste** wählen im Hauptmenü **Ansicht** und dann **Fehlerliste**aus.    

Wenn SQL Server Management Studio versucht hat, eine Variable zu parametrisieren, aber die Parametrisierung misslungen ist, wird die Deklaration der Variablen mit einer Fehlerunterstreichung gekennzeichnet. Wenn Sie den Mauszeiger über der Deklarationsanweisung bewegen, die mit einer Fehlerunterstreichung markiert wurde, erhalten Sie Informationen zum Fehler. In der Ansicht **Fehlerliste** sehen Sie auf der Registerkarte **Fehler** die vollständige Liste von Parametrisierungsfehlern für alle Variablen. Zum Öffnen der Ansicht **Fehlerliste** wählen im Hauptmenü **Ansicht** und dann **Fehlerliste**aus.   

Das nachstehende Bildschirmfoto zeigt ein Beispiel von sechs Variablendeklarationen. SQL Server Management Studio hat die ersten drei Variablen erfolgreich parametrisiert. Die letzten drei Variablen haben nicht die Bedingungen für die Parametrisierung erfüllt, weshalb SQL Server Management Studio nicht versucht hat, sie zu parametrisieren (ihre Deklarationen sind nicht gekennzeichnet).   

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
Ein weiteres nachstehendes Beispiel zeigt zwei Variablen, die die Bedingungen für die Parametrisierung erfüllt haben, doch der Parametrisierungsversuch ist misslungen, weil die Variablen falsch initialisiert waren.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
>   [!NOTE]
>   Da Always Encrypted eine beschränkte Teilmenge von Typumwandlungen unterstützt, ist es in vielen Fällen erforderlich, dass der Datentyp einer Transact-SQL-Variablen dem Typ der Spalte in der Zieldatenbank entspricht. Angenommen, der Typ der Spalte `SSN` in der Tabelle `Patients` ist `char(11)`. Die folgende Abfrage misslingt, da der Typ der Variablen `@SSN` (der `nchar(11)`ist) nicht dem Typ der Spalte entspricht.   

```tsql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.

>   [!NOTE]
>   Ohne Parametrisierung wird die gesamte Abfrage, einschließlich Typumwandlungen, innerhalb von SQL Server/Azure SQL-Datenbank verarbeitet. Bei aktivierter Parametrisierung erfolgen einige Typumwandlungen durch .NET Framework innerhalb von SQL Server Management Studio. Aufgrund der Unterschiede zwischen dem Typsystem von .NET Framework und dem von SQL Server (z.B. verschiedene Genauigkeit einiger Typen wie „float“) kann eine Abfrage mit aktivierter Parametrisierung andere Ergebnisse als die Abfrage liefern, die ohne aktivierte Parametrisierung ausgeführt wird. 

#### <a name="permissions"></a>Berechtigungen      

Zum Anwenden von Abfragen auf verschlüsselte Spalten, einschließlich Abfragen zum Abrufen von Daten in Chiffretext, benötigen Sie für die Datenbank die Berechtigungen `VIEW ANY COLUMN MASTER KEY DEFINITION` und `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` .   
Zusätzlich zu den oben aufgeführten Berechtigungen benötigen Sie zum Entschlüsseln von Abfrageergebnissen oder Verschlüsseln von Abfrageparametern (die durch parametrisierte Transact-SQL-Anweisungen erstellt wurden) auch Zugriff auf den Spaltenhauptschlüssel, der die Zielspalten schützt:   
- **Zertifikatspeiche – lokaler Computer** : Sie benötigen `Read` -Zugriff auf das Zertifikat, das als Spaltenhauptschlüssel verwendet wird, oder Administratorrechte auf dem Computer.   
- **Azure Key Vault** : Sie benötigen die Berechtigungen `get`und `unwrapKey`für den Tresor, der den Spaltenhauptschlüssel enthält.   
- **Schlüsselspeicheranbieter (Cryptography Next Generation; CNG)** : Die erforderlichen Berechtigungen und Anmeldeinformationen, zu deren Eingabe Sie möglicherweise aufgefordert werden, wenn Sie einen Schlüsselspeicher oder einen Schlüssel verwenden, hängen von der Konfiguration des Speichers und des Schlüsselspeicheranbieters (Key Storage Provider; KSP) ab.   
- **Kryptografiedienstanbieter (Kryptografie-API)** : Die erforderlichen Berechtigungen und Anmeldeinformationen, zu deren Eingabe Sie möglicherweise aufgefordert werden, wenn Sie einen Schlüsselspeicher oder einen Schlüssel verwenden, hängen von der Konfiguration des Speichers und des Kryptografiedienstanbieters (cryptographic service provider; CSP) ab.   

Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).


<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>Bereitstellen von Spaltenhauptschlüsseln (Neuer Spaltenhauptschlüssel)

Mit dem Dialogfeld **Neuer Spaltenhauptschlüssel** können Sie einen Spaltenhauptschlüssel generieren oder einen vorhandenen Schlüssel aus einem Schlüsselspeicher auswählen sowie Spaltenhauptschlüssel-Metadaten zu dem erstellten oder ausgewählten Schlüssel in der Datenbank erstellen.

1.  Navigieren Sie über den **Objekt-Explorer** zu dem Ordner **Sicherheit > Always Encrypted-Schlüssel** in Ihrer Datenbank.
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Spaltenhauptschlüssel**, und wählen Sie **Neuer Spaltenhauptschlüssel...** aus. 
3.  Geben Sie im Dialogfeld **Neuer Spaltenhauptschlüssel** den Namen des Spaltenhauptschlüssel-Metadatenobjekts ein.
4.  Wählen Sie einen Schlüsselspeicher aus:
    - **Zertifikatspeicher – Aktueller Benutzer** – Gibt den Zertifikatspeicherort des aktuellen Benutzers im Windows-Zertifikatspeicher an, der Ihrem persönlichen Zertifikatspeicher entspricht. 
    - **Zertifikatspeicher – lokaler Computer** – Gibt den Zertifikatspeicherort des lokalen Computers im Windows-Zertifikatspeicher an. 
    - **Azure Key Vault** – Sie müssen bei Azure anmelden (klicken Sie auf **Anmelden**). Sobald Sie sich angemeldet haben, können Sie eines Ihrer Azure-Abonnements und einen Schlüsselspeicher auswählen.
    - **Schlüsselspeicheranbieter (CNG)** – Gibt einen Schlüsselspeicher an, der über einen Schlüsselspeicheranbieter (KSP) zugänglich ist, der Cryptography Next Generation-API (CNG) implementiert. Bei dieser Art von Speicher handelt sich in der Regel um ein Hardwaresicherheitsmodul (HSM). Nachdem Sie diese Option ausgewählt haben, müssen Sie einen KSP auswählen. Standardmäßig ist der**Softwareschlüsselspeicher-Anbieter von Microsoft** aktiviert. Wenn Sie einen in einem HSM gespeicherten Spaltenhauptschlüssel verwenden möchten, wählen Sie einen KSP für Ihr Gerät aus (muss installiert und auf dem Computer konfiguriert werden, bevor Sie das Dialogfeld öffnen).
    -   **Kryptografiedienstanbieter (Kryptografie-API)** – Ein Schlüsselspeicher, der über einen Kryptografiedienstanbieter (CSP) zugänglich ist, der die Kryptografie-API (Cryptography API; CAPI) implementiert. Bei dieser Art von Speicher handelt sich in der Regel um ein Hardwaresicherheitsmodul (HSM). Nachdem Sie diese Option ausgewählt haben, müssen Sie einen CSP auswählen.  Wenn Sie einen in einem HSM gespeicherten Spaltenhauptschlüssel verwenden möchten, wählen Sie einen CSP für Ihr Gerät aus (muss installiert und auf dem Computer konfiguriert werden, bevor Sie das Dialogfeld öffnen).
    
    >   [!NOTE]
    >   Da es sich bei CAPI um eine veraltete API handelt, ist die Option „Kryptografiedienstanbieter“ (CAPI) standardmäßig deaktiviert. Sie können sie aktivieren, indem Sie den für den CAPI-Anbieter aktivierten DWORD-Wert unter dem Schlüssel **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** in der Windows-Registrierung erstellen und ihn auf 1 festlegen. Sofern Ihr Schlüsselspeicher CNG unterstützt, sollten Sie CNG statt CAPI verwenden.
   
    Weitere Informationen über die oben erwähnten Schlüsselspeicher finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

5.  Wählen Sie einen vorhandenen Schlüssel aus Ihrem Schlüsselspeicher aus, oder klicken Sie auf die Schaltflächen **Schlüssel generieren** oder **Zertifikat generieren** , um einen Schlüssel im Schlüsselspeicher zu erstellen. 
6.  Klicken Sie auf **OK** , und der neue Schlüssel wird in der Liste angezeigt. 

SQL Server Management Studio erstellt Metadaten für Ihren Spaltenhauptschlüssel in der Datenbank. Das Dialogfeld erreicht dies, indem es die Anweisung [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) generiert und ausgibt.


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>Bereitstellen von Spaltenverschlüsselungsschlüsseln (Neuer Spaltenverschlüsselungsschlüssel)

Mit dem Dialogfeld **Neuer Spaltenverschlüsselungsschlüssel** können Sie einen Spaltenverschlüsselungsschlüssel generieren, mit einem Spaltenhauptschlüssel verschlüsseln und Metadaten zu dem Spaltenverschlüsselungsschlüssel in der Datenbank erstellen.

1.  Navigieren Sie über den **Objekt-Explorer**zu dem Ordner **Sicherheit &gt; Always Encrypted-Schlüssel** in Ihrer Datenbank.
2.  Klicken Sie mit der rechten Maustaste auf den Ordner **Spaltenverschlüsselungsschlüssel** , und wählen Sie **Neuer Spaltenverschlüsselungsschlüssel...**aus. 
3.  Geben Sie im Dialogfeld **Neuer Spaltenverschlüsselungsschlüssel** den Namen des Spaltenverschlüsselungsschlüssel-Metadatenobjekts ein.
4.  Wählen Sie ein Metadatenobjekt aus, das Ihren Spaltenhauptschlüssel in der Datenbank darstellt.
5.  Klicken Sie auf **OK**. 


SQL Server Management Studio generiert einen neuen Spaltenverschlüsselungsschlüssel und ruft anschließend die Metadaten für den Spaltenhauptschlüssel ab, den Sie in der Datenbank ausgewählt haben. SQL Server Management Studio verwendet dann die Metadaten des Spaltenhauptschlüssels zur Kontaktaufnahme mit dem Schlüsselspeicher, der Ihren Spaltenhauptschlüssel enthält, und zur Verschlüsselung Ihres Spaltenverschlüsselungsschlüssels. Schließlich werden die Metadaten für den neuen Spaltenverschlüsselungsschlüssel in der Datenbank erstellt. Das Dialogfeld erreicht dies, indem es die Anweisung [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) generiert und ausgibt.

### <a name="permissions"></a>Berechtigungen

in der Datenbank über die Berechtigungen *ALTER ANY ENCRYPTION MASTER KEY* und *VIEW ANY COLUMN MASTER KEY DEFINITION* verfügen, damit das Dialogfeld die Metadaten des Spaltenverschlüsselungsschlüssels erstellen und auf die Metadaten des Spaltenhauptschlüssels zugreifen kann.
Sie benötigen möglicherweise Berechtigungen für Schlüsselspeicher oder/und den Schlüssel, um auf einen Schlüsselspeicher zugreifen und den Spaltenhauptschlüssel verwenden zu können:
- **Zertifikatspeicher – lokaler Computer** – Sie benötigen Lesezugriff auf das Zertifikat, das als Spaltenhauptschlüssel verwendet wird, oder Administratorrechte auf dem Computer.
- **Azure Key Vault** – Sie benötigen die Berechtigungen *get*, *unwrapKey*, *wrapKey*, *sign*und *verify*  für den Tresor, der den Spaltenhauptschlüssel enthält.
- **Schlüsselspeicheranbieter (CNG)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des KSP abhängen.
- **Kryptografiedienstanbieter (CSP)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des CSP abhängen.

Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>Rotieren von Spaltenhauptschlüsseln

Die Rotation eines Spaltenhauptschlüssels ist der Prozess des Ersetzens eines vorhandenen Spaltenhauptschlüssels durch einen neuen. Sie müssen einen Schlüssel möglicherweise rotieren, wenn er kompromittiert wurde. Kryptografische Schlüssel müssen regelmäßig rotiert werden, damit sie die Richtlinien Ihrer Organisation oder die Kompatibilitätsregelungen erfüllen. Die Rotation eines Spaltenhauptschlüssels umfasst die Entschlüsselung von Spaltenverschlüsselungsschlüsseln, die mit dem aktuellen Spaltenhauptschlüssel geschützt werden, deren Neuverschlüsselung mithilfe des neuen Spaltenhauptschlüssels und das Aktualisieren der Schlüsselmetadaten. Weitere Informationen finden Sie unter [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(Übersicht über die Schlüsselverwaltung für Always Encrypted).

**Schritt 1: Bereitstellen eines neuen Spaltenhauptschlüssels**

Stellen Sie einen neuen Spaltenhauptschlüssel anhand der Schritte im obigen Abschnitt „Bereitstellen von Spaltenhauptschlüsseln“ bereit.

**Schritt 2: Verschlüsseln von Spaltenverschlüsselungsschlüsseln mit dem neuen Spaltenhauptschlüssel**

Ein Spaltenhauptschlüssel schützt in der Regel mindestens einen Spaltenverschlüsselungsschlüssel. Jeder Spaltenverschlüsselungsschlüssel verfügt über einen verschlüsselten Wert, der in der Datenbank gespeichert wird und das Produkt der Verschlüsselung des Spaltenverschlüsselungsschlüssels mithilfe des Spaltenhauptschlüssels ist.
In diesem Schritt müssen Sie jeden Spaltenverschlüsselungsschlüssel, der mit dem aktuellen (zu rotierenden) Spaltenhauptschlüssel geschützt ist, mit dem neuen Spaltenhauptschlüssel verschlüsseln, und den neuen verschlüsselten Wert in der Datenbank speichern. Daher verfügt jeder von der Rotation betroffene Spaltenverschlüsselungsschlüssel über zwei verschlüsselte Werte: ein Wert, der mit dem vorhandenen Spaltenhauptschlüssel verschlüsselt wurde, und ein neuer Wert, der mit dem neuen Spaltenhauptschlüssel verschlüsselt wurde.

1.  Navigieren Sie über den **Objekt-Explorer** zu dem Ordner **Sicherheit > Always Encrypted-Schlüssel > Spaltenhauptschlüssel**, und suchen Sie den Spaltenhauptschlüssel, den Sie rotieren möchten.
2.  Klicken Sie mit der rechten Maustaste auf den Spaltenhauptschlüssel, und wählen Sie **Rotieren** aus.
3.  Wählen Sie im Dialogfeld **Column Master Key Rotation** (Rotation der Spaltenhauptschlüssel) den Namen Ihres neuen Spaltenhauptschlüssels im Feld **Ziel** aus, den Sie in Schritt 1 erstellt haben.
4.  Überprüfen Sie die Liste der Spaltenverschlüsselungsschlüssel, die durch den vorhanden Spaltenhauptschlüssel geschützt sind. Die Rotation wirkt sich auf diese Schlüssel aus.
5.  Klicken Sie auf **OK**.

SQL Server Management Studio erhält die Metadaten der Spaltenverschlüsselungsschlüssel, die mit dem alten Spaltenhauptschlüssel geschützt werden, und die Metadaten der alten und neuen Spaltenhauptschlüssel. SSMS verwendet die Metadaten des Spaltenhauptschlüssels anschließend, um auf den Schlüsselspeicher mit dem alten Spaltenhauptschlüssel zuzugreifen und den bzw. die Spaltenverschlüsselungsschlüssel zu entschlüsseln. SSMS greift daraufhin auf den Schlüsselspeicher mit dem neuen Spaltenhauptschlüssel zu, um einen neuen Satz von verschlüsselten Werten zu erzeugen und diese anschließend zu den Metadaten hinzuzufügen (durch Generieren und Ausgeben von [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) -Anweisungen).

> [!NOTE]
> Stellen Sie sicher, dass jeder der Spaltenverschlüsselungsschlüssel, der mit dem alten Spaltenhauptschlüssel verschlüsselt wurde, mit keinem anderen Spaltenhauptschlüssel verschlüsselt wird. Das bedeutet, dass jeder durch die Drehung betroffene Spaltenverschlüsselungsschlüssel genau einen verschlüsselten Wert in der Datenbank enthalten muss. Wenn ein betroffener Spaltenverschlüsselungsschlüssel über mehr als einen verschlüsselten Wert verfügt, müssen Sie den Wert entfernen, bevor Sie die Rotation fortsetzen können (Informationen zum Entfernen eines verschlüsselten Werts eines Spaltenverschlüsselungsschlüssels finden Sie in *Schritt 4* ).

**Schritt 3: Konfigurieren Ihrer Anwendungen mit dem neuen Spaltenhauptschlüssel**

In diesem Schritt geht es um alle Ihre Clientanwendungen, die Datenbankspalten abfragen, die mit dem zu rotierenden Spaltenhauptschlüssel geschützt werden (d.h. mit einem Spaltenverschlüsselungsschlüssel verschlüsselt sind, der wiederum mit dem zu rotierenden Spaltenhauptschlüssel verschlüsselt ist). Sie müssen sicherstellen, dass diese Clientanwendungen auf den neuen Spaltenhauptschlüssel zugreifen können. Ihr Vorgehen in diesem Schritt hängt vom Typ des Zertifikatspeichers ab, in dem sich Ihr neuer Spaltenhauptschlüssel befindet. Beispiel:
- Wenn der neue Spaltenhauptschlüssel ein im Windows-Zertifikatspeicher gespeichertes Zertifikat ist, müssen Sie das Zertifikat an dem Zertifikatspeicherort speichern (*Aktueller Benutzer* oder *Lokaler Computer*), der auch im Schlüsselpfad Ihres Spaltenhauptschlüssels in der Datenbank angegeben ist. Die Anwendung muss auf das Zertifikat zugreifen können:
    - Wenn das Zertifikat am Zertifikatspeicherort *Aktueller Benutzer* gespeichert wird, muss das Zertifikat in den Speicherort „Aktueller Benutzer“ der Windows-Identität (Benutzer) der Anwendung importiert werden.
    - Wenn das Zertifikat am Zertifikatspeicherort *Lokaler Computer* gespeichert wird, benötigt die Windows-Identität der Anwendung die Berechtigung zum Zugriff auf das Zertifikat.
- Wenn der neue Spaltenhauptschlüssel im Microsoft Azure Key Vault gespeichert wird, muss die Anwendung implementiert werden, damit sie für Azure authentifiziert werden kann und die Berechtigung zum Zugriff auf den Schlüssel erhält.

Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

> [!NOTE]
> Zu diesem Zeitpunkt des Rotationsverfahrens sind sowohl der alte als auch der neue Spaltenhauptschlüssel gültig und können für den Datenzugriff verwendet werden.

**Schritt 4: Bereinigen der Werte des Spaltenhauptschlüssels, die mit dem alten Spaltenhauptschlüssel verschlüsselt wurden**

Wenn Sie alle Ihre Anwendungen für die Verwendung des neuen Spaltenhauptschlüssels konfiguriert haben, müssen Sie die Werte der Spaltenverschlüsselungsschlüssel aus der Datenbank entfernen, die mit dem *alten* Spaltenhauptschlüssel verschlüsselt wurden. Das Entfernen der alten Werte stellt sicher, dass Sie bereit für den nächsten Rotationsvorgang sind (denken Sie daran, dass jeder Spaltenverschlüsselungsschlüssel, der mit einem zu rotierenden Spaltenhauptschlüssel geschützt wird, über genau einen verschlüsselten Wert verfügen muss).

Ein weiterer Grund dafür, den alten Wert vor dem Archivieren oder Entfernen des alten Spaltenhauptschlüssels zu bereinigen, ist die Leistung: Beim Abfragen einer verschlüsselten Spalte muss ein für Always Encrypted aktivierter Clienttreiber möglicherweise versuchen, zwei Werte zu entschlüsseln – den alten und den neuen Wert. Dem Treiber ist nicht bekannt, welcher der beiden Spaltenhauptschlüssel in der Umgebung der Anwendung gültig ist, weswegen der Treiber beide verschlüsselten Werte vom Server abruft. Wenn bei der Entschlüsselung eines der Werte ein Fehler auftritt, da er mit dem nicht verfügbaren Spaltenhauptschlüssel geschützt ist (wenn es z. B. der alte Spaltenhauptschlüssel ist, der aus dem Speicher entfernt wurde), versucht der Treiber einen anderen Wert mithilfe des neuen Spaltenhauptschlüssels zu entschlüsseln.

> [!WARNING]
> Wenn Sie den Wert eines Spaltenverschlüsselungsschlüssels entfernen, bevor der zugehörige Spaltenhauptschlüssel für eine Anwendung verfügbar gemacht wurde, kann die Anwendung die Datenbankspalte nicht mehr entschlüsseln.

1.  Navigieren Sie über den **Objekt-Explorer** zu dem Ordner **Sicherheit > Always Encrypted-Schlüssel**, und suchen Sie den vorhandenen Spaltenhauptschlüssel, den Sie ersetzen möchten.
2.  Klicken Sie mit der rechten Maustaste auf den vorhandenen Spaltenhauptschlüssel, und wählen Sie **Cleanup** aus.
3.  Überprüfen Sie die Liste der zu entfernenden Werte für den Spaltenhauptschlüssel.
4.  Klicken Sie auf **OK**.

SQL Server Management Studio gibt [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) -Anweisungen aus, um verschlüsselte Werte von Spaltenverschlüsselungsschlüsseln zu löschen, die mit dem alten Spaltenhauptschlüssel verschlüsselt wurden.

**Schritt 5: Löschen von Metadaten Ihres alten Spaltenhauptschlüssels**

Wenn Sie die Definition des alten Spaltenhauptschlüssels aus der Datenbank entfernen möchten, befolgen Sie diese Schritte. 
1.  Navigieren Sie über den **Objekt-Explorer** zu dem Ordner **Sicherheit > Always Encrypted-Schlüssel > Spaltenhauptschlüssel**, und suchen Sie den alten Spaltenhauptschlüssel, der aus der Datenbank entfernt werden soll.
2.  Klicken Sie mit der rechten Maustaste auf den alten Spaltenhauptschlüssel, und wählen Sie **Löschen** aus. (Dadurch wird eine [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) -Anweisung generiert und ausgegeben, die die Metadaten des Spaltenhauptschlüssels entfernt.)
3.  Klicken Sie auf **OK**.

> [!NOTE]
> Es wird dringend empfohlen, dass Sie den alten Spaltenhauptschlüssel nach der Rotation nicht dauerhaft löschen. Stattdessen sollten Sie den alten Spaltenhauptschlüssel im aktuellen Schlüsselspeicher oder an einem anderen sicheren Ort archivieren. Wenn Sie die Datenbank aus einer Sicherungsdatei auf einen Zeitpunkt vor der Konfiguration des neuen Spaltenhauptschlüssels wiederherstellen, benötigen Sie den alten Schlüssel für den Datenzugriff.

### <a name="permissions"></a>Berechtigungen

Die Rotation eines Spaltenhauptschlüssels erfordert die folgenden Berechtigungen:

- **ALTER ANY COLUMN MASTER KEY** – Für die Erstellung von Metadaten für den neuen Spaltenhauptschlüssel und die Löschung der Metadaten des alten Spaltenhauptschlüssels erforderlich.
- **ALTER ANY COLUMN ENCRYPTION KEY** – Für die Änderung der Metadaten von Spaltenverschlüsselungsschlüsseln erforderlich (neue verschlüsselte Werte hinzufügen).
- **VIEW ANY COLUMN MASTER KEY DEFINITION** – Für den Zugriff auf und das Lesen der Metadaten der Spaltenhauptschlüssel erforderlich.
- **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** – Für den Zugriff auf und das Lesen der Metadaten der Spaltenverschlüsselungsschlüssel erforderlich. 

Sie müssen sowohl auf den alten als auch auf den neuen Spaltenhauptschlüssel in ihren jeweiligen Schlüsselspeichern zugreifen können. Sie benötigen möglicherweise Berechtigungen für Schlüsselspeicher oder/und den Schlüssel, um auf einen Schlüsselspeicher zugreifen und einen Spaltenhauptschlüssel verwenden zu können:
- **Zertifikatspeicher – lokaler Computer** – Sie benötigen Lesezugriff auf das Zertifikat, das als Spaltenhauptschlüssel verwendet wird, oder Administratorrechte auf dem Computer.
- **Azure Key Vault** – Sie benötigen die Berechtigungen *create*, *get*, *unwrapKey*, *wrapKey*, *sign*und *verify* für den Tresor, der den bzw. die Spaltenhauptschlüssel enthält.
- **Schlüsselspeicheranbieter (CNG)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des KSP abhängen.
- **Kryptografiedienstanbieter (CSP)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des CSP abhängen.

Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>Rotieren von Spaltenverschlüsselungsschlüsseln

Die Rotation eines Spaltenverschlüsselungsschlüssels umfasst das Entschlüsseln der Daten in allen Spalten, die mit dem zu rotierenden Schlüssel verschlüsselt wurden, und die Neuverschlüsselung der Daten mithilfe des neuen Spaltenverschlüsselungsschlüssels.

>[!NOTE]
> Die Rotation eines Spaltenverschlüsselungsschlüssels kann sehr viel Zeit in Anspruch nehmen, wenn die Tabellen mit den Spalten, die mit dem zu rotierenden Schlüssel verschlüsselt wurden, groß ist. Während die Daten neu verschlüsselt werden, können Ihre Anwendungen nichts in die betroffenen Tabellen schreiben. Daher muss Ihre Organisation eine Rotation der Spaltenverschlüsselungsschlüssel sehr sorgfältig planen.
Verwenden Sie den Always Encrypted-Assistenten, um einen Spaltenverschlüsselungsschlüssel zu rotieren.

1.  Öffnen Sie den Assistenten für Ihre Datenbank: Klicken Sie mit der rechten Maustaste auf Ihre Datenbank, bewegen Sie den Mauszeiger zu **Aufgaben**, und klicken Sie auf **Spalten verschlüsseln**.
2.  Lesen Sie die Seite **Einführung** , und klicken Sie dann auf **Weiter**.
3.  Erweitern Sie auf der Seite **Spaltenauswahl** die Tabellen, und suchen Sie alle Spalten, die Sie ersetzen möchten und die derzeit mit dem alten Spaltenverschlüsselungsschlüssel verschlüsselt sind.
4.  Legen Sie **Verschlüsselungsschlüssel** für jede mit dem alten Verschlüsselungsschlüssel verschlüsselte Spalte auf einen neuen, automatisch generierten Schlüssel fest. **Hinweis:** Sie können alternativ auch vor dem Ausführen des Assistenten einen neuen Spaltenverschlüsselungsschlüssel erstellen. Weitere Informationen finden Sie im obigen Abschnitt *Bereitstellen von Spaltenverschlüsselungsschlüsseln* .
5.  Wählen Sie auf der Seite **Konfiguration des Hauptschlüssels** einen Speicherort für den neuen Schlüssel aus, wählen Sie eine Hauptschlüsselquelle aus, und klicken Sie anschließend auf **Weiter**. **Hinweis:** Wenn Sie einen vorhandenen Spaltenverschlüsselungsschlüssel verwenden (keinen automatisch generierten), können Sie diesen Schritt überspringen.
6.  Wählen Sie auf der **Überprüfungsseite**aus, ob das Skript sofort ausgeführt oder ob ein PowerShell-Skript erstellt werden soll, und klicken Sie anschließend auf **Weiter**.
7.  Überprüfen Sie die ausgewählten Optionen auf der Seite **Zusammenfassung** , klicken Sie anschließend auf **Fertig stellen** , und schließen Sie den Assistenten, wenn Sie alle Schritte ausgeführt haben.
8.  Navigieren Sie über den **Objekt-Explorer**zu dem Ordner **Sicherheit &gt; Always Encrypted-Schlüssel &gt; Spaltenverschlüsselungsschlüssel** , und suchen Sie Ihren alten Spaltenverschlüsselungsschlüssel, der aus der Datenbank entfernt werden soll. Klicken Sie mit der rechten Maustaste auf den Schlüssel, und wählen Sie anschließend **Löschen**aus.

### <a name="permissions"></a>Berechtigungen

Die Rotation eines Spaltenverschlüsselungsschlüssels erfordert die **ALTER ANY COLUMN MASTER KEY** -Berechtigungen – Für die Verwendung eines neuen, automatisch generierten Spaltenverschlüsselungsschlüssels erforderlich (ein neuer Spaltenhauptschlüssel und die neuen, dazugehörigen Metadaten werden ebenfalls generiert).
**ALTER ANY COLUMN ENCRYPTION KEY** – Für das Hinzufügen von Metadaten für den neuen Spaltenverschlüsselungsschlüssel erforderlich.
**VIEW ANY COLUMN MASTER KEY DEFINITION** – Für den Zugriff auf und das Lesen der Metadaten der Spaltenhauptschlüssel erforderlich.
**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** – Für den Zugriff auf und das Lesen der Metadaten der Spaltenverschlüsselungsschlüssel erforderlich.

Sie müssen sowohl für den alten als auch für den neuen Spaltenverschlüsselungsschlüssel auf den Spaltenhauptschlüssel zugreifen können. Sie benötigen möglicherweise Berechtigungen für Schlüsselspeicher oder/und den Schlüssel, um auf einen Schlüsselspeicher zugreifen und einen Spaltenhauptschlüssel verwenden zu können:
- **Zertifikatspeicher – lokaler Computer** – Sie benötigen einen Lesezugriff auf das Zertifikat, das als Spaltenhauptschlüssel verwendet wird, oder Administratorrechte auf dem Computer.
- **Azure Key Vault** – Sie benötigen die Berechtigungen „get“, „unwrapKey“, und „verify“ für den Tresor, der den Spaltenhauptschlüssel enthält.
- **Schlüsselspeicheranbieter (CNG)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des KSP abhängen.
- **Kryptografiedienstanbieter (CSP)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des CSP abhängen.

Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>Ausführen von DAC-Upgradevorgängen, wenn die Datenbank oder die DACPAC-Datei Always Encrypted verwendet

[DAC-Vorgänge](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) werden für DACPAC-Dateien und Datenbanken mit Schemas unterstützt, die verschlüsselte Spalten enthalten. Bei den Upgradevorgängen von DACs gibt es Besonderheiten zu beachten: Weitere Informationen zu DAC-Upgrades in verschiedenen Tools, einschließlich SSMS, finden Sie unter [Upgrade einer Datenebenenanwendung](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) . 

Beim Upgrade einer Datenbank mithilfe einer DACPAC-Datei, wobei entweder die DACPAC-Datei oder die Zieldatenbank über verschlüsselte Spalten verfügt, wird ein Datenverschlüsselungsvorgang ausgelöst, wenn alle der folgenden Bedingungen zutreffen:
- Die Datenbank enthält eine Datenspalte.
- Dieselbe Spalte ist in der DACPAC-Datei vorhanden.
- Die Verschlüsselungskonfiguration der Spalte in der Datenbank unterscheidet sich von der Konfiguration der entsprechenden Spalte in der DACPAC-Datei. Ausführlichere Informationen finden Sie in der folgenden Tabelle.

| Bedingung|Aktion|
|:---|:---|
|Die Spalte wird in der DACPAC-Datei verschlüsselt, nicht in der Datenbank.| Die Daten in der Spalte werden verschlüsselt.|
|Die Spalte wird nicht in der DACPAC-Datei verschlüsselt, sondern in der Datenbank.| Die Daten in der Spalte werden entschlüsselt (die Verschlüsselung wird für die Spalte entfernt).|
| Die Spalte wird sowohl in der DACPAC-Datei als auch in der Datenbank verschlüsselt. Allerdings verwendet die Spalte in der DACPAC-Datei einen anderen Verschlüsselungstyp und/oder einen Spaltenverschlüsselungsschlüssel als die entsprechende Spalte in der Datenbank.|Die Daten in der Spalte werden entschlüsselt und anschließend neu verschlüsselt, damit sie der Verschlüsselungskonfiguration in DACPAC-Datei entsprechen.|

> [!NOTE]
> Ist der für die Spalte in der Datenbank oder in der DACPAC-Datei konfigurierte Spaltenhauptschlüssel in Azure Key Vault gespeichert, müssen Sie sich in Azure anmelden (wenn sie nicht bereits angemeldet sind).

### <a name="permissions"></a>Berechtigungen

Je nach den Unterschieden zwischen den Schemas der DACPAC-Datei und der Zieldatenbank benötigen Sie eventuell einige oder alle der unten aufgeführten Berechtigungen, um ein DAC-Upgrade auszuführen, wenn Always Encrypted in der DACPAC-Datei oder in der Zieldatenbank eingerichtet ist.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

Wenn der Upgradevorgang eine Datenverschlüsselung auslöst, müssen Sie auch auf die für die betroffenen Spalten konfigurierten Spaltenhauptschlüssel zugreifen können:
- **Zertifikatspeicher – lokaler Computer** – Sie benötigen Lesezugriff auf das Zertifikat, das als Spaltenhauptschlüssel verwendet wird, oder Administratorrechte auf dem Computer.
- **Azure Key Vault** – Sie benötigen die Berechtigungen *create*, *get*, *unwrapKey*, *wrapKey*, *sign*und *verify* für den Tresor, der den Spaltenhauptschlüssel enthält.
- **Schlüsselspeicheranbieter (CNG)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des KSP abhängen.
- **Kryptografiedienstanbieter (CSP)** – Bei der Verwendung eines Schlüsselspeichers oder Schlüssels werden Sie möglicherweise aufgefordert, die erforderlichen Berechtigungen und Anmeldeinformationen anzugeben, welche von der Konfiguration des Speichers und des CSP abhängen.

Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>Migrieren von Datenbanken mit verschlüsselten Spalten mithilfe von BACPAC-Dateien

Beim Exportieren einer Datenbank werden alle in verschlüsselten Spalten gespeicherten Daten abgerufen und (verschlüsselt) in der resultierenden [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) -Datei abgelegt. Die resultierende BACPAC-Datei enthält außerdem die Metadaten der Always Encrypted-Schlüssel.

Wenn Sie eine BACPAC-Datei in eine Datenbank importieren, werden die verschlüsselten Daten der BACPAC-Datei ebenso in die Datenbank geladen, und die Metadaten der Always Encrypted-Schlüssel werden neu erstellt.

Wenn eine Anwendung dazu konfiguriert ist, die verschlüsselten Daten in der Quelldatenbank (die, die Sie exportiert haben) zu ändern oder abzurufen, können Sie die Anwendung ganz einfach für Abfragen der verschlüsselten Daten in der Zieldatenbank aktivieren, da die Schlüssel in beiden Datenbanken identisch sind.


### <a name="permissions"></a>Berechtigungen

Sie benötigen für die Quelldatenbank die Berechtigungen *ALTER ANY COLUMN MASTER KEY* und *ALTER ANY COLUMN ENCRYPTION KEY* . Sie benötigen für die Zieldatenbank die Berechtigungen *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*und *VIEW ANY COLUMN ENCRYPTION* .

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>Migrieren von Datenbanken mit verschlüsselten Spalten mithilfe des SQL Server-Import/Export-Assistenten

Im Vergleich zur Verwendung von BACPAC-Dateien bietet Ihnen der [SQL Server-Import / Export-Assistent](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) mehr Kontrolle über den Umgang mit Daten in verschlüsselten Spalten während der Datenmigration.

- Wenn es sich bei Ihrer Datenquelle um eine Datenbank handelt, die Always Encrypted verwendet, können Sie die Verbindung mit der Datenquelle so konfigurieren, dass die Daten in den verschlüsselten Spalten während des Exportvorgangs entweder entschlüsselt werden oder verschlüsselt bleiben.
- Wenn es sich bei Ihrem Datenziel um eine Datenbank handelt, die Always Encrypted verwendet, können Sie Ihre Datenzielverbindung so konfigurieren, dass Daten, die in verschlüsselte Spalten geschrieben werden sollen, verschlüsselt werden.

Sie müssen die Verbindung mit Ihrer Datenquelle/Ihrem Datenziel so konfigurieren, dass sie den [.Net Framework-Datenanbieter für SqlServer](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) verwendet, und Sie müssen die Verbindungszeichenfolgenkennwörter in der Spaltenverschlüsselungseinstellung auf *Aktiviert*festlegen, um die Entschlüsselung (für die Datenquelle) oder die Verschlüsselung (für das Datenziel) zu aktivieren.

Die folgende Tabelle führt mögliche Migrationsszenarios auf und zeigt, wie sie mit Always Encrypted und den Konfigurationen der Datenquelle und des Datenziels für jede Verbindung in Zusammenhang stehen.

| Szenario|Die Konfiguration der Quellverbindung| Die Konfiguration der Zielverbindung
|:---|:---|:---
|Verschlüsseln von Daten bei der Migration (die Daten werden als Klartext in der Datenquelle gespeichert und zu verschlüsselten Spalten im Datenziel migriert).| Datenanbieter/Treiber: *Alle*<br><br>Column Encryption Setting=Disabled<br><br>(wenn der .NET Framework-Datenanbieter für SqlServer und .NET Framework 4.6 oder höher verwendet wird) | Datenanbieter/Treiber: *.Net Framework-Datenanbieter für SqlServer* (.NET Framework 4.6 oder höher erforderlich)<br><br>Column Encryption Setting=Enabled
| Entschlüsseln von Daten bei der Migration (die Daten werden in verschlüsselten Spalten in der Datenquelle gespeichert und als Klartext zum Datenziel migriert; wenn das Datenziel eine Datenbank ist, werden die Zielspalten nicht verschlüsselt).<br><br>**Hinweis:** Die Zieltabellen mit den verschlüsselten Spalten müssen vor der Migration vorhanden sein.|Datenanbieter/Treiber: *.Net Framework-Datenanbieter für SqlServer* (.NET Framework 4.6 oder höher erforderlich)<br><br>Weitere Eigenschaften|Datenanbieter/Treiber: *Alle*<br><br>Column Encryption Setting=Disabled<br><br>(wenn der .NET Framework-Datenanbieter für SqlServer und .NET Framework 4.6 oder höher verwendet wird)
|Neuverschlüsseln von Daten bei der Migration (die Daten werden in verschlüsselten Spalten in der Datenquelle gespeichert und als Klartext zum Datenziel in die Spalten migriert, die andere Verschlüsselungstypen für Spaltenverschlüsselungsschlüsseln verwenden).<br><br>**Hinweis:** Die Zieltabellen mit den verschlüsselten Spalten müssen vor der Migration vorhanden sein.| Datenanbieter/Treiber: *.Net Framework-Datenanbieter für SqlServer* (.NET Framework 4.6 oder höher erforderlich)<br><br>Weitere Eigenschaften|Datenanbieter/Treiber: *.Net Framework-Datenanbieter für SqlServer* (.NET Framework 4.6 oder höher erforderlich)<br><br>Weitere Eigenschaften
|Verschieben von verschlüsselten Daten ohne sie zu entschlüsseln.<br><br>**Hinweis:** Die Zieltabellen mit den verschlüsselten Spalten müssen vor der Migration vorhanden sein.| Datenanbieter/Treiber: *Alle*<br>Column Encryption Setting=Disabled<br><br>(wenn der .NET Framework-Datenanbieter für SqlServer und .NET Framework 4.6 oder höher verwendet wird)| Datenanbieter/Treiber: *Alle*<br>Column Encryption Setting=Disabled<br><br>(wenn der .NET Framework-Datenanbieter für SqlServer und .NET Framework 4.6 oder höher verwendet wird)<br><br>Der Benutzer muss ALLOW_ENCRYPTED_VALUE_MODIFICATIONS auf ON festgelegt haben.<br><br>Weitere Informationen finden Sie unter [Migrieren von durch Always Encrypted geschützten sensiblen Daten](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).


### <a name="permissions"></a>Berechtigungen

Sie müssen in der Quelldatenbank über die Berechtigungen **VIEW ANY COLUMN MASTER KEY DEFINITION** und **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** verfügen, um Daten in der Quelldatenbank *verschlüsseln* oder *entschlüsseln* zu können.

Außerdem benötigen Sie Zugriff auf die Spaltenhauptschlüssel, die für die Spalten konfiguriert wurden, in denen die zu ver- oder entschlüsselnden Daten gespeichert sind:
- **Zertifikatspeicher – lokaler Computer** – Sie benötigen einen Lesezugriff auf das Zertifikat, das als Spaltenhauptschlüssel verwendet wird, oder Administratorrechte auf dem Computer.
- **Azure Key Vault** – Sie benötigen die Berechtigungen „get“, „unwrapKey“, „wrapKey“, „sign“ und „verify“ für den Tresor mit dem Spaltenhauptschlüssel.
- **Schlüsselspeicheranbieter (Cryptography Next Generation; CNG)** – Die erforderlichen Berechtigungen und Anmeldeinformationen, zu deren Eingabe Sie möglicherweise aufgefordert werden, wenn Sie einen Schlüsselspeicher oder einen Schlüssel verwenden, hängen von der Konfiguration des Speichers und des Schlüsselspeicheranbieters (key storage provider; KSP) ab.
- **Kryptografiedienstanbieter (Kryptografie-API)** – Die erforderlichen Berechtigungen und Anmeldeinformationen, zu deren Eingabe Sie möglicherweise aufgefordert werden, wenn Sie einen Schlüsselspeicher oder einen Schlüssel verwenden, hängen von der Konfiguration des Speichers und des Kryptografiedienstanbieters (cryptographic service provider; CSP) ab.
Weitere Informationen finden Sie unter [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)).

## <a name="see-also"></a>Siehe auch
- [Always Encrypted (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted-Assistent](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Übersicht über die Schlüsselverwaltung für Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted (Cliententwicklung)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [Konfigurieren von Always Encrypted mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)













