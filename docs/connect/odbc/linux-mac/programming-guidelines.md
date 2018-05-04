---
title: Programmierrichtlinien (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a506a6569161241a9334932a0870b3b87b6788ff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="programming-guidelines"></a>Programmierrichtlinien

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Die Features für die Programmierung von der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Mac OS und Linux basieren auf ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client basiert auf ODBC in Windows Data Access Components ([ODBC Programmer's Reference](http://go.microsoft.com/fwlink/?LinkID=45250)).  

Eine ODBC-Anwendung verwenden kann, Multiple Active Result Sets (MARS) und andere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Besonderheiten dazu `/usr/local/include/msodbcsql.h` nach einschließlich der UnixODBC-Header (`sql.h`, `sqlext.h`, `sqltypes.h`, und `sqlucode.h`). Verwenden Sie die gleichen symbolischen Namen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-konkreter Elemente, die Sie in Ihrer Windows-ODBC-Anwendungen verwenden würden.

## <a name="available-features"></a>Verfügbare Funktionen  
Aus den folgenden Abschnitten werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client Dokumentation für ODBC ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) bei Verwendung den ODBC-Treiber unter Mac OS und Linux gültig sind:  

-   [Kommunikation mit SQL Server (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [Verbindungs- und Abfragetimeout-Unterstützung](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [Cursor](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [Uhrzeitverbesserungen Sie Datums-/ (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [Ausführen von Abfragen (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [Behandlung von Fehlern und Meldungen](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos-Authentifizierung](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [Große benutzerdefinierte CLR-Typen (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [Ausführen von Transaktionen (ODBC) (mit Ausnahme von verteilten Transaktionen)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [Verarbeiten von Ergebnissen (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [Ausführen gespeicherter Prozeduren](http://msdn.microsoft.com/library/ms131440.aspx)
-   [Unterstützung für Spalten mit geringer Dichte (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL-Verschlüsselung](http://msdn.microsoft.com/library/ms131691.aspx)
-   [Tabelle Valued Parameter](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 und UTF-16 für die Befehls- und Daten-API](http://msdn.microsoft.com/library/ff878241.aspx)
-   [Verwenden von Katalogfunktionen](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>Nicht unterstützte Funktionen

Die folgenden Funktionen wurden nicht ordnungsgemäß funktioniert in dieser Version des ODBC-Treibers unter Mac OS und Linux überprüft:

-   Failovercluster-Verbindung
-   [Transparentes Netzwerk-IP-Auflösung](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (vor dem ODBC-Treiber 17)
-   [Erweiterte Treiber-Ablaufverfolgung](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Die folgenden Funktionen sind nicht in dieser Version des ODBC-Treibers unter Mac OS und Linux verfügbar: 

-   Verteilte Transaktionen (SQL_ATTR_ENLIST_IN_DTC-Attributs wird nicht unterstützt)  
-   Datenbankspiegelung  
-   FILESTREAM  
-   Profilerstellung für ODBC-Treiber-Leistung, erläutert [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099), und die folgenden leistungsbezogenen Verbindungsattribute:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   C-Intervall-Typen wie z. B. SQL_C_INTERVAL_YEAR_TO_MONTH (dokumentiert [-datentypbezeichnungen und Deskriptoren](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   Der Wert SQL_CUR_USE_ODBC des Attributs SQL_ATTR_ODBC_CURSORS der Funktion SQLSetConnectAttr.

## <a name="character-set-support"></a>Zeichensatz-Unterstützung

Für ODBC Driver 13 and 13.1 muss SQLCHAR-Daten, UTF-8. Keine andere Codierungen werden unterstützt.

Für ODBC-Treiber 17 werden die SQLCHAR-Daten in einem der folgenden Sätze/zeichencodierung unterstützt:

|Name|Description|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS-Lateinisch USA|
|CP850|MS-DOS-Latin 1|
|CP874|Lateinisch/Thai|
|CP932|Shift-JIS Japanisch|
|CP936|Vereinfachtes Chinesisch, GBK|
|CP949|Koreanisch, EUC-KR|
|CP950|Traditionelles Chinesisch, Big5|
|CP1251|Kyrillisch|
|CP1253|Griechisch|
|CP1256|Arabisch|
|CP1257|Baltisch|
|CP1258|Vietnamesisch|
|ISO-8859-1 / CP1252|Latein-1|
|ISO-8859-2 / CP1250|Latein-2|
|ISO-8859-3|Latin-3|
|ISO-8859-4|Latin-4|
|ISO-8859-5|Lateinisch/Kyrillisch|
|ISO-8859-6|Lateinisch/Arabisch|
|ISO-8859-7|Lateinisch/Griechisch|
|ISO-8859-8 / CP1255|Hebräisch|
|ISO-8859-9 / CP1254|Türkisch|
|ISO-8859-13|Latin-7|
|ISO-8859-15|Lateinisch 9|

Beim Herstellen der Verbindung erkennt der Treiber das aktuelle Gebietsschema des Prozesses, der in der Sie geladen wird. Wenn eines der oben genannten Codierungen verwendet wird, verwendet der Treiber mit der Codierung für Daten in SQLCHAR (schmale-Zeichen); Andernfalls wird standardmäßig in UTF-8. Da alle Prozesse im Gebietsschema "C" in der Standardeinstellung starten (und daher dazu führen, den Treiber standardmäßig in UTF-8 dass), wenn eine Anwendung eine der oben genannten Codierungen verwenden muss, sollten Sie verwenden die **Setlocale** Funktion zum entsprechend vor dem Festlegen des Gebietsschemas Herstellen einer Verbindung; entweder indem Sie das gewünschte Gebietsschema explizit angeben oder eine leere Zeichenfolge z. B. `setlocale(LC_ALL, "")` die gebietsschemaeinstellungen der Umgebung zu verwenden.

In einer typischen Linux oder Mac-Umgebung, in dem die Codierung UTF-8 ist, berücksichtigt der ODBC-Treiber 17 ein Upgrade von 13 "oder" 13.1 Benutzer daher nicht Unterschiede. Allerdings Anwendungen verwenden eine nicht-UTF-8-Codierung in der Liste oben über `setlocale()` für Daten von/an den Treiber anstelle von UTF-8-Codierung verwenden müssen.

SQLWCHAR-Daten müssen UTF-16LE (Little Endian) sein.

Beim Binden von Eingabeparametern mit SQLBindParameter, wenn ein schmaler SQL eingeben, wie SQL_VARCHAR angegeben wird, konvertiert der Treiber die bereitgestellten Daten vom Client auf den Standardwert (i. d. r. Codepage 1252) Codierung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Codierung. Für Output-Parameter konvertiert der Treiber aus der Codierung in die Sortierungsinformationen verknüpft sind mit den Daten an den Client, die Codierung angegeben. Allerdings ist Datenverlust möglich---Zeichen in der Quelle Codierung nicht darstellbar ist, in der Ziel-Codierung konvertiert in ein Fragezeichen ("?").

Um diese Datenverluste zu vermeiden, wenn Eingabeparameter gebunden, geben Sie einen Unicode SQL-Zeichentyp z. B. SQL_NVARCHAR. In diesem Fall konvertiert der Treiber vom Client Codierung in UTF-16, die alle Unicode-Zeichen darstellen kann. Darüber hinaus der Zielspalte oder der Parameter auf dem Server zudem muss eine Unicode-Datentyp (**Nchar**, **Nvarchar**, **Ntext**) oder eine mit einer Sortierung/Codierung kann Stellen Sie alle Zeichen aus der ursprünglichen Datenquelle dar. Geben Sie zum Vermeiden von Datenverlust mit Output-Parameter, einen Unicode SQL-Typ und entweder dem Unicode C-Typ (SQL_C_WCHAR), verursacht des Treibers zum Zurückgeben von Daten als UTF-16; oder eine schmale C geben, und stellen Sie sicher, dass die Client Codierung alle Zeichen aus den Quelldaten darstellen kann (Dies ist immer möglich, mit UTF-8.)

Weitere Informationen zu Sortierungen und Codierungen finden Sie unter [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md).

Es gibt einige Codierung Konvertierung Unterschiede zwischen Windows und mehrere Versionen der Iconv-Bibliothek unter Linux und MacOS. Textdaten in der Codepage 1255 (Hebräisch) verfügt über einen Codepunkt (0xCA), die bei der Konvertierung in Unicode anders verhält. Unter Windows konvertiert dieses Zeichen in den UTF-16-Codepunkt des Werts 0x05BA aus. Unter Mac OS und Linux mit Libiconv-Versionen vor 1.15 konvertiert in Werts 0x00CA. Unter Linux mit Iconv-Bibliotheken, die nicht über die 2003-Version des Big5/CP950 unterstützen (mit dem Namen `BIG5-2003`), Zeichen hinzugefügt, die mit dieser Revision nicht ordnungsgemäß konvertiert werden. In Codepage 932 (Japanisch, Shift-JIS) unterscheidet sich auch das Ergebnis der Decodierung von Zeichen, die ursprünglich nicht in die Codierung aus. Beispielsweise das Byte 0 x 80 konvertiert, U + 0080 unter Windows jedoch möglicherweise U + 30FB auf Linux- und MacOS, je nach Iconv-Version.

In ODBC Driver 13 und 13.1 können bei UTF-8-Mehrbytezeichen oder UTF-16-Ersatzzeichen auf SQLPutData-Puffer aufgeteilt werden führt dies zu beschädigten Daten. Für das Streamen von SQLPutData, verwenden Sie Puffer, die nicht in partiellen Zeichencodierungen enden. Diese Einschränkung wurde mit ODBC-Treiber 17 entfernt.

## <a name="additional-notes"></a>Zusätzliche Hinweise  

1.  Sie können eine dedizierte administratorverbindung (DAC) stellen mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Authentifizierung und **hosten, Port**. Ein Mitglied der Sysadmin-Rolle muss zunächst den DAC-Port ermitteln. Finden Sie unter [Diagnoseverbindung für Datenbankadministratoren](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) ermittelt wie. Beispielsweise wenn DAC-Port "33000" wäre, Sie können eine Verbindung herstellen mit `sqlcmd` wie folgt:  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC-Verbindungen müssen verwenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Authentifizierung.  
    
2.  Der UnixODBC-Treiber-Manager gibt „ Attribut-/Optionsbezeichner ungültig“ für alle Anweisungsattribute zurück, wenn sie über SQLSetConnectAttr übergeben werden. Unter Windows Wenn SQLSetConnectAttr einen anweisungsattributwert erhält bewirkt, dass den Treiber, den Wert für alle aktiven Anweisungen festzulegen, die dem Verbindungshandle untergeordnet sind.  

## <a name="see-also"></a>Siehe auch  
[Häufig gestellte Fragen](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Bekannte Probleme in dieser Version des Treibers](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Anmerkungen zu dieser Version](../../../connect/odbc/linux-mac/release-notes.md)
