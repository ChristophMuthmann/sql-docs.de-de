---
title: Gruppieren von Attributelementen (Diskretisierung) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3cc6f6f1bf2acacc481eb9141bb3dd055cc56113
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="attribute-properties---group-attribute-members"></a>Attributeigenschaften - Gruppieren von Attributelementen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Eine Elementgruppe ist eine vom System generierte Auflistung von aufeinander folgenden Dimensionselementen. In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]können die Elemente eines Attributs in eine Anzahl von Elementgruppen mithilfe des so genannten Diskretisierungsprozesses gruppiert werden. In der Ebene einer Hierarchie sind entweder nur Elementgruppen oder nur Elemente enthalten. Wenn geschäftliche Benutzer eine Ebene durchsuchen, die Elementgruppen enthält, werden die Namen und Zellwerte der Elementgruppen angezeigt. Die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zur Unterstützung von Elementgruppen generierten Elemente werden als Gruppierungselemente bezeichnet und ähneln gewöhnlichen Elementen.  
  
 Die **DiscretizationMethod** -Eigenschaft eines Attributs steuert die Gruppierung der Elemente.  
  
|**DiscretizationMethod** -Einstellung|Description|  
|--------------------------------------|-----------------|  
|**InclusionThresholdSetting**|Zeigt die Elemente an.|  
|**Automatisch**|Wählt die Methode aus, welche die Daten besser darstellt: entweder die **EqualAreas** - oder **Clusters** -Methode.|  
|**EqualAreas**|Versucht, die Elemente des Attributs in Gruppen mit der gleichen Anzahl von Elementen zu unterteilen.|  
|**Clusters**|Versucht, die Elemente des Attributs in Gruppen zu unterteilen, wobei Stichproben der Trainingsdaten entnommen werden, diese als Initialisierungswerte einer Reihe von zufällig gewählten Punkten verwendet werden und mehrere Iterationen des Clusteringalgorithmus anhand der EM-Clusteringmethode (Expectation Maximization) ausgeführt werden.<br /><br /> Diese Methode ist nützlich, weil sie für jede Verteilungskurve verwendet werden kann. Sie ist jedoch aufwändiger, da sie mehr Verarbeitungszeit beansprucht.|  
  
 Die **DiscretizationNumber** -Eigenschaft von Attributen gibt die Anzahl von anzuzeigenden Gruppen an. Wenn die Eigenschaft auf den Standardwert 0 festgelegt ist, wird in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] die Anzahl von Gruppen bestimmt, indem abhängig von der **DiscretizationMethod** -Einstellung Stichproben der Daten entnommen oder die Daten gelesen werden.  
  
 Die Sortierreihenfolge der Elemente in den Elementgruppen wird mithilfe der **OrderBy** -Eigenschaft des Attributs gesteuert. Die Elemente einer Elementgruppe werden auf Basis dieser Sortierreihenfolge fortlaufend sortiert.  
  
 Mit Elementgruppen wird üblicherweise ein Drilldown von einer Ebene mit wenigen Elementen zu einer Ebene mit mehreren Elementen durchgeführt. Damit die Benutzer einen Drilldown zwischen Ebenen durchführen können, ändern Sie die **DiscretizationMethod** -Eigenschaft des Attributs für die Ebene, die zahlreiche Elemente enthält, von **None** in eine der in der vorigen Tabelle beschriebenen Diskretisierungsmethoden. Beispielsweise enthält eine Client-Dimension eine Client Name-Attributhierarchie mit 500.000 Elementen. Sie können dieses Attribut in Client Groups umbenennen und die **DiscretizationMethod** -Eigenschaft auf **Automatic** festlegen, um die Elementgruppen auf der Elementebene der Attributhierarchie anzuzeigen.  
  
 Sie können eine weitere Hierarchie für das Client Name-Attribut mit Bindung an dieselbe Tabellenspalte erstellen, um einen Drilldown auf einzelne Clients der jeweiligen Gruppe durchzuführen. Erstellen Sie dann eine neue Benutzerhierarchie auf Basis der beiden Attribute. Die oberste Ebene basiert dann auf dem Client Groups-Attribut, und die untere Ebene basiert auf dem Client Name-Attribut. Die **IsAggregatable** -Eigenschaft hat für beide Attribute den Wert **True** . Somit kann der Benutzer in der Hierarchie die (Alle)-Ebene zum Anzeigen der Gruppenelemente erweitern bzw. die Gruppenelemente zum Anzeigen der Blattelemente der Hierarchie. Sie haben die Möglichkeit, die **AttributeHierarchyVisible** -Eigenschaft im entsprechenden Attribut auf **False** festzulegen, um die Gruppen- bzw. Clientebene auszublenden.  
  
## <a name="naming-template"></a>Benennungsvorlage  
 Die Namen von Elementgruppen werden beim Erstellen der Elementgruppen automatisch generiert. Dabei wird die standardmäßige Benennungsvorlage verwendet, es sei denn, Sie geben eine andere Benennungsvorlage an. Sie können diese Benennungsmethode ändern, indem Sie eine Benennungsvorlage in der **Format** -Option für die **NameColumn** -Eigenschaft eines Attributs angeben. Verschiedene Benennungsvorlagen können für jede Sprache neu definiert werden, die in der **Translations** -Auflistung der Spaltenbindung für die **NameColumn** -Eigenschaft des Attributs angegeben wird.  
  
 Zum Definieren der Benennungsvorlage wird in der **Format** -Einstellung der folgende Zeichenfolgenausdruck verwendet:  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate defintion> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 Der `<First definition>` -Parameter wird nur auf die erste bzw. auf die einzige von der Diskretisierungsmethode generierte Elementgruppe angewendet. Wenn die optionalen `<Intermediate definition>` - und `<Last definition>` -Parameter nicht bereitgestellt werden, wird der `<First definition>` -Parameter für alle für dieses Attribut generierten Measuregruppen verwendet.  
  
 Der `<Last definition>` -Parameter wird nur auf die letzte von der Diskretisierungsmethode generierte Elementgruppe angewendet.  
  
 Der `<Intermediate bucket name>` -Parameter wird auf alle von der Diskretisierungsmethode generierten Elementgruppen angewendet. Ausgeschlossen sind hiervon die erste und die letzte Elementgruppe. Dieser Parameter wird ignoriert, wenn nur zwei oder weniger Elementgruppen generiert werden.  
  
 Der `<Bucket name>` -Parameter ist ein Zeichenfolgenausdruck, in dem Variablen zum Darstellen von Element- oder Elementgruppeninformationen als Teil des Elementgruppennamens enthalten sein können:  
  
|Variable|Description|  
|--------------|-----------------|  
|%{First bucket member}|Der Elementname des ersten, in der aktuellen Elementgruppe einzuschließenden Elements.|  
|%{Last bucket member}|Der Elementname des letzten, in der aktuellen Elementgruppe einzuschließenden Elements.|  
|%{Previous bucket last member}|Der Elementname des letzten, der vorigen Elementgruppe zugewiesenen Elements.|  
|%{Next bucket first member}|Der Elementname des ersten, der nächsten Elementgruppe zuzuweisenden Elements.|  
|%{Bucket Min}|Der Minimalwert der der aktuellen Elementgruppe zuzuweisenden Elemente.|  
|%{Bucket Max}|Der Maximalwert der der aktuellen Elementgruppe zuzuweisenden Elemente.|  
|%{Previous Bucket Max}|Der Maximalwert der der vorigen Elementgruppe zuzuweisenden Elemente.|  
|%{Next Bucket Min}|Der Minimalwert der der nächsten Elementgruppe zuzuweisenden Elemente.|  
  
 Die standardmäßige Benennungsvorlage lautet `"%{First bucket member} - %{Last bucket member}"`, damit die Kompatibilität mit früheren Versionen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]sichergestellt ist.  
  
> [!NOTE]  
>  Um ein Semikolon (;) als Literalzeichen in die Benennungsvorlage einzuschließen, müssen Sie ein Prozentzeichen (%) als Präfix verwenden.  
  
### <a name="example"></a>Beispiel  
 Der folgende Zeichenfolgenausdruck kann beispielsweise verwendet werden, um das Yearly Income-Attribut der Customer-Dimension in der [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] -Beispieldatenbank [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zu klassifizieren, bei der für das Yearly Income-Attribut die folgende Elementgruppierung verwendet wird:  
  
 "Less than %{Next Bucket Min};Between %{First bucket member} and %{Last bucket member};Greater than %{Previous Bucket Max}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>Hinzufügen neuer Elemente in vorhandene Elementgruppen  
 Wenn Sie der Dimension neue Elemente hinzufügen, werden diese den entsprechenden Elementgruppen zugewiesen, indem der Wert des Elements mit dem aktuellen Elementgruppenlayout verglichen wird.  
  
 Wenn ein Element zwischen dem letzten Element der vorigen Elementgruppe und dem ersten Element der nächsten Elementgruppe eingefügt wird, wird das neue Element das letzte Element der vorigen Elementgruppe.  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>Aktualisieren einer Dimension mit diskretisierten Attributen  
 Beim Verarbeiten einer Dimension wird ein diskretisiertes Attribut nur bei einem vollständigen Update (ProcessFull) neu diskretisiert. Wenn ein Attribut neu diskretisiert werden soll, müssen Sie die Dimension vollständig aktualisieren. Wird die Dimensionstabelle eines diskretisierten Attributs aktualisiert, und Sie verarbeiten die Dimension im Rahmen eines inkrementellen Updates (ProcessAdd), wird das diskretisierte Attribut nicht neu diskretisiert. Die Namen und untergeordneten Elemente der neuen Buckets bleiben gleich. Weitere Informationen zur Verarbeitung von Dimensionen finden Sie unter [Verarbeiten von Analysis Services-Objekten](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md).  
  
## <a name="usage-limitations"></a>Nutzungseinschränkungen  
  
-   Elementgruppen können nicht in der obersten bzw. nicht in der untersten Ebene einer Hierarchie erstellt werden. Wenn dies notwendig wird, können Sie eine Ebene hinzufügen, sodass die Ebene, in der Sie Elementgruppen erstellen möchten, nicht länger die oberste oder unterste Ebene ist. Sie können die hinzugefügte Ebene ausblenden, indem Sie den Wert der **Visible** -Eigenschaft auf **False**festlegen.  
  
-   Elementgruppen können zwischen zwei aufeinander folgenden Ebenen einer Hierarchie erstellt werden.  
  
-   Elementgruppen werden für Dimensionen, die den ROLAP-Speichermodus verwenden, nicht unterstützt.  
  
-   Wenn die Dimensionstabelle einer Dimension, die Elementgruppen enthält, aktualisiert wird, und die Dimension wird anschließend vollständig verarbeitet, wird eine neue Elementgruppenmenge generiert. Die Namen und untergeordneten Komponenten der neuen Elementgruppen können sich von alten Elementgruppen unterscheiden.  
  
## <a name="see-also"></a>Siehe auch  
 [Attribute und Attributhierarchien](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
