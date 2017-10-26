---
title: SQLGetPrivateProfileString Funktion | Microsoft Docs
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
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49c1939845ed63f295054afab629389f3e1bbcaf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **SQLGetPrivateProfileString** Ruft eine Liste der Namen von Werten oder Daten, die Systeminformationen Wert entspricht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszSection*  
 [Eingabe] Zeigt auf eine auf Null endende Zeichenfolge, die den Abschnitt mit den Schlüsselnamen angibt. Wenn dieses Argument NULL ist, kopiert die Funktion alle Abschnittsnamen in der Datei in den angegebenen Puffer.  
  
 *lpszEntry*  
 [Eingabe] Verweist auf die Null-terminierte Zeichenfolge mit dem Schlüsselnamen, deren zugeordnete Zeichenfolge ist, abgerufen werden sollen. Wenn dieses Argument NULL ist, werden alle Schlüssel Namen angegeben werden, indem Sie im Bereich der *LpszSection* Argument in den angegebenen Puffer kopiert werden die *RetBuffer* Argument.  
  
 *lpszDefault*  
 [Eingabe] Zeigt auf eine auf Null endende Zeichenfolge, die der Standardwert für den angegebenen Schlüssel gibt an, wenn der Schlüssel in der Initialisierungsdatei gefunden werden kann. Dieses Argument darf nicht NULL sein.  
  
 *RetBuffer*  
 [Ausgabe] Verweist auf den Puffer, der die abgerufenen Zeichenfolge empfängt.  
  
 *cbRetBuffer*  
 [Eingabe] Gibt die Größe in Zeichen des Puffers an, die durch die *RetBuffer* Argument.  
  
 *lpszFilename*  
 [Eingabe] Zeigt auf eine auf Null endende Zeichenfolge, die den Namen der Initialisierungsdatei. Wenn dieses Argument nicht über einen vollständigen Pfad zu der Datei enthält, wird standardmäßig das Verzeichnis durchsucht.  
  
## <a name="returns"></a>Rückgabewert  
 **SQLGetPrivateProfileString** gibt einen ganzzahligen Wert, der die Anzahl der gelesenen Zeichen angibt.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn bei einem Aufruf **SQLGetPrivateProfileString** fehlschlägt, eine zugeordnete * \*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die * \*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLGetPrivateProfileString** wird als eine einfache Möglichkeit, Port-Treiber und Treiber-Setup-DLLs von Microsoft® Windows® für Microsoft Windows/Windows 2000 bereitgestellt. Aufrufe von **GetPrivateProfileString über** , abrufen, die mit eine Profil Zeichenfolge aus der Datei Odbc.ini ersetzt werden sollte, Aufrufe von **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** Aufrufe von Funktionen in der Win32®-API zum Abrufen der angeforderten Namen von Werten oder Daten, die auf einen Wert des Unterschlüssels Odbc.ini Informationen entspricht.  
  
 Der Konfigurationsmodus (entsprechend der Festlegung durch **SQLSetConfigMode**) gibt an, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen ist. Wenn der DSN eine Benutzer-DSN ist (der Konfigurationsmodus USERDSN_ONLY), liest die Funktion aus den Eintrag der Odbc.ini in HKEY_CURRENT_USER. Wenn der DSN eine System-DSN (SYSTEMDSN_ONLY) ist, liest die Funktion aus den Eintrag der Odbc.ini in HKEY_LOCAL_MACHINE. Sollte der Konfigurationsmodus BOTHDSN ist, wird das von HKEY_CURRENT_USER versucht, und falls dies fehlschlägt, gibt HKEY_LOCAL_MACHINE dient.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Schreiben einen Wert in die Systeminformationen|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|

