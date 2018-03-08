---
title: Projekteinstellungen (Migration) (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 82f8857f-7ab1-4738-ab6e-b1e95ea94924
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b032cb4f1453a3b9a2986e5d554d21c62e606001
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-migration-sybasetosql"></a>Projekteinstellungen (Migration) (SybaseToSQL)
Die Seite "Migration", der die **Projekteinstellungen** Dialogfeld enthält Einstellungen, anpassen, wie SSMA Daten aus Sybase Adaptive Server Enterprise (ASE), migriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Der Bereich für die Migration in beiden verfügbar ist die **Projekteinstellungen** und **Projekt Standardeinstellungen** Dialogfelder.  
  
-   Zum Angeben von Einstellungen für alle SSMA-Projekte, auf die **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**, Migrationstyp-Projekt für die Einstellungen erforderlich sind, angezeigt oder geändert werden, wählen **Migration Zielversion** Dropdown-Liste auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Migration**.  
  
-   Zum Angeben von Einstellungen für das aktuelle Projekt auf die **Tools** klicken Sie im Menü **Projekteinstellungen**, klicken Sie auf **allgemeine** am unteren Rand der linken Bereich, und klicken Sie dann auf **Migration**.  
  
## <a name="date-correction-options"></a>Optionen für die Korrektur  
  
|Begriff|Definition|  
|--------|--------------|  
|**Ersetzen von nicht unterstützten Datumsangaben**|Gibt an, ob SSMA Datumsangaben Beseitigung zuständig, die älter als die früheste sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"DateTime"** Datum (01 Januar 1753).<br /><br />Um die Werte aktuell zu halten, wählen Sie **nichts**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Datumsangaben vor 01 Januar 1753 wird in einer Datetime-Spalte nicht akzeptiert werden. Wenn Sie ältere Daten verwenden, müssen Sie die Datums-/ Uhrzeitwerten in Zeichenwerten konvertieren.<br /><br />Wählen Sie zum Konvertieren von Datumsangaben vor 01 Januar 1753 auf NULL **durch NULL Ersetzen**.<br /><br />Wählen Sie zum Ersetzen von Datumsangaben vor 01 Januar 1753 durch eine unterstützte Datum **am nächsten unterstützte Datum ersetzt**.<br /><br />**Standardmodus**: Unternehmen Sie nichts<br /><br />**Vollständige**: Unternehmen Sie nichts<br /><br />**Vollständige Modus**: nächste unterstützte Datum ersetzt|  
  
## <a name="migration-engine"></a>Migrationsmodul  
  
|Begriff|Definition|  
|--------|--------------|  
|**Migrationsmodul**|Gibt an, während der Datenmigration verwendete Datenbankmodul. Datenmigration für Client-Side bezieht sich auf das Abrufen der Daten aus der Quelle und das Einfügen von Daten in SQL Server Bulk SSMA-Client. Server-Side-Datenmigration bezieht sich auf SSMA Migration Datenmodul (Bulk Copy Program) auf das SQL Server ausgeführt wird, als SQL-Agent-Auftrag Abrufen von Daten aus der Quelldatenbank und direkt in SQL Server, wodurch vermieden zusätzliche Client-Hop (eine bessere Leistung) einfügen.<br /><br />**Standardmodus**: Client-Seite-Migration Datenmodul<br /><br />**Vollständige**: Client-Seite-Migration Datenmodul<br /><br />**Vollständige Modus**: Client-Seite-Migration Datenmodul|  
  
> [!IMPORTANT]  
> Wenn die **Migrationsmodul** Option festgelegt wird **Server Side Migration Datenmodul**, ein neues Projekt mit dem Festlegen der Option **verwenden 32-Bit-Server-Seite-Migration-Datenmodul** wird angezeigt. Es gibt an, ob es sich bei 32-Bit oder 64-Bit (Bulk Copy Program, BCP)-Dienstprogramm zum Migrieren von Daten verwendet wird.  
  
## <a name="miscellaneous-options"></a>Sonstige Optionen  
  
|Begriff|Definition|  
|--------|--------------|  
|**Batchgröße**|Gibt den Batch Größe, die während der Migration von Daten verwendet.<br /><br />**Standardmodus**: 10000<br /><br />**Vollständige**: 10000<br /><br />**Vollständige Modus**: 10000|  
|**Check-Einschränkungen**|Gibt an, ob SSMA Einschränkungen überprüft werden sollen, wenn sie Daten in SQL Server-Tabellen einfügt.<br /><br />**Standardmodus**: "false"<br /><br />**Vollständige**: "false"<br /><br />**Vollständige Modus**: "false"|  
|**Data Migration Timeout**|Gibt das Timeout verwendet wird, während der Datenmigration<br /><br />**Standardmodus**: 15<br /><br />**Vollständige**: 15<br /><br />**Vollständige Modus**: 15|  
|**Die erweiterten Daten Migrationsoptionen**|Zeigt zusätzliche Daten Migrationsoptionen für jede Tabelle in separaten detailregisterkarte.<br /><br />**Standardmodus**: Ausblenden<br /><br />**Vollständige**: Ausblenden<br /><br />**Vollständige Modus**: Ausblenden|  
|**Trigger auslösen**|Gibt an, ob SSMA einfügen Trigger ausgelöst werden soll, wenn Daten in SQL Server-Tabellen hinzugefügt.<br /><br />**Standardmodus**: "false"<br /><br />**Vollständige**: "false"<br /><br />**Vollständige Modus**: "false"|  
|**Identität beibehalten**|Gibt an, ob SSMA Sybase-Identity-Werte beibehalten, wenn Daten mit SQL Server hinzugefügt. Der Wert "false" bewirkt, dass die Identitätswerte vom Ziel zugewiesen werden.<br /><br />**Standardmodus**: "true"<br /><br />**Vollständige**: "true"<br /><br />**Vollständige Modus**: "true"|  
|**NULL-Werte beibehalten**|Gibt an, ob SSMA behält null-Werte in den Quelldaten aus, wenn Daten mit SQL Server, unabhängig von den Standardwerten hinzugefügt, die in SQL Server angegeben werden.<br /><br />**Standardmodus**: "true"<br /><br />**Vollständige**: "true"<br /><br />**Vollständige Modus**: "true"|  
|**On Error**|Die Datenmigration beendet, wenn ein Fehler auftritt. Es gibt drei Optionen:<br /><br />**Beenden Sie die Migration:** Datenmigration beendet<br /><br />**Fahren Sie mit der nächsten Tabelle:** beendet die Datenmigration für die aktuelle Tabelle und geht zum nächsten Endpunkt<br /><br />**Fahren Sie mit der nächsten Batch:** Migration von Daten zu den aktuellen Batch beendet und geht zum nächsten Endpunkt<br /><br />**Standardmodus**: fahren Sie mit den nächsten Batch<br /><br />**Vollständige**: fahren Sie mit den nächsten Batch<br /><br />**Vollständige Modus**: fahren Sie mit den nächsten Batch|  
|**Teil mit Bruchzahlen enthält Runden von Zahlen**|Gibt an, ob die Sekundenbruchteile decimal und numeric-Daten während der Migration zu Ganzzahltypen trim oder Fehlermeldung angezeigt, wenn Teil mit Bruchzahlen nicht triviale ist<br /><br />**Standardmodus**: Nein<br /><br />**Vollständige**: Nein<br /><br />**Vollständige Modus**: Nein|  
|**Sybase Unicode-Endian**|Gibt den endian Typ für die Sybase Unicode-Zeichenfolgen. Die folgenden Optionen können für diese bestimmte Einstellung festgelegt werden:<br /><br />Little-endian<br /><br />Big-endian<br /><br />**Standardmodus**: Little-Endian<br /><br />**Vollständige**: Little-Endian<br /><br />**Vollständige Modus**: Little-Endian|  
|**Tabellensperre**|Gibt an, ob SSMA Tabellen sperrt, wenn sie Daten während der Datenmigration für Tabellen hinzufügt. Ruft eine Massenaktualisierungssperre für die Dauer des Massenkopiervorgangs ab. Wenn der Wert "false" ist, wird eine Sperre auf Zeilenebene festgelegt.<br /><br />**Standardmodus**: "true"<br /><br />**Vollständige**: "true"<br /><br />**Vollständige Modus**: "true"|  
|**Verwenden von Cursorn**|Die Daten werden abgerufen, aus der Quelldatenbank Cursor verwenden, wenn diese Option festgelegt ist.<br /><br />**Standardmodus**: "false"<br /><br />**Vollständige**: "false"<br /><br />**Vollständige Modus**: "false"|  
  
## <a name="parallel-data-migration"></a>Parallele Datenmigration  
  
|Begriff|Definition|  
|--------|--------------|  
|**Parallel Data Migrationsmodus**|Gibt den Modus für Verzweigung Threads verwendet werden, um parallele Datenmigration zu aktivieren. Im Auto-Modus wählt SSMA für die Anzahl der Threads (standardmäßig 10) verzweigt, um Daten zu migrieren. In benutzerdefinierten-Modus kann Benutzer angeben, die Anzahl der Threads, die zum Migrieren von Daten verzweigt (Mindestwert beträgt 1, und der Maximalwert ist 100). Zurzeit unterstützt nur Client Side Migration Datenmodul parallele Datenmigration.<br /><br />**Standardmodus**: Auto<br /><br />**Vollständige**: Auto<br /><br />**Vollständige Modus**: Auto|  
  
> [!IMPORTANT]  
> Wenn die **Parallel Daten Migrationsmodus** Option festgelegt wird **benutzerdefinierte**, ein neues Projekt mit dem Festlegen der Option **Threadanzahl** wird angezeigt. Anzahl der Threads, die für die Migration von Daten verwendet wird.  
  
