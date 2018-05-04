---
title: ConfigDSN Funktion | Microsoft Docs
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
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a8b75fb1b87a4f6199999e5d5e33d8cd0083bac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configdsn-function"></a>ConfigDSN-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0  
  
 **Zusammenfassung**  
 **ConfigDSN** hinzufügt, ändert oder löscht Sie Datenquellen aus der Systeminformationen. Sie können den Benutzer zur Verbindungsinformationen aufzufordern. Sie können in der Treiber-DLL oder eine separate Installation DLL sein.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL ConfigDSN(  
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
  
 ODBC_ADD_DSN: Fügen Sie eine neue Datenquelle hinzu.  
  
 ODBC_CONFIG_DSN: Konfigurieren (ändern) einer vorhandenen Datenquelle.  
  
 ODBC_REMOVE_DSN: Entfernen einer vorhandenen Datenquelle.  
  
 *lpszDriver*  
 [Eingabe] Beschreibung (normalerweise der Name des zugehörigen DBMS) anstelle des Namens des physischen Treiber präsentiert.  
  
 *lpszAttributes*  
 [Eingabe] Eine doppelt auf Null endende Liste der Attribute in Form von Schlüsselwort-Wert-Paaren. Weitere Informationen finden Sie unter "Kommentare".  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **ConfigDSN** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert wird in den Puffer der Installer-Fehler durch einen Aufruf von gebucht **SQLPostInstallerError** und erhalten Sie, indem Aufrufen **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *HwndParent* Argument war ungültig.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Ungültige Schlüsselwort-Wert-Paaren|Die *LpszAttributes* Argument enthalten einen Syntaxfehler.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszDriver* Argument war ungültig. Es konnte nicht in der Registrierung gefunden werden.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *häufigsten* Argument war nicht eines der folgenden:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*Anforderung* fehlgeschlagen|Den angeforderte Vorgang konnte nicht ausgeführt werden die *häufigsten* Argument.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Treiber-Konvertierer spezifische Fehler|Ein treiberspezifischen Fehler für die kein definierten ODBC-Installer-Fehler vorliegt. Die *SzError* Argument in einem Aufruf der **SQLPostInstallerError** Funktion sollte die treiberspezifische Fehlermeldung enthalten.|  
  
## <a name="comments"></a>Kommentare  
 **ConfigDSN** empfängt Verbindungsinformationen vom Installationsprogramm DLL als eine Liste der Attribute in Form von Schlüsselwort-Wert-Paaren. Jedes Paar wird durch ein Nullbyte beendet, und die gesamte Liste wird mit null Byte beendet. (D. h. kennzeichnen zwei null-Bytes am Ende der Liste.) Leerzeichen sind nach dem Gleichheitszeichen im Schlüsselwort-Wert-Paar nicht zulässig. **ConfigDSN** lässt Schlüsselwörter, die keine gültigen Schlüsselwörter für sind **SQLBrowseConnect** und **SQLDriverConnect**. **ConfigDSN** unterstützt allerdings nicht unbedingt alle Schlüsselwörter, die gültigen Schlüsselwörter für **SQLBrowseConnect** und **SQLDriverConnect**. (**ConfigDSN** nimmt nicht an die **Treiber** Schlüsselwort.) Die Schlüsselwörter von verwendet die **ConfigDSN** -Funktion muss die Optionen, die zum Neuerstellen der Datenquelle mithilfe der Funktion für automatische Einrichtung des Installationsprogramms erforderlich unterstützt. Wenn die Verwendungen der der **ConfigDSN** Werte und die Werte der Verbindungszeichenfolgen sind identisch, die gleichen Schlüsselwörter verwendet werden sollte.  
  
 Wie in **SQLBrowseConnect** und **SQLDriverConnect**, Schlüsselwörter und deren Werte dürfen nicht die **[]{}(),? \*=! @** Zeichen und der Wert der **DSN** Schlüsselwort darf nicht ausschließlich aus Leerzeichen bestehen. Aufgrund der Grammatik Registrierung Schlüsselwörter und Namen von Datenquellen können nicht den umgekehrten Schrägstrich enthalten (\\) Zeichen.  
  
 **ConfigDSN** sollten Aufrufen **SQLValidDSN** überprüfen die Länge der Namen der Datenquelle und stellen Sie sicher, dass keine ungültigen Zeichen im Namen enthalten sind. Wenn der Name der Datenquelle länger als SQL_MAX_DSN_LENGTH ist oder ungültige Zeichen enthält **SQLValidDSN** gibt einen Fehler zurück und **ConfigDSN** gibt einen Fehler zurück. Die Länge der Namen der Datenquelle wird auch durch überprüft **SQLWriteDSNToIni**.  
  
 Um eine Datenquelle zu konfigurieren, die Benutzer-ID, Kennwort und Datenbankname ist erforderlich, übergeben eine setupanwendung z. B. die folgenden Schlüsselwort-Wert-Paaren:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Weitere Informationen zu diesen Schlüsselwörtern finden Sie unter [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) und in der Dokumentation des Treibers.  
  
 Um ein Dialogfeld anzuzeigen *HwndParent* darf nicht null sein.  
  
## <a name="adding-a-data-source"></a>Hinzufügen von Datenquellen  
 Wenn an ein Datenquellennamen übergeben wird **ConfigDSN** in *LpszAttributes*, **ConfigDSN** stellt sicher, dass der Name gültig ist. Wenn der Name der Datenquelle einen existierender Datenquellenname übereinstimmt und *HwndParent* ist null, **ConfigDSN** überschreibt den vorhandenen Namen. Wenn sie einen vorhandenen Namen übereinstimmt und *HwndParent* ist ungleich null, **ConfigDSN** fordert den Benutzer auf den vorhandenen Namen zu überschreiben.  
  
 Wenn *LpszAttributes* genügend Informationen für die Verbindung mit einer Datenquelle enthält **ConfigDSN** hinzufügen können, die Datenquelle oder zeigt ein Dialogfeld, mit denen der Benutzer kann die Verbindungsinformationen zu ändern. Wenn *LpszAttributes* enthält nicht genügend Informationen für die Verbindung mit einer Datenquelle **ConfigDSN** müssen die erforderliche zu ermitteln, ob *HwndParent* ist ungleich null, Es zeigt ein Dialogfeld, um die Informationen vom Benutzer abgerufen werden.  
  
 Wenn **ConfigDSN** zeigt ein Dialogfeld, es muss alle Verbindungsinformationen in übergebenen anzeigen *LpszAttributes*. Insbesondere, wenn Sie ein Datenquellennamen, übergebene **ConfigDSN** zeigt diese Namen, jedoch lässt sich nicht auf den Benutzer aus, um ihn zu ändern. **ConfigDSN** können Standardwerte für nicht übergebenen Verbindungsinformationen angeben *LpszAttributes*.  
  
 Wenn **ConfigDSN** kann nicht abgerufen werden vollständige Verbindungsinformationen für eine Datenquelle wird FALSE zurückgegeben.  
  
 Wenn **ConfigDSN** erhalten vollständige Verbindungsinformationen für eine Datenquelle, sondern ruft **SQLWriteDSNToIni** im Installationsprogramm DLL-Datei Odbc.ini Datei (oder Registrierung) Angabe der neuen Datenquelle hinzugefügt. **SQLWriteDSNToIni** wird der Name der Datenquelle im Abschnitt [ODBC-Datenquellen], Abschnitt Data Source-Spezifikation erstellt und fügt die **Treiber** Schlüsselwort mit der treiberbeschreibung "als Wert. **ConfigDSN** Aufrufe **SQLWritePrivateProfileString** im Installationsprogramm DLL-Datei fügen alle zusätzlichen Schlüsselwörter und Werte, die vom Treiber verwendet wird.  
  
## <a name="modifying-a-data-source"></a>Ändern einer Datenquelle  
 Um eine Datenquelle zu ändern, ein Datenquellennamen übergeben werden muss, um **ConfigDSN** in *LpszAttributes*. **ConfigDSN** überprüft, ob der Name der Datenquelle in der Datei Odbc.ini (oder ein Registrierungsschlüsselwert).  
  
 Wenn *HwndParent* ist null, **ConfigDSN** verwendet die Informationen in *LpszAttributes* so ändern Sie die Informationen in der Datei Odbc.ini (oder Registrierung). Wenn *HwndParent* ist ungleich null, **ConfigDSN** wird anhand der Informationen in das Dialogfeld *LpszAttributes*; Informationen, die nicht in *LpszAttributes* , Informationen aus der Systeminformationen verwendet. Der Benutzer kann die Informationen, bevor ändern **ConfigDSN** speichert diesen in die Systeminformationen.  
  
 Wenn der Name der Datenquelle geändert wurde, **ConfigDSN** ruft zuerst **SQLRemoveDSNFromIni** im Installer source DLL-Datei entfernen Sie die vorhandenen Daten Spezifikation aus der Datei Odbc.ini (oder Registrierung). Es folgt dann die Schritte im vorherigen Abschnitt der Angabe der neuen Datenquelle hinzufügen. Wenn der Name der Datenquelle nicht geändert wurde, **ConfigDSN** Aufrufe **SQLWritePrivateProfileString** im Installationsprogramm DLL-Datei vornehmen anderer Änderungen. **ConfigDSN** möglicherweise nicht löschen oder ändern Sie den Wert, der die **Treiber** Schlüsselwort.  
  
## <a name="deleting-a-data-source"></a>Löschen einer Datenquelle  
 Um eine Datenquelle zu löschen, ein Datenquellennamen übergeben werden muss, um **ConfigDSN** in *LpszAttributes*. **ConfigDSN** überprüft, ob der Name der Datenquelle in der Datei Odbc.ini (oder ein Registrierungsschlüsselwert). Er ruft dann **SQLRemoveDSNFromIni** im Installationsprogramm-DLL für die Datenquelle zu entfernen.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen einer Datenquelle|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Abrufen eines Werts aus der Datei Odbc.ini oder in der Registrierung|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Entfernen die Standarddatenquelle|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Entfernen einen Datenquellennamen Odbc.ini (oder der Registrierung)|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Hinzufügen von einem Datenquellennamen Odbc.ini (oder Registrierung)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Schreiben einen Wert in der Datei Odbc.ini oder in der Registrierung|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
