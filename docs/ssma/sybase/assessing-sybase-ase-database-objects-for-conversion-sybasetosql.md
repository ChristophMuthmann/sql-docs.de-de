---
title: "Bewertung Sybase ASE für die Konvertierung (SybaseToSQL Datenbankobjekte) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ae77c759c4856ecb3b74cbaeb36f0123398c2e16
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="assessing-sybase-ase-database-objects-for-conversion-sybasetosql"></a>Bewerten von Sybase ASE Datenbankobjekte für die Konvertierung (SybaseToSQL)
Bevor Sie Objekte laden und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, sollten Sie bestimmen, wie komplex die Migration gestellt werden und wie lange dauert die Migration. SSMA kann einen Assessment-Bericht, der zeigt den Prozentsatz der Objekte und Prozeduren, die in erfolgreich konvertiert werden erstellen [!INCLUDE[tsql](../../includes/tsql_md.md)]. SSMA können auch die spezifischen Probleme anzeigen, die Fehler bei der Konvertierung verursachen.  
  
## <a name="creating-assessment-reports"></a>Erstellen von Berichten Assessment  
Bei der Erstellung dieser Bewertungsbericht konvertiert SSMA die ausgewählten Datenbankobjekte von Sybase Adaptive Server Enterprise (ASE), [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax, und klicken Sie dann die Ergebnisse werden angezeigt.  
  
**So erstellen Sie einen Assessment-Bericht**  
  
1.  Wählen Sie im Sybase-Metadaten-Explorer Datenbanken, die Sie bewerten möchten.  
  
2.  Einzelne Objekte auslassen möchten, deaktivieren Sie die Kontrollkästchen neben den Objekten, die nicht bewertet werden sollen.  
  
3.  Mit der rechten Maustaste **Datenbanken**, und wählen Sie dann **Bericht erstellen**.  
  
    Sie können auch einzelne Objekte analysieren, indem Sie ein Objekt mit der rechten Maustaste, und wählen Sie dann **Bericht erstellen**.  
  
    SSMA wird Fortschritt in der Statusleiste am unteren Rand des Fensters angezeigt wird. Wenn im Ausgabebereich angezeigt wird, wird auch Nachrichten aus dem Ausgabebereich angezeigt.  
  
    Wenn die Analyse abgeschlossen ist, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Sybase: Bewertungsbericht Fenster wird angezeigt.  
  
## <a name="using-assessment-reports"></a>Verwenden von Assessment-Berichten  
Das Assessment Berichtsfenster enthält drei Bereiche:  
  
-   Der linke Bereich enthält die Hierarchie der Objekte, die in den Bewertungsbericht enthalten sind. Sie können die Hierarchie durchsuchen und auswählen, Objekte und Kategorien von Objekten, die Konvertierungsstatistiken anzeigen und Code.  
  
-   Den Inhalt im rechten Bereich hängt von der im linken Bereich ausgewählten Elements ab.  
  
    Wenn eine Gruppe von Objekten ausgewählt ist, solche ein Schema oder eine Tabelle ausgewählt ist der rechte Bereich enthält einen Konvertierung Statistiken und Objekten von Bereich "Kategorien". Die Konvertierungsstatistiken Bereich zeigt die Konvertierungsstatistiken für die ausgewählten Objekte. Objekte nach Bereich "Kategorien" zeigt die Konvertierungsstatistiken für das Objekt oder Kategorien von Objekten.  
  
    Wenn eine gespeicherte Prozedur, Sicht oder Trigger ausgewählt ist, enthält den rechte Bereich Statistiken, Quellcode und Zielcode.  
  
    -   Der obere Bereich zeigt die Gesamtstatistik für das Objekt. Möglicherweise müssen Sie erweitern **Statistiken** zum Anzeigen dieser Informationen.  
  
    -   Der Quellbereich zeigt den Quellcode des Objekts, das im linken Bereich ausgewählt ist. Die hervorgehobenen Bereiche anzeigen problematisch Quellcode  
  
    -   Der Zielbereich zeigt den konvertierten Code. Rot formatierter Text zeigt die problematische Code und Fehlermeldungen an.  
  
-   Unteren Bereich zeigt die Konvertierung Nachrichten, gruppiert nach der Meldungsnummer. Klicken Sie auf **Fehler**, **Warnungen**, oder **Info** zeigt Kategorien von Nachrichten, und erweitern dann eine Gruppe von Nachrichten. Klicken Sie auf eine einzelne Nachricht, wählen Sie im linken Bereich das Objekt und die Details im rechten Bereich angezeigt.  
  
## <a name="analyzing-conversion-problems-using-the-assessment-report"></a>Analysieren Probleme bei der Konvertierung mit den Assessment-Bericht  
Die Konvertierungsstatistiken Bereiche anzeigen, die Konvertierungsstatistiken. Wenn der Prozentsatz für eine beliebige Kategorie weniger als 100 Prozent beträgt, sollten Sie ermitteln, warum die Konvertierung nicht erfolgreich war.  
  
**So zeigen Sie Probleme bei der Konvertierung an**  
  
1.  Mithilfe der Anweisungen im vorherigen Verfahren, um den Assessment-Bericht zu erstellen.  
  
2.  Erweitern Sie im linken Bereich Schemas oder Ordner, in denen ein rotes Fehlersymbol haben. Weiterhin Elemente erweitern, bis Sie ein einzelnes Element auswählen, die Fehler bei der Konvertierung.  
  
3.  Klicken Sie im oberen Bereich des Bereichs "Quelle" auf **weiter Problem**.  
  
    Die problematische Code wird hervorgehoben, wie der zugehörige Code im Navigationsbereich Ziel ist.  
  
4.  Überprüfen Sie alle Fehlermeldungen, und klicken Sie dann ermitteln Sie, was möchten Sie mit dem Objekt zu tun, die das Problem Konvertierung verursacht:  
  
    -   Aktualisieren Sie die Syntax "ASE" in SSMA. Sie können die Syntax nur für gespeicherte Prozeduren und Triggern aktualisieren. Um die Syntax zu aktualisieren, wählen Sie das Objekt in der Sybase-Metadaten-Explorer-Bereich, klicken Sie auf die **SQL** Registerkarte, und klicken Sie dann den SQL-Code bearbeiten. Wenn Sie das Element verlassen, werden Sie aufgefordert, um die aktualisierte Syntax zu speichern. Sie können die berichtete Fehler ggf. für das Objekt anzeigen, auf die **Bericht** Registerkarte.  
  
    -   In ASE können Sie die ASE-Objekt zum Entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer und Sybase-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure und Migrieren von Daten aus ASE.  
  
## <a name="next-step"></a>Nächster Schritt  
[Konvertieren von Sybase ASE Datenbankobjekte &#40; SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
