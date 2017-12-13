---
title: "Sortieren von Daten in einer Tabelle (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6cfced262d6b178712da538e9b678ac46357bc1a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>Sortieren von Daten in einer Tabelle (SSAS – tabellarisch)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Sie können Daten nach Text (A bis Z oder Z bis A) und Zahlen (kleinsten zu größten oder größten zu kleinsten) in einer oder mehreren Spalten sortieren.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>So sortieren Sie die Daten in einer Tabelle anhand einer Textspalte  
  
1.  Wählen Sie im Modell-Designer eine Spalte mit alphanumerischen Daten oder einen Zellbereich in einer Spalte aus, oder stellen Sie sicher, dass sich die aktive Zelle in einer Tabellenspalte befindet, die alphanumerische Daten enthält. Klicken Sie dann auf den Pfeil in der Kopfzeile der Spalte, nach der Sie filtern möchten.  
  
2.  Führen Sie im Menü AutoFilter einen der folgenden Schritte aus:  
  
    -   Um in aufsteigender alphanumerischer Reihenfolge zu sortieren, klicken Sie auf **Von A bis Z sortieren**.  
  
    -   Um in absteigender alphanumerischer Reihenfolge zu sortieren, klicken Sie auf **Von Z bis A sortieren**.  
  
    > [!NOTE]  
    >  In einigen Fällen können vor Daten, die aus anderen Anwendungen importiert werden, Leerzeichen eingefügt sein. Sie müssen diese Leerzeichen entfernen, um die Daten ordnungsgemäß sortieren zu können.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>So sortieren Sie die Daten in einer Tabelle anhand einer numerischen Spalte  
  
1.  Wählen Sie im Modell-Designer eine Spalte mit alphanumerischen Daten oder einen Zellbereich in einer Spalte aus, oder stellen Sie sicher, dass sich die aktive Zelle in einer Tabellenspalte befindet, die alphanumerische Daten enthält. Klicken Sie dann auf den Pfeil in der Kopfzeile der Spalte, nach der Sie filtern möchten.  
  
2.  Führen Sie im Menü AutoFilter einen der folgenden Schritte aus:  
  
    -   Um von niedrigen Zahlen zu hohen Zahlen zu sortieren, klicken Sie auf **Nach Größe sortieren (aufsteigend)**.  
  
    -   Um von hohen Zahlen zu niedrigen Zahlen zu sortieren, klicken Sie auf **Nach Größe sortieren (absteigend).**  
  
    > [!NOTE]  
    >  Wenn die Ergebnisse nicht die erwarteten sind, enthält die Spalte möglicherweise als Text und nicht als Zahlen gespeicherte Zahlen. Zum Beispiel werden aus einigen Abrechnungssystemen importierte negative Zahlen oder Zahlen, denen ein ' (Apostroph) vorangeht, als Text gespeichert.  
  
## <a name="see-also"></a>Siehe auch  
 [Filtern und Sortieren von Daten &#40;SSAS – tabellarisch&#41;](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspektiven &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
