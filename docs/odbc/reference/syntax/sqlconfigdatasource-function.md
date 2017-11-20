---
title: SQLConfigDataSource-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d1fddaf67cfbdb8f8c8df7e66b86a681ca2e23d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0  
  
 **Zusammenfassung**  
 **SQLConfigDataSource** hinzufügt, ändert oder löscht Sie Datenquellen.  
  
 Die Funktionalität des **SQLConfigDataSource** kann auch mit zugegriffen [ODBCCONF. EXE-Datei](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argumente  
 *hwndParent*  
 [Eingabe] Handle des übergeordneten Fensters. Die Funktion wird keine Dialogfelder angezeigt, wenn das Handle null ist.  
  
 *Häufigsten*  
 [Eingabe] Typ der Anforderung. Die *häufigsten* Argument muss einen der folgenden Werte enthalten:  
  
 ODBC_ADD_DSN: Fügen Sie eine neue Datenquelle für den Benutzer hinzu.  
  
 ODBC_CONFIG_DSN: Konfigurieren (ändern) einer vorhandenen Datenquelle für den Benutzer.  
  
 ODBC_REMOVE_DSN: Entfernen einer vorhandenen Datenquelle für den Benutzer.  
  
 ODBC_ADD_SYS_DSN: Fügen Sie eine neue Systemdatenquelle hinzu.  
  
 ODBC_CONFIG_SYS_DSN: Ändern einer vorhandenen System-Datenquelle.  
  
 Mit ODBC_REMOVE_SYS_DSN: Entfernen einer vorhandenen System-Datenquelle.  
  
 ODBC_REMOVE_DEFAULT_DSN: Entfernen Sie den Standardabschnitt Data Source-Spezifikation aus der Systeminformationen. (Es entfernt auch Spezifikation den Standardabschnitt-Treiber aus den Eintrag "Odbcinst.ini" in die Systeminformationen. Dies *häufigsten* führt die gleiche Funktion wie die veraltete **SQLRemoveDefaultDataSource** Funktion.) Wenn diese Option angegeben wird, alle anderen Parameter im Aufruf von **SQLConfigDataSource** sollte Null-Werte, wenn sie nicht NULL sind, sie werden ignoriert.  
  
 *lpszDriver*  
 [Eingabe] Beschreibung (normalerweise der Name des zugehörigen DBMS) anstelle des Namens des physischen Treiber präsentiert.  
  
 *lpszAttributes*  
 [Eingabe] Eine doppelt auf Null endende Liste der Attribute in Form von Schlüsselwort-Wert-Paaren. Weitere Informationen finden Sie unter [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten. Wenn kein Eintrag in der Systeminformationen ist vorhanden, wenn diese Funktion aufgerufen wird, gibt die Funktion "false" zurück.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLConfigDataSource** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *HwndParent* Argument war ungültig oder NULL.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *häufigsten* Argument war nicht eines der folgenden:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszDriver* Argument war ungültig. Es konnte nicht in der Registrierung gefunden werden.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Ungültige Schlüsselwort-Wert-Paaren|Die *LpszAttributes* Argument enthalten einen Syntaxfehler.|  
|ODBC_ERROR_REQUEST_FAILED|*Anforderung* fehlgeschlagen|Der Installer konnte nicht ausgeführt werden, den angeforderte Vorgang der *häufigsten* Argument. Der Aufruf von **ConfigDSN** ist fehlgeschlagen.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Die Treiber oder das Konvertierungsprogramm Setup-Bibliothek konnte nicht geladen werden.|Die Setup-Treiberbibliothek konnte nicht geladen werden.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLConfigDataSource** verwendet den Wert der *LpszDriver* den vollständigen Pfad der Setup-DLL für den Treiber von der Systeminformationen zu lesen. Es lädt die DLL und ruft **ConfigDSN** mit den gleichen Argumenten, die an sie übergeben wurden.  
  
 **SQLConfigDataSource** gibt "false" zurück, wenn es nicht gefunden, oder laden die Setup-DLL ist oder wenn der Benutzer das Dialogfeld abbricht. Andernfalls wird den Status vom erhalten zurückgegeben **ConfigDSN**.  
  
 **SQLConfigDataSource** ordnet das System-DSN *häufigsten*s, um die Benutzer-DSN *häufigsten*s (ODBC_ADD_SYS_DSN, ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN und ODBC_REMOVE_SYS _DSN auf ODBC_REMOVE_DSN). Benutzer und System-DSNs unterscheiden **SQLConfigDataSource** legt der Installer Konfigurationsmodus entsprechend der folgenden Tabelle. Vor der Rückgabe, **SQLConfigDataSource** Konfigurationsmodus auf BOTHDSN zurückgesetzt. **ConfigDSN** (von-Treibern implementiert) sollten Aufrufen **SQLWriteDSNToIni** und **SQLWritePrivateProfileString** um ein System-DSN zu unterstützen. Weitere Informationen finden Sie unter [ConfigDSN Funktion](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*Häufigsten*|Konfigurationsmodus|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|MIT ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (in der Setup-DLL)|  
|Entfernen einen Datenquellennamen aus der Systeminformationen|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Die Systeminformationen hinzugefügt einen Datenquellennamen|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|

