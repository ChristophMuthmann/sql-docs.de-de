---
title: Rückgabecodes ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12751f87c9f9832567dc04ba7df7659e80e66897
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="return-codes-odbc"></a>Rückgabecodes ODBC
Jede Funktion in ODBC gibt einen Code, bekannt als seine *Rückgabecode,* gibt den Erfolg oder Fehler bei der Funktion an. Die Programmlogik basiert im Allgemeinen auf Rückgabecodes.  
  
 Im folgenden Codebeispiel beispielsweise Aufrufe **SQLFetch** zum Abrufen der Zeilen in einem Resultset. Er überprüft den Rückgabecode der Funktion zu bestimmen, ob das Ende des Resultsets (SQL_NO_DATA), erreicht wurde, wenn alle Warnungsinformationen (SQL_SUCCESS_WITH_INFO) zurückgegeben wurde, oder bei einem Fehler (SQL_ERROR).  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 Der Rückgabecode SQL_INVALID_HANDLE gibt immer einen Programmierfehler an und sollte zur Laufzeit nie auftreten. Alle anderen Rückgabecodes stellen Laufzeitinformationen bereit, wenngleich SQL_ERROR einen Programmierfehler angeben kann.  
  
 Der folgenden Tabelle werden die Rückgabecodes.  
  
|Rückgabecode|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|Die Funktion wurde erfolgreich abgeschlossen. Ruft die Anwendung **SQLGetDiagField** um zusätzliche Informationen aus den Headerdatensatz abzurufen.|  
|SQL_SUCCESS_WITH_INFO|Die Funktion wurde erfolgreich abgeschlossen, möglicherweise eine nicht schwerwiegende Fehler (Warnung). Ruft die Anwendung **SQLGetDiagRec** oder **SQLGetDiagField** um weitere Informationen abzurufen.|  
|SQL_ERROR|Fehler bei der Funktion. Ruft die Anwendung **SQLGetDiagRec** oder **SQLGetDiagField** um weitere Informationen abzurufen. Der Inhalt der Ausgabeargumente an die Funktion ist nicht definiert.|  
|SQL_INVALID_HANDLE|Fehler bei der Funktion aufgrund eines ungültigen Handles für Umgebung, Verbindung, Anweisung oder Deskriptor. Hiermit wird einen Programmierfehler. Keine zusätzlichen Informationen steht über **SQLGetDiagRec** oder **SQLGetDiagField**. Dieser Code wird zurückgegeben, nur, wenn das Handle ein null-Zeiger ist oder den falschen Typ hat, z. B. wenn ein Anweisungshandle für ein Argument übergeben wird, die ein Verbindungshandle erforderlich sind.|  
|SQL_NO_DATA|Es wurde keine weiteren Daten verfügbar. Ruft die Anwendung **SQLGetDiagRec** oder **SQLGetDiagField** um weitere Informationen abzurufen. Einen oder mehrere treiberdefinierten Statusdatensätze in der Klasse 02xxx können zurückgegeben werden. **Hinweis:** In ODBC 2. *X*, dadurch Code hieß SQL_NO_DATA_FOUND zurückgegeben.|  
|SQL_NEED_DATA|Weitere Daten erforderlich ist, z. B. wenn die Parameterdaten zur Ausführungszeit gesendet wird, oder zusätzliche Verbindungsinformationen ist erforderlich. Ruft die Anwendung **SQLGetDiagRec** oder **SQLGetDiagField** zusätzliche Informationen abrufen, sofern vorhanden.|  
|SQL_STILL_EXECUTING|Eine Funktion, die asynchron gestartet wurde, wird weiterhin ausgeführt. Ruft die Anwendung **SQLGetDiagRec** oder **SQLGetDiagField** zusätzliche Informationen abrufen, sofern vorhanden.|
