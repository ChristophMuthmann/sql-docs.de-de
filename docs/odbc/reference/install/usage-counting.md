---
title: Zählen Verbrauch | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 066c96d8b4ab6617216f5e4b3f924386b42d7f60
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="usage-counting"></a>Zählen Verbrauch
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Zwei Typen von Verwendungszähler bleiben in der Registrierung für die einzelnen Komponenten: einen Verwendungszähler für die Komponente und eine oder mehrere optionale Datei Verwendungszähler. Die Verwendungsanzahl der Komponente unterstützt das Installationsprogramm DLL Registrierungseinträge beizubehalten. Er wird im UsageCount Wert unter der ODBC Core, Treiber und Konvertierer Unterschlüsseln gespeichert. Das Format des Werts UsageCount und Weitere Informationen zu dieser Unterschlüssel, finden Sie unter [Registrierungseinträge für ODBC-Komponenten](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Wenn eine Komponente erstmals installiert wird, erstellt das Installationsprogramm DLL einen Unterschlüssel für sie und legt die Daten für den UsageCount-Wert in dieser Unterschlüssel auf 1 fest. Wenn die Komponente erneut installiert wird, erhöht das Installationsprogramm DLL die Verwendungsanzahl der. Wenn die Komponente entfernt wird, der Installer DLL verringert die Auslastung gezählt. Fällt die Verwendungsanzahl auf 0, entfernt das Installationsprogramm DLL den Unterschlüssel für die Komponente an.  
  
> [!CAUTION]  
>  Eine Anwendung sollte nicht physisch Treibermanager-Dateien entfernen, wenn die Verwendungsanzahl der Komponente und die Verwendungsanzahl der Datei 0 (null) erreichen.  
  
 Dateinutzung Anzahlen feststellen, wenn eine Datei muss tatsächlich kopiert oder gelöscht werden, als dagegen spricht, erhöhen oder Verringern der Verwendungszähler. Dies ist wichtig, da der ODBC-Komponenten und daher die Dateien in ODBC-Komponenten werden freigegeben und können installiert oder entfernt werden durch eine Vielzahl von Anwendungen. Die Anwendung kann Treiber und Konvertierer Dateien löschen, ist die Verwendungsanzahl der Komponente und die Verwendungsanzahl der Datei 0 (null) erreicht. Treiber-Manager-Dateien sollten jedoch nicht, werden gelöscht, sobald die Verwendungsanzahl der Komponente und die Verwendungsanzahl der Datei NULL ist, erreicht haben, da diese Dateien von einer anderen Anwendung verwendet werden können, die nicht die Verwendungsanzahl der Datei erhöht haben.  
  
> [!NOTE]  
>  Verwendungszähler für die Datei sind in Microsoft® WindowsNT®/Windows2000 optional.  
  
 Verwendungszähler für die Datei vom Setupprogramm verwaltet werden, nach dem Aufruf **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**, oder **SQLRemoveTranslator**.  
  
 Als eine Komponente zum ersten Mal installiert ist, erstellt das Setup-Programm oder Installer DLL einen Wert unter dem folgenden Schlüssel für jede Datei in dieser Komponente, die nicht bereits auf dem System befindet:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  SOFTWARE  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 Legt die Daten für diese Werte auf 1 fest, und kopiert die Datei in das System. Wenn die Komponente erneut installiert wird, erhöht die Setup-Programm oder DLL-Installer die Verwendungszähler. Wenn die Komponente entfernt wird, zählt der Setup-Programm oder Installer DLL verringert die Auslastung. Fällt Verwendungsanzahl auf 0, der Setup-Programm oder DLL-Installer entfernt den Wert für die Datei und die Komponente ist ein Treiber oder ein Konvertierungsprogramm löscht die Datei. Treiber-Manager-Dateien sollten nicht gelöscht werden.  
  
 Das Format der Datei-Wert für die Anzahl der Auslastung wird in der folgenden Tabelle gezeigt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|*Full-path*|REG_DWORD-WERT|*count*|  
  
 Beispielsweise nehmen an, dass ein Treiber für Informix Infrmx32.dll und Infrmx32.hlp-Dateien verwendet, und nehmen Sie an, dass dieser Treiber zweimal installiert wurde. Die Werte unter dem Unterschlüssel SharedDlls für den Treiber Informix würde wie folgt lauten:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
