---
title: "Festlegen von Optionen für den Treiber Paradox programmgesteuert | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c4b822a41f18250e92ed9fe4475507fef01127b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Festlegen von Optionen für den Treiber Paradox programmgesteuert
|Option|Description|Methode|  
|------------|-----------------|------------|  
|Verzeichnis|Legt das gezielte Verzeichnis an.|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Sortierreihenfolge|Die Reihenfolge, in der die Felder sortiert werden.<br /><br /> Die Sequenz kann ASCII (Standard), internationale, Schwedisch Finnisch oder Norwegisch Dänisch.|Um diese Option dynamisch festzulegen, verwenden die **COLLATINGSEQUENCE** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Description|Eine optionale Beschreibung der Daten in der Datenquelle; z. B. "Hire Date, Gehaltsverlauf und aktuelle Überprüfung aller Mitarbeiter."|Um diese Option dynamisch festzulegen, verwenden die **Beschreibung** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusive|Wenn die **exklusive** aktiviert ist, wird die Datenbank im exklusiven Modus geöffnet wird, und kann jeweils nur ein einziger Benutzer zugegriffen werden. Leistung wird verbessert, wenn im exklusiven Modus ausgeführt wird.|Um diese Option dynamisch festzulegen, verwenden die **exklusive** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|NET-Stil|Das Format des Netzwerk-Zugriff zu verwendende Paradox-Daten: entweder "3.*x*" für Paradox 3. *X* oder "4. *X*"für Paradox 4. *X* oder 5. *X*. Kann auf "3. festgelegt werden *x*"oder" 4. *X*"ist die Version Paradox 4. *X* oder 5. *X*; Wenn die Version 3 Paradox. *X*, muss das Format "3. *X*".|Um diese Option dynamisch festzulegen, verwenden die **PARADOXNETSTYLE** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Timeout der Seite "|Gibt die Zeitspanne in Zehntelsekunden, die eine Seite (sofern nicht verwendet) im Puffer bleibt, bevor Sie entfernt werden. Die Standardeinstellung ist 600 Zehntelsekunden (60 Sekunden). Diese Option gilt für alle Datenquellen, die den ODBC-Treiber verwenden.<br /><br /> Das Timeout der Seite darf nicht aufgrund einer inhärenten Verzögerung 0 sein. Das Timeout der Seite darf nicht kleiner als die inhärenten Verzögerung sein, auch wenn die Seite "Timeout (Option) unter diesen Wert festgelegt ist.|Um diese Option dynamisch festzulegen, verwenden die **' pagetimeout '** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Schreibgeschützt|Legt die Datenbank als schreibgeschützt fest.|Um diese Option dynamisch festzulegen, verwenden die **READONLY** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Wählen Sie Verzeichnis|Zeigt ein Dialogfeld, in dem Sie ein Verzeichnis mit den Dateien, die Sie zugreifen möchten auswählen können.<br /><br /> Beim Definieren eines Quellverzeichnisses Daten geben Sie das Verzeichnis, in dem die am häufigsten Dateien verwendeten, befinden. Der ODBC-Treiber verwendet dieses Verzeichnis als Standardverzeichnis. Kopieren Sie andere Dateien in dieses Verzeichnis, wenn sie häufig verwendet werden. Alternativ können Sie den Dateinamen in einer SELECT-Anweisung mit dem Verzeichnisnamen qualifizieren:<br /><br /> WÄHLEN SIE \* AUS C:\MYDIR\EMP<br /><br /> Sie können ein neues Standardverzeichnis angeben, mit der **SQLSetConnectOption** Funktion mit der Option SQL_CURRENT_QUALIFIER.|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Wählen Sie Netzwerkverzeichnis|Der vollständige Pfad des Verzeichnisses, eine Datenbank Paradox Sperren enthält, da sie entweder die Datei Pdoxusrs.net enthält (in 4 Paradox. *X*) oder die Datei Paradox.net (5 Paradox. *X*). Wenn das Verzeichnis nicht eine dieser Dateien enthält, erstellt der Paradox-Treiber eine. Informationen zu diesen Dateien finden Sie unter der Paradox-Dokumentation.<br /><br /> Bevor Sie einem Netzwerkverzeichnis auswählen können, geben Sie Ihren Benutzernamen Paradox in der **Benutzername** Textfeld. Klicken Sie auf **Netzwerkverzeichnis wählen** einem Netzwerkverzeichnis auswählen.|Um diese Option dynamisch festzulegen, verwenden die **x** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Benutzername|Der Benutzername des Paradox. Dies ist der Name, die an andere Benutzer von Paradox Dateien angezeigt werden, wenn eine Sperre auftritt.|Um diese Option dynamisch festzulegen, verwenden die **PARADOXUSERNAME** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
