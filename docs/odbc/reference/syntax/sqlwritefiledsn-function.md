---
title: SQLWriteFileDSN Funktion | Microsoft Docs
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
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 47cc9672aecb91917a5abc15de2fc34fac59d2c2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLWriteFileDSN** schreibt Informationen in eine Datei-DSN.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszFileName*  
 [Eingabe] Ein Zeiger auf den Namen der Datei-DSN. Eine DSN-Erweiterung wird an alle Dateinamen angefügt, die noch nicht über eine DSN-Erweiterung verfügen.  
  
 *lpszAppName*  
 [Eingabe] Ein Zeiger auf den Namen der Anwendung. Dies ist "ODBC" für den ODBC-Abschnitt.  
  
 *lpszKeyName*  
 [Eingabe] Ein Zeiger auf den Namen des Schlüssels, der gelesen werden. Reservierte Schlüsselwörter finden Sie unter "Kommentare".  
  
 *lpszString*  
 [Ausgabe] Verwies auf die Zeichenfolge, die dem Schlüssel geschrieben werden. Die maximale Länge der Zeichenfolge verweist dieses Argument ist 32.767 Bytes.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLWriteFileDSN** gibt "false", ein zugehöriges * \*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die * \*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_PATH|Ungültiger Installationspfad|Der Pfad der Datei im angegebenen der *LpszFileName* Argument war ungültig.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *LpszAppName*, *LpszKeyName*, oder *LpszString* -Argument war NULL.|  
  
## <a name="comments"></a>Kommentare  
 ODBC reserviert der Name des Abschnitts [ODBC], in dem Sie die Verbindungsinformationen zu speichern. Die reservierten Schlüsselwörter für diesen Abschnitt sind identisch für eine Verbindungszeichenfolge in reservierten **SQLDriverConnect**. (Weitere Informationen finden Sie unter der [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) funktionsbeschreibung.)  
  
 Anwendungen können diese reservierte Schlüsselwörter verwenden, um Informationen direkt in eine Datei-DSN schreiben. Wenn eine Anwendung erstellen oder ändern die DSN-lose Verbindung-Zeichenfolge, die einen Datei-DSN zugeordnet, rufen sie **SQLWriteFileDSN** für keines der reservierten Schlüsselwörter für Verbindungszeichenfolgen im Abschnitt [ODBC].  
  
 Wenn die *LpszString* Argument ist ein null-Zeiger, das Schlüsselwort verweist, zu der *LpszKeyName* Argument die DSN-Datei gelöscht wird. Wenn die *LpszString* und *LpszKeyName* Argumente sind beide null-Zeiger im Abschnitt verweist, zu der *LpszAppName* Argument die DSN-Datei gelöscht wird.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Lesen von Informationen aus der Datei-DSNs|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
