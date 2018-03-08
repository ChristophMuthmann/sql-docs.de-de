---
title: SQLRemoveDriverManager Funktion | Microsoft Docs
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
apiname: SQLRemoveDriverManager
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveDriverManager
helpviewer_keywords: SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d74b3b3eda914210f8d69d6089eb9a474416318
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager-Funktion
**Konformität**  
 Version wurde erstmals: ODBC 3.0: in Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 und höher veraltet.  
  
 **Zusammenfassung**  
 **SQLRemoveDriverManager** ändert oder Informationen zu den ODBC-Komponenten den Eintrag "Odbcinst.ini" in die Systeminformationen entfernt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumente  
 *pdwUsageCount*  
 [Ausgabe] Die Verwendungsanzahl der Treiber-Manager, nachdem diese Funktion aufgerufen wurde.  
  
## <a name="returns"></a>Rückgabewert  
 Die Funktion gibt "true" zurück, wenn erfolgreich, "false" ist dabei ein Fehler aufgetreten. Wenn kein Eintrag in der Systeminformationen ist vorhanden, wenn diese Funktion aufgerufen wird, gibt die Funktion "false" zurück.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLRemoveDriverManager** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Komponente wurde nicht in der Registrierung gefunden.|Der Installer konnte nicht der Treiber-Manager-Informationen entfernt, da sie in der Registrierung nicht vorhanden noch oder nicht in der Registrierung gefunden werden konnte.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Nicht inkrementiert oder dekrementiert die Verwendungsanzahl der Komponente|Installerfehler beim die Verwendungsanzahl der Treiber-Manager zu verringern.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="comments"></a>Kommentare  
 **SQLRemoveDriverManager** ergänzt die **SQLInstallDriverManager** -Funktion und Updates, die die Verwendung von Komponenten in die Systeminformationen zu zählen. Diese Funktion sollte nur von einer setupanwendung aufgerufen werden.  
  
 **SQLRemoveDriverManager** wird die Anzahl von Kernen Komponente Verwendung um 1 verringert. Fällt die Verwendungsanzahl der Komponente auf 0, wird die Systeminformationen Eintrag entfernt werden. Die zentrale Komponente Eintrag wird am folgenden Speicherort in der Systeminformationen, unter dem Titel "ODBC Core":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Eine Anwendung sollte nicht physisch Treibermanager-Dateien entfernen, wenn die Verwendungsanzahl der Komponente und die Verwendungsanzahl der Datei 0 (null) erreichen.  
  
 **SQLRemoveDriverManager** Dateien wird nicht tatsächlich entfernt. Das aufrufende Programm ist verantwortlich für das Löschen von Dateien und zählt die Verwendung der Datei beibehalten. Treiber-Manager-Dateien sollten jedoch nicht, werden entfernt, wenn die Verwendungsanzahl der Komponente und die Datei Verwendungsanzahl NULL ist, erreicht haben, da diese Dateien von einer anderen Anwendung verwendet werden können, die nicht die Verwendungsanzahl der Datei erhöht haben.  
  
 **SQLRemoveDriverManager** im Rahmen des Deinstallationsvorgangs aufgerufen wird. ODBC-Komponenten (darunter Treiber-Manager, Cursorbibliothek, Installer, Language-Bibliothek, Administrator, thunking Dateien und usw.) werden als Ganzes deinstalliert. Die folgenden Dateien werden nicht entfernt wird, wenn **SQLRemoveDriverManager** im Rahmen des Deinstallationsvorgangs aufgerufen wird:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. DLL|  
|DATEI ODBCCR32. DLL|ODBC16GT. DLL|  
|ODBCCU32. DLL|ODBC32GT. DLL|  
|ODBCINT. DLL|DS16GT. DLL|  
|ODBCTRAC. DLL|DS32GT. DLL|  
|MSVCRT40. DLL|ODBCAD32. EXE-DATEI|  
|ODBCCP32. SYSTEMSTEUERUNGSOPTION||  
  
 **SQLRemoveDriverManager** wird auch als Teil eines Updatevorgangs bezeichnet. Wenn eine Anwendung erkennt, dass sie ein Upgrade durchführen und den Treiber wurde bereits installierte, sollte der Treiber entfernt und anschließend neu installiert.  
  
 **SQLRemoveDriverManager** sollte zuerst aufgerufen werden, um die Verwendungsanzahl der Komponente zu verringern. **SQLInstallDriverEx** sollte dann aufgerufen werden, um die Verwendungsanzahl der Komponente zu erhöhen. Das Setupprogramm der Anwendung muss die alten Kerndateien Komponente durch die neuen Dateien ersetzen. Die Datei Verwendungszähler bleibt gleich, und Verwenden anderer Anwendungen, die die älteren Version Komponente Kerndateien verwenden nun die Dateien der neueren Version.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Installieren einen Treiber-Manager|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
