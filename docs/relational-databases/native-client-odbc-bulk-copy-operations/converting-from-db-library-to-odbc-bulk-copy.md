---
title: Konvertieren von DB-Library zum Massenkopieren in ODBC | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e861e35bbc32f5f97cad5c637a1f0815ee1ee55c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>Konvertieren von DB-Library-Programmen zum Massenkopieren in ODBC-Programme
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Konvertieren von DB-Library-Massenkopierprogramm in ODBC ist einfach, da vom unterstützten Funktionen für das Massenkopieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber die DB-Library-Funktionen zum Massenkopieren, mit Ausnahme der folgenden ähneln:  
  
-   DB-Library-Anwendungen übergeben als ersten Parameter von Funktionen zum Massenkopieren einen Zeiger auf eine DBPROCESS-Struktur. In ODBC-Anwendungen wird der DBPROCESS-Zeiger durch ein ODBC-Verbindungshandle ersetzt.  
  
-   DB-Library-Anwendungen rufen **BCP_SETL** vor dem Herstellen einer Verbindung, um Massenkopiervorgänge für eine DBPROCESS-Struktur zu aktivieren. ODBC-Anwendungen rufen stattdessen [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) vor dem Herstellen einer Verbindung, um Massenkopiervorgänge für ein Verbindungshandle zu aktivieren:  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt keine DB-Library-Meldungs- und Fehlerbehandlungsroutinen; Sie müssen Aufrufen **SQLGetDiagRec** zum Abrufen von ODBC-Massenkopierfunktionen ausgelöste Fehler und Meldungen. Die ODBC-Versionen der Massenkopierfunktionen geben die Standardrückgabecodes SUCCEED bzw. FAILED für das Massenkopieren zurück statt der Rückgabecodes im ODBC-Stil, wie SQL_SUCCESS oder SQL_ERROR.  
  
-   Die Werte für die DB-Library [Bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*Varlen* Parameter werden anders interpretiert als die ODBC **Bcp_bind***CbData*Parameter.  
  
    |Angegebene Bedingung|DB-Library- *Varlen* Wert|ODBC *CbData* Wert|  
    |-------------------------|--------------------------------|-------------------------|  
    |Angabe von NULL-Werten|0|-1 (SQL_NULL_DATA)|  
    |Angabe von variablen Daten|-1|-10 (SQL_VARLEN_DATA)|  
    |Zeichen oder binäre Zeichenfolge mit der Länge 0|NA|0|  
  
     In der DB-Library eine *Varlen* Wert-1 gibt an, dass Daten variabler Länge angegeben wird, die in der ODBC *CbData* wird interpretiert, dass nur NULL-Werte übergeben werden. Ändern Sie alle DB-Library *Varlen* Spezifikationen von-1 in SQL_VARLEN_DATA und alle *Varlen* von 0 in SQL_NULL_DATA.  
  
-   Die DB-Library **Bcp_colfmt***File_collen* und den ODBC- [Bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*CbUserData* haben dasselbe Problem wie die  **Bcp_bind***Varlen* und *CbData* Parametern wie oben beschrieben. Ändern Sie alle DB-Library *File_collen* Spezifikationen von-1 in SQL_VARLEN_DATA und alle *File_collen* von 0 in SQL_NULL_DATA.  
  
-   Die *iValue* Parameter der ODBC- [Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) Funktion ist ein void-Zeiger. In der DB-Library *iValue* wurde eine ganze Zahl. Wandeln Sie die Werte für die ODBC *iValue* in void *.  
  
-   Die **Bcp_control** -Option bcpmaxerrs legt fest, wie viele Zeilen Fehler enthalten können, bevor ein Massenkopiervorgang fehlschlägt. Der Standardwert für BCPMAXERRS ist 0 (Fehlschlagen beim ersten Fehler) in der DB-Library-Version von **Bcp_control** und 10 in der ODBC-Version. DB-Library-Anwendungen, die abhängig von der Standardwert von 0 beendet einen Massenkopiervorgang müssen geändert werden, um die ODBC call **Bcp_control** BCPMAXERRS auf 0 festlegen.  
  
-   Die ODBC **Bcp_control** Funktion unterstützt die folgenden Optionen, die nicht von der DB-Library-Version unterstützt **Bcp_control**:  
  
    -   BCPODBC  
  
         Bei Festlegung auf "true", gibt an, dass **"DateTime"** und **Smalldatetime** müssen im Zeichenformat gespeicherten Werte ODBC-Zeitstempel Escape-Sequenz-Präfix und Suffix. Dies gilt nur für BCP_OUT-Vorgänge.  
  
         Bcpodbc auf FALSE gesetzt eine **"DateTime"** -Wert konvertiert in eine Zeichenfolge wie folgt ausgegeben:  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         Bcpodbc auf TRUE festgelegt, die gleiche **"DateTime"** -Wert wie folgt ausgegeben:  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         Durch die Festlegung dieser Option auf TRUE wird angegeben, dass Massenkopierfunktionen Datenwerte einfügen, die für Spalten mit einer IDENTITY-Einschränkung bereitgestellt werden. Wenn dies nicht festgelegt ist, werden neue Identitätswerte für die eingefügten Zeilen generiert.  
  
    -   BCPHINTS  
  
         Gibt verschiedene Optimierungen für das Massenkopieren an. Diese Option kann in Version 6.5 und früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht verwendet werden.  
  
    -   BCPFILECP  
  
         Gibt die Codepage für die Datendatei des Massenkopiervorgangs an.  
  
    -   BCPUNICODEFILE  
  
         Gibt an, dass eine Datendatei für das Massenkopieren im Zeichenmodus eine Unicode-Datei ist.  
  
-   Die ODBC **Bcp_colfmt** -Funktion nicht unterstützt die *File_type* Indikator für SQLCHAR da ein Konflikt mit der ODBC SQLCHAR-Typdefinition. Verwenden Sie stattdessen SQLCHARACTER für **Bcp_colfmt**.  
  
-   In der ODBC-Versionen der Funktionen zum Massenkopieren, das Format für die Arbeit mit **"DateTime"** und **Smalldatetime** -Werte in Zeichenfolgen wird die ODBC-Format Yyyy-mm-tt ss.sss verarbeitet werden; **Smalldatetime** Werte verwenden, die ODBC-Format Yyyy-mm-tt hh: mm:.  
  
     Die DB-Library-Versionen der Funktionen zum Massenkopieren akzeptieren **"DateTime"** und **Smalldatetime** -Werte in Zeichenfolgen, die mit verschiedenen Formaten:  
  
    -   Das Standardformat ist *mmm Dd Yyyy mmXX* , in denen *Xx* ist AM oder PM.  
  
    -   **"DateTime"** und **Smalldatetime** Zeichenfolgen in einem beliebigen Format, das von der DB-Library unterstützt **Dbconvert** Funktion.  
  
    -   Wenn die **internationale Einstellungen verwenden** Kontrollkästchen aktiviert ist, auf die DB-Library **Optionen** auf der Registerkarte die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Clientkonfiguration, die DB-Library-Funktionen zum Massenkopieren auch akzeptieren Datumsangaben in regionalen das Datumsformat für die gebietsschemaeinstellung des der Registrierungs des Computers definiert.  
  
     Die DB-Library-Funktionen zum Massenkopieren akzeptieren die ODBC keine **"DateTime"** und **Smalldatetime** Formate.  
  
     Wenn das SQL_SOPT_SS_REGIONALIZE-Anweisungsattribut auf SQL_RE_ON festgelegt wurde, akzeptieren die ODBC-Funktionen zum Massenkopieren auch Datumsangaben in dem regionalen Datumsformat, das für die Einstellung des Gebietsschemas in der Registrierung des Clientcomputers definiert wurde.  
  
-   Bei der Ausgabe **Money** Werte im Zeichenformat, ODBC Bulk Copy Funktionen geben vier Dezimalstellen und keine Kommas als Trennzeichen; DB-Library-Versionen nur zwei Dezimalstellen angeben und die Kommas als Trennzeichen enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Massenkopiervorgängen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
