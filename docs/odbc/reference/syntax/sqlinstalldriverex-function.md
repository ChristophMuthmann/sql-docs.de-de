---
title: SQLInstallDriverEx Funktion | Microsoft Docs
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
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4179bf04131f256c5a37cb01c079035a569a07af
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLInstallDriverEx** den Eintrag "Odbcinst.ini" in die Systeminformationen Informationen über den Treiber hinzugefügt, und erhöht des Treibers *UsageCount* um 1. Jedoch, wenn eine Version der Treiber ist bereits vorhanden, aber die *UsageCount* Wert für der Treiber nicht vorhanden ist, die neue *UsageCount* Wert auf 2 festgelegt ist.  
  
 Diese Funktion wird nicht tatsächlich keine Dateien kopiert werden. Es ist die Zuständigkeit für das aufrufende Programm die Treiberdateien ordnungsgemäß in das Zielverzeichnis kopiert.  
  
 Die Funktionalität des **SQLInstallDriverEx** kann auch mit zugegriffen [ODBCCONF. EXE-Datei](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszDriver*  
 [Eingabe] Um die treiberbeschreibung (normalerweise der Name des zugehörigen DBMS) anstelle des Namens des physischen Treiber präsentiert. Die *LpszDriver* Argument muss eine doppelt auf Null endende Liste der Schlüsselwort-Wert-Paare, beschreibt des Treibers enthalten. Weitere Informationen zu den Schlüsselwort-Wert-Paare, finden Sie unter [Treiber Spezifikation Unterschlüssel](../../../odbc/reference/install/driver-specification-subkeys.md). Weitere Informationen zu den doppelt auf Null endende Zeichenfolge, finden Sie unter [ConfigDSN Funktion](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Eingabe] Vollständiger Pfad des Zielverzeichnisses der Installation oder ein null-Zeiger. Wenn *LpszPathIn* ist ein null-Zeiger, die Treiber in das Verzeichnis "System" installiert werden soll.  
  
 *lpszPathOut*  
 [Ausgabe] Der Pfad für das Zielverzeichnis, in dem der Treiber installiert werden soll. Wenn der Treiber noch nicht installiert wurde, *LpszPathOut* sollten identisch sein *LpszPathIn*. Wenn der Treiber zuvor installiert war, *LpszPathOut* ist der Pfad der vorherigen Installation.  
  
 *cbPathOutMax*  
 [Eingabe] Länge des *LpszPathOut*.  
  
 *pcbPathOut*  
 [Ausgabe] Gesamtanzahl der Bytes (ausgenommen die Null-Abschlusszeichen) verfügbar, für die zurückzugebenden in *LpszPathOut*. Die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als oder gleich *CbPathOutMax*, in den Ausgabepfad *LpszPathOut* auf abgeschnitten *CbPathOutMax* minus der NULL-Abschlusszeichen. Die *PcbPathOut* -Argument ein null-Zeiger sein.  
  
 *Häufigsten*  
 [Eingabe] Typ der Anforderung. Die *häufigsten* Argument muss einen der folgenden Werte enthalten:  
  
 ODBC_INSTALL_INQUIRY: Informationen Sie über ein, in denen ein Treiber installiert werden kann.  
  
 ODBC_INSTALL_COMPLETE: Führen Sie die Anforderung zur Installation.  
  
 *lpdwUsageCount*  
 [Ausgabe] Die Verwendungsanzahl des Treibers, nachdem diese Funktion aufgerufen wurde.  
  
 Anwendungen sollten die Verwendungsanzahl nicht festlegen. ODBC wird dieser Zähler zu verwalten.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLInstallDriverEx** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *LpszPathOut* Argument war nicht groß genug für den Ausgabepfad enthalten. Der Puffer enthält den abgeschnittenen Pfad.<br /><br /> Die *CbPathOutMax* -Argument lautete 0 (null) und *häufigsten* ODBC_INSTALL_COMPLETE wurde.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Ungültiger Typ der Anforderung|Die *häufigsten* Argument war nicht eines der folgenden:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Ungültige Schlüsselwort-Wert-Paaren|Die *LpszDriver* Argument enthalten einen Syntaxfehler.|  
|ODBC_ERROR_INVALID_PATH|Ungültiger Installationspfad|Die *LpszPathIn* Argument enthalten einen ungültigen Pfad.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Die Treiber oder das Konvertierungsprogramm Setup-Bibliothek konnte nicht geladen werden.|Die Setup-Treiberbibliothek konnte nicht geladen werden.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Ungültiger Parameter-Sequenz|Die *LpszDriver* Argument keine Liste der Schlüsselwort-Wert-Paare enthalten.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Nicht inkrementiert oder dekrementiert die Verwendungsanzahl der Komponente|Installerfehler beim Verwendungsanzahl der Treiber zu erhöhen.|  
  
## <a name="comments"></a>Kommentare  
 Die *LpszDriver* Argument ist eine Liste der Attribute in Form von Schlüsselwort-Wert-Paaren. Jedes Paar wird durch ein Nullbyte beendet, und die gesamte Liste wird mit null Byte beendet. (D. h. kennzeichnen zwei null-Bytes am Ende der Liste.) Das Format dieser Liste wird wie folgt aus:  
  
 *Treiber-"DESC"*  **\\** 0Driver**=***-Treiber-DLL-Dateiname*  **\\** 0 [Setup**=***Setup-DLL-Dateiname***\\**0]  
  
 [*-Treiber-Attr-Schlüsselwort1***=***value1***\\**0] [*-Treiber-Attr-Schlüsselwort2*   **=**  *value2***\\**0]...  **\\** 0  
  
 \0 ist, in dem ein Nullbyte und *-Treiber-Attr-Keywordn* alle Treiber-Attribut-Schlüsselwort ist. Die Schlüsselwörter müssen in der angegebenen Reihenfolge angezeigt werden. Beispielsweise nehmen wir an, dass ein Treiber für Textdateien formatierte separate Treiber und -Setup-DLLs verwendet, und mit den Erweiterungen ".txt" und CSV verwenden Sie-Dateien. Die *LpszDriver* Argument für diesen Treiber möglicherweise wie folgt:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Nehmen Sie an, dass ein Treiber für SQL Server eine separate DLL-Setup verfügt nicht über und verfügt nicht über alle Schlüsselwörter der Treiber-Attribut. Die *LpszDriver* Argument für diesen Treiber möglicherweise wie folgt:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Nach dem **SQLInstallDriverEx** Ruft Informationen über den Treiber von der *LpszDriver* Argument, um die treiberbeschreibung Abschnitt [ODBC Drivers] des Eintrags "Odbcinst.ini" im System hinzugefügt Informationen. Klicken Sie dann einen Abschnitt mit der Beschreibung der Treiber erstellt, und fügt die vollständigen Pfade der Treiber-DLL und der Setup-DLL. Schließlich werden gibt den Pfad des Zielverzeichnisses der Installation jedoch nicht kopieren die Treiberdateien darauf. Das aufrufende Programm muss die Treiberdateien tatsächlich in das Zielverzeichnis kopieren.  
  
 **SQLInstallDriverEx** die Verwendungsanzahl der Komponente für die installierte Treiber um 1 erhöht. Wenn eine Version des Treibers ist bereits vorhanden, aber die Verwendungsanzahl der Komponente für den Treiber ist nicht vorhanden, wird die neue Komponente Nutzung Count-Wert auf 2 festgelegt.  
  
 Installationsprogramm der Anwendung ist verantwortlich für physisch Kopieren der Datei des Treibers und verwalten die Verwendungsanzahl der Datei. Die Treiberdatei noch nicht installiert wurde, muss die Installationsprogramm der Anwendung kopieren der Datei in die *LpszPathIn* Pfad und die Verwendungsanzahl der Datei zu erstellen. Wenn die Datei zuvor installiert wurde, das Setup-Programm lediglich erhöht die Verwendungsanzahl der Datei und gibt den Pfad der vorherigen Installation in der *LpszPathOut* Argument.  
  
> [!NOTE]  
>  Weitere Informationen zu Verwendungszähler für die Komponente und Verwendungszähler für die Datei, finden Sie unter [zählen Verbrauch](../../../odbc/reference/install/usage-counting.md).  
  
 Wenn eine ältere Version der Treiberdatei zuvor von der Anwendung installiert wurde, sollte der Treiber deinstalliert und anschließend erneut installieren, damit, dass der Verwendungszähler für Treiber Komponente gültig ist. **SQLConfigDriver** (mit einer *häufigsten* von ODBC_REMOVE_DRIVER) zuerst aufgerufen werden soll, und klicken Sie dann **SQLRemoveDriver** sollte aufgerufen werden, um die Verwendungsanzahl der Komponente zu verringern. **SQLInstallDriverEx** sollte dann aufgerufen werden, um den Treiber, erhöht die Verwendungsanzahl der Komponente installieren. Das Setupprogramm der Anwendung muss die alte Datei mit der neuen Datei ersetzen. Die Verwendungsanzahl der Datei bleibt gleich, und eine andere Anwendung, die die ältere Versionsdatei verwendet, wird jetzt die neuere Version verwenden.  
  
> [!NOTE]  
>  Wenn der Treiber zuvor installiert war und **SQLInstallDriverEx** wird aufgerufen, um den Treiber in einem anderen Verzeichnis zu installieren, die Funktion gibt "true", zurück, aber *LpszPathOut* umfasst das Verzeichnis auf dem der Treiber bereits installiert wurde. Es umfasst nicht das eingegebene im Verzeichnis der *LpszDriver* Argument.  
  
 Die Länge des Pfads in *LpszPathOut* in **SQLInstallDriverEx** können Sie für einen Prozess zweiphasigen installieren, sodass eine Anwendung, welche bestimmen kann *CbPathOutMax* sollte sein. Aufrufen von **SQLInstallDriverEx** mit einem *häufigsten* ODBC_INSTALL_INQUIRY-Modus. Dadurch wird zurückgegeben, die Gesamtanzahl der Byte in den *PcbPathOut* Puffer. **SQLInstallDriverEx** kann dann aufgerufen werden, mit einer *häufigsten* von ODBC_INSTALL_COMPLETE und *CbPathOutMax* Argument festgelegt wird, auf den Wert in der *PcbPathOut*Puffer plus Null-Abschlusszeichen.  
  
 Wenn Sie nicht verwenden, das zwei-Phasen-Modell für **SQLInstallDriverEx**, müssen Sie festlegen *CbPathOutMax*, der die Größe des Arbeitsspeichers für den Pfad des Zielverzeichnisses an die _MAX_PATH Wert als definiert definiert die in Stdlib.h, um das Abschneiden zu verhindern.  
  
 Wenn *häufigsten* ist ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** lässt keine *LpszPathOut* gleich NULL sein (oder *CbPathOutMax* sein (0). Wenn *häufigsten* ODBC_INSTALL_COMPLETE ist, "false" wird zurückgegeben, wenn die Anzahl der Bytes, die für die Rückgabe verfügbar ist, größer als oder gleich *CbPathOutMax*, mit dem Ergebnis tritt auf, dass Daten abgeschnitten.  
  
 Nach dem **SQLInstallDriverEx** aufgerufen wurde und das Setupprogramm der Anwendung kopiert hat die Treiberdatei (falls erforderlich), der Setup-Treiber, die DLL aufrufen muss **SQLConfigDriver** beim Festlegen der Konfiguration für die Treiber.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Installieren des Treiber-Managers|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
