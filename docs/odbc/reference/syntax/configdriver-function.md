---
title: ConfigDriver Funktion | Microsoft Docs
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
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 100cf1cc68287c2eb5914176cb307f9a450344d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configdriver-function"></a>ConfigDriver-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.5  
  
 **Zusammenfassung**  
 **ConfigDriver** ermöglicht ein Setupprogramm, das zum Installieren und deinstallieren Funktionen ohne das Programm aufrufen **ConfigDSN**. Diese Funktion wird treiberspezifische Funktionen, z. B. treiberspezifische Systeminformationen zu erstellen und DSN Konvertierungen ausführen, während der Installation von Elementen sowie das Bereinigen von System Informationen Änderungen während der Deinstallation ausgeführt. Diese Funktion wird vom Treiber Setup, DLL oder eine separate DLL verfügbar gemacht.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argumente  
 *hwndParent*  
 [Eingabe] Handle des übergeordneten Fensters. Die Funktion wird keine Dialogfelder angezeigt, wenn das Handle null ist.  
  
 *Häufigsten*  
 [Eingabe] Typ der Anforderung. Die *häufigsten* Argument muss einen der folgenden Werte enthalten:  
  
 ODBC_INSTALL_DRIVER: Installieren eines neuen Treibers.  
  
 ODBC_REMOVE_DRIVER: Entfernen eines Treibers.  
  
 Diese Option kann auch treiberspezifische, in diesem Fall die *häufigsten* nach dem ersten Argument muss aus ODBC_CONFIG_DRIVER_MAX + 1 beginnen. Die *häufigsten* Argument für eine zusätzliche Option muss auch aus einem Wert größer als ODBC_CONFIG_DRIVER_MAX + 1 beginnen.  
  
 *lpszDriver*  
 [Eingabe] Der Name des Treibers im Schlüssel "Odbcinst.ini" die Systeminformationen registriert.  
  
 *lpszArgs*  
 [Eingabe] Eine Null-terminierte Zeichenfolge mit Argumenten für eine treiberspezifische *häufigsten*.  
  
 *lpszMsg*  
 [Ausgabe] Eine auf Null endende Zeichenfolge, die eine Ausgabenachricht von der Setup-Treiber enthält.  
  
 *cbMsgMax*  
 [Eingabe] Länge des *LpszMsg*.  
  
 *pcbMsgOut*  
 [Ausgabe] Gesamtanzahl der Bytes im zurückzugebenden verfügbar *LpszMsg*.  
  
 Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *CbMsgMax*, die Ausgabenachricht im *LpszMsg* auf abgeschnitten *CbMsgMax* minus der Null-Terminierung Zeichen. Die *PcbMsgOut* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **ConfigDriver** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert wird in den Puffer der Installer-Fehler durch einen Aufruf von gebucht **SQLPostInstallerError** und kann abgerufen werden, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *HwndParent* Argument war ungültig.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *häufigsten* Argument war nicht eines der folgenden:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> Der Treiber-spezifische Option war kleiner oder gleich ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszDriver* Argument war ungültig. Es konnte nicht in der Registrierung gefunden werden.|  
|ODBC_ERROR_REQUEST_FAILED|*Anforderung* fehlgeschlagen|Den angeforderte Vorgang konnte nicht ausgeführt werden die *häufigsten* Argument.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Treiber-Konvertierer spezifische Fehler|Ein treiberspezifischen Fehler für die kein definierten ODBC-Installer-Fehler vorliegt. Die *SzError* Argument in einem Aufruf der **SQLPostInstallerError** Funktion sollte die treiberspezifische Fehlermeldung enthalten.|  
  
## <a name="comments"></a>Kommentare  
  
### <a name="driver-specific-options"></a>Treiberspezifische Optionen  
 Eine Anwendung kann anfordern treiberspezifische Funktionen, die vom Treiber verfügbar gemacht, mit der *häufigsten* Argument. Die *häufigsten* für die erste Option ODBC_CONFIG_DRIVER_MAX plus 1, zusätzliche Optionen werden von den Wert 1 erhöht. Übergeben von Argumenten, die vom Treiber erforderlich sind, für die Funktion in eine Null-terminierte Zeichenfolge bereitgestellt werden soll die *LpszArgs* Argument. Treiber, die solche Funktionen bereitstellen, sollten eine Tabelle mit treiberspezifischen Optionen beibehalten. Die Optionen sollten vollständig im Treiber-Dokumentation dokumentiert werden. Anwendungsentwickler, die treiberspezifische Optionen verwenden, sollten bedenken, dass diese die Anwendung weniger interoperable tätigt.  
  
### <a name="messages"></a>Meldungen  
 Eine Treiber-Setup-Routine eine Textnachricht senden kann, zu einer Anwendung als eine Null-terminierte Zeichenfolge in der *LpszMsg* Puffer. Die Nachricht wird abgeschnitten und *CbMsgMax* minus der Null-Abschlusszeichen von der **ConfigDriver** funktioniert, wenn er größer als oder gleich ist *CbMsgMax* Zeichen.
