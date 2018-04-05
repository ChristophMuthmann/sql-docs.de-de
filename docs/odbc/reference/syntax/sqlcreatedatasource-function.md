---
title: SQLCreateDataSource Funktion | Microsoft Docs
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
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9077489c1380b0c750c9a725dfa50f813a5418da
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **SQLCreateDataSource** zeigt ein Dialogfeld, in dem der Benutzer eine Datenquelle hinzufügen kann.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argumente  
 *HWND*  
 [Eingabe] Handle des übergeordneten Fensters.  
  
 *lpszDS*  
 [Eingabe] Datenquellenname. *LpszDS* kann ein null-Zeiger oder eine leere Zeichenfolge sein.  
  
## <a name="returns"></a>Rückgabewert  
 **SQLCreateDataSource** gibt TRUE zurück, wenn die Datenquelle erstellt wird. Andernfalls wird "false" zurückgegeben.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLCreateDataSource** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_HWND|Ungültige Fensterhandle|Die *Hwnd* Argument war ungültig oder NULL.|  
|ODBC_ERROR_INVALID_DSN|Ungültige DSN|Die *LpszDS* Argument enthalten sind, eine Zeichenfolge, die für eine DSN ungültig war.|  
|ODBC_ERROR_REQUEST_FAILED|*Anforderung* fehlgeschlagen|Der Aufruf von **ConfigDSN** mit der Option ODBC_ADD_DSN ist fehlgeschlagen.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Die Treiber oder das Konvertierungsprogramm Setup-Bibliothek konnte nicht geladen werden.|Die Setup-Treiberbibliothek konnte nicht geladen werden.|  
|ODBC_ERROR_USER_CANCELED|Vorgang wurde vom Benutzer abgebrochen|Die Erstellung einer neuen Datenquelle wurde vom Benutzer abgebrochen.|  
|ODBC_ERROR_CREATE_DSN_FAILED|Den angeforderte DSN konnte nicht erstellt werden.|Konnte keine Verbindung zur Datenbank hergestellt werden; der Aufruf von **SQLDriverConnect** für eine erfolgreiche Verbindung nicht in Datei-DSN zurückgegeben wurde.<br /><br /> Die Datei konnte nicht geschrieben werden.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 Wenn *Hwnd* ist null, **SQLCreateDataSource** gibt "false" zurück. Andernfalls zeigt es die **neue Datenquelle erstellen** Dialogfeld mit einer Seite des Assistenten für die Auswahl des Typs der Datenquelle eingerichtet werden, wie in der folgenden Abbildung dargestellt.  
  
 ![Erstellen neue Datenquelle (Dialogfeld): Wählen Sie](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 Ist die Standardoption **Dateidatenquelle**. Wenn eine Datenquelle gewählt wurde und **Weiter** geklickt haben, wird der folgenden Seite des Assistenten, die eine Liste der installierten Treiber enthält angezeigt.  
  
 ![Erstellen neue Datenquelle (Dialogfeld): Treiber auswählen](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Wenn **"Abbrechen"** geklickt wird, wird das Dialogfeld Feld wird nicht mehr und **SQLCreateDataSource** gibt "false" zurück, mit dem Fehlercode des ODBC_ERROR_USER_CANCELED. Wenn entweder die **Benutzerdatenquelle** oder **Systemdatenquelle** Option wurde ausgewählt, die **erweitert** Schaltfläche ist nicht verfügbar.  
  
 Wenn die **Weiter** Schaltfläche geklickt wird, erfolgt eine der folgenden, abhängig davon, welche Art von Daten Quelle ausgewählt wurde:  
  
-   Wenn **Dateidatenquelle** wurde ausgewählt, wird eine Seite des Assistenten für den Benutzer zur Eingabe eines Namens für die Datei angezeigt.  
  
-   Wenn entweder **Benutzerdatenquelle** oder **Systemdatenquelle** wurde ausgewählt, wird eine Seite des Assistenten, die den Typ der Datenquelle und Treiber anzeigen zur Überprüfung, angezeigt und wann **Fertig stellen** ist geklickt haben, wird die Datenquelle klein eingerichtet werden.  
  
 Wenn **erweitert** geklickt wird auf der Seite Neue Datenquelle erstellen-Assistenten wird eine Seite des Assistenten für den Benutzer zur Eingabe von treiberspezifische Informationen angezeigt. Geben Sie in das Textfeld dieses Dialogfelds die Treiber und Schlüsselwörter, die zurückgegeben wird, ein senkrechter wie in der folgenden Abbildung dargestellt.  
  
 ![Erweiterte Einstellungen zum Datei-DSN erstellen (Dialogfeld)](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Zusätzliche Treiber-spezifische Schlüsselwörter finden Sie unter der Beschreibung der **SQLDriverConnect**. Alle außer **DSN** sind zulässig.  
  
 Die Standardeinstellung für die **überprüfen Sie diese Verbindung** Option ist "true". Diese Standardeinstellung gilt, und zwar unabhängig davon, ob dieser Seite des Assistenten aktiviert ist. Wenn **OK** geklickt wird, wird die Zeichenfolge in das Textfeld angegeben und die **überprüfen Sie diese Verbindung** Optionswert zwischengespeichert werden. (Wenn die **schließen** Schaltfläche oder **"Abbrechen"** geklickt wird, werden alle neu eingegebenen treiberspezifische Informationen geht verloren, da die Zeichenfolge in das Textfeld angegeben und die **überprüfen Sie diese Verbindung** Optionswert werden nicht zwischengespeichert.)  
  
 Wenn **Dateidatenquelle** in der ersten Seite des Assistenten ausgewählt wurde, und klicken Sie dann nach ein Treiber ausgewählt wurde, und das Schlüsselwortwerte auf der Seite Erweitert des Assistenten eingegeben wurden, der Benutzer so aufgefordert wird, um einen Dateinamen eingeben. Klicken Sie auf **Durchsuchen** für einen Dateinamen in diesem Fall das Standardverzeichnis in Suchen der **Durchsuchen** Feld durch eine Kombination von CommonFileDir in HKEY_LOCAL_MACHINE\SOFTWARE\ angegebene Pfad angegeben ist Microsoft\Windows\CurrentVersion und "ODBC\DataSources". (Wenn CommonFileDir "C:\Program Files\Common Files" war, würde das Standardverzeichnis "C:\Programme\Microsoft c:\Programme\Gemeinsame Dateien\ODBC\Data Sources" sein.)  
  
 Wenn ein Dateiname eingegeben wurde und **Weiter** geklickt wird, wird die Datei eingegebene Name wird auf Gültigkeit anhand der standard-Dateibenennung Regeln des Betriebssystems überprüft. Wenn der Dateiname ungültig ist, wird der Benutzer eine Fehlermeldung angezeigt, dass ein ungültiger Dateiname eingegeben wurde benachrichtigt. Nachdem der Benutzer das Meldungsfeld bestätigt hat, wird der Fokus auf der Assistentenseite zurückgegeben, in dem der Dateiname eingegeben wird. Wenn der Dateiname gültig ist, wird eine Seite des Assistenten, die die ausgewählte Schlüsselwort-Wert-Paare zur Überprüfung angezeigt, wie in der folgenden Abbildung dargestellt.  
  
 ![Erstellen neue Datenquelle (Dialogfeld): Überprüfen Sie](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Wenn **Fertig stellen** geklickt wird und **Dateidatenquelle** ausgewählt wurde, als Typ der Datenquelle, und wenn die **Verbindung überprüfen** Option ist "true",  **SQLDriverConnect** aufgerufen wird und die **SAVEFILE** und **Treiber** Schlüsselwörter. Die *DriverCompletion* Argument auf SQL_DRIVER_COMPLETE festgelegt ist. Der Dateiname für die **SAVEFILE** -Schlüsselwort ist der Name, der eingegeben wurde oder ausgewählt und den Namen des Treibers für die **Treiber** -Schlüsselwort ist der Name, der ausgewählt wurde. Wenn eine treiberspezifische Verbindungszeichenfolge auf der Seite Erweitert des Assistenten angegeben wurde, wird diese Zeichenfolge angefügt, nach der **Treiber** Schlüsselwort.  
  
 Wenn **SQLDriverConnect** gibt SQL_SUCCESS zurück, der Treiber-Manager wurde die Datei-DSN erstellt. **SQLCreateDataSource** gibt "true" zurück. Wenn **SQLDriverConnect** gibt keinen SQL_SUCCESS, eine Warnmeldung zurück Feld zeigt an, dass keine Verbindung mit der Datenquelle hergestellt werden konnte. Ein DSN mit minimalen Verbindungsinformationen kann dennoch erstellt werden. Dieses Meldungsfeld ermöglicht dem Benutzer das "Abbrechen", oder fahren Sie mit der Datei-DSN-Erstellung fort.  
  
 Dieser Prozess wird fortgesetzt, wenn der Benutzer entscheidet, um den Vorgang fortzusetzen, erstellen den DSN, als ob die **Verbindung überprüfen** Option auf "false" festgelegt wurden. Wenn der Benutzer entscheidet, "Abbrechen", wird "false" zurückgegeben, für die **SQLCreateDataSource** mit einem Fehlercode von ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Wenn **Dateidatenquelle** wurde als Typ der Datenquelle ausgewählt und die **Verbindung überprüfen** Option ist "false", Datei-DSN wird erstellt, mit der **Treiber** Schlüsselwort und benutzerdefinierte Verbindungszeichenfolge (sofern vorhanden) von der erweiterten Assistenten-Seite. Wenn die Erstellung erfolgreich war, wird "true" zurückgegeben, für die **SQLCreateDataSource**. Wenn die Erstellung der Datei nicht erfolgreich war, benachrichtigt eine Fehlermeldung zu den Benutzer der Fehler vom Betriebssystem zurückgegeben wurde. "False" wird zurückgegeben, für die **SQLCreateDataSource** mit einem Fehlercode von ODBC_ERROR_CREATE_DSN_FAILED. Weitere Informationen zu Datenquellen finden Sie unter [Herstellen einer Verbindung mithilfe von Dateidatenquellen](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), oder finden Sie unter [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Wenn **Benutzer** oder **Systemdatenquelle** ausgewählt wurde, als den Datenquellentyp **ConfigDSN** Bibliothek heißt in der Setup-Treiber mit der ODBC_ADD_DSN  *Häufigsten*. Weitere Informationen finden Sie unter [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Verwalten von Datenquellen|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
