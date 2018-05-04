---
title: SQLRemoveTranslator Funktion | Microsoft Docs
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
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 594769c8cfb8bc1a30568a11cdd50505892eee24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLRemoveTranslator** entfernt Informationen zu einem Konvertierer im Abschnitt "Odbcinst.ini" der Systeminformationen und verringert das Konvertierungsprogramm Komponente Verwendungsanzahl um 1.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszTranslator*  
 [Eingabe] Der Name des konvertierers, wie im Schlüssel "Odbcinst.ini" die Systeminformationen registriert.  
  
 *lpdwUsageCount*  
 [Ausgabe] Die Verwendungsanzahl des konvertierers, nachdem diese Funktion aufgerufen wurde.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten. Wenn kein Eintrag in der Systeminformationen ist vorhanden, wenn diese Funktion aufgerufen wird, gibt die Funktion "false" zurück.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLRemoveTranslator** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Komponente wurde nicht in der Registrierung gefunden.|Der Installer konnte nicht Konvertierer Informationen entfernt, weil sie in der Registrierung nicht vorhanden noch oder nicht in der Registrierung gefunden werden konnte.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszTranslator* Argument war ungültig.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Nicht inkrementiert oder dekrementiert die Verwendungsanzahl der Komponente|Installerfehler beim die Verwendungsanzahl des Treibers zu verringern.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLRemoveTranslator** ergänzt die [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) -Funktion und Updates zählen die Verwendung von Komponenten in die Systeminformationen. Diese Funktion sollte nur von einer setupanwendung aufgerufen werden.  
  
 **SQLRemoveTranslator** die Verwendungsanzahl der Komponente um 1 verringert wird. Fällt die Verwendungsanzahl der Komponente auf 0, wird der Konvertierer-Eintrag in die Systeminformationen entfernt werden. Der Konvertierer-Eintrag ist an folgendem Speicherort in der Systeminformationen, unter dem Namen des Konvertierungsprogramms:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** Dateien wird nicht tatsächlich entfernt. Das aufrufende Programm ist dafür verantwortlich, Löschen von Dateien und die Verwendungsanzahl der Datei beibehalten. Nur, nachdem die Verwendungsanzahl der Komponente und die Verwendungsanzahl der Datei erreicht ist 0 (null) eine Datei, die physisch gelöscht. Einige Dateien in einer Komponente können gelöscht werden, und andere nicht gelöscht, je nachdem, ob die Dateien von einer anderen Anwendung verwendet werden, die die Verwendungsanzahl der Datei erhöht haben.  
  
 **SQLRemoveTranslator** wird auch als Teil eines Updatevorgangs bezeichnet. Wenn eine Anwendung erkennt, dass sie ein Upgrade durchführen und den Treiber wurde bereits installierte, sollte der Treiber entfernt und anschließend neu installiert. **SQLRemoveTranslator** muss zuerst aufgerufen werden, um die Verwendungsanzahl der Komponente zu verringern und dann **SQLInstallTranslatorEx** aufgerufen werden, um die Verwendungsanzahl der Komponente zu erhöhen. Das Setupprogramm der Anwendung muss die alten Dateien physisch durch die neuen Dateien ersetzen. Die Verwendungsanzahl der Datei bleibt gleich, und andere Anwendungen, die Dateien für die älteren Version verwenden jetzt die neuere Version verwenden.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Installieren ein Konvertierungsprogramm|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
