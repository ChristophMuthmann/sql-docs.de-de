---
title: Behandeln von Fehlern und Meldungen | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f85a24a8b40d54051fe504d44a57b4c939bb85ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="handling-errors-and-messages"></a>Behandlung von Fehlern und Meldungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Wenn eine Anwendung eine ODBC-Funktion aufruft, führt der Treiber die Funktion aus und gibt Diagnoseinformationen zurück: Ein Rückgabecode gibt das Ergebnis einer ODBC-Funktion zurück (Erfolg oder Fehlschlagen), und Diagnosedatensätze liefern detaillierte Informationen über die Funktion. Diagnosedatensätze enthalten einen Headerdatensatz und Statusdatensätze. Auch wenn die Funktion erfolgreich ausgeführt wurde, wird zumindest ein Diagnosedatensatz, der Headerdatensatz, zurückgegeben.  
  
 Die Diagnoseinformationen dienen während der Entwicklung zur Erfassung von Programmierfehlern wie ungültigen Handles und Syntaxfehlern in hartcodierten SQL-Anweisungen. Darüber hinaus dienen sie zur Laufzeit dazu, Laufzeitfehler und Warnungen zu erfassen, beispielsweise das Abschneiden von Daten, Regelverstöße und Syntaxfehler in benutzerdefinierten SQL-Anweisungen. Die Programmlogik basiert im Allgemeinen auf Rückgabecodes.  
  
 Beispiel: Nachdem eine Anwendung ruft **SQLFetch** zum Abrufen von Zeilen in einem Resultset, Rückgabecode: angibt, ob das Ende des Resultsets (SQL_NO_DATA), erreicht wurde bei informationsmeldungen (SQL_SUCCESS_ zurückgegeben wurden WITH_INFO), oder bei einem Fehler (SQL_ERROR).  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt etwas anderes als SQL_SUCCESS, die Anwendung rufen **SQLGetDiagRec** zum Abrufen, die Informations- oder Fehlermeldungen. Verwendung **SQLGetDiagRec** , führen Sie einen Bildlauf nach oben oder unten der Nachricht festgelegt, wenn mehr als eine Meldung vorhanden ist.  
  
 Der Rückgabecode SQL_INVALID_HANDLE gibt immer einen Programmierfehler an und sollte zur Laufzeit nie auftreten. Alle anderen Rückgabecodes stellen Laufzeitinformationen bereit, wenngleich SQL_ERROR einen Programmierfehler angeben kann.  
  
 Die ursprüngliche [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] systemeigene API, die DB-Library für C, ermöglicht einer Anwendung, die Rückruf-Fehlerbehandlung installieren und Meldungsbehandlung Funktionen, Fehler oder Meldungen zurückgeben. Einige [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, wie PRINT, RAISERROR, DBCC und SET, geben ihre Ergebnisse an die Meldungshandlerfunktion der DB-Library anstatt an ein Resultset zurück. Jedoch verfügt die ODBC-API über keine solche Rückruffähigkeit. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber Meldungen erkennt wieder aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], er legt den ODBC-Rückgabecode auf SQL_SUCCESS_WITH_INFO oder SQL_ERROR fest und gibt die Nachricht als ein oder mehrere DiagnoseDatensätze zurück. Eine ODBC-Anwendung muss sorgfältig testen Sie daher für diese Codes, und rufen zurückgeben **SQLGetDiagRec** um Meldungsdaten abzurufen.  
  
 Informationen zur Ablaufverfolgung von Fehlern finden Sie unter [Datenzugriffsablaufverfolgung](http://go.microsoft.com/fwlink/?LinkId=125805). Informationen zu Verbesserungen hinzugefügten fehlerablaufverfolgung [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], finden Sie unter [Zugriff auf Diagnoseinformationen im Protokoll für erweiterte Ereignisse](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Verarbeiten von Anweisungen, die Meldungen generieren](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [Diagnosedatensätze und -felder](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [Systemeigene Fehlernummern](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40; ODBC-Fehlercodes &#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [Fehlermeldungen](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
