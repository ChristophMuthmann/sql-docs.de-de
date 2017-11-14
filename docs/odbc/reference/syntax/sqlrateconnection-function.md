---
title: SQLRateConnection Funktion | Microsoft Docs
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
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e63a6312a6f4b637d13282e25311204ea3879fd5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlrateconnection-function"></a>SQLRateConnection-Funktion
**Konformität**  
 Version eingeführt: ODBC 3,81 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLRateConnection** bestimmt, ob ein Treiber eine vorhandene Verbindung im Verbindungspool wiederverwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argumente  
 *hRequest*  
 [Eingabe] Ein token-Handle, das die neue verbindungsanforderung für die Anwendung darstellt.  
  
 *hCandidateConnection*  
 [Eingabe] Die vorhandene Verbindung im Verbindungspool. Die Verbindung muss geöffnet sein.  
  
 *fRequiredTransactionEnlistment*  
 [Eingabe] Bei "true", Wiederverwendung der vorhandenen Verbindungs *hCandidateConnection* für die neue verbindungsanforderung (*hRequest*) erfordert eine zusätzliche Eintragung.  
  
 *Transaktions*  
 [Eingabe] Wenn *fRequiredTransactionEnlistment* ist "true", *Transaktions* stellt die DTC-Transaktion, die die Anforderung eingetragen wird. Wenn *fRequiredTransactionEnlistment* ist "false", *Transaktions* werden ignoriert.  
  
 *pRating*  
 [Ausgabe] *hCandidateConnection*die Wiederverwendung, die für die Bewertung der *hRequest*. Diese Bewertung wird zwischen 0 und 100 (einschließlich) sein.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Der Treiber-Manager verarbeitet keine Diagnoseinformationen, die von dieser Funktion zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 **SQLRateConnection** erzeugt eine Bewertung zwischen 0 und 100 (einschließlich), der angibt, wie gut eine vorhandene Verbindung mit der Anforderung übereinstimmt.  
  
|Ergebnis|Bedeutung (wenn SQL_SUCCESS zurückgegeben wird)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* dürfen nicht wiederverwendet werden, für die *hRequest*.|  
|Alle Werte zwischen 1 und 98 (inklusiv)|Je höher die Bewertung, desto weiter, *hCandidateConnection* abgestimmt *hRequest*.|  
|99|In der nicht signifikante Attribute auftreten nur Konflikte.  Der Treiber-Manager sollten die Bewertung Schleife beenden.|  
|100|Perfekte Übereinstimmung.  Der Treiber-Manager sollten die Bewertung Schleife beenden.|  
|Alle anderen Werte, die größer als 100|*hCandidateConnection* als Warteschlange für unzustellbare Nachrichten und ihn auch in einer zukünftigen verbindungsanforderung nicht wiederverwendet werden markiert.|  
  
 Der Treiber-Manager wird eine Verbindung als Warteschlange für unzustellbare Nachrichten markieren, wenn der Rückgabecode etwas anderes als SQL_SUCCESS wird (einschließlich SQL_SUCCESS_WITH_INFO) oder die Bewertung größer als 100 ist. Stillgelegten Verbindung wird nicht wiederverwendet werden (auch in zukünftigen verbindungsanforderungen) und schließlich Timeout nach CPTimeout übergibt. Der Treiber-Manager weiterhin finden eine andere Verbindung aus dem Pool zu Rate.  
  
 Wenn der Treiber-Manager eine Verbindung wiederverwendet werden, deren Ergebnis streng kleiner als 100 (einschließlich 99) ist, wird der Treiber-Manager SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) zum Zurücksetzen der Verbindung wieder in den Zustand, der von der Anwendung angeforderte aufgerufen. Der Treiber sollte die Verbindung nicht in dieser Funktionsaufruf nicht zurückgesetzt werden.  
  
 Wenn *fRequiredTransactionEnlistment* ist "true", Wiederverwenden von *hCandidateConnection* benötigt eine zusätzliche Eintragung (*Transaktions* ! = NULL) oder Unenlistment ( *Transaktions* == NULL). Hiermit wird die Kosten für das Wiederverwenden von eine Verbindung und gibt an, ob der Treiber eintragen / tragen Sie die Verbindung, wenn sie also die Verbindung erneut verwenden soll. Wenn *fRequireTransactionEnlistment* ist "false", Treiber sollte der Wert der ignoriert *Transaktions*.  
  
 Der Treiber-Manager wird sichergestellt, dass das übergeordnete Element HENV Behandeln der *hRequest* und *hCandidateConnection* sind identisch. Der Treiber-Manager wird sichergestellt, dass die Pool-ID zugeordneten *hRequest* und *hCandidateConnection* sind identisch.  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Schließen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Entwickeln von Verbindungspool wissen in eine ODBC-Treiber](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

