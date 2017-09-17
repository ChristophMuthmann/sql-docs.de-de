---
title: SQLInstallerError Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb17b0ab5da8770c4622c7359c16de6876688c17
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstallererror-function"></a>SQLInstallerError-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLInstallerError** Fehler oder Status Informationen für die Funktionen der ODBC-Installationsprogramm zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumente  
 *IFehler*  
 [Eingabe] Datensatz-Fehlernummer. Gültige Zahlen reichen von 1 bis 8.  
  
 *pfErrorCode*  
 [Ausgabe] Installer-Fehlercode. (Weitere Informationen finden Sie unter "Kommentare".)  
  
 *lpszErrorMsg*  
 [Ausgabe] Zeiger auf Speicher für den Text der Fehlermeldung.  
  
 *cbErrorMsgMax*  
 [Eingabe] Maximale Länge von der *von SQLDiagRec()* Puffer. Dies muss kleiner als oder gleich SQL_MAX_MESSAGE_LENGTH minus der Null-Abschlusszeichen.  
  
 *cbErrorMsgMax*  
 [Eingabe] Maximale Länge von der *von SQLDiagRec()* Puffer. Dies muss kleiner als oder gleich SQL_MAX_MESSAGE_LENGTH minus der Null-Abschlusszeichen.  
  
 *pcbErrorMsg*  
 [Ausgabe] Zeiger auf die Gesamtanzahl der Bytes (ausgenommen die Null-Abschlusszeichen) verfügbar, für die zurückzugebenden in *LpszErrorMsg*. Die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als oder gleich *CbErrorMsgMax*, der Text der Fehlermeldung im *LpszErrorMsg* auf abgeschnitten *CbErrorMsgMax* minus der NULL-Abschlusszeichen Bytes. Die *PcbErrorMsg* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA oder SQL_ERROR zurück.  
  
## <a name="diagnostics"></a>Diagnose  
 **SQLInstallerError** Fehlerwerte für sich selbst wird nicht gesendet. **SQLInstallerError** gibt SQL_NO_DATA zurück, wenn sie Fehlerinformationen abrufen kann (in diesem Fall *PfErrorCode* ist nicht definiert). Wenn **SQLInstallerError** Fehlerwerte kann nicht zugegriffen werden, die aus irgendeinem Grund, die normalerweise SQL_ERROR, zurückgeben würde **SQLInstallerError** gibt SQL_ERROR zurück, aber keine Fehlerwerte gebucht. Wenn Sie nicht, dass die Länge der Zeichenfolge Warnung wissen (*LpszErrorMsg*), können Sie festlegen, *LpszErrorMsg* auf NULL, und rufen **SQLInstallerError**. **SQLInstallerError** wird zurückgegeben: die Länge der Zeichenfolge Warnung in *CbErrorMsgMax*. Wenn der Puffer für die Fehlermeldung zu kurz ist **SQLInstallerError** gibt SQL_SUCCESS_WITH_INFO zurück und gibt den richtigen *PfErrorCode* Wert für **SQLInstallerError**.  
  
 Um zu bestimmen, ob eine abgeschnittenen Daten in der Fehlermeldung, kann eine Anwendung vergleichen Sie den Wert in der *CbErrorMsgMax* Argument an die tatsächliche Länge der den Meldungstext geschrieben der *PcbErrorMsg* Argument. Wenn Kürzung auftritt, sollte die richtige Pufferlänge zugeordnet werden, für die *LpszErrorMsg* und **SQLInstallerError** erneut aufgerufen werden soll, mit dem entsprechenden *IFehler*Datensatz.  
  
## <a name="comments"></a>Kommentare  
 Ruft die Anwendung **SQLInstallerError** bei ein vorherigen Aufruf der ODBC-Installer-Funktion gibt "false" zurück. ODBC-Funktionen mit dem Setup-Installer und Treiber oder Konvertierer post NULL oder mehr Fehler nur, wenn die Funktion fehlerhaft ist (gibt "false"); Ruft die Anwendung daher **SQLInstallerError** erst nach eine ODBC-Installer-Funktion fehlschlägt.  
  
 Der ODBC-Installer-Fehlerwarteschlange wird jedes Mal geleert, wenn eine neue Installer-Funktion aufgerufen wird. Aus diesem Grund kann nicht erwarten, dass eine Anwendung Fehler für Funktionen außer aus dem letzten Aufruf der Installer-Funktion abgerufen.  
  
 Um mehrere Fehler für einen Funktionsaufruf abzurufen, eine Anwendung ruft **SQLInstallerError** mehrere Male.  
  
 Wenn es keine zusätzlichen Informationen sind **SQLInstallerError** SQL_NO_DATA zurückgibt, die *PfErrorCode* Argument ist nicht definiert ist, die *PcbErrorMsg* Argument gleich 0 ist, und die *LpszErrorMsg* -Argument enthält ein einzelnes Zeichen für die Null-Terminierung (es sei denn, die *CbErrorMsgMax* Argument gleich 0 ist).
