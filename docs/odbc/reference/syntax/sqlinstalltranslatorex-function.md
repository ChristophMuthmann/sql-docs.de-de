---
title: SQLInstallTranslatorEx Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallTranslatorEx
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallTranslatorEx
helpviewer_keywords: SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 220d3e6b0cc62c2d3d238332975c32e9c38bc030
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLInstallTranslatorEx** Fügt Informationen über ein Konvertierungsprogramm im Abschnitt "Odbcinst.ini" die Systeminformationen (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC Übersetzer Registrierungsschlüssel).  
  
 Die Funktionalität des **SQLInstallTranslatorEx** kann auch mit zugegriffen [ODBCCONF. EXE-Datei](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszTranslator*  
 [Eingabe] Dies muss eine doppelt auf Null endende Liste der Schlüsselwort-Wert-Paare, die das Konvertierungsprogramm beschreibt enthalten. Weitere Informationen zur Syntax von Schlüsselwort-Wert-Paar finden Sie unter [Konvertierer Spezifikation Unterschlüssel](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 Die **Konvertierer** und **Setup** Schlüsselwörter enthalten sein müssen, der *LpszTranslator* Zeichenfolge. Die Übersetzung DLL wird aufgeführt, mit der **Konvertierer** -Schlüsselwort und das Konvertierungsprogramm Setup DLL wird aufgeführt, mit der **Setup** Schlüsselwort. Jedes Paar wird mit NULL Byte beendet, und die gesamte Liste wird mit NULL Byte beendet. (D. h. kennzeichnen zwei NULL-Bytes am Ende der Liste.) Das Format der *LpszTranslator* lautet wie folgt:  
  
 \0Translator=*Translator-DLL-Dateiname*\0[Setup=*Setup-DLL-Dateiname*\0]\0  
  
 *lpszPathIn*  
 [Eingabe] Vollständiger Pfad, in dem das Konvertierungsprogramm ist installiert werden oder ein null-Zeiger. Wenn *LpszPath* ist ein null-Zeiger der Übersetzer in das Verzeichnis "System" installiert werden soll.  
  
 *lpszPathOut*  
 [Ausgabe] Der Pfad des Zielverzeichnisses, in dem das Konvertierungsprogramm installiert werden soll. Wenn das Konvertierungsprogramm noch nie installiert war, *LpszPathOut* ist identisch mit *LpszPathIn*. Wenn Sie vorhanden sind, die eine vorherige Installation des konvertierers, *LpszPathOut* ist der Pfad der vorherigen Installation.  
  
 *cbPathOutMax*  
 [Eingabe] Länge der *LpszPathOut.*  
  
 *pcbPathOut*  
 [Ausgabe] Gesamtanzahl der Bytes im zurückzugebenden verfügbar *LpszPathOut*. Die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als oder gleich *CbPathOutMax*, in den Ausgabepfad *LpszPathOut* auf abgeschnitten *PcbPathOutMax* minus der NULL-Abschlusszeichen. Die *PcbPathOut* -Argument ein null-Zeiger sein.  
  
 *Häufigsten*  
 [Eingabe] Typ der Anforderung. *Häufigsten* muss einen der folgenden Werte enthalten:  
  
 ODBC_INSTALL_INQUIRY: Informationen Sie über ein, in dem ein Konvertierungsprogramm installiert werden kann.  
  
 ODBC_INSTALL_COMPLETE: Führen Sie die Anforderung zur Installation.  
  
 *lpdwUsageCount*  
 [Ausgabe] Die Verwendungsanzahl des konvertierers, nachdem diese Funktion aufgerufen wurde.  
  
 Anwendungen sollten die Verwendungsanzahl nicht festlegen. ODBC wird dieser Zähler zu verwalten.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLInstallTranslatorEx** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *LpszPathOut* Argument war nicht groß genug für den Ausgabepfad enthalten. Der Puffer enthält den abgeschnittenen Pfad.<br /><br /> Die *CbPathOutMax* -Argument lautete 0 (null) und die *häufigsten* Argument war ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *häufigsten* Argument war nicht eines der folgenden:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Ungültige Schlüsselwort-Wert-Paaren|Die *LpszTranslator* Argument enthalten einen Syntaxfehler.|  
|ODBC_ERROR_INVALID_PATH|Ungültiger Installationspfad|Die *LpszPathIn* Argument enthalten einen ungültigen Pfad.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Ungültiger Parameter-Sequenz|Die *LpszTranslator* Argument keine Liste der Schlüsselwort-Wert-Paare enthalten.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Nicht inkrementiert oder dekrementiert Verwendungszähler für die Registrierung-Komponente|Installerfehler beim Verwendungsanzahl der Übersetzer zu erhöhen.|  
  
## <a name="comments"></a>Kommentare  
 **SQLInstallTranslatorEx** bietet einen Mechanismus, um nur das Konvertierungsprogramm installieren. Diese Funktion wird nicht tatsächlich keine Dateien kopiert werden. Das aufrufende Programm ist verantwortlich für das Kopieren der Dateien Konvertierungsprogramm.  
  
 **SQLInstallTranslatorEx** die Verwendungsanzahl der Komponente für das installierte Konvertierungsprogramm um 1 erhöht. Wenn bereits eine Version des konvertierers, aber die Verwendungsanzahl der Komponente für das Konvertierungsprogramm ist nicht vorhanden, wird die neue Komponente Nutzung Count-Wert auf 2 festgelegt.  
  
 Installationsprogramm der Anwendung ist verantwortlich für physisch Kopieren der Datei Konvertierer und verwalten die Verwendungsanzahl der Datei. Wenn die Konvertierer Datei noch nicht installiert wurde, muss Installationsprogramm der Anwendung kopieren Sie die Datei(en) und erstellen die Datei(en) Verwendungsanzahl. Wenn die Datei zuvor installiert hat, erhöht das Setup-Programm einfach die Verwendungsanzahl der Datei.  
  
 Wenn eine ältere Version des konvertierers zuvor von der Anwendung installiert wurde, sollte das Konvertierungsprogramm deinstalliert und anschließend erneut installieren, damit, dass der Verwendungszähler für Konvertierer Komponente gültig ist. **SQLRemoveTranslator** sollte aufgerufen werden, um die Verwendungsanzahl der Komponente zu verringern und dann **SQLInstallTranslatorEx** aufgerufen werden, um die Verwendungsanzahl der Komponente zu erhöhen. Das Setupprogramm der Anwendung muss die alte Datei oder Dateien mit der neuen Datei ersetzen. Die Verwendungsanzahl der Datei bleibt gleich, und anderen Anwendungen, die ältere Versionsdatei verwendet, werden jetzt die neuere Version verwenden.  
  
 Die Länge des Pfads in *LpszPathOut* in **SQLInstallTranslatorEx** können Sie für einen Prozess zweiphasigen installieren, sodass eine Anwendung, welche bestimmen kann *CbPathOutMax* sollten durch den Aufruf werden **SQLInstallTranslatorEx** mit einer *häufigsten* ODBC_INSTALL_INQUIRY-Modus. Dadurch wird zurückgegeben, die Gesamtanzahl der Byte in den *PcbPathOut* Puffer. **SQLInstallTranslatorEx** kann dann aufgerufen werden, mit einer *häufigsten* von ODBC_INSTALL_COMPLETE und *CbPathOutMax* Argument festgelegt wird, auf den Wert in der *PcbPathOut* Puffer plus Null-Abschlusszeichen.  
  
 Wenn Sie nicht verwenden, das zwei-Phasen-Modell für **SQLInstallTranslatorEx**, müssen Sie festlegen *CbPathOutMax*, der die Größe des Arbeitsspeichers für den Pfad des Zielverzeichnisses an die _MAX_PATH Wert als definiert definiert die in Stdlib.h, um das Abschneiden zu verhindern.  
  
 Wenn *häufigsten* ist ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** lässt keine *LpszPathOut* gleich NULL sein (oder *CbPathOutMax* 0 sein). Wenn *häufigsten* ODBC_INSTALL_COMPLETE ist, "false" wird zurückgegeben, wenn die Anzahl der Bytes, die für die Rückgabe verfügbar ist, größer als oder gleich *CbPathOutMax*, mit dem Ergebnis tritt auf, dass Daten abgeschnitten.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Eine Übersetzung Standardoption zurückgeben|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Konvertierer auswählen|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Entfernen von Konvertierer|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
