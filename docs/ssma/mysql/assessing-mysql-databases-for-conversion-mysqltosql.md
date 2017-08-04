---
title: "Bewerten MySQL-Datenbanken für die Konvertierung (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
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
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 24e18761f50997b32da67a8ed2277259f5d53516
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>Bewerten MySQL-Datenbanken für die Konvertierung (MySQLToSQL)
Bevor Sie Objekte laden und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, sollten Sie bestimmen, wie komplex die Migration gestellt werden und wie lange dauert die Migration. SSMA kann einen Assessment-Bericht erstellen, die den Prozentsatz von Objekten, die erfolgreich konvertiert werden. SSMA können auch die spezifischen Probleme anzeigen, die dazu führen, dass bei der Konvertierung auftreten.  
  
## <a name="creating-assessment-reports"></a>Erstellen von Berichten Assessment  
Bei der Erstellung dieser Bewertungsbericht konvertiert SSMA die ausgewählten MySQL-Datenbankobjekte, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax, und klicken Sie dann die Ergebnisse werden angezeigt.  
  
**So erstellen Sie einen Assessment-Bericht**  
  
1.  Wählen Sie Schemata zu bewerten, in MySQL-Metadaten-Explorer.  
  
2.  Einzelne Objekte auslassen möchten, deaktivieren Sie die Kontrollkästchen neben den.  
  
3.  Mit der rechten Maustaste **Schemas**, und wählen Sie dann **Bericht erstellen**.  
  
    Mit der rechten Maustaste in ein Objekt, um einzelne Objekte zu analysieren. Aktivieren Sie das Kontrollkästchen **Bericht erstellen**.  
  
    SSMA wird Fortschritt in der Statusleiste am unteren Rand des Fensters angezeigt wird. Wenn im Ausgabebereich angezeigt wird, wird auch Nachrichten aus dem Ausgabebereich angezeigt.  
  
    Wenn die Analyse abgeschlossen ist, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für MySQL Bewertungsbericht Fenster wird angezeigt.  
  
## <a name="using-assessment-reports"></a>Verwenden von Assessment-Berichten  
Das Assessment Berichtsfenster enthält drei Bereiche:  
  
-   Der linke Bereich enthält die Hierarchie der Objekte, die in den Bewertungsbericht enthalten sind. Sie können durchsuchen die Hierarchie, und wählen Sie Objekte und Kategorien von Objekten, die Konvertierungsstatistiken und Code anzuzeigen.  
  
-   Der Inhalt im rechten Bereich hängt das Element, das im linken Bereich ausgewählt ist.  
  
    Wenn eine Gruppe von Objekten, z. B. Schema aktiviert ist, enthält den rechte Bereich eine Konvertierung Statistiken Bereich und Objekte nach Bereich "Kategorien" an. Die Konvertierungsstatistiken Bereich zeigt die Konvertierungsstatistiken für die ausgewählten Objekte. Objekte nach Bereich "Kategorien" zeigt die Konvertierungsstatistiken für das Objekt oder Kategorien von Objekten.  
  
    Wenn die Funktion, Prozedur, Tabelle oder Ansicht ausgewählt ist, enthält Bereich Rechte Statistiken, Quellcode und Zielcode.  
  
    -   Der obere Bereich zeigt die Gesamtstatistik für das Objekt. Möglicherweise müssen Sie erweitern **Statistiken** zum Anzeigen dieser Informationen.  
  
    -   Der Quellbereich zeigt den Quellcode des Objekts, das im linken Bereich ausgewählt ist. Die hervorgehobenen Bereiche anzeigen problematisch Quellcode  
  
    -   Der Zielbereich zeigt den konvertierten Code. Rot formatierter Text zeigt die problematische Code und Fehlermeldungen an.  
  
-   Unteren Bereich zeigt die Konvertierung Nachrichten, gruppiert nach der Meldungsnummer. Klicken Sie auf **Fehler**, **Warnungen**, oder **Info** zeigt Kategorien von Nachrichten, und erweitern dann eine Gruppe von Nachrichten. Klicken Sie auf eine einzelne Nachricht, wählen Sie im linken Bereich das Objekt und die Details im rechten Bereich angezeigt.  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>Analysieren Probleme bei der Konvertierung mithilfe der Bewertungsbericht  
Die Konvertierungsstatistiken Bereich zeigt die Konvertierungsstatistiken. Wenn der Prozentsatz für eine beliebige Kategorie weniger als 100 Prozent beträgt, sollten Sie ermitteln, warum die Konvertierung nicht erfolgreich war.  
  
**So zeigen Sie Probleme bei der Konvertierung an**  
  
1.  Mithilfe der Anweisungen im vorherigen Verfahren, um den Assessment-Bericht zu erstellen.  
  
2.  Erweitern Sie im linken Bereich Schemas oder Ordner, in denen ein rotes Fehlersymbol haben. Weiterhin Elemente erweitern, bis Sie ein einzelnes Element auswählen, die Fehler bei der Konvertierung.  
  
3.  Klicken Sie im oberen Bereich des Bereichs "Quelle" auf **weiter Problem**.  
  
    Die problematische Code wird hervorgehoben, wie der zugehörige Code im Navigationsbereich Ziel ist.  
  
4.  Überprüfen Sie alle Fehlermeldungen, und klicken Sie dann zu bestimmen Sie, was Sie möchten mit dem Objekt, das die Konvertierung Problem verursacht hat.  
  
-   Aktualisieren Sie die MySQL-Syntax in SSMA. Sie können die Syntax nur für Prozeduren und Funktionen aktualisieren. Um die Syntax zu aktualisieren, wählen Sie das Objekt in der MySQL-Metadaten-Explorer-Bereich, klicken Sie auf die **SQL** Registerkarte, und ändern Sie den SQL-Code. Wenn Sie das Element verlassen, werden Sie aufgefordert, um die aktualisierte Syntax zu speichern. Sie können die berichtete Fehler ggf. für das Objekt anzeigen, auf die **Bericht** Registerkarte.  
  
-   In MySQL können Sie die MySQL-Objekt zum Entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit MySQL &#40; MySQLToSQL &#41; ](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).  
  
-   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer und MySQL-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure und Migrieren von Daten aus MySQL.  
  
## <a name="next-step"></a>Nächster Schritt  
[Konvertieren von MySQL-Datenbanken &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

