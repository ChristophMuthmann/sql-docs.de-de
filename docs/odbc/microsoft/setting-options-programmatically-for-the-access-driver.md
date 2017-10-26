---
title: "Festlegen von Optionen für die Access-Treiber programmgesteuert | Microsoft Docs"
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
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1bc2426cdceebcd3537815e9bb1238eba160729f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Festlegen von Optionen für die Access-Treiber programmgesteuert
|Option|Description|Methode|  
|------------|-----------------|------------|  
|Puffergröße|Die Größe des internen Puffers, in Kilobyte, die von Microsoft Access, zum Übertragen von Daten in und aus dem Datenträger verwendet wird. Die Standardpuffergröße beträgt 2048 KB, die (als 2048 angezeigt). Jeder ganzzahlige Wert teilbar von 256 kann eingegeben werden.|Um diese Option dynamisch festzulegen, verwenden Sie das MAXBUFFERSIZE-Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Datenquellenname|Ein Name, der die Datenquelle, z. B. Gehaltsabrechnungen oder Mitarbeiter identifiziert.|Um diese Option dynamisch festzulegen, verwenden die **DSN** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Datenbank|Eine Microsoft Access-Datenquelle kann ohne auswählen oder erstellen eine Datenbank eingerichtet werden. Wenn beim Setup keine Datenbank angegeben ist, wird der Benutzer aufgefordert werden, um eine Datei auszuwählen, beim Verbinden mit der Datenquelle.|Um diese Option dynamisch festzulegen, verwenden die **DBQ** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Description|Eine optionale Beschreibung der Daten in der Datenquelle; z. B. "Hire Date, Gehaltsverlauf und aktuelle Überprüfung aller Mitarbeiter."|Um diese Option dynamisch festzulegen, verwenden die **Beschreibung** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusive|Wenn die **exklusive** aktiviert ist, wird die Datenbank im exklusiven Modus geöffnet wird, und kann jeweils nur ein einziger Benutzer zugegriffen werden. Leistung wird verbessert, wenn im exklusiven Modus ausgeführt wird.|Um diese Option dynamisch festzulegen, verwenden die **exklusive** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Bestimmt, wie die Änderungen, die außerhalb einer Transaktion in die Datenbank geschrieben werden. Dieser Wert wird anfangs festgelegt, auf "Ja", was bedeutet, dass der Microsoft Access-Treiber Commits in eine interne/implizite Transaktion abgeschlossen werden gewartet wird.|Diese Option ist in enthalten die **erweiterte Optionen festlegen** im Dialogfeld für die Microsoft Access-Treiber.|  
|Timeout der Seite "|Gibt die Zeitspanne in Millisekunden, die eine Seite (sofern nicht verwendet) in den Puffer bleibt, bevor Sie entfernt werden. Microsoft Access-Treiber ist der Standardwert 500 Millisekunden (0,5 Sekunden). Diese Option gilt für alle Datenquellen, die den ODBC-Treiber verwenden.<br /><br /> Das Timeout der Seite darf nicht aufgrund einer inhärenten Verzögerung 0 sein. Das Timeout der Seite darf nicht kleiner als die inhärenten Verzögerung sein, auch wenn die Seite "Timeout (Option) unter diesen Wert festgelegt ist.|Um diese Option dynamisch festzulegen, verwenden die **' pagetimeout '** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Schreibgeschützt|Legt die Datenbank als schreibgeschützt fest.|Um diese Option dynamisch festzulegen, verwenden die **READONLY** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Systemdatenbank|Der vollständige Pfad der Microsoft Access-Systemdatenbank, die mit der Microsoft Access-Datenbank verwendet werden, die Sie zugreifen möchten.<br /><br /> Klicken Sie auf die **Systemdatenbank** klicken, um die Systemdatenbank zu verwendende auszuwählen. Der ODBC Microsoft Access-Treiber fordert den Benutzer für einen Namen und ein Kennwort. Der Standardname lautet Admin, und das Standardkennwort in Microsoft Access für den Admin-Benutzer ist eine leere Zeichenfolge.<br /><br /> Zur Erhöhung der Sicherheit Ihrer Microsoft Access-Datenbank erstellen Sie einen neuen Benutzer zum Ersetzen des Admin-Benutzers und zum Löschen des Admin-Benutzers oder ändern Sie die Objekte, die auf die Admin-Benutzer Zugriff hat.|Um diese Option dynamisch festzulegen, verwenden die **SYSTEMDB** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Threads|Die Anzahl der Hintergrundthreads für das Modul nutzen. Microsoft Access-Treiber wird dieser Wert wird standardmäßig auf 3 jedoch geändert werden kann. Der Benutzer möchte eventuell die Anzahl der Threads zu erhöhen, wenn eine große Menge an Aktivität in der Datenbank vorhanden ist.<br /><br /> Diese Option ist in enthalten die **erweiterte Optionen festlegen** im Dialogfeld für die Microsoft Access-Treiber.|Um diese Option dynamisch festzulegen, verwenden die **THREADS** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Bestimmt, ob die Microsoft Access-Treiber eine explizite Transaktionen für eine benutzerdefinierte asynchron durchführen. Dieser Wert wird anfangs festgelegt, auf "Ja", was bedeutet, dass der Microsoft Access-Treiber in einer benutzerdefinierten Transaktion ausgeführt werden Commits wartet.<br /><br /> Diese Einstellung auf "false" kann unvorhersehbare Folgen in einer mehrbenutzerumgebung haben.|Um diese Option dynamisch festzulegen, verwenden die **USERCOMMITSYNC** Schlüsselwort in einem Aufruf von [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|

