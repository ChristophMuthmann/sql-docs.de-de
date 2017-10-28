---
title: Unterschiedliche Abfragedefinitionen (Dialogfeld) (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 630593a904b4fb28e39e94a81e02481c0e6a8e1d
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>Unterschiedliche Abfragedefinitionen (Dialogfeld) (Visual Database Tools)
In diesem Dialogfeld werden Sie darauf hingewiesen, dass die Abfrage in den Bereichen Diagramm und Kriterien grafisch nicht dargestellt und daher nur im SQL-Bereich bearbeitet werden kann.  
  
Dieses Dialogfeld wird angezeigt, wenn Sie eine SQL-Anweisung im SQL-Bereich eingeben oder bearbeiten, dann zu einem anderen Bereich wechseln, die Abfrage überprüfen oder versuchen, sie auszuführen, und gleichzeitig eine der folgenden Bedingungen zutrifft:  
  
-   Die SQL-Anweisung ist unvollständig oder enthält mindestens einen Syntaxfehler.  
  
-   Die SQL-Anweisung ist gültig, wird aber von den grafischen Bereichen nicht unterstützt (z. B. eine Union-Abfrage).  
  
-   Die SQL-Anweisung ist gültig, enthält aber Syntax, die nur für die verwendete Datenverbindung gilt.  
  
> [!TIP]  
> Sie können die Gültigkeit einer Anweisung auf der Symbolleiste **Abfrage** mithilfe der Schaltfläche **Analysieren** überprüfen.  
  
Das Dialogfeld zeigt eine Meldung mit dem Hinweis an, dass die SQL-Anweisung nicht dargestellt werden kann. Geben Sie an, wie Sie weiter vorgehen möchten.  
  
> [!NOTE]  
> Das Dialogfeld **Unterschiedliche Abfragedefinitionen** wird nicht angezeigt, wenn die Bereiche „Diagramm“ und „Kriterien“ ausgeblendet sind.  
  
## <a name="options"></a>enthalten  
**Schaltfläche Ignorieren**  
Mit dieser Schaltfläche können Sie die SQL-Anweisung übernehmen, um sie weiter zu bearbeiten oder auszuführen. Wenn Sie die Anweisung übernehmen, werden die Bereiche Diagramm und Kriterien abgeblendet, um anzuzeigen, dass die Anweisung im SQL-Bereich darin nicht dargestellt wird.  
  
**Schaltfläche Rückgängig**  
Mit dieser Schaltfläche können Sie die im SQL-Bereich vorgenommenen Änderungen verwerfen.  
  
> [!NOTE]  
> Wenn die Anweisung richtig ist, aber vom Abfrage- und Sicht-Designer nicht grafisch unterstützt wird, können Sie sie ausführen, obwohl sie nicht in den Bereichen Diagramm und Kriterien dargestellt wird. Wenn Sie beispielsweise eine Union-Abfrage eingeben, kann die Anweisung ausgeführt, aber nicht in den anderen Bereichen dargestellt werden.  
  
## <a name="see-also"></a>Siehe auch  
[Tools im Abfrage- und Sicht-Designer &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  

