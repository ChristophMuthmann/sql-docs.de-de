---
title: "Bewerten von Oracle-Schemas für die Konvertierung (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Analyzing Conversion Problems
ms.assetid: 4de9bcf6-1346-4740-87f9-7f24a8226357
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 27faa50ad384ec9061252e056d90976687f7e3d3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="assessing-oracle-schemas-for-conversion-oracletosql"></a>Bewerten von Oracle-Schemas für die Konvertierung (OracleToSQL)
Bevor Sie Objekte laden und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], sollten Sie bestimmen, wie komplex die Migration gestellt werden und wie lange dauert die Migration. SSMA kann einen Assessment-Bericht erstellen, die den Prozentsatz von Objekten, die erfolgreich konvertiert werden. SSMA können auch die spezifischen Probleme anzeigen, die dazu führen, dass bei der Konvertierung auftreten.  
  
## <a name="creating-assessment-reports"></a>Erstellen von Berichten Assessment  
Bei der Erstellung dieser Bewertungsbericht konvertiert SSMA die ausgewählte Oracle-Datenbankobjekte, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und klicken Sie dann die Ergebnisse werden angezeigt.  
  
**So erstellen Sie einen Assessment-Bericht**  
  
1.  Wählen Sie Schemata zu bewerten, in Oracle-Metadaten-Explorer.  
  
2.  Einzelne Objekte auslassen möchten, deaktivieren Sie die Kontrollkästchen neben den.  
  
3.  Mit der rechten Maustaste **Schemas**, und wählen Sie dann **Bericht erstellen**.  
  
    Sie können auch einzelne Objekte analysieren, indem Sie ein Objekt mit der rechten Maustaste, und wählen Sie dann **Bericht erstellen**.  
  
    SSMA wird Fortschritt in der Statusleiste am unteren Rand des Fensters angezeigt wird. Wenn im Ausgabebereich angezeigt wird, wird auch Nachrichten aus dem Ausgabebereich angezeigt.  
  
    Wenn die Analyse abgeschlossen ist, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Oracle: Bewertungsbericht Fenster wird angezeigt.  
  
## <a name="using-assessment-reports"></a>Verwenden von Assessment-Berichten  
Das Assessment Berichtsfenster enthält drei Bereiche:  
  
-   Der linke Bereich enthält die Hierarchie der Objekte, die in den Bewertungsbericht enthalten sind. Sie können durchsuchen die Hierarchie, und wählen Sie Objekte und Kategorien von Objekten, die Konvertierungsstatistiken und Code anzuzeigen.  
  
-   Der Inhalt im rechten Bereich hängt das Element, das im linken Bereich ausgewählt ist.  
  
    Wenn eine Gruppe von Objekten ausgewählt ist, ein Schema, oder wenn eine Tabelle ausgewählt ist, der rechte Bereich enthält eine Konvertierung Statistiken Bereich und eine Objekte nach Bereich "Kategorien". Die Konvertierungsstatistiken Bereich zeigt die Konvertierungsstatistiken für die ausgewählten Objekte. Objekte nach Bereich "Kategorien" zeigt die Konvertierungsstatistiken für das Objekt oder Kategorien von Objekten.  
  
    Wenn eine Funktion, Paket, Prozedur, Sequenz oder Ansicht ausgewählt ist, enthält den rechte Bereich Statistiken, Quellcode und Zielcode.  
  
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
  
4.  Überprüfen Sie alle Fehlermeldungen, und klicken Sie dann ermitteln Sie, was möchten Sie mit dem Objekt zu tun, die das Problem Konvertierung verursacht:  
  
    -   Aktualisieren Sie die Oracle-Syntax in SSMA. Sie können die Syntax für Prozeduren, Funktionen, Trigger, Paketfunktionen und gepackte Prozeduren aktualisieren. Um die Syntax zu aktualisieren, wählen Sie das Objekt in der Oracle-Metadaten-Explorer-Bereich, klicken Sie auf die **SQL** Registerkarte, und ändern Sie den SQL-Code. Wenn Sie das Element verlassen, werden Sie aufgefordert, um die aktualisierte Syntax zu speichern. Sie können die berichtete Fehler ggf. für das Objekt anzeigen, auf die **Bericht** Registerkarte.  
  
    -   In Oracle können Sie die Oracle-Objekt zum Entfernen oder zu überarbeiten problematischen Code ändern. Um den aktualisierten Code in SSMA zu laden, müssen Sie die Metadaten zu aktualisieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit Oracle-Datenbank &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
    -   Sie können das Objekt von der Migration ausschließen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer und Oracle-Metadaten-Explorer, deaktivieren Sie das Kontrollkästchen neben dem Element vor dem Laden der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Migrieren von Daten aus Oracle-Datenbanken.  
  
## <a name="next-step"></a>Nächster Schritt  
[Konvertieren von Oracle-Schemas &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
