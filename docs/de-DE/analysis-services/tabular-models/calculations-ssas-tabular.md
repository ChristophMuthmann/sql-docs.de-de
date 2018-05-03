---
title: Berechnungen | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b657318ac3e03759f39031a92b73a098d3334e6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calculations"></a>Berechnungen 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Nachdem Sie Daten in das Modell importiert haben, können Sie Berechnungen hinzufügen, um Daten zu aggregieren, filtern, erweitern, kombinieren und schützen. Tabellarische Modelle verwenden Data Analysis Expressions (DAX), eine neue Formelsprache zum Erstellen von benutzerdefinierten Berechnungen. In tabellarischen Modellen werden die Berechnungen, die Sie mit DAX-Formeln erstellen, in *berechneten Spalten*, *Measures*und *Zeilenfiltern*verwendet.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Grundlegendes zu DAX in tabellarischen Modellen](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|Beschreibt die Data Analysis Expressions (DAX)-Formelsprache, die zum Erstellen von Berechnungen für berechnete Spalten, Measures und Zeilenfilter in tabellarischen Modellen verwendet wird.|  
|[DAX-formelkompatibilität im DirectQuery-Modus](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|Beschreibt die Unterschiede und listet die Funktionen auf, die nicht im DirectQuery-Modus unterstützt werden. Des Weiteren werden die Funktionen aufgelistet, die unterstützt werden, aber andere Ergebnisse zurückgeben können.|  
|[DAX-Referenz (Data Analysis Expressions)](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)|Dieser Abschnitt enthält ausführliche Beschreibungen der DAX-Syntax, -Operatoren und -Funktionen.|  
  
> [!NOTE]  
>  Dieser Abschnitt enthält keine Schritt-für-Schritt-Anweisungen zum Erstellen von Berechnungen. Da Berechnungen in berechneten Spalten, Measures und Zeilenfiltern (in Rollen) angegeben werden, werden die Anweisungen zum Erstellen von DAX-Formeln in Aufgaben für diese Funktionen bereitgestellt. Weitere Informationen finden Sie unter [erstellen Sie eine berechnete Spalte](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md), [erstellen und Verwalten von Measures](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md), und [erstellen und Verwalten von Rollen](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Obwohl DAX auch zum Abfragen eines tabellarischen Modells verwendet werden kann, wird in den Themen dieses Abschnitts schwerpunktmäßig das Erstellen von Berechnungen mithilfe von DAX-Formeln behandelt.  
  
  
