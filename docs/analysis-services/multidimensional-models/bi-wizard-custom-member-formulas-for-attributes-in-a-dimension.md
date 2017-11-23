---
title: "Festlegen benutzerdefinierter Elementformeln für Attribute in einer Dimension | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f6cd6ca41dab2aa9d213281de94882c03f50db2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
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
  
  
