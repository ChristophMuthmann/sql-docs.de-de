---
title: Bewertung, SAP ASE für die Konvertierung (SybaseToSQL Datenbankobjekte) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: bbf01a03734e3167091fd827581dbe3597bfeb53
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>Bewerten von SAP ASE Datenbankobjekte für die Konvertierung (SybaseToSQL)
Bevor Sie Objekte laden und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, sollten Sie ermitteln, wie die Komplexität der Migration und wie lange es dauern soll. SSMA kann einen Assessment-Bericht, der zeigt den Prozentsatz der Objekte und Prozeduren, die in erfolgreich konvertiert werden erstellen [!INCLUDE[tsql](../../includes/tsql_md.md)]. SSMA können auch die spezifischen Probleme anzeigen, die zu Konvertierungsfehlern führen können.  
  
## <a name="create-assessment-reports"></a>Assessment-Berichte erstellen  
Beim Erstellen dieses Berichts Assessment konvertiert SSMA die ausgewählten Datenbankobjekte für SAP Adaptive Server Enterprise (ASE), [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Syntax, und klicken Sie dann die Ergebnisse werden angezeigt.  
  
**So erstellen Sie einen Assessment-Bericht**  
  
1.  Wählen Sie im Sybase-Metadaten-Explorer Datenbanken, die Sie bewerten möchten.  
  
2.  Einzelne Objekte auslassen möchten, deaktivieren Sie die Kontrollkästchen neben den Objekten, die nicht bewertet werden sollen.  
  
3.  Mit der rechten Maustaste **Datenbanken**, und wählen Sie dann **Bericht erstellen**.  
  
    Sie können auch einzelne Objekte analysieren, indem Sie ein Objekt mit der rechten Maustaste, und wählen Sie dann **Bericht erstellen**.  
  
    SSMA wird Fortschritt in der Statusleiste am unteren Rand des Fensters. Wenn im Ausgabebereich angezeigt wird, sehen Sie auch verwandten Fehlermeldungen.  
  
    Wenn die Analyse abgeschlossen ist, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Sybase: Bewertungsbericht Fenster wird angezeigt.  
  
## <a name="use-assessment-reports"></a>Verwenden von Assessment-Berichte  
Das Assessment Berichtsfenster enthält drei Bereiche:  
  
-   Der linke Bereich enthält die Hierarchie der Objekte, die in den Bewertungsbericht enthalten sind. Sie können durchsuchen die Hierarchie und wählen Sie Objekte und Objektkategorien Konvertierungsstatistiken und Code anzeigen.  
  
-   Der Inhalt im rechten Bereich variiert abhängig, welches Element im linken Bereich ausgewählt wird.  
  
    Wenn eine Gruppe von Objekten (z. B. ein Schema) oder eine Tabelle ausgewählt ist, zeigt den rechte Bereich zwei Bereiche. Die **Konvertierungsstatistiken** Bereich zeigt die Konvertierungsstatistiken für die ausgewählten Objekte. Die **Objekte nach Kategorien** Bereich zeigt die Konvertierungsstatistiken für das Objekt oder Kategorien von Objekten.  
  
    Wenn eine gespeicherte Prozedur, Sicht oder Trigger ausgewählt ist, enthält den rechte Bereich Statistiken, Quellcode und Zielcode.  
  
    -   Der obere Bereich zeigt die Gesamtstatistik für das Objekt. Möglicherweise müssen Sie erweitern **Statistiken** zum Anzeigen dieser Informationen. 
    -   Der Quellbereich zeigt den Quellcode des Objekts, das im linken Bereich ausgewählt ist. Die hervorgehobenen Bereiche anzeigen problematisch Quellcode  
    -   Der Zielbereich zeigt den konvertierten Code. Rot formatierter Text zeigt die problematische Code und Fehlermeldungen an.  
  
-   Unteren Bereich zeigt die Konvertierung Nachrichten, gruppiert nach der Meldungsnummer. Wählen Sie **Fehler**, **Warnungen**, oder **Info** zeigt Kategorien von Nachrichten, und erweitern dann eine Gruppe von Nachrichten. Klicken Sie auf eine einzelne Nachricht an das Objekt im linken Bereich, und klicken Sie dann anzeigen auswählen die Details im rechten Bereich aus.  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>Analysieren Sie Probleme bei der Konvertierung mit den Assessment-Bericht  
Die **Konvertierungsstatistiken Bereiche** zeigen die Statistik für die Konvertierung. Wenn der Prozentsatz für eine beliebige Kategorie weniger als 100 Prozent beträgt, sollten Sie ermitteln, warum die Konvertierung nicht erfolgreich war.  
  
**So zeigen Sie Probleme bei der Konvertierung an**  
  
1.  Mithilfe der Anweisungen im vorherigen Verfahren, um den Assessment-Bericht zu erstellen.  
  
2.  Erweitern Sie im linken Bereich Schemas oder Ordner, in denen ein rotes Fehlersymbol haben. Weiterhin Elemente erweitern, bis Sie ein einzelnes Element auswählen, die Fehler bei der Konvertierung.  
  
3.  Wählen Sie im oberen Bereich des Bereichs "Quelle" **weiter Problem**.  
    Die problematische Code hervorgehoben, wie der zugehörige in Code der **Ziel Navigation** Bereich.  
  
4.  Überprüfen Sie alle Fehlermeldungen, und klicken Sie dann ermitteln Sie, was möchten Sie mit dem Objekt zu tun, die das Problem Konvertierung verursacht:  
  
    -   Aktualisieren Sie die Syntax "ASE" in SSMA. Sie können die Syntax nur für gespeicherte Prozeduren und Triggern aktualisieren. Um die Syntax zu aktualisieren, wählen Sie das Objekt in der Sybase-Metadaten-Explorer-Bereich, klicken Sie auf die **SQL** Registerkarte, und klicken Sie dann den SQL-Code bearbeiten. Wenn Sie das Element verlassen, werden Sie aufgefordert, um die aktualisierte Syntax zu speichern. Zeigen Sie die gemeldeten Fehler für das Objekt, auf die **Bericht** Registerkarte.  
  
    -   In ASE können Sie die ASE-Objekt zum Entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
    -   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Metadaten-Explorer und Sybase-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure und Migrieren von Daten aus ASE.
  
## <a name="next-steps"></a>Nächste Schritte  
[Konvertieren von SAP ASE Datenbankobjekte &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von SAP ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
