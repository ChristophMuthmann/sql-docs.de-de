---
title: Filtern von Daten in einer Tabelle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.notallitemsshowing.f1
- sql13.asvs.bidtoolset.autofiltermenu.f1
- sql13.asvs.bidtoolset.customfilterdb.f1
ms.assetid: 3223059d-f525-4835-bf88-ebc195d9dbdc
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 817ee61a90eb9810b42765f9031641ba15d45aef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="filter-data-in-a-table"></a>Filtern von Daten in einer Tabelle 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Sie können beim Importieren von Daten Filter anwenden, um zu steuern, welche Zeilen in eine Tabelle geladen werden. Nachdem Sie die Daten importiert haben, können Sie keine einzelnen Zeilen löschen. Sie können jedoch benutzerdefinierte Filter anwenden, um zu steuern, wie Zeilen angezeigt werden. Zeilen, die die Filterkriterien nicht erfüllen, werden ausgeblendet. Sie können nach einer oder mehreren Spalten filtern. Filter sind additiv. Das bedeutet, dass jeder zusätzliche Filter auf dem aktuellen Filter basiert und die Teilmenge der Daten weiter reduziert.  
  
> [!NOTE]  
>  Das Filtervorschaufenster schränkt die Anzahl der unterschiedlichen Werte ein, die angezeigt werden. Wenn die Grenze überschritten wird, wird eine Meldung angezeigt.  
  
### <a name="to-filter-data-based-on-column-values"></a>So filtern Sie Daten auf Grundlage von Spaltenwerten  
  
1.  Wählen Sie im Modell-Designer eine Tabelle aus, und klicken Sie dann auf den Pfeil in der Kopfzeile der Spalte, nach der Sie filtern möchten.  
  
2.  Führen Sie im Menü AutoFilter einen der folgenden Schritte aus:  
  
    -   Wählen Sie in der Liste der Spaltenwerte mindestens einen Wert aus, nach dem gefiltert werden soll, bzw. heben Sie die Auswahl auf, und klicken Sie auf **OK**.  
  
         Wenn die Anzahl der Werte sehr groß ist, kann es sein, dass einzelne Elemente nicht in der Liste angezeigt werden. Stattdessen wird eine Meldung angezeigt, dass zu viele Elemente zum Anzeigen vorhanden sind.  
  
    -   Klicken Sie je nach Typ der Spalte auf **Zahlenfilter** oder **Textfilter** , und klicken Sie anschließend auf einen der Vergleichsoperatorbefehle (wie **Ist gleich**), oder klicken Sie auf **Benutzerdefinierter Filter**. Erstellen Sie im Dialogfeld **Benutzerdefinierter Filter** den Filter, und klicken Sie dann auf **OK**.  
  
### <a name="to-clear-a-filter-for-a-column"></a>So löschen Sie einen Filter für eine Spalte  
  
1.  Klicken Sie auf den Pfeil in der Kopfzeile der Spalte, für die Sie den Filter löschen möchten.  
  
2.  Klicken Sie auf **Filter löschen aus \<Spaltenname >**.  
  
### <a name="to-clear-all-filters-for-a-table"></a>So löschen Sie alle Filter für eine Tabelle  
  
1.  Wählen Sie im Modell-Designer die Tabelle aus, für die Sie die Filter löschen möchten.  
  
2.  Klicken Sie auf das Menü **Spalte** und dann auf **Alle Filter löschen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Filtern und Sortieren von Daten](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspektiven](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
