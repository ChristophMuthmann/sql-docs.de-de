---
title: ODBC-Glossar | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], glossary
- glossary [ODBC]
ms.assetid: e8227000-1944-42e5-a881-1f549e1ff9d1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a3f6211095c5f2a1506b31ca45846c15deb619b2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-glossary"></a>ODBC-Glossar
## <a name="a"></a>Ein  
 **Zugriffsplan**  
 Ein Plan, durch das Datenbankmodul generierte eine SQL­Anweisung ausführen. Entspricht dem ausführbaren Code kompiliert, die in einer anderen Sprache wie z. B. c dritten generation  
  
 **Aggregate-Funktion**  
 Eine Funktion, die einen einzelnen Wert aus einer Gruppe von Werten, die mit häufig verwendeten generiert **GROUP BY** und **HAVING** Klauseln. Aggregatfunktionen **AVG**, **Anzahl**, **MAX**, **MIN**, und **Summe**. Auch bekannt als *Mengenfunktionen*. *Siehe auch* Skalarfunktion.  
  
 **ANSI**  
 American National Standards Institute. Die ODBC-API basiert auf der ANSI-Call-Level-Schnittstelle.  
  
 **APD**  
 *Finden Sie unter* anwendungsparameterdeskriptor (APD).  
  
 **API**  
 Application Programming Interface. Ein Satz von Routinen, die eine Anwendung zum Anfordern und Ausführen von Diensten niedrigerer Ebene verwendet. Die ODBC-API besteht aus der ODBC-Funktionen.  
  
 **Anwendung**  
 Ein ausführbares Programm, das Funktionen der ODBC-API aufruft.  
  
 **anwendungsparameterdeskriptor (APD)**  
 Ein Deskriptor, der beschreibt, die dynamischen Parameter in einer SQL-Anweisung vor der Konvertierung angegeben, die von der Anwendung verwendet.  
  
 **Zeile Anwendungsdiensts (ARD)**  
 Ein Deskriptor, der Metadaten und Daten in die Anwendung Puffer, die eine Zeile mit Daten, die nach der Datenkonvertierung von der Anwendung angegebenes beschreibt darstellt.  
  
 **ARD**  
 *Finden Sie unter* Zeile Anwendungsdiensts (ARD).  
  
 **Autocommit-Modus**  
 Eine Commit-Transaktionsmodus, in dem eine Transaktionen ein Commit ausgeführt werden, sofort, nachdem sie ausgeführt werden.  
  
## <a name="b"></a>B  
 **verhaltensänderung**  
 Eine Änderung in bestimmte Funktionen von ODBC 3.*.x* Verhalten mit ODBC 2..* X* Verhalten, oder umgekehrt. Durch Ändern des Attributs Umgebung SQL_ATTR_ODBC_VERSION verursacht.  
  
 **Binary large Object (BLOB)**  
 Alle Binärdaten über eine bestimmte Anzahl von Bytes, beispielsweise 255. In der Regel wesentlich länger. Diese Daten in der Regel an gesendet und abgerufen, die aus der Datenquelle in Teilen. Auch bekannt als *long-Daten*.  
  
 **Bindung**  
 Verb, das Act eine Spalte in einem Resultset oder ein Parameter in einer SQL­Anweisung mit einer Anwendungsvariablen zu verknüpfen. Als ein Nomen, die Zuordnung.  
  
 **Offset der Bindung**  
 Ein Wert, der auf die Daten Puffer und Längenindikator/Puffer Adressen hinzugefügt werden, für alle Spalten- oder Parameternamen Daten erzeugen neue Adressen gebunden.  
  
 **Blockcursor**  
 Ein Cursor kann mehr als eine Zeile mit Daten zu einem Zeitpunkt abrufen.  
  
 **Puffer**  
 Ein Codesegment Anwendungsspeicher verwendet, um Daten zwischen der Anwendung und den Treiber übergeben. Sind Puffer häufig einander paarweise zugeordnet: ein *Datenpuffer* und ein *Länge Datenpuffer*.  
  
 **Byte**  
 Acht Bits oder ein Oktett. *Siehe auch* Oktett.  
  
## <a name="c"></a>C  
 **C-Datentyp**  
 Der Datentyp einer Variablen in einem C-Programm in diesem Fall die Anwendung.  
  
 **Katalog**  
 Der Satz von Systemtabellen in einer Datenbank, die die Form der Datenbank zu beschreiben. Auch bekannt als ein *Schema* oder *Datenwörterbuch*.  
  
 **Katalogfunktion**  
 Eine ODBC-Funktion zum Abrufen von Informationen aus der Datenbank-Katalog verwendet wird.  
  
 **CLI**  
 *Finden Sie unter* API.  
  
 **Client/server**  
 Eine Datenbank-Zugriffsmethode, in denen eine oder mehrere Clients Daten über einen Server zugreifen. Die Clients implementieren normalerweise die Benutzeroberfläche während der Serversteuerelemente Access-Datenbank.  
  
 **Spalte**  
 Der Container für ein einzelnes Element der Informationen in einer Zeile. Auch bekannt als *Feld*.  
  
 **Commit**  
 Um die Änderungen in einer Transaktion permanent zu machen.  
  
 **Parallelität**  
 Die Fähigkeit von mehr als eine Transaktion, die Zugriff auf die gleichen Daten zur gleichen Zeit.  
  
 **Konformitätsgrad**  
 Einen diskreten Satz von Funktionen, die durch einen Treiber oder eine Datenquelle unterstützt. ODBC definiert Übereinstimmungsebenen API und SQL-Übereinstimmungsebenen.  
  
 **Verbindung**  
 Eine bestimmte Instanz einer Treiber und die Datenquelle.  
  
 **Verbindung zu durchsuchen**  
 Suchen das Netzwerk für die Datenquellen für die Verbindung an. Durchsuchen von Verbindung möglicherweise mehrere Schritte umfassen. Beispielsweise kann der Benutzer zunächst das Netzwerk nach Servern durchsuchen und navigieren Sie dann auf einen bestimmten Server für eine Datenbank.  
  
 **Verbindungshandles**  
 Ein Handle für eine Datenstruktur, die Informationen über eine Verbindung enthält.  
  
 **aktuelle Zeile**  
 Die Zeile, die derzeit vom Cursor verweist. Positionierte Operationen wirken sich auf die aktuelle Zeile.  
  
 **Cursor**  
 Eine Softwarekomponente, die Zeilen von Daten an die Anwendung zurückgibt. Wahrscheinlich die nach der blinkender Cursor auf einem Computer terminal benannt werden. genauso Cursor zeigt die aktuelle Position auf dem Bildschirm, ein Cursor für ein Resultset gibt die aktuelle Position im Resultset an.  
  
## <a name="d"></a>D  
 **Datenpuffer**  
 Ein Puffer, der zum Übergeben von Daten verwendet wird. Häufig mit einem Puffer ist ein *Länge Datenpuffer*.  
  
 **Datenwörterbuch**  
 *Finden Sie unter* Katalog.  
  
 **Länge des Datenpuffers**  
 Ein Puffer verwendet, um die Länge des Werts in ein entsprechendes übergeben *Datenpuffer*. Der Datenpuffer Länge dient auch zum Speichern von Indikatoren, z. B., ob der Datenwert Null-terminiert ist.  
  
 **Datenquelle**  
 Die Daten, die der Benutzer Zugriff und seiner zugeordneten Operating System, DBMS und Netzwerkplattform (sofern vorhanden) möchte.  
  
 **Datentyp**  
 Der Typ der Daten. ODBC definiert C und SQL-Datentypen. *Siehe auch* "Typindikator".  
  
 **Data-at-Execution-Spalte**  
 Eine Spalte für die Daten, nach dem gesendet werden **SQLSetPos** aufgerufen wird. Bezeichnung stammt daher, weil die Daten auf, die in einem Rowset Puffer platziert wird, statt Ausführungszeit gesendet werden. Long-Daten werden im Allgemeinen in Teilen zum Zeitpunkt der Ausführung gesendet.  
  
 **Data-at-Execution-parameter**  
 Ein Parameter für die Daten, nach dem gesendet werden **SQLExecute** oder **SQLExecDirect** aufgerufen wird. Die Bezeichnung stammt daher, da die Daten gesendet werden, wenn die SQL-Anweisung ausgeführt wird, anstatt in einem Parameterpuffer platziert wird. Long-Daten werden im Allgemeinen in Teilen zum Zeitpunkt der Ausführung gesendet.  
  
 **database**  
 Eine separate Auflistung von Daten in einem DBMS. Auch ein DBMS.  
  
 **Datenbankmodul**  
 Die Software in einem DBMS, der analysiert und SQL-Anweisungen ausgeführt und greift auf die physischen Daten.  
  
 **DBMS**  
 Datenbank-Managementsystem. Eine Softwareebene zwischen der physischen Datenbank und dem Benutzer. Das DBMS dient zur Verwaltung des gesamten Zugriffs auf die Datenbank.  
  
 **DBMS-basierten Treiber**  
 Ein Treiber, der physische Daten über ein eigenständiges Datenbankmodul zugreift.  
  
 **DDL**  
 Die Datendefinitionssprache. Diese Anweisungen in SQL, die im Gegensatz zum Bearbeiten von Daten definieren. Beispielsweise **CREATE TABLE**, **CREATE INDEX**, **GRANT**, und **widerrufen**.  
  
 **Begrenzungsbezeichner**  
 Ein Bezeichner, der in Anführungszeichen Bezeichner eingeschlossen ist, damit können Sonderzeichen enthalten oder Schlüsselwörtern (auch bekannt als aus einem Bezeichner in Anführungszeichen) entsprechen.  
  
 **der Deskriptor**  
 Eine Datenstruktur, die Informationen zum Spaltendaten oder dynamische Parameter enthält. Die physikalische Darstellung des Deskriptors ist nicht definiert. Anwendungen erhalten direkten Zugriff auf ein Deskriptor, der nur durch ihre Felder durch Aufrufen von ODBC-Funktionen mit dem Deskriptorhandles bearbeiten.  
  
 **Desktop-Datenbank**  
 Ein DBMS auf einem Computer ausgeführt werden sollen. Im Allgemeinen wird diese DBMS bieten kein eigenständiges Datenbankmodul und müssen über einen dateibasierten-Treiber zugegriffen werden. Die Module in dieser Treiber eingeschränkte Unterstützung für SQL und Transaktionen in der Regel. Z. B. dBASE, Paradox, Btrieve oder Microsoft® FoxPro.  
  
 **Diagnose**  
 Ein Datensatz mit Diagnoseinformationen über die letzte Funktion aufgerufen wird, verwendet ein bestimmtes Handle. DiagnoseDatensätze sind Umgebung, Verbindungs-, Anweisung und Deskriptorhandles zugeordnet.  
  
 **DML**  
 Data Manipulation Language. Diese Anweisungen in SQL, die im Gegensatz um zu definieren, Daten zu bearbeiten. Beispielsweise **einfügen**, **UPDATE**, **löschen**, und **wählen**.  
  
 **Treiber**  
 Eine Routine-Bibliothek, die die Funktionen der ODBC-API verfügbar macht. Treiber sind spezifisch für eine einzelnes DBMS.  
  
 **Treiber-Manager**  
 Eine Routine-Bibliothek, die Zugriff auf den Treiber für die Anwendung verwaltet. Der Treiber-Manager geladen und entladen wird (oder eine Verbindung mit her, und trennt) Aufrufe Treiber und übergibt an die ODBC-Funktionen, um die richtigen Treiber.  
  
 **Treiber-Setup-DLL**  
 Eine DLL, treiberspezifische Funktionen für Installation und Konfiguration enthält.  
  
 **Dynamische cursor**  
 Einen bildlauffähigen Cursor kann aktualisiert, gelöscht oder eingefügt werden, in das Resultset Zeilen zu ermitteln.  
  
 **Dynamische SQL-Anweisungen**  
 Ein Typ von embedded SQL-Anweisungen sind in dem SQL erstellt und zur Laufzeit kompiliert. *Siehe auch* statischen SQL.  
  
## <a name="e"></a>E  
 **Embedded SQL**  
 SQL-Anweisungen, die direkt in einem in einer anderen Sprache, z. B. COBOL oder ODBC c-Programm enthalten sind embedded SQL nicht verwendet. *Siehe auch* statischen SQL *und* dynamischem SQL.  
  
 **Umgebung**  
 Einem globalen Kontext, in dem auf Daten zugegriffen; die Umgebung zugeordnet ist alle Informationen, die ihrem Wesen her, z. B. eine Liste aller Verbindungen in dieser Umgebung global ist.  
  
 **Umgebungshandles**  
 Ein Handle für eine Datenstruktur, die Informationen über die Umgebung enthält.  
  
 **ESCAPE-Klausel**  
 Eine Klausel in einer SQL-Anweisung.  
  
 **Führen Sie**  
 Um eine SQL­Anweisung ausführen.  
  
## <a name="f"></a>V  
 **FAT cursor**  
 *Finden Sie unter* Blockcursor.  
  
 **Abrufen von Daten**  
 Um eine oder mehrere Zeilen aus einem Resultset abgerufen werden.  
  
 **Feld**  
 *Finden Sie unter* Spalte.  
  
 **dateibasierte-Treiber**  
 Ein Treiber, der direkt auf physischen Daten zugreift. In diesem Fall wird der Treiber ein Datenbankmodul enthält und als Treiber und Datenquelle fungiert.  
  
 **Datei als Datenquelle**  
 Eine Datenquelle, für welche, die Verbindung Informationen in einem DSN-Datei gespeichert werden.  
  
 **Fremdschlüssel**  
 Eine Spalte oder Spalten in einer Tabelle, die den Primärschlüssel in einer anderen Tabelle entsprechen.  
  
 **Vorwärtscursor**  
 Ein Cursor, der nur über das Resultset und im Allgemeinen weitergehen kann dadurch nur eine Zeile zu einem Zeitpunkt. Die meisten relationalen Datenbanken unterstützen nur Vorwärtscursor.  
  
## <a name="h"></a>H  
 **Handle**  
 Ein Wert, der eindeutig etwas wie z. B. eine Datei oder eine Struktur identifiziert. Handles sind sinnvoll, nur für die Software, die erstellt und verwendet sie jedoch durch eine andere Software zur Identifizierung der Dinge übergeben werden. ODBC definiert Handles für Umgebungen, Verbindungen, Anweisungen und Deskriptoren.  
  
## <a name="i"></a>I  
 **Implementation Parameter Descriptor, (IPD)**  
 Ein Deskriptor, der beschreibt, die dynamischen Parameter in einer SQL­Anweisung nach der Konvertierung von der Anwendung spezifiziertes verwendet.  
  
 **Implementierungszeilendeskriptor (IRD)**  
 Ein Deskriptor, der eine Zeile mit Daten vor der Konvertierung angegeben, die von der Anwendung beschreibt.  
  
 **Installer DLL**  
 Eine DLL, die ODBC-Komponenten installiert und konfiguriert Datenquellen.  
  
 **Integritätserweiterungsfunktion**  
 Eine Teilmenge von SQL Server entwickelt, um die Integrität einer Datenbank zu verwalten.  
  
 **Schnittstelle Konformitätsgrad**  
 Das Maß an die ODBC-3.7-Schnittstelle, die durch einen Treiber unterstützt; Core, Ebene 1 oder Ebene 2 möglich.  
  
 **Interoperabilität**  
 Die Fähigkeit eines einer Anwendung in den gleichen Code verwenden, beim Zugriff auf Daten in anderen DBMS.  
  
 **IPD**  
 *Finden Sie unter* Implementation Parameter Descriptor (Implementierungsparameterdeskriptor, Implementierungszeilendeskriptor).  
  
 **IRD**  
 *Finden Sie unter* Implementierung Zeilendeskriptor (IRD).  
  
 **ISO/IEC**  
 Internationale Normen Organisation/Internationale elektrotechnische Kommission. Die ODBC-API basiert auf dem ISO/IEC Call-Level-Schnittstelle.  
  
## <a name="j"></a>J  
 **Join**  
 Ein Vorgang in einer relationalen Datenbank, die die Zeilen in zwei oder mehr Tabellen verknüpft, von übereinstimmenden Werten in angegebenen Spalten.  
  
## <a name="k"></a>K  
 **Schlüssel**  
 Eine Spalte oder Spalten, deren Werte eine Zeile zu identifizieren. *Siehe auch* Fremdschlüssel *und* Primärschlüssel.  
  
 **Keyset**  
 Ein Satz von Schlüsseln, die von einem gemischten oder keysetgesteuerte Cursor verwendet, um Zeilen erneut abzurufen.  
  
 **Keysetgesteuerte cursor**  
 Einen bildlauffähigen Cursor, der aktualisierte und gelöschte Zeilen erkennt, mit der ein Keyset.  
  
## <a name="l"></a>L  
 **Zeichenfolgenliterale**  
 Eine zeichendarstellung der einen Datenwert in einer SQL­Anweisung.  
  
 **Sperren**  
 Der Prozess, mit dem ein DBMS den Zugriff auf eine Zeile in einer mehrbenutzerumgebung beschränkt. DBMS in der Regel legt ein bit auf eine Zeile oder die physische Seite mit je einer Zeile, die die Zeile angibt, oder Seite gesperrt ist.  
  
 **Long-Daten**  
 Binär- oder Zeichendatentypen Daten über eine bestimmte Länge, z. B. 255 Bytes oder Zeichen. In der Regel wesentlich länger. Diese Daten in der Regel an gesendet und abgerufen, die aus der Datenquelle in Teilen. Auch bekannt als *BLOB*s oder *CLOB*s.  
  
## <a name="m"></a>M  
 **Computer-Datenquelle**  
 Eine Datenquelle, für welche, die Verbindung Informationen auf dem System (z. B. der Registrierung) gespeichert werden.  
  
 **Manualcommit-Modus**  
 Eine Transaktion Commit-Modus in der Transaktionen explizit Ausführen von werden durch den Aufruf Commits müssen **SQLTransact**.  
  
 **Metadaten**  
 Daten, die einen Parameter in einer SQL­Anweisung oder eine Spalte in einem Resultset zu beschreiben. Z. B. Datentyp, Länge und Genauigkeit eines Parameters.  
  
 **Treiber mit mehreren Ebenen**  
 *Finden Sie unter* DBMS-basierten Treiber.  
  
## <a name="n"></a>N  
 **NULL-Wert**  
 Kann keine explizit zugewiesenen Wert an. Insbesondere unterscheidet sich ein NULL-Wert von NULL oder leer.  
  
## <a name="o"></a>O  
 **Oktett**  
 Acht Bits oder ein Byte. *Siehe auch* Byte.  
  
 **Oktettlänge**  
 Die Länge in Oktetten einen Puffer oder die darin enthaltenen Daten.  
  
 **ODBC**  
 Open Sie Database Connectivity. Eine Spezifikation für eine API, die einen Standardsatz von Routinen definiert, mit denen eine Anwendung Daten in einer Datenquelle zugreifen kann.  
  
 **ODBC-Administrator**  
 Ein ausführbares Programm, das Installationsprogramm DLL zum Konfigurieren von Datenquellen aufruft.  
  
 Gruppe öffnen  
 Ein Unternehmen, das Standards veröffentlicht. Insbesondere, veröffentlicht er SQL Zugriff Gruppe (SAG)-Standards.  
  
 **vollständige Parallelität**  
 Eine Strategie zum Parallelität zu erhöhen, in denen Zeilen nicht gesperrt werden. Bevor sie aktualisiert oder gelöscht werden, überprüft ein Cursor stattdessen, um festzustellen, ob sie geändert wurden, seit sie zuletzt gelesen wurden. Wenn dies der Fall ist, schlägt die Update- oder Delete. *Siehe auch* eingeschränkte Parallelität.  
  
 **Äußerer join**  
 Ein join, bei die entsprechenden und nicht übereinstimmenden Zeilen zurückgegeben werden. Die Werte aller Spalten aus der nicht übereinstimmenden Tabelle in der nicht übereinstimmenden Zeilen werden auf NULL festgelegt.  
  
 **Besitzer**  
 Der Besitzer einer Tabelle.  
  
## <a name="p"></a>P  
 **Parameter**  
 Eine Variable in einer SQL­Anweisung mit einer parametermarkierung oder Fragezeichen (?) markiert. Parameter werden an Anwendungsvariablen und ihre Werte abgerufen, wenn die Anweisung ausgeführt wird, gebunden.  
  
 **Parameterdeskriptor**  
 Ein Deskriptor, der beschreibt, die zur Laufzeit-Parameter, die in einer SQL­Anweisung entweder vor der Konvertierung angegeben, von der Anwendung (ein anwendungsparameterdeskriptor oder APD) oder nach der Konvertierung angegeben, die von der Anwendung (Implementierung verwendet Parameterdeskriptor oder IPD).  
  
 **Parameterarray-Vorgang**  
 Ein Array mit Werten, die eine Anwendung festgelegt werden können, um anzugeben, dass der entsprechende Parameter sollen, in ignoriert werden einer **SQLExecDirect** oder **SQLExecute** Vorgang.  
  
 **Parameterarray-status**  
 Ein Array mit den Status eines Parameters nach einem Aufruf von **SQLExecDirect** oder **SQLExecute**.  
  
 **die eingeschränkte Parallelität**  
 Eine Strategie zum Implementieren der Serialisierbarkeit, in dem Zeilen gesperrt werden, sodass andere Transaktionen, die sie ändern können. *Siehe auch* vollständige Parallelität *und* Serialisierbarkeit.  
  
 **positionierte operation**  
 Jeder Vorgang, der für die aktuelle Zeile fungiert. Beispielsweise positioniert Update und delete-Anweisungen, **SQLGetData**, und **SQLSetPos**.  
  
 **positionierte Update-Anweisung**  
 Eine SQL-Anweisung verwendet, um die Werte in der aktuellen Zeile zu aktualisieren.  
  
 **positionierte Delete-Anweisung**  
 Eine SQL-Anweisung verwendet, um die aktuelle Zeile zu löschen.  
  
 **Vorbereiten**  
 Um eine SQL-Anweisung zu kompilieren. Ein Plans wird erstellt, indem eine SQL-Anweisung wird vorbereitet.  
  
 **Primärschlüssel**  
 Eine Spalte oder Spalten, die eine Zeile in einer Tabelle eindeutig identifiziert.  
  
 **Prozedur**  
 Eine Gruppe von eine oder mehrere vorkompilierte SQL-Anweisungen, die als ein benanntes Objekt in einer Datenbank gespeichert sind.  
  
 **Prozedurspalte**  
 Ein Argument in einem Prozeduraufruf, den Rückgabewert von einer Prozedur oder eine Spalte in einem Resultset, das von einer Prozedur erstellt.  
  
## <a name="q"></a>Q  
 **Qualifizierer**  
 Eine Datenbank, die eine oder mehrere Tabellen enthält.  
  
 **Abfrage**  
 Eine SQL-Anweisung. In einigen Fällen verwendet, um bedeuten, dass eine **wählen** Anweisung.  
  
 **Bezeichner in Anführungszeichen**  
 Ein Bezeichner, der in Anführungszeichen Bezeichner eingeschlossen ist, damit können Sonderzeichen enthalten oder mit Schlüsselwörtern (die auch in SQL-92 als ein Begrenzungsbezeichner bezeichnet wird) übereinstimmen.  
  
## <a name="r"></a>R  
 **Basis**  
 Die Basis eines Systems Anzahl. In der Regel 2 oder 10.  
  
 **Datensatz**  
 *Finden Sie unter* Zeile.  
  
 **Resultset**  
 Der Satz von Zeilen erstellt, durch das Ausführen einer **wählen** Anweisung.  
  
 **Rückgabecode**  
 Der Wert, der von einer ODBC-Funktion zurückgegeben wird.  
  
 **Rollback**  
 Um die Werte geändert, indem eine Transaktion in ihren ursprünglichen Zustand zurück.  
  
 **Zeile**  
 Ein Satz von verknüpften Spalten, die eine bestimmte Entität beschreiben. Auch bekannt als ein *Datensatz*.  
  
 **Zeilendeskriptor**  
 Ein Deskriptor, der die Spalten eines Resultsets, die entweder vor der Konvertierung angegeben, von der Anwendung (ein eingebauter Zeilendeskriptor oder IRD) oder nach der Konvertierung angegeben, die von der Anwendung (eine Zeile Anwendungsdiensts oder ARD) beschreibt.  
  
 **Zeile Operation-array**  
 Ein Array mit Werten, die eine Anwendung festgelegt werden können, um anzugeben, dass die entsprechende Zeile soll, in ignoriert werden einem **SQLSetPos** Vorgang.  
  
 **zeilenstatusarray**  
 Ein Array mit den Status einer Zeile nach einem Aufruf von **SQLFetch**, **SQLFetchScroll**, oder **SQLSetPos**.  
  
 **Rowset**  
 Der Satz von eines Blockcursors in eine einzelne Abrufoperation zurückgegebenen Zeilen.  
  
 **Rowset-Puffer**  
 Die Puffer gebunden an die Spalten eines Resultsets und in welche die Daten für eine gesamte Rowset zurückgegeben wird.  
  
## <a name="s"></a>S  
 **SAG**  
 *Finden Sie unter* SQL-Zugriffsgruppe (SAG).  
  
 **Skalarfunktion**  
 Eine Funktion, die einen einzelnen Wert aus einem einzelnen Wert generiert. Angenommen, eine Funktion, die die Groß-/Kleinschreibung von Zeichendaten geändert.  
  
 **Schema**  
 *Finden Sie unter* Katalog.  
  
 **bildlauffähige cursor**  
 Ein Cursor, der über das Resultset vorwärts oder rückwärts bewegen kann.  
  
 **Serialisierbarkeit**  
 Gibt an, ob zwei Transaktionen gleichzeitig ausführen ein Resultset erzeugen, identisch mit der seriellen (oder nacheinander) Ausführung der Transaktionen ist. Serialisierbare Transaktionen sind erforderlich, um die Datenbankintegrität zu verwalten.  
  
 **Server-Datenbank**  
 Ein DBMS in einer Client-/Server-Umgebung ausgeführt werden soll. Diese DBMS Geben Sie ein eigenständiges Datenbankmodul, die bietet umfangreiche Unterstützung für SQL und Transaktionen. Sie werden über die DBMS-basierten Treibern zugegriffen. Angenommen, Oracle, Informix, DB/2 oder Microsoft® SQL Server.  
  
 **Set-Funktion**  
 *Finden Sie unter* Aggregatfunktion.  
  
 **Setup-DLL**  
 *Finden Sie unter* Treiber-Setup-DLL *und* Konvertierer Setup-DLL.  
  
 **ein-Ebenen-Treiber**  
 *Finden Sie unter* dateibasierte Treiber.  
  
 **location**  
 SQL (isql). Eine Sprache, die von relationalen Datenbanken verwendet werden, um Abfragen, aktualisieren und Verwalten von Daten.  
  
 **SQL-Zugriffsgruppe (SAG)**  
 Ein branchenweit Consortium von Unternehmen mit SQL-DBMS. Die Open Group Call-Level-Interface basiert auf der Arbeit, die ursprünglich von der SQL-Zugriffsgruppe.  
  
 **SQL-Konformitätsgrad**  
 Die Ebene der SQL-92-Grammatik, die vom Treiber unterstützt; Eintrag, FIPS Transitional, zwischen- oder vollständige möglich.  
  
 **SQL-Datentyp**  
 Der Datentyp einer Spalte oder Parameter, wie er ist in der Datenquelle gespeichert.  
  
 **SQLSTATE**  
 Einen fünf Zeichen-Wert, der einen bestimmten Fehler angibt.  
  
 **SQL-Anweisung**  
 Eine vollständige Ausdruck in SQL, die mit einem Schlüsselwort beginnt und vollständig beschreibt eine Aktion, die ausgeführt werden. Wählen Sie z. B. * FROM Orders. SQL-Anweisungen sollten nicht mit Anweisungen verwechselt werden.  
  
 **Status**  
 Eine klar definierte Bedingung eines Elements. Beispielsweise hat eine Verbindung sieben Zustände, einschließlich nicht zugeordnete, zugeordnete verbundenen und korrekturbedürftige Daten. Bestimmte Vorgänge möglich nur, wenn ein Element in einem bestimmten Zustand befindet. Beispielsweise kann eine Verbindung freigegeben werden, nur bei im reservierten Zustand und nicht der Fall, z. B. wenn es verbunden ist.  
  
 **Zustandsübergang**  
 Die Verschiebung eines Datenelements von einem Zustand in einen anderen. ODBC definiert strengen Zustandsübergänge für Umgebungen, Verbindungen und Anweisungen.  
  
 **statement**  
 Ein Container für alle Informationen, die im Zusammenhang mit einer SQL-Anweisung. Anweisungen sollten nicht mit SQL-Anweisungen verwechselt werden.  
  
 **Anweisungshandle**  
 Ein Handle für eine Datenstruktur, die Informationen zu einer Anweisung enthält.  
  
 **statische cursor**  
 Welches ein bildlauffähigen Cursor, der Updates nicht gefunden werden kann, löschen oder Einfügen von im Resultset. Durch Erstellen einer Kopie des Resultsets implementiert in der Regel.  
  
 **statische SQL**  
 Ein Typ von embedded SQL-Anweisungen sind in dem SQL hartcodierte und kompiliert, wenn der Rest des Programms kompiliert wird. *Siehe auch* dynamischem SQL.  
  
 **gespeicherte Prozedur**  
 *Finden Sie unter* Prozedur.  
  
## <a name="t"></a>T  
 **table**  
 Eine Auflistung von Zeilen.  
  
 **Thunking**  
 Die Konvertierung von 16-Bit-Adressen auf 32-Bit-Adressen (oder umgekehrt), wenn 16-Bit-Anwendungen mit 32-Bit-ODBC-Treiber verwendet werden.  
  
 **Transaktion**  
 Eine unteilbare Arbeitseinheit. Die Arbeit in einer Transaktion muss als Ganzes abgeschlossen werden; Wenn Sie einen beliebigen Teil der Transaktion ein Fehler auftritt, schlägt die gesamte Transaktion fehl.  
  
 **Transaktionsisolation**  
 Der Vorgang, der eine Transaktion von den Auswirkungen von allen anderen Transaktionen isoliert.  
  
 **Transaktionsisolationsstufe**  
 Ein Maß, wie gut eine Transaktion isoliert ist. Es gibt fünf Isolationsstufen von Transaktionen: Read Uncommitted Read Committed, Repeatable Read, Serializable und Versionskontrolle.  
  
 **Konvertierer DLL**  
 Eine DLL verwendet, um Daten aus einem Zeichensatz in eine andere übersetzen.  
  
 **Setup-DLL für Konvertierer**  
 Eine DLL, Translator-spezifischen Funktionen, die Installation und Konfiguration enthält.  
  
 **Zweiphasen-commit**  
 Der Prozess der Commit einer verteilten Transaktion in zwei Phasen. In der ersten Phase überprüft der Prozessor für die Transaktion an, dass alle Teile der Transaktion ein Commit ausgeführt werden können. In der zweiten Phase werden alle Teile der Transaktion ein Commit ausgeführt wurde. Wenn Sie einen beliebigen Teil der Transaktion in der ersten Phase angibt, dass sie ein Commit ausgeführt werden kann, erfolgt die zweite Phase nicht. ODBC unterstützt nicht das Zweiphasen-Commits.  
  
 **Typindikator**  
 Ein ganzzahliger Wert übergeben oder aus einer ODBC-Funktion an, dass der Datentyp einer Anwendungsvariablen, einen Parameter oder einer Spalte zurückgegeben. ODBC definiert typindikatoren für C- und SQL-Datentypen.  
  
## <a name="v"></a>B  
 **Anzeigen**  
 Eine alternative Möglichkeit, sehen Sie die Daten in einer oder mehreren Tabellen. Eine Sicht ist in der Regel eine Teilmenge der Spalten aus einer oder mehreren Tabellen erstellt. In ODBC sind Ansichten, Tabellen in der Regel entspricht.
