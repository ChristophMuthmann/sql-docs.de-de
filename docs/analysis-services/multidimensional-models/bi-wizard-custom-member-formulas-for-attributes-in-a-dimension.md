---
title: "Festlegen benutzerdefinierter Elementformeln für Attribute in einer Dimension | Microsoft Docs"
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
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], custom member formulas
- member formulas [Analysis Services]
- dimensions [Analysis Services], Business Intelligence enhancements
- custom member formulas [Analysis Services]
- CustomRollupColumn property
ms.assetid: c4467b08-ce59-4de7-a2d9-c22e246bdd52
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e9f2afe453c4321ec9767a3cb8a97215d55c877
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="bi-wizard---custom-member-formulas-for-attributes-in-a-dimension"></a>BI-Assistent – benutzerdefinierte Elementformeln für Attribute in einer Dimension
  Fügen Sie einem Cube oder einer Dimension eine Erweiterung für benutzerdefinierte Elementformeln hinzu, um die Standardaggregation, die einem Dimensionselement zugeordnet ist, durch die Ergebnisse eines MDX-Ausdrucks (Multidimensional Expressions) zu ersetzen. (Durch diese Erweiterung wird die **CustomRollupColumn** -Eigenschaft für ein angegebenes Attribut in einer Dimension festgelegt.)  
  
> [!NOTE]  
>  Benutzerdefinierte Formeln stehen nur für Dimensionen zur Verfügung, die auf bestehenden Datenquellen basieren. Bei Dimensionen, die ohne Datenquelle erstellt wurden, müssen Sie den Schemagenerierungs-Assistenten ausführen, um eine Datenquellensicht vor dem Hinzufügen einer benutzerdefinierten Elementformel zu erstellen.  
  
 Verwenden Sie zum Hinzufügen einer benutzerdefinierten Elementformel den Business Intelligence-Assistenten, und wählen Sie auf der Seite **Erweiterung auswählen** die Option **Benutzerdefinierte Elementformel erstellen** aus. Der Assistent führt Sie durch die Schritte zum Auswählen einer Dimension, auf die eine benutzerdefinierte Elementformel angewendet werden soll, sowie zum Aktivieren der Formel.  
  
## <a name="selecting-a-dimension"></a>Auswählen einer Dimension  
 Auf der ersten Seite des Assistenten unter **Benutzerdefinierte Elementformel erstellen** geben Sie die Dimension an, auf die eine benutzerdefinierte Elementformel angewendet werden soll. Durch Anwenden der benutzerdefinierten Elementformel auf die ausgewählte Dimension werden Änderungen an der Dimension vorgenommen. Diese Änderungen werden an alle Cubes vererbt, die die ausgewählte Dimension enthalten.  
  
## <a name="enabling-a-custom-member-formula"></a>Aktivieren einer benutzerdefinierten Elementformel  
 Auf der zweiten Seite unter **Benutzerdefinierte Elementformel erstellen** ordnen Sie die Quellspalte, die die benutzerdefinierte Elementformel enthält, einem oder mehreren Attributen in der Dimension zu. Aktivieren Sie in der **Attribut** -Spalte das Kontrollkästchen neben dem Attribut, das der Spalte mit der benutzerdefinierten Elementformel zugeordnet werden soll. Nach dem Auswählen der einzelnen Attribute zeigt der Assistent das Dialogfeld **Spalte auswählen** an. Klicken Sie in diesem Dialogfeld auf die Spalte in der Dimensionstabelle, die die Formel enthält. Wenn Sie eine Auswahl nach dem Schließen des Dialogfelds **Spalte auswählen** ändern möchten, klicken Sie auf die zu ändernde **Quellspaltenzelle** , und klicken Sie dann auf die Auslassungspunkte (**...**), um das Dialogfeld **Spalte auswählen** erneut zu öffnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des Business Intelligence-Assistenten zum Erweitern von Dimensionen](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
  
  
