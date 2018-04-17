---
title: SQLPoolConnect Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 130c39d4aab986b5053192d2fe2c548e89ccef2e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.8 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLPoolConnect** wird verwendet, um eine neue Verbindung zu erstellen, wenn keine Verbindung im Pool wiederverwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>Argumente  
 *hDbc*  
 [Eingabe] Das Verbindungshandle.  
  
 *hDbcInfoToken*  
 [Eingabe] Das token Handle für die neue verbindungsanforderung für die Anwendung.  
  
 *wszOutConnectString*  
 [Ausgabe] Ein Zeiger auf einen Puffer für die vervollständigte Verbindungszeichenfolge. Bei erfolgreicher Verbindung an die Zieldatenquelle enthält dieser Puffer vervollständigte Verbindungszeichenfolge an. Anwendungen sollten mindestens 1.024 Zeichen für diesen Puffer zuweisen.  
  
 Wenn *WszOutConnectString* NULL ist, *CchConnectStringLen* weiterhin die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) zurück zur Rückgabe in der Puffer verweist *WszOutConnectString*.  
  
 *cchConnectStringBuffer*  
 [Eingabe] Länge der **WszOutConnectString* Puffers in Zeichen.  
  
 *cchConnectStringLen*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen (mit Ausnahme von Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *WszOutConnectString*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *CchConnectStringBuffer*, die Verbindungszeichenfolge in abgeschlossen \* *WszOutConnectString* auf abgeschnitten*CchConnectStringBuffer* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Ähnlich wie [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) für alle Validierungsfehler, Eingabe-, mit dem Unterschied, dass der Treiber-Manager verwendet eine **HandleType** von SQL_HANDLE_DBC_INFO_TOKEN und ein **behandeln** von *hDbcInfoToken*.  
  
## <a name="remarks"></a>Hinweise  
 Der Treiber-Manager wird sichergestellt, dass das übergeordnete Element HENV Behandeln der *hDbc* und *hDbcInfoToken* sind identisch.  
  
 Im Gegensatz zu [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md), es ist keine *DriverCompletion* Argument, um Benutzer zur Eingabe von Verbindungsinformationen aufzufordern. Ein aufforderungsstufe Dialogfeld ist im Lightweightpooling-Szenario nicht zulässig.  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Immer ein Treiber SQL_ERROR oder SQL_INVALID_HANDLE zurückgibt, gibt der Treiber-Manager den Fehler an die Anwendung (in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) oder [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 Immer ein Treiber SQL_SUCCESS_WITH_INFO zurückgegeben wird, erhält der Treiber-Manager die Diagnoseinformationen aus *hDbcInfoToken*, und geben Sie an die Anwendung in SQL_SUCCESS_WITH_INFO zurück [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)und [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Wenn eine Anwendung mithilfe [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md), *WszOutConnectString* wird ein NULL-Puffer (die letzten drei Parameter werden alle festgelegt werden auf NULL, 0, NULL) sein. Der Treiber muss die Ausgabe-Verbindungszeichenfolge, die an die Anwendung zurückgegeben werden, andernfalls zurückgeben [SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md) aufrufen.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Developing Connection-Pool Awareness in an ODBC Driver (Entwickeln von Verbindungspool-Unterstützung in einem ODBC-Treiber)](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
