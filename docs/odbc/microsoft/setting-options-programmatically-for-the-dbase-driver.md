---
title: Festlegen von Optionen programmgesteuert dBASE-Treiber | Microsoft Docs
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
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc037c3db2eddaf91338d1ce74aa4894f2a3b7b0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Festlegen von Optionen programmgesteuert dBASE-Treiber
|Option|Description|Methode|  
|------------|-----------------|------------|  
|Ungefähre Zeilenanzahl|Bestimmt, ob Statistiken für Tabellen Größe angeglichen werden. Diese Option gilt für alle Datenquellen, die den ODBC-Treiber verwenden.|Um diese Option dynamisch festzulegen, verwenden die **Statistiken** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Sortierreihenfolge|Die Reihenfolge, in der die Felder sortiert werden.<br /><br /> Die Sequenz sein kann: ASCII (Standard) oder International.|Um diese Option dynamisch festzulegen, verwenden die **COLLATINGSEQUENCE** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Datenquellenname|Ein Name, der die Datenquelle, z. B. Gehaltsabrechnungen oder Mitarbeiter identifiziert.|Um diese Option dynamisch festzulegen, verwenden die **DSN** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Datenbank|Eine Microsoft Access-Datenquelle kann ohne auswählen oder erstellen eine Datenbank eingerichtet werden. Wenn beim Setup keine Datenbank angegeben ist, werden Benutzer aufgefordert werden, um eine Datei auszuwählen, beim Herstellen Verbindung mit der Datenquelle einer.|Um diese Option dynamisch festzulegen, verwenden die **DBQ** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Description|Eine optionale Beschreibung der Daten in der Datenquelle; z. B. "Hire Date, Gehaltsverlauf und aktuelle Überprüfung aller Mitarbeiter."|Um diese Option dynamisch festzulegen, verwenden die **Beschreibung** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusive|Wenn die **exklusive** aktiviert ist, wird die Datenbank im exklusiven Modus geöffnet wird, und kann jeweils nur ein einziger Benutzer zugegriffen werden. Leistung wird verbessert, wenn er im exklusiven Modus ausgeführt wird.|Um diese Option dynamisch festzulegen, verwenden die **exklusive** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Timeout der Seite "|Gibt die Zeitspanne in Zehntelsekunden, die eine Seite (sofern nicht verwendet) in den Puffer bleibt, bis er entfernt wird. Die Standardeinstellung ist 600 Zehntelsekunden (60 Sekunden). Diese Option gilt für alle Datenquellen, die den ODBC-Treiber verwenden.<br /><br /> Das Timeout der Seite darf nicht aufgrund einer inhärenten Verzögerung 0 sein. Das Timeout der Seite darf nicht kleiner als die inhärenten Verzögerung sein, auch wenn die Seite "Timeout (Option) unter diesen Wert festgelegt ist.|Um diese Option dynamisch festzulegen, verwenden die **' pagetimeout '** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Schreibgeschützt|Legt die Datenbank als schreibgeschützt fest.|Um diese Option dynamisch festzulegen, verwenden die **READONLY** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Wählen Sie Verzeichnis|Zeigt ein Dialogfeld, in dem Sie ein Verzeichnis auswählen können, die die Dateien enthält, die Sie zugreifen möchten.<br /><br /> Wenn Sie ein Quellverzeichnis Daten definieren, geben Sie das Verzeichnis, in dem am häufigsten verwendeten Dateien gespeichert sind. Der ODBC-Treiber verwendet dieses Verzeichnis als Standardverzeichnis. Kopieren Sie andere Dateien in dieses Verzeichnis, wenn sie häufig verwendet werden. Alternativ können Sie den Dateinamen in einer SELECT-Anweisung mit dem Verzeichnisnamen qualifizieren:<br /><br /> WÄHLEN SIE \* AUS C:\MYDIR\EMP<br /><br /> Sie können ein neues Standardverzeichnis angeben, mit der **SQLSetConnectOption** Funktion mit der Option SQL_CURRENT_QUALIFIER.|Um diese Option dynamisch festzulegen, verwenden die **Wert** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Gelöschte Zeilen anzeigen|Gibt an, ob Zeilen, die als gelöscht markiert wurden abgerufen oder auf positioniert werden können. Wenn deaktiviert, werden gelöschte Zeilen nicht angezeigt. Gelöschte Zeilen werden behandelt, wenn ausgewählt, die nicht vorläufig gelöschte Zeilen identisch. Standardmäßig ist das Kontrollkästchen deaktiviert.|Um diese Option dynamisch festzulegen, verwenden die **gelöschte** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
