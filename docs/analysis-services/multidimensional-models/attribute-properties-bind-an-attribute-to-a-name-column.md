---
title: Binden eines Attribut an eine Namensspalte | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8507545714c24e62be80f58546308f2b9e89fab7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---bind-an-attribute-to-a-name-column"></a>Attributeigenschaften: Binden eines Attribut an eine Namensspalte
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In diesem Verfahren wird beschrieben, wie Sie ein Attribut manuell an eine Namensspalte binden, indem Sie den Bereich **Attribute** im Dimensions-Designer und das Dialogfeld **Objektbindung** verwenden.  
  
### <a name="to-bind-an-attribute-to-a-name-column"></a>So binden Sie ein Attribut an eine Namensspalte  
  
1.  Öffnen Sie im Dimensions-Designer die Dimension, in der Sie das Attribut erstellen möchten.  
  
2.  Klicken Sie im Bereich **Attribute** auf der Registerkarte **Dimensionsstruktur** mit der rechten Maustaste auf das Attribut, das Sie konfigurieren möchten, und klicken Sie anschließend auf **Eigenschaften**.  
  
3.  Suchen Sie im Fenster **Eigenschaften** die **NameColumn** -Eigenschaft, und wählen Sie anschließend **(Neu)** aus.  
  
4.  Wählen Sie im Dialogfeld **Objektbindung** für **Bindungstyp**die Option **Spaltenbindung**aus.  
  
5.  Wählen Sie in der Liste **Quellspalte** die Spalte aus, an die das Attribut gebunden wird, und klicken Sie dann auf **OK**.  
  
  
