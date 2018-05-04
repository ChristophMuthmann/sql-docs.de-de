---
title: SQLReadFileDSN Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32804ed9657a4438c3509fc57b266eb97af9db5b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLReadFileDSN** liest Informationen aus einer Datei-DSN.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszFileName*  
 [Eingabe] Zeiger auf den Datenpuffer, der mit dem Namen des DSN-Datei. Eine DSN-Erweiterung wird an alle Dateinamen angefügt, die noch nicht über eine DSN-Erweiterung verfügen. Der Wert in  *\*LpszFileName* muss eine Null-terminierte Zeichenfolge sein.  
  
 *lpszAppName*  
 [Eingabe] Zeiger auf den Datenpuffer, der mit dem Namen der Anwendung. Dies ist "ODBC" für den ODBC-Abschnitt. Der Wert in  *\*LpszAppName* muss eine Null-terminierte Zeichenfolge sein.  
  
 *lpszKeyName*  
 [Eingabe] Zeiger auf den Datenpuffer, der mit dem Namen des Schlüssels, der gelesen werden. Reservierte Schlüsselwörter finden Sie unter "Kommentare". Der Wert in  *\*LpszAppName* muss eine Null-terminierte Zeichenfolge sein.  
  
 *lpszString*  
 [Ausgabe] Zeiger auf den Datenpuffer, die mit der Zeichenfolge, die dem Schlüssel gelesen werden.  
  
 Wenn  *\*LpszFileName* ist der Name einer gültigen DSN-Datei jedoch *LpszAppName* Argument ist ein null-Zeiger und der *LpszKeyName* Argument ist ein null-Zeiger  *\*LpszString* enthält eine Liste der gültigen Anwendungen. Wenn  *\*LpszFileName* ist der Name einer gültigen DSN-Datei und  *\*LpszAppName* ist ein gültiger Anwendungsname angegeben wird, aber die *LpszKeyName* Argument ist ein NULL-Wert Zeiger, dann  *\*LpszString* enthält eine Liste der gültigen reservierten Schlüsselwörter im entsprechenden Abschnitt der DSN-Datei, die durch ein Semikolon getrennt. Wenn  *\*LpszFileName* ist der Name einer gültigen DSN-Datei jedoch  *\*LpszAppName* ist ein null-Zeiger und der *LpszKeyName* Argument ist ein null-Zeiger Klicken Sie dann  *\*LpszString* enthält eine Liste der Abschnitte in der DSN-Datei durch ein Semikolon getrennt.  
  
 *cbString*  
 [Eingabe] Länge der  *\*LpszString* Puffer.  
  
 *pcbString*  
 [Ausgabe] Gesamtanzahl der Bytes im zurückzugebenden verfügbar  *\*LpszString*. Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *CbString*, in die Ausgabezeichenfolge  *\*LpszString* auf abgeschnitten *CbString* minus die Null-Abschlusszeichen. Die *PcbString* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLReadFileDSN** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *LpszString* -Argument war NULL.<br /><br /> Die *CbString* Argument war kleiner oder gleich 0.|  
|ODBC_ERROR_INVALID_PATH|Ungültiger Installationspfad|Der Pfad der Datei im angegebenen der *LpszFileName* Argument war ungültig.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *LpszAppName* -Argument war NULL, während die *LpszKeyName* Argument war ungültig.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|Ausgabezeichenfolge abgeschnitten|Die Zeichenfolge, die im zurückgegebenen  *\*LpszString* wurde abgeschnitten, da der Wert in *CbString* war kleiner oder gleich dem Wert in  *\*PcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|Fehler bei der Anforderung|Das Schlüsselwort nicht in der Datei-DSN vorhanden.|  
  
## <a name="comments"></a>Kommentare  
 ODBC reserviert der Name des Abschnitts [ODBC], in dem Sie die Verbindungsinformationen zu speichern. Die reservierten Schlüsselwörter für diesen Abschnitt sind identisch für eine Verbindungszeichenfolge in reservierten **SQLDriverConnect**. (Weitere Informationen finden Sie unter der [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) funktionsbeschreibung.)  
  
 Anwendungen können diese reservierte Schlüsselwörter verwenden, lesen Sie die Informationen in eine Datei-DSN. Wenn ein Anwendungen ermitteln, der einen Datei-DSN zugeordneten DSN-lose Verbindung-Zeichenfolge aufrufen möchte **SQLReadFileDSN** für keines der reservierten Schlüsselwörter für Verbindungszeichenfolgen im Abschnitt [ODBC]. Die vollständige Verbindungszeichenfolge übergeben, die in einer DSN-lose Verbindung ist eine Kombination aller Schlüsselwörter (reservierte und treiberspezifische) im Abschnitt [ODBC].  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Schreiben von Informationen in eine Datei-DSN|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
