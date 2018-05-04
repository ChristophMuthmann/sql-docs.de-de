---
title: Erstellen eine währungstypdimension | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 32a1047475192b68c30e4ff8b7185c3572c2cc56
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="database-dimensions---create-a-currency-type-dimension"></a>Datenbankdimensionen – Erstellen einer währungstypdimension
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist eine Dimension vom Typ "Währung" eine Dimension, deren Attribute eine Auflistung von Währungen für Finanzberichte darstellt.  
  
 Mit einer Währungsdimension können Sie einem Cube in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Funktionen für die Währungsumrechnung hinzufügen. Wenn Sie einem Cube die Währungsumrechnung hinzufügen möchten, verwenden Sie den Business Intelligence-Assistenten zum Definieren eines Multidimensional Expressions-(MDX-)Skriptbefehls, der Währungsmeasures in Werte konvertiert, die für das Gebietsschema der Clientanwendung geeignet sind. Um dieses MDX-Skript erstellen zu können, benötigt der Business Intelligence-Assistent folgende Informationen:  
  
-   Eine Währungsdimension, die Quellwährungen darstellt. (Bei dieser Dimension handelt es sich um die Quellwährungsdimension.)  
  
-   Eine Measuregruppe, die die zu verwendenden Wechselkurse darstellt.  
  
 Anhand dieser Informationen entwirft der Business Intelligence-Assistent einen Währungsumrechnungsprozess, der die entsprechende Zielwährungsdimension (die Währungsdimension, die Zielwährungen darstellt) identifiziert. Abhängig von der Anzahl der Währungsumrechnungen, die für Ihre Business Intelligence-Lösung erforderlich sind, kann der Business Intelligence-Assistent mehrere Zielwährungsdimensionen definieren. Weitere Informationen zum Definieren von Währungsumrechnungen finden Sie unter [Währungsumrechnungen &#40;Analysis Services&#41;](../../analysis-services/currency-conversions-analysis-services.md).  
  
 Wenn Sie eine Dimension als Währungsdimension identifizieren möchten, legen Sie die **Type** -Eigenschaft der Dimension auf **Currency**fest.  
  
## <a name="dimension-structure"></a>Dimensionsstruktur  
 Eine Währungsdimension enthält zumindest ein Schlüsselattribut, das die einzelnen Währungen in der Dimensionstabelle für die Währungsdimension identifiziert. Der Wert des Schlüsselattributs ist in Quell- und Zielwährungsdimensionen unterschiedlich.  
  
-   Wenn Sie ein Attribut als Schlüsselattribut einer Quellwährungsdimension identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencySource**fest.  
  
-   Wenn Sie ein Attribut als Zielwährungsdimension identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencyDestination**fest.  
  
 Für Berichtszwecke enthalten sowohl Quell- als auch Zielwährungsdimensionen optional folgende Attribute:  
  
-   Ein Attribut für den Namen der Währung.  
  
     Wenn Sie ein Attribut als Attribut für den Namen der Währung identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencyName**fest.  
  
-   Ein Attribut für die Quelle der Währung.  
  
     Wenn Sie ein Attribut als Attribut für die Quelle der Währung identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencySource**fest.  
  
-   Einen Währungscode gemäß der International Standards Organization (ISO).  
  
     Wenn Sie ein Attribut als Attribut für den ISO-Währungscode identifizieren möchten, legen Sie die **Type** -Eigenschaft des Attributs auf **CurrencyIsoCode**fest.  
  
 Weitere Informationen zu Attributtypen finden Sie unter [Konfigurieren von Attributtypen](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="defining-account-intelligence-with-the-business-intelligence-wizard"></a>Definieren von Kontointelligenz mit dem Business Intelligence-Assistenten  
 Nachdem Sie eine Kontodimension definiert und diese Dimension einem Cube hinzugefügt haben, können Sie den Business Intelligence-Assistenten verwenden, um der Dimension die Kontointelligenzfunktionalität hinzuzufügen, beispielsweise das Identifizieren und Zuordnen von Kontotypen. Weitere Informationen finden Sie unter [Hinzufügen von Kontointelligenz zu einer Dimension](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Business Intelligence-Assistent F1-Hilfe](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Dimensionstypen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
