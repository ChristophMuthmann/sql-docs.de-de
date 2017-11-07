---
title: "Erstellen eines Finanzkontos des über-und untergeordneten Typs Dimension | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1f4006934f9c92e492a984b02de9e585ec8ee84b
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimensions---finance-account-of-parent-child-type"></a>Datenbankdimensionen - Finanzkontos des über-und untergeordnete Dimension
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ist eine Dimension vom Typ "Konto" eine Dimension, deren Attribute ein Kontodiagramm für Finanzberichte darstellen.  
  
 Mit einer Kontodimension können Sie selektiv das Aggregationsverhalten für Konten im Lauf der Zeit verwalten. Eine Kontodimension ermöglicht auch das Verwenden eines Standardmechanismus, mit dem die meisten der vom Standard abweichenden Aggregationsprobleme behoben werden können, die in Business Intelligence-Projektmappen für den Umgang mit Finanzdaten typischerweise auftreten. Wenn Sie bisher nicht über einen solchen Standardmechanismus verfügt haben, waren zum Beheben dieser vom Standard abweichenden Aggregationsprobleme benutzerdefinierte Rollupformeln, berechnete Elemente oder MDX-Skripts (Multidimensional Expressions) erforderlich.  
  
 Um eine Dimension als eine Kontodimension zu identifizieren, legen Sie die **Type** -Eigenschaft der Dimension auf **Accounts**fest.  
  
## <a name="dimension-structure"></a>Dimensionsstruktur  
 Eine Kontodimension enthält mindestens zwei Attribute:  
  
-   Ein Schlüsselattribut – ein Attribut, das individuelle Konten in der Dimensionstabelle für die Kontodimension identifiziert.  
  
-   Ein Kontoattribut – ein übergeordnetes Attribut, das beschreibt, wie Konten innerhalb der Kontodimension hierarchisch angeordnet sind.  
  
     Um ein Attribut als Kontoattribut zu identifizieren, legen Sie die **Type** -Eigenschaft des Attributs auf **Account** und die **Usage** -Eigenschaft auf **Parent**fest.  
  
 Kontodimensionen können optional die folgenden Attribute enthalten:  
  
-   Ein Kontotypattribut – ein Attribut, das den Kontotyp für jedes Konto in der Dimension definiert. Die Elementnamen des Kontotypattributs sind in den Kontotypen zugeordnet, die für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank oder das Projekt definiert sind, und geben die Aggregatfunktion an, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für diese Konten verwendet wird. Sie können auch unäre Operatoren oder benutzerdefinierte Rollupformeln verwenden, um das Aggregationsverhalten für Kontoattribute zu bestimmen, aber mit Kontotypen können Sie problemlos ein einheitliches Verhalten für ein Kontodiagramm durchsetzen, ohne dass dazu Änderungen an der zugrunde liegenden relationalen Datenbank erforderlich sind.  
  
     Um ein Kontotypattribut zu identifizieren, legen Sie die **Type** -Eigenschaft des Attributs auf **AccountType**fest.  
  
-   Ein Kontonamenattribut – ein Attribut, das zu Berichtszwecken verwendet wird. Um ein Kontonamenattribut zu identifizieren, legen Sie die **Type** -Eigenschaft des Attributs auf **AccountName**fest.  
  
-   Ein Kontonummernattribut – ein Attribut, das zu Berichtszwecken verwendet wird. Um ein Kontonummernattribut zu identifizieren, legen Sie die **Type** -Eigenschaft des Attributs auf **AccountNumber**fest.  
  
 Weitere Informationen zu Attributtypen finden Sie unter [Konfigurieren von Attributtypen](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Hinzufügen von Kontointelligenz mit dem Business Intelligence-Assistenten  
 Nachdem Sie eine Kontodimension definiert und diese Dimension zu einem Cube hinzugefügt haben, können Sie den Business Intelligence-Assistenten verwenden, um der Dimension Kontointelligenzfunktionalität hinzuzufügen, z. B. zum Identifizieren und Zuordnen von Kontotypen. Weitere Informationen finden Sie unter [Hinzufügen von Kontointelligenz zu einer Dimension](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Business Intelligence-Assistent F1-Hilfe](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Dimensionstypen](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  

