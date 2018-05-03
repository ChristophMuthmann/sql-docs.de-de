---
title: Definieren von benutzerdefinierten Elementformeln | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8c1654b15b79871e4e45c583f6c068e05490d288
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---define-custom-member-formulas"></a>Attributeigenschaften: Definieren von benutzerdefinierten Elementformeln
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Sie können einen MDX-Ausdruck (Multidimensional Expressions), eine so genannte benutzerdefinierte Elementformel, erstellen, um die Werte für die Mitglieder eines angegebenen Attributs bereitzustellen. Eine Spalte in einer Tabelle einer Datenquellensicht stellt für jedes Mitglied in einem Attribut den Ausdruck bereit, der zur Bereitstellung des Wertes für dieses Element verwendet wird.  
  
 Benutzerdefinierte Elementformeln bestimmen die Zellwerte, die mit Elementen verknüpft sind, und überschreiben die Aggregatfunktionen von Measures. Benutzerdefinierte Elementformeln sind in MDX geschrieben. Jede benutzerdefinierte Elementformel gilt für ein einziges Element. Benutzerdefinierte Elementformeln werden in der Dimensionstabelle oder in einer anderen Tabelle gespeichert, für die eine Fremdschlüsselbeziehung mit der Dimensionstabelle besteht.  
  
 Die **CustomRollupColumn** -Eigenschaft für ein Attribut gibt die Spalte an, in der die benutzerdefinierten Elementformeln für Elemente des Attributs enthalten sind. Ist eine Zeile in der Spalte leer, wird der Zellwert für das Element normal zurückgegeben. Ist die Formel in der Spalte nicht gültig, gibt es einen Laufzeitfehler, sobald ein Zellwert abgerufen wird, der das Element verwendet.  
  
 Vor dem Angeben benutzerdefinierter Elementformeln für ein Attribut sollten Sie sicherstellen, dass die Dimensionstabelle, die das Attribut enthält, bzw. eine direkt verknüpfte Tabelle über eine Zeichenfolgenspalte zum Speichern der benutzerdefinierten Elementformeln verfügt. Wenn dies der Fall ist, können Sie entweder die **CustomRollupColumn** -Eigenschaft für ein Attribut manuell festlegen oder die Erweiterung für das Festlegen benutzerdefinierter Elementformeln des Business Intelligence-Assistenten verwenden, um eine benutzerdefinierte Elementformel für ein Attribut zu aktivieren. Weitere Informationen zum Verwenden dieser Erweiterung finden Sie unter [Festlegen benutzerdefinierter Elementformeln für Attribute in einer Dimension](../../analysis-services/multidimensional-models/bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md).  
  
## <a name="evaluating-custom-member-formulas"></a>Auswerten von benutzerdefinierten Elementformeln  
 Benutzerdefinierte Elementformeln unterscheiden sich von berechneten Elementen. Benutzerdefinierte Elementformeln gelten für Elemente in Dimensionstabellen und stellen lediglich den Wert des Elements bereit. Berechnete Elemente hingegen werden nicht in Dimensionstabellen gespeichert, und berechnete Elementausdrücke definieren sowohl Daten als auch Metadaten für zusätzliche Elemente in einer Dimension oder Hierarchie.  
  
 Benutzerdefinierte Elementformeln überschreiben die zu Measures gehörenden Aggregationsfunktionen. Bevor beispielsweise eine benutzerdefinierte Elementformel angegeben wird, weist ein Measure bei Verwendung der **Sum** -Aggregationsfunktion die folgenden Werte für die Elemente der Time-Dimension auf:  
  
-   2003: 2100  
  
    -   Quartal 1: 700  
  
    -   Quartal 2: 500  
  
    -   Quartal 3: 100  
  
    -   Quartal 4: 800  
  
-   2004: 1500  
  
    -   Quartal 1: 600  
  
    -   Quartal 2: 200  
  
    -   Quartal 3: 300  
  
    -   Quartal 4: 400  
  
 Bei einer benutzerdefinierten Elementformel wird der Wert des Elements stattdessen von der benutzerdefinierten Rollupformel bereitgestellt. Die folgende benutzerdefinierte Elementformel kann z. B. verwendet werden, um den Wert 450 für das untergeordnete Quarter 4-Element des 2004-Elements in der Time-Dimension anzugeben.  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 Benutzerdefinierte Elementformeln werden in einer Spalte der Dimensionstabelle gespeichert. Benutzerdefinierte Rollupformeln werden durch Festlegen der **CustomRollupColumn** -Eigenschaft für ein Attribut aktiviert.  
  
 Um einen einzelnen MDX-Ausdruck auf alle Elemente eines Attributs anzuwenden, erstellen Sie eine benannte Berechnung für die Dimensionstabelle, die einen MDX-Ausdruck als Literalzeichenfolge zurückgibt. Legen Sie dann die benannte Berechnung mit der **CustomRollupColumn** -Eigenschaftseinstellung für das Attribut fest, das Sie konfigurieren wollen. Eine benannte Berechnung ist eine Spalte in einer Tabelle für die Datenquellensicht, die durch einen SQL-Ausdruck definierte Zeilenwerte zurückgibt. Weitere Informationen zum Erstellen von benannten Berechnungen finden Sie unter [Definieren von benannten Berechnungen in einer Datenquellensicht &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
> [!NOTE]  
>  Um einen MDX-Ausdruck auf Elemente einer bestimmten Ebene und nicht basierend auf einem bestimmten Attribut auf Elemente aller Ebenen anzuwenden, können Sie den Ausdruck als MDX-Skript für die Ebene definieren. Weitere Informationen finden Sie unter [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
 Wenn Sie berechnete Elemente und benutzerdefinierte Rollupformeln für Mitglieder eines Attributs verwenden, sollten Sie die Reihenfolge der Auswertung berücksichtigen. Berechnete Elemente werden vor benutzerdefinierten Rollupformeln aufgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Festlegen Sie benutzerdefinierter Elementformeln für Attribute in einer Dimension](../../analysis-services/multidimensional-models/bi-wizard-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  
