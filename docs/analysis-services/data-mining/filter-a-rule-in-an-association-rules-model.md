---
title: Filtern einer Regel in einer Zuordnung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtering rules [Analysis Services]
- Mining Model Viewer [Analysis Services], rules
- Rules Viewer
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a7f0a74cc5f14d268b5854781786608ee9e4fc4d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="filter-a-rule-in-an-association-rules-model"></a>Filtern einer Regel in einem Zuordnungsregelmodell
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sie können Filterung mit zuordnungsmodellen verwenden, um die Ergebnisse auf die Zuordnungen zu beschränken, die Sie interessieren. Zum Beispiel können Sie die Regeln filtern, damit nur die Ergebnisse angezeigt werden, die ein bestimmtes Produkt enthalten.  
  
 Im Data Mining-Designer verwenden Sie die Steuerelemente auf der Registerkarte **Regeln** des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Zuordnungsregeln-Viewers, um die angezeigten Regeln zu filtern.  Sie können auch eine Abfrage für das Modell erstellen, um nur Itemsets anzuzeigen, die einen bestimmten Wert enthalten.  
  
> [!NOTE]  
>  Diese Option ist nur für Miningmodelle verfügbar, die mit dem Microsoft Association-Algorithmus erstellt wurden.  
  
### <a name="filter-a-rule-in-an-association-model"></a>Filtern einer Regel in einem Zuordnungsmodell  
  
1.  Öffnen Sie das Miningmodell mit dem **Zuordnungsregeln-Viewer**. In SQL Server Management Studio müssen Sie hierzu mit der rechten Maustaste auf den Modellnamen klicken und **Durchsuchen**auswählen. Doppelklicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf die Miningstruktur, die das Modell enthält, und klicken Sie anschließend auf die Registerkarte **Miningmodell-Viewer** im **Data Mining-Designer**.  
  
2.  Klicken Sie im **Zuordnungsregeln-Viewer** auf die Registerkarte **Regeln**.  
  
3.  Geben Sie in das Feld **Filterregel** eine Regelbedingung ein. Eine Regelbedingung könnte z. B. "Bike Stand" sein, die auch "Bike Stands" zurückgibt.  
  
     Das Textfeld **Filterregel** unterstützt reguläre Ausdrücke, wie diese von der .NET-Sprache definiert werden. Daher können Sie z. B. folgende Ausdrücke verwenden: `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))`. Dieser Ausdruck gibt alle Itemsets zurück, die Attribute mit den Wörtern Helmets und Fenders in beliebiger Reihenfolge enthalten.  
  
4.  Erhöhen Sie unter **Minimale Wahrscheinlichkeit**den Wert für die Wahrscheinlichkeit, um mehr Regeln anzuzeigen, und verringern Sie den Wert, um weniger Regeln anzuzeigen.  
  
5.  Erhöhen Sie unter **Minimale Wichtigkeit**den Wert für die Wichtigkeit, um mehr Regeln anzuzeigen, und verringern Sie den Wert, um weniger Regeln anzuzeigen.  
  
6.  Wählen Sie für **Anzeigen**eine der folgenden Optionen aus: **Attributnamen und Wert anzeigen**, **Nur Attributnamen anzeigen**oder **Nur Attributwert anzeigen**.  
  
7.  Erhöhen Sie den Wert für **Maximale Zeilenanzahl**, um die Gesamtzahl von Regeln zu erhöhen, die die angegebenen Bedingungen erfüllen, oder verringern Sie den Wert, um die Anzahl der zurückgegebenen Regeln zu beschränken. Regeln werden nach Wahrscheinlichkeit sortiert. Daher können Sie zusätzliche Regeln ausschließen, die die angegebenen Bedingungen für Wahrscheinlichkeit oder Wichtigkeit erfüllen.  
  
8.  Aktivieren oder deaktivieren Sie das Kontrollkästchen **Langen Namen anzeigen** , um umzuschalten, wie die Namen der Regeln angezeigt werden.  
  
     Die Regeln werden daraufhin gefiltert und es werden nur Regeln angezeigt, die das angegebene Element enthalten. Die Filterbedingung gilt für Attributwerte, die entweder vor oder nach dem Regeltrennzeichen "->" stehen.  
  
    > [!NOTE]  
    >  Der Viewer speichert die ursprüngliche Liste der Regeln basierend auf einer Abfrage des Miningmodells und aktualisiert die Liste der Regeln nur, wenn Sie die Bedingungen für die Abfrage ändern, indem Sie die maximale Zeilenanzahl, die Wahrscheinlichkeit, die Wichtigkeit oder die Anzeige langer Namen festlegen. Wenn Sie eine Bedingung eingeben und die Anzeige nicht sofort aktualisiert wird, können Sie im Viewer daher eine Aktualisierung der Daten erzwingen, indem Sie das Kontrollkästchen **Langen Namen anzeigen** aktivieren und anschließend wieder deaktivieren.  
  
### <a name="create-a-query-on-the-itemsets-in-an-association-model"></a>Erstellen einer Abfrage in den Itemsets in einem Zuordnungsmodell  
  
-   [Beispiele für Zuordnungsmodellabfragen](../../analysis-services/data-mining/association-model-query-examples.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Tasks und Anweisungen für Miningmodell-Viewer](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Durchsuchen eines Modells mit dem Microsoft Association Rules-Viewer](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [Lektion 3: Erstellen eines Warenkorbszenarios &#40; Datamining-Lernprogramm für fortgeschrittene &#41;](http://msdn.microsoft.com/library/651eef38-772e-4d97-af51-075b1b27fc5a)  
  
  
