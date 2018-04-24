---
title: Interaktives Durchsuchen von Dokumenten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 78859e16a613bc6e40078bcf196b632f768fcb86
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="search-documents-interactively"></a>Interaktives Durchsuchen von Dokumenten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Mithilfe des Dialogfelds **Suchen und Ersetzen** können Sie einzelne oder mehrere geöffnete Dateien oder Fenster durchsuchen und sich einzeln durch die Suchübereinstimmungen bewegen. Bei dieser Technik können Sie einzelne Suchübereinstimmungen im Kontext der jeweiligen Textpassage überprüfen. Außerdem können Sie Massensuchvorgänge ausführen und Suchübereinstimmungen über das Dialogfeld **Suchen und Ersetzen** im Berichtsformat überprüfen.  
  
### <a name="to-search-all-open-documents"></a>So durchsuchen Sie alle geöffneten Dokumente  
  
1.  Öffnen Sie die Elemente, die Sie durchsuchen möchten.  
  
2.  Zeigen Sie im Menü **Bearbeiten** auf **Suchen und Ersetzen** , und klicken Sie dann auf **Schnellsuche**.  
  
3.  Geben Sie in das Textfeld **Suchen und Ersetzen** den Text ein, nach dem Sie suchen möchten.  
  
4.  Wählen Sie in der Liste **Suchen in** die Option **Alle geöffneten Dokumente**aus.  
  
    > [!NOTE]  
    >  Bestimmte geöffnete Dateien lassen sich möglicherweise nicht durchsuchen, wenn die Option **Alle geöffneten Dokumente** ausgewählt ist. In die Suchvorgänge werden nur Dateien einbezogen, die zurzeit in einer Textansicht geöffnet sind, z. B. in der Codeansicht. Dateien in der Entwurfssicht werden nicht in Suchvorgänge einbezogen.  
  
5.  Wählen Sie weitere Suchoptionen aus, um die Genauigkeit des Suchvorgangs zu erhöhen.  
  
6.  Klicken Sie auf **Weitersuchen** , um die Suche zu starten, und klicken Sie wiederholt auf **Weitersuchen** , bis die letzte Datei durchsucht wurde.  
  
 Wenn der Suchvorgang am Anfang oder Ende des Dokuments angelangt, wird auf der Statusleiste eine Meldung angezeigt. Wenn der Suchvorgang am Anfangspunkt der Suche angelangt ist, wird ein Meldungsfeld angezeigt.  
  
#### <a name="to-replace-in-all-active-files-interactively"></a>So können Sie Elemente in allen aktiven Dateien interaktiv ersetzen  
  
1.  Zeigen Sie im Menü **Bearbeiten** auf **Suchen und Ersetzen**, und klicken Sie dann auf **Schnellersetzung**.  
  
2.  Geben Sie in das Feld **Suchen nach** den Text ein, nach dem Sie suchen möchten.  
  
3.  Geben Sie in das Feld **Ersetzen durch** den Text ein, durch den der Suchtext ersetzt werden soll.  
  
4.  Wählen Sie in der Liste **Suchen in** die Option **Alle geöffneten Dokumente**aus.  
  
5.  Klicken Sie auf **Ersetzen**, und klicken Sie wiederholt auf **Ersetzen** , bis die letzte Übereinstimmung in der letzten Datei ersetzt wurde. Wenn Sie eine Übereinstimmung auslassen möchten, die nicht ersetzt werden soll, klicken Sie auf **Weitersuchen** .  
  
     -oder-  
  
     Wählen Sie die Option **Alle ersetzen** aus, um alle Übereinstimmungen zu ersetzen. In einem Meldungsfeld wird die Gesamtanzahl der Ersetzungen angezeigt.  
  
 Mit dem Befehl **Alle ersetzen** werden alle Suchübereinstimmungen ersetzt. Dazu gehören auch die Übereinstimmungen, die Sie zuvor mit der Schaltfläche **Weitersuchen** ausgelassen haben. Um den Befehl **Alle ersetzen**abzubrechen, klicken Sie im Menü **Bearbeiten** auf **Rückgängig** , bevor Sie eine der Dateien schließen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Inkrementelles Durchsuchen eines aktiven Dokuments](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [Suchen und Ersetzen](../../relational-databases/scripting/search-and-replace.md)   
 [Durchsuchen von Dokumenten mithilfe von Ergebnislisten](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Suchen von Text mit Platzhaltern](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Suchen von Text mit regulären Ausdrücken](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
