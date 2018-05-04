---
title: Erstellen von benannten Mengen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52248437e6de4039fd0b2d7d3cc7bec42686a312
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-named-sets"></a>Erstellen von benannten Mengen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine benannte Menge ist eine Menge von Dimensionselementen oder ein Mengenausdruck, der zur Wiederverwendung, z. B. in MDX-Abfragen (Multidimensional Expressions), erstellt wird. Sie können benannte Mengen durch Kombinieren von Cubedaten, arithmetischen Operatoren, Zahlen und Funktionen erstellen. Sie können beispielsweise eine benannte Menge mit dem Namen Top Ten Factories erstellen, die die zehn Elemente der Factories-Dimension mit den höchsten Werten des Production-Measures enthält. Top Ten Factories kann dann von Endbenutzern in Abfragen verwendet werden. Ein Endbenutzer kann Top Ten Factories z. B. auf eine Achse und die Measures-Dimension, einschließlich Production, auf eine andere Achse platzieren. Weitere Informationen finden Sie unter [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md) und [Erstellen von benannten Mengen in MDX &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
 Mithilfe des Befehls **Neue benannte Menge** auf der Registerkarte **Berechnungen** des Cube-Designers können Sie eine benannte Menge erstellen. Dieser Befehl kann im Menü **Cube** auf der Symbolleiste der Registerkarte **Berechnungen** aufgerufen werden. Mit diesem Befehl wird ein Formular zum Angeben der folgenden Optionen für die benannte Menge angezeigt:  
  
 **Name**  
 Wählt den Namen der benannten Menge aus. Dieser Name wird Endbenutzern angezeigt, wenn sie den Cube durchsuchen.  
  
 **expression**  
 Gibt den Ausdruck an, der die benannte Menge erzeugt. Dieser Ausdruck kann in MDX geschrieben werden. Der Ausdruck kann Folgendes enthalten:  
  
-   Datenausdrücke, die für Cubekomponenten wie Dimensionen, Ebenen, Measures usw. stehen.  
  
-   Arithmetische Operatoren.  
  
-   Zahlen.  
  
-   Funktionen  
  
 Sie können Cubekomponenten von der Registerkarte **Metadaten** des Bereichs **Berechnungstools** in das Feld **Ausdruck** im Bereich des **Formular-Editors für benannte** Mengen kopieren oder ziehen. Sie können Funktionen von der Registerkarte **Funktionen** des Bereichs **Berechnungstools** in das Feld **Ausdruck** im Bereich des **Formular-Editors für benannte** Mengen kopieren oder ziehen.  
  
> [!IMPORTANT]  
>  Wenn Sie Mengenausdrucks durch explizite Benennung der Elemente in der Gruppe erstellen, schließen Sie die Liste der Elemente in einem Paar von geschweiften Klammern ({}).  
  
## <a name="see-also"></a>Siehe auch  
 [Berechnungen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
