---
title: Zusammenfassung der Installer DLL-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 42b2338cafa53a2813929c3d674d9ed0a9789bdb
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="installer-dll-function-summary"></a>Zusammenfassung der Installer DLL-Funktion
Die folgende Tabelle beschreibt die Funktionen der DLL-Installer. Weitere Informationen zur Syntax und Semantik für die einzelnen Funktionen finden Sie unter [Installer DLL-API-Referenz](../../../odbc/reference/syntax/installer-dll-api-reference-function.md).  
  
|Task|Funktionsname|Zweck|  
|----------|-------------------|-------------|  
|Installieren von ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Lädt die treiberspezifischen-Setup-DLL.|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Gibt eine Liste der installierten Treiber zurück.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Die Systeminformationen hinzugefügt einen Treiber.|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Gibt das Zielverzeichnis für den Treiber-Manager zurück.|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Gibt Fehler oder Status für das Installer-Funktionen zurück.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Die Systeminformationen hinzugefügt ein Konvertierungsprogramm.|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Ermöglicht eine Treiber oder Konvertierer Setup-Bibliothek, um Fehler zu melden.|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Entfernt einen Treiber aus den Systeminformationen.|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Die Systeminformationen entzieht ODBC-Kernkomponenten.|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Entfernt das Konvertierungsprogramm aus der Systeminformationen.|  
|Konfigurieren von Datenquellen|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Ruft die treiberspezifischen-Setup-DLL.|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Zeigt ein Dialogfeld zum Hinzufügen einer Datenquelle an.|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Ruft den Konfigurationsmodus, der angibt, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen ab.|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Schreibt einen Wert in die Systeminformationen.|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Zeigt ein Dialogfeld, um ein Konvertierungsprogramm auszuwählen.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Zeigt ein Dialogfeld zum Konfigurieren von Datenquellen und Treiber an.|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Liest Informationen aus der Datei-DSNs.|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Entfernt die Standarddatenquelle an.|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Entfernt eine Datenquelle an.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Legt fest, der Konfigurationsmodus, der angibt, in dem der Odbc.ini Eintrag auflisten DSN-Werte in die Systeminformationen.|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Überprüft die Länge und die Gültigkeit der Namen der Datenquelle.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Fügt eine Datenquelle hinzu.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Schreibt Informationen in der Datei-DSNs.|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Ruft einen Wert aus der Systeminformationen ab.|
