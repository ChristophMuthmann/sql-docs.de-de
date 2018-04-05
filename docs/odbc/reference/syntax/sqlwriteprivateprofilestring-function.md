---
title: SQLWritePrivateProfileString Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 081d91ac2c257fbaa60b93de24dd134ea698bcd9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **SQLWritePrivateProfileString** schreibt einen Wertnamen und die Daten in den Unterschlüssel Odbc.ini Informationen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszSection*  
 [Eingabe] Verweist auf einen Null-terminierte Zeichenfolge, die mit dem Namen des Abschnitts, in dem die Zeichenfolge kopiert werden. Wenn der Abschnitt nicht vorhanden ist, wird er erstellt. Der Name des Abschnitts ist unabhängig von Groß-/Kleinschreibung. die Zeichenfolge kann eine beliebige Kombination von Groß- und Kleinbuchstaben sein.  
  
 *lpszEntry*  
 [Eingabe] Verweist auf einen Null-terminierte Zeichenfolge, die mit dem Namen des Schlüssels mit einer Zeichenfolge zugeordnet werden soll. Wenn der Schlüssel nicht im angegebenen Abschnitt vorhanden ist, wird es erstellt. Wenn dieses Argument NULL ist, wird der gesamte Abschnitt, einschließlich der Einträge im Abschnitt mit gelöscht.  
  
 *lpszString*  
 [Eingabe] Verweist auf eine Null-terminierte Zeichenfolge in die Datei geschrieben werden sollen. Wenn dieses Argument NULL ist, der Schlüssel verweist, zu der *LpszEntry* Argument wird gelöscht.  
  
 *lpszFilename*  
 [Ausgabe] Zeigt auf eine auf Null endende Zeichenfolge, die den Namen der Initialisierungsdatei.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLWritePrivateProfileString** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_REQUEST_FAILED|Fehler bei der Anforderung|Die angeforderte Systeminformationen konnte nicht geschrieben werden.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLWritePrivateProfileString** wird als eine einfache Möglichkeit, Port-Treiber und Treiber-Setup-DLLs von Microsoft® Windows® für Microsoft Windows/Windows 2000 bereitgestellt. Aufrufe von **Systemaufrufen** schreiben, der eine Profil-Zeichenfolge in die Datei Odbc.ini ersetzt werden sollte, durch Aufrufe von **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** Aufrufe von Funktionen in der Win32®-API auf die angegebenen Wertnamen und die Daten auf den Unterschlüssel Odbc.ini Informationen hinzufügen.  
  
 Eine Konfigurationsmodus gibt an, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen ist. Wenn der DSN eine Benutzer-DSN ist (die Statusvariable USERDSN_ONLY), schreibt die Funktion auf den Eintrag der Odbc.ini in HKEY_CURRENT_USER. Wenn der DSN eine System-DSN (SYSTEMDSN_ONLY) ist, schreibt die Funktion zum Eintrag Odbc.ini im HKEY_LOCAL_MACHINE. Sollte die Statusvariable BOTHDSN ist, wird das von HKEY_CURRENT_USER versucht, und falls dies fehlschlägt, wird die HKEY_LOCAL_MACHINE verwendet.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Abrufen eines Werts aus der Systeminformationen|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
