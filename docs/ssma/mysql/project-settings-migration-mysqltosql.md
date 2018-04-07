---
title: Projekteinstellungen (Migration) (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6616502c370733bf0efa19eed97e6e2f022c5a0
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="project-settings-migration-mysqltosql"></a>Projekteinstellungen (Migration) (MySQLToSQL)
Die Seite "Migration", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA Daten aus MySQL zu SQL Server migriert.  
  
Der Bereich für die Migration finden Sie in der **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Zum Angeben von Einstellungen für alle SSMA-Projekte, auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, wählen Sie den Projekttyp in **Migration Zielversion** Dropdown-Liste von dem Sie die Einstellungen zugreifen möchten, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Migration**.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Migration**.  
  
## <a name="options"></a>enthalten  
  
### <a name="bulk-copy"></a>Massenkopieren  
  
|Begriff|Definition|  
|--------|--------------|  
|**Batchgröße**|Gibt den Batch Größe, die während der Migration von Daten verwendet.<br /><br />**Standardmodus**: 1000<br /><br />**Vollständige**: 1000<br /><br />**Vollständige Modus**: 1000|  
|**Check-Einschränkungen**|Gibt an, ob SSMA Einschränkungen überprüft werden sollen, wenn sie Daten in SQL Server-Tabellen einfügt.<br /><br />**Standardmodus**: "false"<br /><br />**Vollständige**: "false"<br /><br />**Vollständige Modus**: "false"|  
|**Trigger auslösen**|Gibt an, ob SSMA einfügen Trigger ausgelöst werden soll, wenn Daten in SQL Server-Tabellen hinzugefügt.<br /><br />**Standardmodus**: "false"<br /><br />**Vollständige**: "false"<br /><br />**Vollständige Modus**: "false"|  
|**Identität beibehalten**|Gibt an, ob SSMA MySQL-Identity-Werte beibehalten, wenn Daten mit SQL Server hinzugefügt. Der Wert "false" bewirkt, dass die Identitätswerte vom Ziel zugewiesen werden.<br /><br />**Standardmodus**: "true"<br /><br />**Vollständige**: "true"<br /><br />**Vollständige Modus**: "true"|  
|**NULL-Werte beibehalten**|Gibt an, ob SSMA behält null-Werte in den Quelldaten aus, wenn Daten mit SQL Server, unabhängig von den Standardwerten hinzugefügt, die in SQL Server angegeben werden.<br /><br />**Standardmodus**: "true"<br /><br />**Vollständige**: "true"<br /><br />**Vollständige Modus**: "true"|  
|**Tabellensperre**|Gibt an, ob SSMA Tabellen sperrt, wenn sie Daten während der Datenmigration für Tabellen hinzufügt. Ruft eine Massenaktualisierungssperre für die Dauer des Massenkopiervorgangs ab. Wenn der Wert "false" ist, wird eine Sperre auf Zeilenebene festgelegt.<br /><br />**Standardmodus**: "false"<br /><br />**Vollständige**: "false"<br /><br />**Vollständige Modus**: "false"|  
  
### <a name="data-modification"></a>Datenänderung  
  
|Begriff|Definition|  
|--------|--------------|  
|**Ungültige Datumsangaben-Migration**|Gibt an, wie migrieren ungültige Datumsangaben mit z. B. ' 2007-04-23 "oder" 2000-06-31 10:00:00 "in Formate für Datum und" DateTime ".<br /><br />**Standardmodus**: NULL festlegen<br /><br />**Vollständige**: NULL festlegen<br /><br />**Vollständige Modus**: NULL festlegen|  
|**Negative Zeitwerte Migration**|Gibt an, wie zum Migrieren von negativer Werten wie "-30:11:00" in-Spalten.<br /><br />**Standardmodus**: NULL festlegen<br /><br />**Vollständige**: NULL festlegen<br /><br />**Vollständige Modus**: NULL festlegen|  
|**TIME-Werten mehr als 24 Stunden Migration**|Gibt an, wie zum Migrieren von TIME-Werten von maximal ' 23: 59:59 "in-Spalten.<br /><br />**Standardmodus**: NULL festlegen<br /><br />**Vollständige**: NULL festlegen<br /><br />**Vollständige Modus**: NULL festlegen|  
|**Abschneiden Binärwerte in Spalte anpassen**|Falls Ja, SSMA schneidet Binärwerte von MySQL, die SQL-Tabellenspalten nicht ausreicht, und entsprechende Fehlermeldung generiert. Wenn Nein, verursacht die Zeile einen Fehler<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Nein|  
|**TRUNCATE Zeichenwerten enthalten, die in der Spalte anpassen**|SSMA wird gekürzt Zeichenwerte von MySQL, die nicht in SQL-Tabellenspalten passen, und entsprechende Fehlermeldung generiert.<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Nein|  
|**0 (null) Datumsangaben-Migration**|Gibt an, wie zum Migrieren von 0 (null) Datumsangaben wie "0000-00-00" oder "0000-00-00-00:00:00" in DATE und DATETIME-Spalten.<br /><br />**Standardmodus**: NULL festlegen<br /><br />**Vollständige**: NULL festlegen<br /><br />**Vollständige Modus**: NULL festlegen|  
|**0 (null) bei Migrationen von Datumsangaben**|Gibt an, wie Datumsangaben mit 0 (null) Elementen wie migrieren "2009-01-00' oder ' 2000-00-00-11:00:00" in DATE und DATETIME-Spalten.<br /><br />**Standardmodus**: NULL festlegen<br /><br />**Vollständige**: NULL festlegen<br /><br />**Vollständige Modus**: NULL festlegen|  
  
### <a name="migration-engine"></a>Migrationsmodul  
  
|Begriff|Definition|  
|--------|--------------|  
|**Migrationsmodul**|Gibt an, während der Datenmigration verwendete Datenbankmodul. Datenmigration für Client-Side bezieht sich auf das Abrufen der Daten aus der Quelle und das Einfügen von Daten in SQL Server Bulk SSMA-Client. Server-Side-Datenmigration bezieht sich auf SSMA Migration Datenmodul (Bulk Copy Program) auf das SQL Server ausgeführt wird, als SQL-Agent-Auftrag Abrufen von Daten aus der Quelldatenbank und direkt in SQL Server, wodurch vermieden zusätzliche Client-Hop (eine bessere Leistung) einfügen.<br /><br />**Standardmodus**: Client-Seite-Migration Datenmodul<br /><br />**Vollständige**: Client-Seite-Migration Datenmodul<br /><br />**Vollständige Modus**: Client-Seite-Migration Datenmodul|  
  
> [!IMPORTANT]  
> Wenn die **Migrationsmodul** Option festgelegt wird **Server Side Migration Datenmodul**, ein neues Projekt mit dem Festlegen der Option **verwenden 32-Bit-Server-Seite-Migration-Datenmodul** wird angezeigt. Es gibt an, ob es sich bei 32-Bit oder 64-Bit (Bulk Copy Program, BCP)-Dienstprogramm zum Migrieren von Daten verwendet wird.  
  
### <a name="misc"></a>Sonstiges  
  
|Begriff|Definition|  
|--------|--------------|  
|**Die erweiterten Daten Migrationsoptionen**|Zeigt zusätzliche Daten Migrationsoptionen für jede Tabelle in separaten detailregisterkarte.<br /><br />**Standardmodus**: Ausblenden<br /><br />**Vollständige**: Ausblenden<br /><br />**Vollständige Modus**: Ausblenden|  
|**On Error**|Die Datenmigration beendet, wenn ein Fehler auftritt. Es gibt drei Optionen:<br /><br />**Beenden Sie die Migration:** Datenmigration beendet<br /><br />**Fahren Sie mit der nächsten Tabelle:** beendet die Datenmigration für die aktuelle Tabelle und geht zum nächsten Endpunkt<br /><br />**Fahren Sie mit der nächsten Batch:** Migration von Daten zu den aktuellen Batch beendet und geht zum nächsten Endpunkt<br /><br />**Standardmodus**: fahren Sie mit den nächsten Batch<br /><br />**Vollständige**: fahren Sie mit den nächsten Batch<br /><br />**Vollständige Modus**: fahren Sie mit den nächsten Batch|  
  
### <a name="parallel-data-migration"></a>Parallele Datenmigration  
  
|Begriff|Definition|  
|--------|--------------|  
|**Parallel Data Migrationsmodus**|Gibt den Modus für Verzweigung Threads verwendet werden, um parallele Datenmigration zu aktivieren. Im Auto-Modus wählt SSMA für die Anzahl der Threads (standardmäßig 10) verzweigt, um Daten zu migrieren. In benutzerdefinierten-Modus kann Benutzer angeben, die Anzahl der Threads, die zum Migrieren von Daten verzweigt (Mindestwert beträgt 1, und der Maximalwert ist 100). Zurzeit unterstützt nur Client Side Migration Datenmodul parallele Datenmigration.<br /><br />**Standardmodus**: Auto<br /><br />**Vollständige**: Auto<br /><br />**Vollständige Modus**: Auto|  
  
> [!IMPORTANT]  
> Wenn die **Parallel Daten Migrationsmodus** Option festgelegt wird **benutzerdefinierte**, ein neues Projekt mit dem Festlegen der Option **Threadanzahl** wird angezeigt. Anzahl der Threads, die für die Migration von Daten verwendet wird.  
  
### <a name="spatial-data"></a>Räumliche Daten  
  
|Begriff|Definition|  
|--------|--------------|  
|**Behandlung von Fehlern**|Gibt an, wie Fehler bei der Migration der Werte der Typen von räumlichen Daten behandelt werden. Wenn 'Ersetzen durch NULL' angegeben ist, werden alle räumlichen Werte, die Fehler verursachen durch NULL ersetzt. Kein Ersatz andernfalls erfolgt.<br /><br />**Standardmodus**: ein Fehler generiert<br /><br />**Vollständige**: ein Fehler generiert<br /><br />**Vollständige Modus**: ein Fehler generiert|  
|**Wert-Überprüfung**|Gibt an, wie ungültige räumliche Werte behandelt werden. Wenn "Versuchen stellen gültige" angegeben ist, wird ein Versuch unternommen wird, so ändern Sie ungültige Werte um gültig zu machen.<br /><br />**Standardmodus**: gültig<br /><br />**Vollständige**: nicht ändern<br /><br />**Vollständige Modus**: gültig|  
  
