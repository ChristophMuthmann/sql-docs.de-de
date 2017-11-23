---
title: Erstellen eine SQL Server Native Client ODBC-Treiber-Anwendung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC, architecture
- SQL Server Native Client ODBC driver, creating applications
- ODBC function calls
- ODBC, header files
- ODBC applications
- ODBC applications, creating
- SQL Server Native Client ODBC driver, extensions
- applications [SQL Server Native Client]
- SQL Server Native Client ODBC driver, ODBC architecture
- extensions [ODBC]
- ODBC, driver extensions
- function calls [ODBC]
ms.assetid: c83c36e2-734e-4960-bc7e-92235910bc6f
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27f2495ef99f499e9e041f488f8effee328437f5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="creating-a-driver-application"></a>Erstellen einer Treiberanwendung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Die ODBC-Architektur verfügt über vier Komponenten, die die folgenden Funktionen ausführen.  
  
|Komponente|Funktion|  
|---------------|--------------|  
|Application|Ruft ODBC-Funktionen auf, um mit einer ODBC-Datenquelle zu kommunizieren, sendet SQL-Anweisungen und verarbeitet Resultsets.|  
|Treiber-Manager|Verwaltet die Kommunikation zwischen einer Anwendung und allen von der Anwendung verwendeten ODBC-Treibern.|  
|Treiber|Verarbeitet alle ODBC-Funktionsaufrufe von der Anwendung, stellt eine Verbindung zu einer Datenquelle her, übergibt SQL-Anweisungen von der Anwendung an die Datenquelle und gibt Ergebnisse an die Anwendung zurück. Bei Bedarf übersetzt der Treiber ODBC SQL-Code von der Anwendung in den von der Datenquelle verwendeten systemeigenen SQL-Code.|  
|Datenquelle|Enthält alle Informationen, die ein Treiber für den Zugriff auf eine bestimmte Instanz der Daten in einem DBMS benötigt.|  
  
 Eine Anwendung, verwendet der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber für die Kommunikation mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] führt die folgenden Aufgaben:  
  
-   Eine Verbindung mit einer Datenquelle  
  
-   Senden von SQL-Anweisungen an die Datenquelle  
  
-   Verarbeiten der Ergebnisse von Anweisungen von der Datenquelle  
  
-   Verarbeiten von Fehlern und Meldungen  
  
-   Beenden der Verbindung mit der Datenquelle  
  
 Eine komplexere Anwendung geschrieben wird, für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber können möglicherweise auch die folgenden Aufgaben durchführen:  
  
-   Verwenden von Cursorn, um die Position in einem Resultset zu bestimmen  
  
-   Anforderung von Commit- oder Rollbackvorgängen zur Steuerung von Transaktionen  
  
-   Ausführen von verteilten Transaktionen, an denen zwei oder mehr Server beteiligt sind  
  
-   Ausführen von gespeicherten Prozeduren auf dem Remoteserver  
  
-   Aufrufen von Katalogfunktionen für die Abfrage der Attribute eines Resultsets  
  
-   Durchführen von Massenkopiervorgängen  
  
-   Verwalten großer Datenvorgänge (**varchar(max)**, **nvarchar(max)**, und **varbinary(max)** Spalten) Vorgänge  
  
-   Verwenden einer Logik zum Wiederherstellen einer Verbindung, um bei der Konfiguration der Datenbankspiegelung ein Failover zu ermöglichen  
  
-   Protokollieren von Leistungsdaten und Abfragen mit langer Ausführungszeit  
  
 Um ODBC-Funktionen aufrufen können, muss eine C- oder C++-Anwendung die Headerdateien sql.h, sqlext.h und sqltypes.h enthalten. Um API-Funktionen des ODBC-Installationsprogramms aufrufen zu können, muss eine Anwendung die Headerdatei odbcinst.h enthalten. Eine ODBC-Unicode-Anwendung muss die Headerdatei sqlucode.h enthalten. ODBC-Anwendungen müssen mit der Datei odbc32.lib verknüpft werden. ODBC-Anwendungen, die API-Funktionen des ODBC-Installationsprogramms aufrufen, müssen mit der Datei odbccp32.lib verknüpft werden. Diese Dateien sind im Windows Platform SDK enthalten.  
  
 Viele ODBC-Treiber, einschließlich der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber bieten ODBC-Treiber spezifischen Erweiterungen. Nutzen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber-spezifischen Erweiterungen, eine Anwendung sollte die Headerdatei sqlncli.h enthalten. Diese Headerdatei enthält Folgendes:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC-Treiber-spezifische Verbindungsattribute  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC-Treiber-spezifische Anweisungsattribute  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client-ODBC-Treiber-spezifische Spaltenattribute  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-spezifische Datentypen  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-spezifische, benutzerdefinierte Datentypen  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC-Treiber-spezifische [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) Typen.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC-Treiber spezifische Diagnosefelder  
  
-   Für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] spezifische, dynamische Diagnosefunktionscodes  
  
-   C/C++-Definitionen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-spezifische, systemeigene C-Datentypen (die zurückgegeben werden, wenn Spalten an den C-Datentyp SQL_C_BINARY gebunden werden).  
  
-   Typdefinition für die SQLPERF-Datenstruktur  
  
-   Massenkopiermakros und Prototypen zur Unterstützung von APIs für das Massenkopieren über eine ODBC-Verbindung  
  
-   Aufrufen der API-Funktionen für verteilte Abfragemetadaten für Listen mit verknüpften Servern und den zugehörigen Katalogen  
  
 Jede C- oder C++-ODBC-Anwendung, die die Massenkopierfunktion von der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber muss mit der Datei sqlncli11.lib verknüpft werden. Anwendungen, die die API-Funktionen für verteilte Abfragemetadaten aufrufen, müssen ebenfalls mit der Datei sqlncli11.lib verknüpft werden. Die Dateien sqlncli.h und sqlncli11.lib werden im Rahmen des verteilt die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] des Entwicklertools. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verzeichnisse Include und Lib müssen sich wie im folgenden Beispiel in den Verzeichnissen INCLUDE und LIB des Compilers befinden:  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 Ob es erforderlich ist, dass bei der Anwendung mehrere ODBC-Aufrufe gleichzeitig ausstehen können, ist eine Entwurfsentscheidung, die früh im Prozess der Erstellung einer Anwendung getroffen werden muss. Es gibt zwei Methoden zur Unterstützung mehrerer gleichzeitiger ODBC-Aufrufe, die in den verbleibenden Themen dieses Abschnitts beschrieben werden. Weitere Informationen finden Sie unter der [ODBC Programmer's Reference](http://go.microsoft.com/fwlink/?LinkId=45250).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Asynchroner Modus und SQLCancel](../../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)  
  
-   [Multithreadanwendungen](../../../relational-databases/native-client/odbc/creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; ODBC &#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
