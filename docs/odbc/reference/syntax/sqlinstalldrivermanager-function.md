---
title: SQLInstallDriverManager Funktion | Microsoft Docs
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
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6bc56b9045ae3f9a53b410ef0546d539e3c25ee8
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager-Funktion
**Konformität**  
 Version wurde erstmals: ODBC 1.0: veraltetes Feature in Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 und höher  
  
 **Zusammenfassung**  
 **SQLInstallDriverManager** gibt den Pfad des Verzeichnisses für die Installation des ODBC-Kernkomponenten Ziel zurück. Das aufrufende Programm muss der Treiber-Manager-Dateien tatsächlich in das Zielverzeichnis kopieren.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszPath*  
 [Ausgabe] Der Pfad des Zielverzeichnisses der Installation.  
  
 *cbPathMax*  
 [Eingabe] Länge des *LpszPath*. Diese Angabe muss mindestens _MAX_PATH Bytes.  
  
 *pcbPathOut*  
 [Ausgabe] Gesamte Anzahl der Bytes, die (mit Ausnahme der Null-Terminierung Byte) im zurückgegebenen *LpszPath*. Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *CbPathMax*, den Pfad im *LpszPath* auf abgeschnitten *CbPathMax* minus der Null-Terminierung Zeichen. Die *PcbPathOut* -Argument ein null-Zeiger sein.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLInstallDriverManager** gibt "false", ein zugehöriges * \*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die * \*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Ungültige Pufferlänge.|Die *LpszPath* Argument war nicht groß genug für den Ausgabepfad enthalten. Der Puffer enthält den abgeschnittenen Pfad.<br /><br /> Die *CbPathMax* Arguments ist kleiner als _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Nicht inkrementiert oder dekrementiert die Verwendungsanzahl der Komponente|Installerfehler beim Erhöhen der Verwendungszähler für ODBC Core Komponente.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLInstallDriverManager** wird aufgerufen, um den Pfad zurückgegeben, für die ODBC-Komponenten und Inkrementwerts der Verwendung von Komponenten in die Systeminformationen zählen. Wenn eine Version der Treiber-Manager ist bereits vorhanden, aber die Verwendungsanzahl der Komponente für den Treiber ist nicht vorhanden, wird die neue Komponente Nutzung Count-Wert auf 2 festgelegt.  
  
 Das Setupprogramm für die Anwendung ist verantwortlich für das Kopieren von der Komponente Kerndateien physisch und zählt die Verwendung der Datei beibehalten. Wenn eine zentrale Komponentendatei noch nicht installiert wurde, muss das Setupprogramm der Anwendung kopieren Sie die Datei und erstellen die Verwendungsanzahl der Datei. Wenn die Datei zuvor installiert hat, erhöht das Setupprogramm lediglich die Verwendungsanzahl der Datei.  
  
 Eine ältere Version des Treiber-Managers durch das Setupprogramm für die Anwendung zuvor installiert war, sollten die wichtigsten Komponenten deinstalliert und anschließend erneut installieren, damit, dass der Verwendungszähler für Core Komponente gültig ist. **SQLRemoveDriverManager** sollte zuerst aufgerufen werden, um die Verwendungsanzahl der Komponente zu verringern. **SQLInstallDriverManager** sollte dann aufgerufen werden, um die Verwendungsanzahl der Komponente zu erhöhen. Das Setupprogramm der Anwendung muss die alten Kerndateien Komponente durch die neuen Dateien ersetzen. Die Datei Verwendungszähler bleibt gleich, und verwenden andere Clientanwendungen, die die älteren Version Komponente Kerndateien verwendet nun die Dateien der neueren Version.  
  
 In einer Neuinstallation von der ODBC-Kernkomponenten, Treiber und Konvertierer, sollte das Setupprogramm für die Anwendung die folgenden Funktionen aufrufen, nacheinander: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (mit einer *häufigsten* von ODBC_INSTALL_DRIVER), und klicken Sie dann **SQLInstallTranslatorEx**. In die Core-Komponenten und Treibern sowie Übersetzer zu deinstallieren, sollte das Setupprogramm für die Anwendung die folgenden Funktionen aufrufen, nacheinander: **SQLRemoveTranslator**, **SQLRemoveDriver**, und klicken Sie dann **SQLRemoveDriverManager**. Diese Funktionen müssen in der folgenden Reihenfolge aufgerufen werden. Upgrade aller Komponenten nacheinander alle deinstallieren Funktionen aufgerufen werden, und klicken Sie dann nacheinander alle installieren-Funktionen aufgerufen werden sollte.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen eines Treibers|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Installation des Treibers|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Installieren ein Konvertierungsprogramm|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Entfernen eines Treibers|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Entfernen den Treiber-Manager|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Entfernen ein Konvertierungsprogramm|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|

