---
title: SQLRemoveDriver Funktion | Microsoft Docs
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
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d191f3ce9d30d241c4d4d37d9961a590ae33817b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0  
  
 **Zusammenfassung**  
 **SQLRemoveDriver** ändert oder Informationen über den Treiber aus den Eintrag "Odbcinst.ini" in die Systeminformationen entfernt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumente  
 *lpszDriver*  
 [Eingabe] Der Name des Treibers im Schlüssel "Odbcinst.ini" die Systeminformationen registriert.  
  
 *fRemoveDSN*  
 [Eingabe] Gültige Werte sind:  
  
 "True": Entfernen DSNs im Zusammenhang mit dem Treiber, die im angegebenen *LpszDriver*. "False": Entfernen Sie nicht DSNs im Zusammenhang mit dem Treiber, die im angegebenen *LpszDriver*.  
  
 *lpdwUsageCount*  
 [Ausgabe] Die Verwendungsanzahl des Treibers, nachdem diese Funktion aufgerufen wurde.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten. Wenn kein Eintrag in der Systeminformationen ist vorhanden, wenn diese Funktion aufgerufen wird, gibt die Funktion "false" zurück.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLRemoveDriver** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Komponente wurde nicht in der Registrierung gefunden.|Der Installer konnte nicht die Treiberinformationen entfernt, da sie in der Registrierung nicht vorhanden noch oder nicht in der Registrierung gefunden werden konnte.|  
|ODBC_ERROR_INVALID_NAME|Ungültiger Name für Treiber oder das Konvertierungsprogramm|Die *LpszDriver* Argument war ungültig.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Nicht inkrementiert oder dekrementiert die Verwendungsanzahl der Komponente|Installerfehler beim die Verwendungsanzahl des Treibers zu verringern.|  
|ODBC_ERROR_REQUEST_FAILED|Fehler bei der Anforderung|Die *fRemoveDSN* Argument war "true", jedoch eine oder mehrere DSNs konnte nicht entfernt werden. Der Aufruf von **SQLConfigDriver** mit der ODBC_REMOVE_DRIVER Anforderung fehlgeschlagen ist.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLRemoveDriver** ergänzt die [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) -Funktion und Updates zählen die Verwendung von Komponenten in die Systeminformationen. Diese Funktion sollte nur von einer setupanwendung aufgerufen werden.  
  
 **SQLRemoveDriver** wird der Wert für die Komponente Verwendung um 1 verringert. Wenn die Verwendungsanzahl der Komponente auf 0 geht, geschieht Folgendes:  
  
1.  Die **SQLConfigDriver** Funktion mit der Option ODBC_REMOVE_DRIVER wird aufgerufen. Wenn die *fRemoveDSN* Option wird festgelegt, auf "true", die **ConfigDSN** Funktionsaufrufe **SQLRemoveDSNFromIni** So entfernen Sie alle Datenquellen, die im angegebenen Treibers zugeordnet *LpszDriver.* Wenn die *fRemoveDSN* Option auf "false" festgelegt ist, die Datenquellen nicht gelöscht werden.  
  
2.  Der Eintrag Driver in die Systeminformationen werden entfernt. Der Eintrag Driver ist im folgenden System Informationen Pfad, unter dem Treibernamen:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** Dateien wird nicht tatsächlich entfernt. Das aufrufende Programm ist verantwortlich für das Löschen von Dateien und die Verwendungsanzahl der Datei beibehalten. Nur, nachdem die Verwendungsanzahl der Komponente und die Verwendungsanzahl der Datei erreicht ist 0 (null) eine Datei, die physisch gelöscht. Einige Dateien in einer Komponente können gelöscht werden, und andere nicht gelöscht, je nachdem, ob die Dateien von einer anderen Anwendung verwendet werden, die die Verwendungsanzahl der Datei erhöht haben.  
  
 **SQLRemoveDriver** wird auch als Teil eines Updatevorgangs bezeichnet. Wenn eine Anwendung erkennt, dass sie ein Upgrade durchführen und den Treiber wurde bereits installierte, sollte der Treiber entfernt und anschließend neu installiert. **SQLRemoveDriver** muss zuerst aufgerufen werden, um die Verwendungsanzahl der Komponente zu verringern und dann **SQLInstallDriverEx** aufgerufen werden, um die Verwendungsanzahl der Komponente zu erhöhen. Das Setupprogramm der Anwendung muss die alten Dateien durch die neuen Dateien ersetzen. Die Verwendungsanzahl der Datei bleibt gleich, und andere Anwendungen, die Dateien für die älteren Version verwenden jetzt die neuere Version verwenden.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Hinzufügen, ändern oder Entfernen eines Treibers|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (in der Setup-DLL)|  
|Hinzufügen, ändern oder Entfernen eines Treibers|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Installation des Treibers|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|

