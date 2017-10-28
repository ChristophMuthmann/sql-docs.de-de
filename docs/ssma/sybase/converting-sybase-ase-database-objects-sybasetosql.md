---
title: Konvertieren von Sybase ASE-Datenbankobjekte (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: dd8fba1682d270251a865675f047e69a66e12479
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="converting-sybase-ase-database-objects-sybasetosql"></a>Konvertieren von Sybase ASE-Datenbankobjekte (SybaseToSQL)
Nachdem Sie auf Sybase Adaptive Server Enterprise (ASE) verbunden sind, verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und Festlegen von Projekt- und Datenoptionen für die Zuordnung, können Sie Datenbankobjekte Sybase Adaptive Server Enterprise (ASE) konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte.  
  
## <a name="the-conversion-process"></a>Konvertierungsprozess  
Konvertieren von Datenbankobjekten die Objektdefinitionen aus ASE dauert, konvertiert diese in ähnlichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte und lädt dann diese Informationen in die SSMA-Metadaten. Es lädt nicht die Informationen in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können dann die Objekte und deren Eigenschaften anzeigen, mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer.  
  
Bei der Konvertierung druckt SSMA Ausgabenachrichten in den Ausgabebereich und Fehlermeldungen in den Bereich Fehlerliste. Verwenden Sie die Ausgabe und Fehler Informationen, um festzustellen, ob Sie so ändern Sie Ihre ASE-Datenbank und die Konvertierung in die gewünschte Konvertierungsergebnisse zu erhalten haben.  
  
## <a name="setting-conversion-options"></a>Festlegen von Optionen  
Lesen Sie vor dem Konvertieren von Objekten, das Projekt Konvertierungsoptionen in der **Projekteinstellungen** (Dialogfeld). Mithilfe dieses Dialogfelds können Sie festlegen, wie SSMA Funktionen und globalen Variablen konvertiert. Weitere Informationen finden Sie unter [Projekteinstellungen &#40; Konvertierung &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
## <a name="converting-ase-database-objects"></a>Konvertieren von Datenbankobjekten ASE  
Für das Konvertieren von Datenbankobjekten ASE, stellen Sie zunächst wählen Sie die Objekte, die Sie konvertieren möchten, und lassen dann SSMA Durchführen der Konvertierung. Anzeige von Ausgabenachrichten bei der Konvertierung auf der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Konvertieren von ASE Objekte in SQL Server- bzw. SQL Azure-syntax**  
  
1.  In der Sybase-Metadaten-Explorer, erweitern Sie den Server ASE, und erweitern Sie dann **Datenbanken**.  
  
2.  Wählen Sie Objekte zu konvertieren:  
  
    -   Um alle Datenbanken zu konvertieren, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
    -   Zum konvertieren, oder lassen Sie eine Datenbank, wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zum konvertieren, oder lassen Sie die einzelnen Schemas, erweitern Sie die Datenbank und **Schemas**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben dem Schema.  
  
    -   Zum konvertieren, oder lassen Sie eine Kategorie von Objekten, erweitern Sie das Schema und aktivieren Sie oder deaktivieren Sie das Kontrollkästchen neben der Kategorie.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Objekte, erweitern Sie den Kategorieordner wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt.  
  
3.  Um alle ausgewählten Objekte zu konvertieren, Maustaste **Datenbanken** , und wählen Sie **Schema konvertieren**.  
  
    Sie können auch die einzelne Objekte oder Kategorien von Objekten konvertieren, indem das Objekt oder einem enthaltenden Ordner mit der rechten Maustaste, und anschließend **Schema konvertieren**.  
  
> [!NOTE]  
> Einige der Systemfunktionen Sybase stimmen die entsprechenden SQL Server-Systemfunktionen Verhalten nicht genau überein. Zum Emulieren des Verhaltens Sybase ASE generiert SSMA benutzerdefinierte Funktionen in der konvertierten SQL Server-Datenbank unter einem Schema "s2ss" aufgerufen. Je nach den Projekteinstellungen werden einige der SQL Server-Systemfunktionen mit diesen Funktionen "emuliert" ersetzt. SSMA erstellt die folgenden benutzerdefinierten Funktionen:  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**INTTOHEX**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**HEXTOINT**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-sql-azure"></a>Objekte, die in SQL Azure nicht unterstützt.  
Die folgenden T-SQL-Schlüsselwörter werden von SSMA für Sybase verwendet, während der Konvertierung in eine reguläre SQL Server, aber diese Schlüsselwörter werden von SQL Azure-T-SQL-Syntax nicht unterstützt:  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>Probleme bei der Konvertierung anzeigen  
Einige Objekte ASE können nicht konvertiert werden. Sie können die Erfolgsquoten Konvertierung durch Anzeigen der Zusammenfassung Konvertierungsbericht bestimmen.  
  
**So zeigen Sie einen Zusammenfassungsbericht an**  
  
1.  Wählen Sie im Metadaten-Explorer Sybase **Datenbanken**.  
  
2.  Wählen Sie im rechten Bereich die **Bericht** Registerkarte.  
  
    Dieser Bericht zeigt die Zusammenfassung Bewertungsbericht für alle Datenbankobjekte, die bewertet oder konvertiert wurden. Sie können auch einen Zusammenfassungsbericht für einzelne Objekte anzeigen:  
  
    -   Um den Bericht für eine einzelne Datenbank anzuzeigen, wählen Sie die Datenbank im Sybase-Metadaten-Explorer aus.  
  
    -   Um den Bericht für ein einzelnes Datenbankobjekt anzuzeigen, wählen Sie das Objekt in Sybase-Metadaten-Explorer aus. Objekte sind, die haben Probleme bei der Konvertierung, ein rotes Fehlersymbol.  
  
Für Objekte, die Fehler bei der Konvertierung, können Sie die Syntax anzeigen, die in der Konvertierungsfehler bewirkt, dass geführt haben.  
  
**Einzelne Konvertierungsprobleme anzeigen**  
  
1.  Erweitern Sie im Metadaten-Explorer Sybase **Datenbanken**.  
  
2.  Erweitern Sie die Datenbank, in der ein rotes Fehlersymbol angezeigt.  
  
3.  Erweitern Sie die **Schemas** Ordner, und erweitern Sie dann das Schema, das ein rotes Fehlersymbol zeigt.  
  
4.  Erweitern Sie einen Ordner mit einem roten Fehlersymbol, unter dem Schema.  
  
5.  Wählen Sie das Objekt, das ein rotes Fehlersymbol verfügt.  
  
6.  Klicken Sie im rechten Bereich auf die **Bericht** Registerkarte.  
  
7.  Am oberen Rand der **Bericht** Registerkarte ist eine Dropdown-Liste. Wenn die Liste zeigt **Statistiken**, ändern Sie die Auswahl auf **Quelle**.  
  
    SSMA wird der Quellcode und mehrere Schaltflächen direkt über dem Code angezeigt.  
  
8.  Klicken Sie auf die **weiter Problem** Schaltfläche. Dies ist ein rotes Fehlersymbol mit einem Pfeil nach rechts.  
  
    SSMA für die ASE wird die erste problematisch Quellcode zu markieren, die in das aktuelle Objekt gefunden.  
  
Für jedes Element, das nicht konvertiert werden konnte, müssen Sie ermitteln, was Sie mit diesem Objekt ausführen möchten:  
  
-   Sie können den Quellcode für Prozeduren und Trigger bearbeiten, auf die **SQL** Registerkarte.  
  
-   Sie können die ASE-Objekt zum Entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer und Sybase-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure und Migrieren von Daten aus ASE.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [laden konvertiert-Datenbankobjekte in SQLServer / SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

