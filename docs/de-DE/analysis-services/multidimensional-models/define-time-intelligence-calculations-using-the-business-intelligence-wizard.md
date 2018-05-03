---
title: Definieren von Zeitintelligenzberechnungen mithilfe des Business Intelligence-Assistenten | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 74fa3f0001979da21b22e056e03711bd6037f9a8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="define-time-intelligence-calculations-using-the-business-intelligence-wizard"></a>Definieren von Zeitintelligenzberechnungen mithilfe des Business Intelligence-Assistenten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Bei der Zeitintelligenz handelt es sich um eine Cubeerweiterung, durch die der ausgewählten Hierarchie Zeitberechnungen (oder Zeitsichten) hinzugefügt werden. Diese Erweiterung unterstützt die folgenden Berechnungskategorien:  
  
-   Zeitraum bis Datum.  
  
-   Zeitraumbasiertes Wachstum.  
  
-   Gleitender Durchschnitt.  
  
-   Vergleiche paralleler Zeiträume.  
  
 Zeitintelligenz kann auf Cubes angewendet werden, die über eine Zeitdimension verfügen. (Eine Zeitdimension ist eine Dimension, deren **Type** -Eigenschaft auf **Time**festgelegt ist.) Darüber hinaus müssen die Zeitattribute dieser Dimension auch die entsprechende Einstellung (z.B. Jahre oder Monate) für ihre **Type** -Eigenschaft aufweisen. Die **Type** -Eigenschaft sowohl der Dimension als auch ihrer Attribute wird richtig festgelegt, wenn Sie den Dimensions-Assistenten zum Erstellen der Zeitdimension verwenden.  
  
 Zum Hinzufügen von Zeitintelligenz zu einem Cube verwenden Sie den Business Intelligence-Assistenten, und wählen Sie auf der Seite **Erweiterung auswählen** die Option **Zeitintelligenz definieren** aus. Dieser Assistent führt Sie durch die Schritte zum Auswählen einer Hierarchie, der Sie Zeitintelligenz hinzufügen, sowie zum Angeben der Mitglieder in der Hierarchie, auf die Zeitintelligenz angewendet werden soll. Auf der letzten Seite des Assistenten werden die Änderungen an der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank angezeigt, die durch das Hinzufügen der ausgewählten Zeitintelligenz vorgenommen werden.  
  
## <a name="selecting-a-time-hierarchy"></a>Auswählen einer Zeithierarchie  
 Wählen Sie auf der Seite **Zielhierarchie und Berechnungen auswählen** die Zeithierarchie aus, auf die sich die Zeiterweiterung beziehen soll. Die Zeiterweiterung kann je Ausführung des Business Intelligence-Assistenten nur einmal auf eine einzelne Zeithierarchie angewendet werden. Soll die Erweiterung auf mehrere Zeithierarchien angewendet werden, müssen Sie den Assistenten erneut ausführen.  
  
 Nach dem Auswählen einer Zeithierarchie wählen Sie in der Liste **Verfügbare Zeitberechnungen** die Berechnungen aus, die sich auf die Hierarchie beziehen. Die Berechnungen, die aufgelistet werden, sind abhängig von den Hierarchieebenen und von der **Type** -Eigenschaftseinstellung des Attributs jeder Ebene. So unterstützt beispielsweise eine Jahre-Hierarchie die Optionen Jahr-bis-heute und Wachstum im Vergleich zum Vorjahr, nicht jedoch eine Quartale-Hierarchie.  
  
> [!NOTE]  
>  Die Vorlagendatei Timeintelligence.xml definiert die Zeitberechnungen, die in **Verfügbare Zeitberechnungen**aufgelistet sind. Erfüllen die aufgelisteten Berechnungen Ihre Anforderungen nicht, können Sie die vorhandenen Berechnungen entweder ändern oder der Datei Timeintelligence.xml neue Berechnungen hinzufügen.  
  
> [!TIP]  
>  Zum Anzeigen der Beschreibung einer Berechnung markieren Sie die Berechnung mithilfe der Pfeile nach oben und nach unten.  
  
## <a name="apply-time-views-to-members"></a>Anwenden von Zeitsichten auf Elemente  
 Auf der Seite **Umfang der Berechnungen definieren** geben Sie die Elemente an, auf die die neuen Zeitsichten angewendet werden. Sie können die neuen Zeitsichten auf eines der folgenden Objekte anwenden:  
  
-   **Elemente einer Kontodimension** Kontodimensionen sind auf der Seite **Umfang der Berechnungen definieren** in der Liste **Verfügbare Measures** enthalten. Die **Type** -Eigenschaften von Kontodimensionen sind auf **Accounts**festgelegt. Wird eine Kontodimension nicht in der Liste **Verfügbare Measures** angezeigt, können Sie die Kontointelligenz mithilfe des Business Intelligence-Assistenten auf diese Dimension anwenden. Weitere Informationen finden Sie unter [Hinzufügen von Kontointelligenz zu einer Dimension](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
-   **Measures** Anstatt eine Kontodimension anzugeben, können Sie die Measures angeben, auf die die Zeitsichten angewendet werden sollen. Wählen Sie in diesem Fall die Sichten aus, auf die bestimmte Zeitberechnungen angewendet werden sollen. So sind beispielsweise Gesamtkapital und Passiva Daten, die auf Jahr-bis-heute basieren, und deshalb wird eine Jahr-bis-heute-Berechnung nicht auf solche Measures angewendet.  
  
## <a name="viewing-the-time-intelligence-enhancement"></a>Anzeigen der Zeitintelligenzerweiterung  
 Auf der letzten Seite des Business Intelligence-Assistenten können Sie die Änderungen anzeigen, die an der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank vorgenommen werden. Bei einer Zeitintelligenzerweiterung ändert der Assistent die ausgewählte Zeitdimension, die zugehörige Datenquellensicht und den zugehörigen Cube gemäß der Beschreibung in der folgenden Tabelle.  
  
|Objekt|Ändern|  
|------------|------------|  
|Zeitdimension|Fügt ein Attribut für jede Berechnung (oder Sicht) hinzu.|  
|Datenquellensicht|Fügt eine berechnete Spalte in der Zeittabelle für jedes neue Attribut in der Zeitdimension hinzu.|  
|Cube|Fügt ein berechnetes Element hinzu, das den MDX-Code (Multidimensional Expressions) für die Berechnung definiert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von berechneten Elementen](../../analysis-services/multidimensional-models/create-calculated-members.md)  
  
  
