---
title: Erstellen von benannten Mengen | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculations [Analysis Services], named sets
- named sets [Analysis Services]
- members [Analysis Services], named sets
ms.assetid: 03cf97a4-1a18-45f3-acb0-35123bd619be
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ef4ed9ac6f34555cada6dabbb33f20ef01f8626d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="create-named-sets"></a>Erstellen von benannten Mengen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Eine benannte Menge ist eine Menge von Dimensionselementen oder ein Mengenausdruck, der zur Wiederverwendung, z. B. in Abfragen (Multidimensional Expressions) erstellt wird. Sie können benannte Mengen durch Kombinieren von Cubedaten, arithmetischen Operatoren, Zahlen und Funktionen erstellen. Sie können beispielsweise eine benannte Menge mit dem Namen Top Ten Factories erstellen, die die zehn Elemente der Factories-Dimension mit den höchsten Werten des Production-Measures enthält. Top Ten Factories kann dann von Endbenutzern in Abfragen verwendet werden. Ein Endbenutzer kann Top Ten Factories z. B. auf eine Achse und die Measures-Dimension, einschließlich Production, auf eine andere Achse platzieren. Weitere Informationen finden Sie unter [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md) und [Erstellen von benannten Mengen in MDX &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
 Mithilfe des Befehls **Neue benannte Menge** auf der Registerkarte **Berechnungen** des Cube-Designers können Sie eine benannte Menge erstellen. Dieser Befehl kann im Menü **Cube** auf der Symbolleiste der Registerkarte **Berechnungen** aufgerufen werden. Mit diesem Befehl wird ein Formular zum Angeben der folgenden Optionen für die benannte Menge angezeigt:  
  
 **Name**  
 Wählt den Namen der benannten Menge aus. Dieser Name wird Endbenutzern angezeigt, wenn sie den Cube durchsuchen.  
  
 **Ausdruck**  
 Gibt den Ausdruck an, der die benannte Menge erzeugt. Dieser Ausdruck kann in MDX geschrieben werden. Der Ausdruck kann Folgendes enthalten:  
  
-   Datenausdrücke, die für Cubekomponenten wie Dimensionen, Ebenen, Measures usw. stehen.  
  
-   Arithmetische Operatoren.  
  
-   Zahlen.  
  
-   Funktionen  
  
 Sie können Cubekomponenten von der Registerkarte **Metadaten** des Bereichs **Berechnungstools** in das Feld **Ausdruck** im Bereich des **Formular-Editors für benannte** Mengen kopieren oder ziehen. Sie können Funktionen von der Registerkarte **Funktionen** des Bereichs **Berechnungstools** in das Feld **Ausdruck** im Bereich des **Formular-Editors für benannte** Mengen kopieren oder ziehen.  
  
> [!IMPORTANT]  
>  Beim Erstellen des Mengenausdrucks durch explizite Benennung der Elemente in der Menge schließen Sie die Liste der Elemente in geschweifte Klammern ein ({}).  
  
## <a name="see-also"></a>Siehe auch  
 [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
