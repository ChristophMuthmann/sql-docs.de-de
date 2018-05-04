---
title: SQLConfigDriver Funktion | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0e1057eab4abdb2e7b9ee0109f56c5732cc2724
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.5  
  
 **Zusammenfassung**  
 **SQLConfigDriver** lädt die Setup-DLL für geeigneter Treiber und ruft die **ConfigDriver** Funktion.  
  
 Die Funktionalität des **SQLConfigDriver** kann auch mit zugegriffen [ODBCCONF. EXE-Datei](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argumente  
 *hwndParent*  
 [Eingabe] Handle des übergeordneten Fensters. Die Funktion wird keine Dialogfelder angezeigt, wenn das Handle null ist.  
  
 *Häufigsten*  
 [Eingabe] Typ der Anforderung. *Häufigsten* muss einen der folgenden Werte enthalten:  
  
 ODBC_CONFIG_DRIVER: Ändert den Verbindungs-pooling Timeout, die vom Treiber verwendet wird.  
  
 ODBC_INSTALL_DRIVER: Installiert einen neuen Treiber.  
  
 ODBC_REMOVE_DRIVER: Entfernt einen vorhandenen Treiber.  
  
 Diese Option kann auch treiberspezifische, in diesem Fall die *häufigsten* für die erste Option muss von ODBC_CONFIG_DRIVER_MAX + 1 beginnen. Die *häufigsten* für eine zusätzliche Option muss auch aus einem Wert größer als ODBC_CONFIG_DRIVER_MAX + 1 beginnen.  
  
 *lpszDriver*  
 [Eingabe] Der Name des Treibers in die Systeminformationen registriert.  
  
 *lpszArgs*  
 [Eingabe] Eine auf Null endende Zeichenfolge, die Argumente für eine treiberspezifische enthält *häufigsten*.  
  
 *lpszMsg*  
 [Ausgabe] Eine auf Null endende Zeichenfolge, die eine Ausgabenachricht von der Setup-Treiber enthält.  
  
 *cbMsgMax*  
 [Eingabe] Länge der *LpszMsg.*  
  
 *pcbMsgOut*  
 [Ausgabe] Gesamtanzahl der Bytes im zurückzugebenden verfügbar *LpszMsg*. Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *CbMsgMax*, die Ausgabenachricht im *LpszMsg* auf abgeschnitten *CbMsgMax* minus der Null-Terminierung Zeichen. Die *PcbMsgOut* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLConfigDriver** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *LpszMsg* Argument war ungültig.|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *HwndParent* Argument war ungültig.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *häufigsten* Argument war nicht eines der folgenden:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> Die *häufigsten* Argument wurde eine treiberspezifische-Option, die kleiner oder gleich ODBC_CONFIG_DRIVER_MAX wurde.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszDriver* Argument war ungültig. Es konnte nicht in der Registrierung gefunden werden.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Ungültige Schlüsselwort-Wert-Paaren|Die *LpszArgs* Argument enthalten einen Syntaxfehler.|  
|ODBC_ERROR_REQUEST_FAILED|*Anforderung* fehlgeschlagen|Der Installer konnte nicht ausgeführt werden, den angeforderte Vorgang der *häufigsten* Argument. Der Aufruf von **ConfigDriver** ist fehlgeschlagen.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Die Treiber oder das Konvertierungsprogramm Setup-Bibliothek konnte nicht geladen werden.|Die Setup-Treiberbibliothek konnte nicht geladen werden.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLConfigDriver** ermöglicht es einer Anwendung zum Aufrufen des Treibers **ConfigDriver** routinemäßige ohne den Namen kennen und die treiberspezifischen-Setup-DLL zu laden. Ein Setupprogramm ruft diese Funktion nach Abschluss des Setups von Treiber, die DLL installiert wurde. Das aufrufende Programm sollten bedenken, dass diese Funktion möglicherweise nicht für alle Treiber verfügbar. In einem solchen Fall muss das aufrufende Programm ohne Fehler fortgesetzt werden.  
  
## <a name="driver-specific-options"></a>Treiberspezifische Optionen  
 Eine Anwendung kann anfordern treiberspezifische Funktionen, die vom Treiber verfügbar gemacht, mit der *häufigsten* Argument. Die *häufigsten* für die erste Option ODBC_CONFIG_DRIVER_MAX + 1, zusätzliche Optionen werden von den Wert 1 erhöht. Übergeben von Argumenten, die vom Treiber erforderlich sind, für die Funktion in eine Null-terminierte Zeichenfolge bereitgestellt werden soll die *LpszArgs* Argument. Treiber, die solche Funktionen bereitstellen, sollten eine Tabelle mit treiberspezifischen Optionen beibehalten. Die Optionen sollten vollständig im Treiber-Dokumentation dokumentiert werden. Anwendungsentwickler, die treiberspezifische Optionen verwenden, sollten bedenken, dass diese Verwendung die Anwendung weniger interoperable tätigt.  
  
## <a name="setting-connection-pooling-timeout"></a>Verbindungs-Pooling-Timeout festlegen  
 Verbindungspooling Timeouteigenschaften kann festgelegt werden, wenn Sie die Konfiguration des Treibers festlegen. **SQLConfigDriver** aufgerufen wird und ein *häufigsten* von ODBC_CONFIG_DRIVER und *LpszArgs* festgelegt **CPTimeout**. **CPTimeout** bestimmt den Zeitraum, der eine Verbindung im Verbindungspool verbleiben kann, ohne verwendet wird. Wenn das Timeout abläuft, wird die Verbindung geschlossen und aus dem Pool entfernt. Der Standardtimeout beträgt 60 Sekunden.  
  
 Wenn **SQLConfigDriver** aufgerufen wird und *häufigsten* ODBC_INSTALL_DRIVER oder ODBC_REMOVE_DRIVER festgelegt, der Treiber-Manager lädt, die Setup-DLL für geeigneter Treiber und ruft die  **ConfigDriver** Funktion. Wenn **SQLConfigDriver** aufgerufen wird und ein *häufigsten* von ODBC_CONFIG_DRIVER, gesamte Verarbeitung erfolgt im ODBC-Installer, damit der Treiber-Setup-DLL nicht geladen werden.  
  
## <a name="messages"></a>Meldungen  
 Eine Treiber-Setup-Routine eine Textnachricht senden kann, zu einer Anwendung als Null endende Zeichenfolgen, in der *LpszMsg* Puffer. Die Nachricht wird abgeschnitten und *CbMsgMax* minus der Null-Abschlusszeichen von der **ConfigDriver** funktioniert, wenn er größer als oder gleich ist *CbMsgMax* Zeichen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen eines Treibers|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(in der Setup-DLL)|  
|Entfernen die Standarddatenquelle|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
