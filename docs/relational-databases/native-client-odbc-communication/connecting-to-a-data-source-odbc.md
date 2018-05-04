---
title: Herstellen einer Verbindung mit einer Datenquelle (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- checking connection states
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- SQLBrowseConnect function
- ODBC applications, connections
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLConnect function
- SQLDriveConnect function
- verifying connection states
- SQL Server Native Client ODBC driver, data sources
- SQL Server Native Client ODBC driver, connections
ms.assetid: ae30dd1d-06ae-452b-9618-8fd8cd7ba074
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4daa642cbd60846cc4211de5e33cdad8e7a6d8db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-a-data-source-odbc"></a>Herstellen einer Verbindung mit einer Datenquelle (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Nach dem Zuweisen der Umgebungs- und Verbindungshandles und dem Festlegen der Verbindungsattribute stellt die Anwendung eine Verbindung zur Datenquelle oder zum Treiber her. Es gibt drei Funktionen, die Sie verwenden können, um eine Verbindung herzustellen:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLBrowseConnect**  
  
 Weitere Informationen zum Herstellen von Verbindungen mit einer Datenquelle, einschließlich der verschiedenen verfügbaren Zeichenfolgenoptionen, finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
## <a name="sqlconnect"></a>SQLConnect  
 **SQLConnect** ist die einfachste Verbindungsfunktion. Sie akzeptiert drei Parameter: Datenquellenname, Benutzer-ID und Kennwort. Verwendung **SQLConnect** Wenn diese drei Parameter enthalten alle Informationen, die für die Verbindung mit der Datenbank benötigt. Zu diesem Zweck erstellen Sie eine Liste der Datenquellen mit **SQLDataSources**; der Benutzer für eine Datenquelle, Benutzer-ID und Kennwort aufgefordert, und rufen dann **SQLConnect**.  
  
 **SQLConnect** wird davon ausgegangen, dass Datenquellenname, Benutzer-ID und Kennwort sind ausreichend für die Verbindung mit einer Datenquelle und die ODBC-Datenquelle sämtliche anderen Informationen enthält der ODBC-Treiber zum Herstellen die Verbindung muss. Im Gegensatz zu [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) und [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md), **SQLConnect** verwendet eine Verbindungszeichenfolge nicht.  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
 **SQLDriverConnect** wird verwendet, wenn mehr Informationen als Datenquellenname, Benutzer-ID und Kennwort erforderlich ist. Einer der Parameter auf **SQLDriverConnect** ist eine Verbindungszeichenfolge, die treiberspezifische Informationen enthält. Sie können **SQLDriverConnect** anstelle von **SQLConnect** folgende Gründe vorliegen:  
  
-   Um zum Zeitpunkt des Verbindungsaufbaus treiberspezifische Informationen anzugeben.  
  
-   Um anzugeben, dass der Treiber den Benutzer zur Eingabe von Verbindungsinformationen auffordert.  
  
-   Um eine Verbindung herzustellen, ohne eine ODBC-Datenquelle zu verwenden.  
  
 Die **SQLDriverConnect** Verbindungszeichenfolge enthält eine Reihe von Schlüsselwort-Wert-Paare, die alle von einem ODBC-Treiber unterstützten Verbindungsinformationen angeben. Bei allen vom Treiber unterstützten Verbindungsinformationen unterstützt jeder Treiber über die treiberspezifischen Schlüsselwörter hinaus die standardmäßigen ODBC-Schlüsselwörter (DSN, FILEDSN, DRIVER, UID, PWD und SAVEFILE). **SQLDriverConnect** genutzt werden, ohne eine Datenquelle zu verbinden. Z. B. eine Anwendung, die darauf ausgelegt ist, eine "DSN-lose" Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erreichen **SQLDriverConnect** mit einer Verbindungszeichenfolge, die definiert, einer der Anmelde-ID, Kennwort, Netzwerkbibliothek, Servernamen, um Herstellen einer Verbindung mit und die Standarddatenbank verwendet.  
  
 Bei Verwendung **SQLDriverConnect**, es gibt zwei Optionen für den Benutzer für Verbindungsinformationen benötigten aufzufordern:  
  
-   Dialogfeld "Anwendung"  
  
     Sie können eine Anwendung Dialogfeld "erstellen", die Verbindungsinformationen auffordert und ruft dann **SQLDriverConnect** mit einem Fensterhandle von NULL und *DriverCompletion* auf SQL_DRIVER_NOPROMPT festgelegt. Diese Parametereinstellungen verhindern, dass der ODBC-Treiber ein eigenes Dialogfeld öffnet. Diese Methode wird verwendet, wenn die Benutzeroberfläche der Anwendung gesteuert werden muss.  
  
-   Dialogfeld "Filter"  
  
     Sie können code für die Anwendung ein gültiges Fensterhandle an übergeben **SQLDriverConnect** und legen Sie die *DriverCompletion* -Parameter auf SQL_DRIVER_COMPLETE, SQL_DRIVER_PROMPT oder SQL_DRIVER_COMPLETE_ Erforderlich. Der Treiber generiert dann ein Dialogfeld, um den Benutzer zur Eingabe von Verbindungsinformationen aufzufordern. Diese Methode vereinfacht den Anwendungscode.  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
 **SQLBrowseConnect**, z. B. **SQLDriverConnect**, verwendet eine Verbindungszeichenfolge. Indem jedoch **SQLBrowseConnect**, eine Anwendung kann eine vollständige Verbindungszeichenfolge iterativ mit der Datenquelle zur Laufzeit erstellen. Dadurch kann die Anwendung zwei Funktionen erfüllen:  
  
-   Erstellen eigener Dialogfelder, um zur Eingabe dieser Informationen aufzufordern, wodurch die Kontrolle über die Benutzeroberfläche beibehalten wird.  
  
-   Durchsuchen des Systems nach Datenquellen, die von einem bestimmten Treiber verwendet werden können. Dies sollte nach Möglichkeit in mehreren Schritten erfolgen.  
  
     Beispielsweise kann der Benutzer zunächst das Netzwerk nach Servern durchsuchen und, sobald er einen Server ausgewählt hat, diesen nach Datenbanken durchsuchen, auf die der Treiber zugreifen kann.  
  
 Wenn **SQLBrowseConnect** Abschluss eine erfolgreiche Verbindung wird eine Verbindungszeichenfolge, die bei nachfolgenden Aufrufen verwendet werden kann **SQLDriverConnect**.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt stets SQL_SUCCESS_WITH_INFO zurück, bei einem erfolgreichen **SQLConnect**, **SQLDriverConnect**, oder **SQLBrowseConnect**. Wenn eine ODBC-Anwendung aufruft **SQLGetDiagRec** nach SQL_SUCCESS_WITH_INFO den Parameter erhalten sie die folgenden Meldungen:  
  
 5701  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Kontext des Benutzers in die in der Datenquelle angegebene Standarddatenbank oder, wenn für die Datenquelle keine Standarddatenbank angegeben ist, in die Standarddatenbank der zur Verbindung verwendeten Anmelde-ID einfügt.  
  
 5703  
 Gibt die auf dem Server verwendete Sprache an.  
  
 Bei einer erfolgreichen Verbindung wird die folgende Meldung vom Systemadministrator zurückgegeben:  
  
```  
szSqlState = "01000", *pfNativeError = 5701,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed database context to 'pubs'."  
szSqlState = "01000", *pfNativeError = 5703,  
szErrorMsg="[Microsoft][SQL Server Native Client][SQL Server]  
       Changed language setting to 'us_english'."  
```  
  
 Sie können die Meldungen 5701 und 5703 ignorieren; sie dienen nur zu Informationszwecken. Den Rückgabecode SQL_SUCCESS_WITH_INFO hingegen sollten Sie nicht ignorieren, da auch andere Meldungen als 5701 oder 5703 zurückgegeben werden können. Beispielsweise verbindet ein Treiber für einen Server mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit veralteten gespeicherten Prozeduren für Kataloginformationen, einer der Fehler durch zurückgegebenen **SQLGetDiagRec** nach erfolgreichem SQL_SUCCESS_WITH_INFO:  
  
```  
SqlState:   01000  
pfNative:   0  
szErrorMsg: "[Microsoft][SQL Server Native Client]The ODBC  
            catalog stored procedures installed on server  
            my65server are version 06.50.0193; version 07.00.0205  
            or later is required to ensure proper operation.  
            Please contact your system administrator."  
```  
  
 Die Fehlerbehandlungsfunktion einer Anwendung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verbindungen sollten Aufrufen **SQLGetDiagRec** bis SQL_NO_DATA zurückgegeben. Sie sollten anschließend Aktionen für alle Meldungen mit einem *PfNative* -Code 5701 oder 5703.  
  
## <a name="see-also"></a>Siehe auch  
 [Bei der Kommunikation mit SQLServer &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
