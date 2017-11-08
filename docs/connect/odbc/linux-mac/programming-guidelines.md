---
title: Programmierrichtlinien | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 50f9efe65f14dbd73ccbc3c6e81307c3893c469f
ms.openlocfilehash: 85ba8b35fa698769bd390837855729f3edbc7291
ms.contentlocale: de-de
ms.lasthandoff: 11/08/2017

---
# <a name="programming-guidelines"></a>Programmierrichtlinien

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Die Features für die Programmierung von der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 and 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Mac OS und Linux basieren auf ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client basiert auf ODBC in Windows Data Access Components ([ODBC Programmer's Reference](http://go.microsoft.com/fwlink/?LinkID=45250)).  

Eine ODBC-Anwendung verwenden kann, Multiple Active Result Sets (MARS) und andere [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Besonderheiten dazu `/usr/local/include/msodbcsql.h` nach einschließlich der UnixODBC-Header (`sql.h`, `sqlext.h`, `sqltypes.h`, und `sqlucode.h`). Verwenden Sie die gleichen symbolischen Namen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-konkreter Elemente, die in Ihrer Windows-ODBC-Anwendungen aus.  

## <a name="available-features"></a>Verfügbare Funktionen  
Aus den folgenden Abschnitten werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client Dokumentation für ODBC ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) bei Verwendung den ODBC-Treiber unter Mac OS und Linux gültig sind:  

-   [Bei der Kommunikation mit SQLServer (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [Verbindungs- und Abfragetimeout-Unterstützung](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [Cursor](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [Uhrzeitverbesserungen Sie Datums-/ (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [Ausführen von Abfragen (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [Behandeln von Fehlern und Meldungen](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Kerberos-Authentifizierung](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [Große benutzerdefinierte CLR-Typen (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [Ausführen von Transaktionen (ODBC) (mit Ausnahme von verteilten Transaktionen)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [Verarbeiten von Ergebnissen (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [Ausführen von gespeicherten Prozeduren](http://msdn.microsoft.com/library/ms131440.aspx)
-   [Unterstützung für Spalten mit geringer Dichte (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [SSL-Verschlüsselung](http://msdn.microsoft.com/library/ms131691.aspx)
-   [Tabelle Valued Parameter](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 und UTF-16 für die Befehls- und Daten-API](http://msdn.microsoft.com/library/ff878241.aspx)
-   [Verwenden von Katalogfunktionen](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>Nicht unterstützte Funktionen

Die folgenden Funktionen wurden nicht ordnungsgemäß funktioniert in dieser Version des ODBC-Treibers unter Mac OS und Linux überprüft:

-   Failovercluster-Verbindung
-   [Transparentes Netzwerk-IP-Auflösung](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)
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

Die Client-Codierung kann einer der folgenden sein:
  -  UTF-8
  -  ISO-8859-1
  -  ISO-8859-2
  -  ISO-8859-3
  -  ISO-8859-4
  -  ISO-8859-5
  -  ISO-8859-6
  -  ISO-8859-7
  -  ISO-8859-8
  -  ISO-8859-9
  -  ISO-8859-13
  -  ISO-8859-15
  
SQLCHAR-Daten müssen einen der unterstützten Zeichen sein. SQLWCHAR-Daten müssen UTF-16LE (Little Endian) sein.  

Wenn SQLDescribeParameter keinen SQL-Typ auf dem Server angibt, verwendet der Treiber den SQL-Typ, der im *ParameterType* -Parameter von SQLBindParameter angegeben ist. Wenn ein schmaler SQL-Typ, wie SQL_VARCHAR, in SQLBindParameter angegeben ist, konvertiert der Treiber die bereitgestellten Daten von der Codepage des Clients auf den Standardwert [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Codepage. (Die Standardeinstellung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Codepage ist in der Regel 1252.) Wenn die Clientcodepage nicht unterstützt wird, wird er in UTF-8 festgelegt. In diesem Fall konvertiert der Treiber die UTF-8-Daten dann in die Standardcodepage. Es können jedoch Datenverluste auftreten. Wenn Codepage 1252 ein Zeichen nicht darstellen kann, konvertiert der Treiber das Zeichen in ein Fragezeichen („?“). Um diese Datenverluste zu vermeiden, geben Sie in SQLBindParameter einen Unicode SQL-Zeichentyp an, z. B. SQL_NVARCHAR. In diesem Fall konvertiert der Treiber die angegebenen Unicode-Daten in UTF-8-Codierung in UTF-16 ohne Datenverlust.

Es ist ein textcodierung Konvertierung Unterschied zwischen Windows und mehrere Versionen der Iconv-Bibliothek unter Linux und Mac OS. Textdaten, die in der Codepage 1255 (Hebräisch) codiert werden hat einen Codepunkt (0xCA), die bei der Konvertierung anders verhält. Konvertieren dieses Zeichen in Unicode unter Windows erzeugt einen UTF-16-Codepunkt des Werts 0x05BA. Konvertieren in Unicode unter Mac OS und Linux mit Libiconv Versionen erzeugt älter als 1.15 einen UTF-16-Codepunkt des Werts 0x00CA.

Wenn UTF-8-Mehrbytezeichen oder UTF-16-Ersatzzeichen auf SQLPutData-Puffer aufgeteilt werden, entsteht Datenbeschädigung. Für das Streamen von SQLPutData, verwenden Sie Puffer, die nicht in partiellen Zeichencodierungen enden.  

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

[Versionsanmerkungen](../../../connect/odbc/linux-mac/release-notes.md)

