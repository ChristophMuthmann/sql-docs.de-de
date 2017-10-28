---
title: "Beurteilen den Zugriff auf Datenbankobjekte für die Konvertierung (AccessToSQL) | Microsoft Docs"
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
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 61e0ad607f242d6d96f81326621f46df9602c023
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>Beurteilen den Zugriff auf Datenbankobjekte für die Konvertierung (AccessToSQL)
Bevor Sie Objekte laden und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, Sie sollten bestimmen, wie viel kann die Migration erfolgreich sein, und wie lange die Konvertierung dauern. SSMA kann einen Assessment-Bericht, der den Prozentsatz der Objekte, die in erfolgreich konvertiert wurden erstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax und die Uhrzeit für die Migration durchführen schätzt. SSMA können auch die spezifischen Probleme anzeigen, die Konvertierungsfehler verursacht hat.  
  
## <a name="creating-assessment-reports"></a>Erstellen von Berichten Assessment  
Beim Erstellen eines Berichts Assessment konvertiert SSMA der ausgewählten den Zugriff auf Datenbankobjekte zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax, und klicken Sie dann die Ergebnisse werden angezeigt.  
  
**So erstellen Sie einen Assessment-Bericht**  
  
1.  Wählen Sie in Access-Metadaten-Explorer mindestens eine Datenbank, die Sie bewerten möchten.  
  
2.  Einzelne Objekte auslassen möchten, deaktivieren Sie die Kontrollkästchen neben den Objekten, die Sie nicht bewerten möchten.  
  
3.  Mit der rechten Maustaste **Datenbanken**, und wählen Sie dann **Bericht erstellen**.  
  
    Sie können auch einzelne Objekte analysieren, indem ein Objekt mit der rechten Maustaste, und wählen Sie dann **Bericht erstellen**.  
  
    SSMA wird Fortschritt in der Statusleiste am unteren Rand des Fensters. Wenn im Ausgabebereich angezeigt wird, wird auch Nachrichten aus dem Ausgabebereich angezeigt.  
  
Wenn die Analyse abgeschlossen ist, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Access: Bewertungsbericht Fenster wird angezeigt.  
  
## <a name="using-assessment-reports"></a>Verwenden von Assessment-Berichten  
Das Assessment Berichtsfenster enthält drei Bereiche: einen Explorer, ein Detailbereich und einen Meldungsbereich.  
  
-   Explorerbereich können Sie die Objekte zu durchsuchen, die bewertet wurden. Sie können Elemente in diesem Bereich Drilldown auf einzelne Tabellen, Indizes und Schlüssel klicken.  
  
-   Im Detailbereich werden die Konvertierungsstatistiken für das ausgewählte Objekt.  
  
-   Im Meldung angezeigt wird, die Fehler, Warnungen und informationsmeldungen für die Konvertierung, und die geschätzte Dauer, für die Migration und die einzelnen Fehler Korrektur Schritte ausführen.  
  
Fehler sollten korrigiert werden, bevor Sie den Assessment-Bericht erneut ausführen, oder Konvertieren von Schemas. Um Fehler zu finden, klicken Sie auf die **Fehler** im Meldungsbereich Schaltfläche, und erweitern Sie dann die einzelnen Fehler um eine Liste von Objekten anzuzeigen, in dem der Fehler aufgetreten ist. Wenn Sie ein Objekt im Meldungsbereich, klicken Sie auf alle Fehler und Warnungen für dieses Objekt werden im Detailbereich angezeigt.  
  
## <a name="next-step"></a>Nächster Schritt  
[Konvertieren den Zugriff auf Datenbankobjekte](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

