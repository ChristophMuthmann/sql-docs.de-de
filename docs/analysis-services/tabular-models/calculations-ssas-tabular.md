---
title: "Berechnungen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 05f6498fce6fbc92aa497c210c3caf9a9cef6f64
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="calculations-ssas-tabular"></a>Berechnungen (SSAS – tabellarisch)
  Nachdem Sie Daten in das Modell importiert haben, können Sie Berechnungen hinzufügen, um Daten zu aggregieren, filtern, erweitern, kombinieren und schützen. Tabellarische Modelle verwenden Data Analysis Expressions (DAX), eine neue Formelsprache zum Erstellen von benutzerdefinierten Berechnungen. In tabellarischen Modellen werden die Berechnungen, die Sie mit DAX-Formeln erstellen, in *berechneten Spalten*, *Measures*und *Zeilenfiltern*verwendet.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Grundlegendes zu DAX in tabellarischen Modellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|Beschreibt die Data Analysis Expressions (DAX)-Formelsprache, die zum Erstellen von Berechnungen für berechnete Spalten, Measures und Zeilenfilter in tabellarischen Modellen verwendet wird.|  
|[DAX-Formelkompatibilität im DirectQuery-Modus (SQL Server Analysis Services)](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|Beschreibt die Unterschiede und listet die Funktionen auf, die nicht im DirectQuery-Modus unterstützt werden. Des Weiteren werden die Funktionen aufgelistet, die unterstützt werden, aber andere Ergebnisse zurückgeben können.|  
|[DAX-Referenz (Data Analysis Expressions)](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)|Dieser Abschnitt enthält ausführliche Beschreibungen der DAX-Syntax, -Operatoren und -Funktionen.|  
  
> [!NOTE]  
>  Dieser Abschnitt enthält keine Schritt-für-Schritt-Anweisungen zum Erstellen von Berechnungen. Da Berechnungen in berechneten Spalten, Measures und Zeilenfiltern (in Rollen) angegeben werden, werden die Anweisungen zum Erstellen von DAX-Formeln in Aufgaben für diese Funktionen bereitgestellt. Weitere Informationen finden Sie unter [Erstellen einer berechneten Spalte &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md), [Erstellen und Verwalten von Measures &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md) und [Erstellen und Verwalten von Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Obwohl DAX auch zum Abfragen eines tabellarischen Modells verwendet werden kann, wird in den Themen dieses Abschnitts schwerpunktmäßig das Erstellen von Berechnungen mithilfe von DAX-Formeln behandelt.  
  
  

