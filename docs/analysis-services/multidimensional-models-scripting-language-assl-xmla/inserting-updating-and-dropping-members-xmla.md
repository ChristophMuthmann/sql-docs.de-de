---
title: "Einfügen, aktualisieren und Löschen von Elementen (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb089245a47a70890bb45ed2499bdf6e852d3ef6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Einfügen, Aktualisieren und Löschen von Elementen (XMLA)
  Können Sie die [einfügen](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [aktualisieren](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), und [löschen](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) -Befehle in XML for Analysis (XMLA) bzw. einfügen, aktualisieren oder Löschen von Elementen aus einer Dimension mit aktiviertem Schreibzugriff. Weitere Informationen zu Dimensionen mit aktiviertem Schreibzugriff finden Sie unter [Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Einfügen von neuen Elementen  
 Die **einfügen** Befehl angegebenen Attribute in einer Dimension mit aktiviertem Schreibzugriff neue Elemente eingefügt.  
  
 Vor der Erstellung der **einfügen** -Befehls sollten Sie folgende Informationen verfügen, für die neuen Elemente eingefügt werden:  
  
-   Die Dimension, in die die neuen Elemente eingefügt werden sollen.  
  
-   Das Dimensionsattribut, in die die neuen Elemente eingefügt werden sollen.  
  
-   Die Namen der neuen Elemente, einschließlich alle entsprechenden Übersetzungen für den Namen.  
  
-   Die Schlüssel der neuen Elemente. Wenn ein Attribut einen zusammengesetzten Schlüssel verwendet, erfordert der Schlüssel möglicherweise mehrere Werte.  
  
-   Werte für alle entsprechenden Attributeigenschaften, die nicht als andere Attribute innerhalb der Dimension implementiert wurden. Derartige Attributeigenschaften umfassen unäre Operationen, Übersetzungen, benutzerdefinierte Rollups, benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen.  
  
 Die **einfügen** -Befehl unterstützt nur zwei Eigenschaften:  
  
-   Die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) -Eigenschaft, die einen Objektverweis für die Dimension enthält, in dem die Elemente eingefügt werden. Der Objektverweis enthält den Datenbankbezeichner, den Cubebezeichner sowie den Dimensionsbezeichner für die Dimension.  
  
-   Die [Attribute](../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md) -Eigenschaft, die einer mehreren oder [Attribut](../../analysis-services/xmla/xml-elements-properties/attribute-element-xmla.md) Elemente die Attribute zu identifizieren, in dem Elemente eingefügt werden. Jede **Attribut** -Element identifiziert ein Attribut enthält Name, Wert, Übersetzungen, unäroperator, benutzerdefinierte Rollups, Benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen für ein einzelnes Element auf dem identifizierten Attribut hinzugefügt werden.  
  
    > [!NOTE]  
    >  Alle Eigenschaften für die **Attribut** -Element müssen eingefügt werden. Andernfalls tritt möglicherweise ein Fehler auf.  
  
## <a name="updating-existing-members"></a>Aktualisieren von vorhandenen Elementen  
 Die **Update** Befehl aktualisiert vorhandene Elemente in festgelegten Attributen basierend auf Beziehungen zu anderen Elementen in anderen Attributen in einer Dimension mit aktiviertem Schreibzugriff. Die **Update** Befehl Elemente auf andere Ebenen in Hierarchien der Dimension enthalten und können verwendet werden, um die über-/ unterordnungshierarchien von übergeordneten Attributen definierte umstrukturieren verschieben.  
  
 Vor der Erstellung der **Update** -Befehls sollten Sie folgende Informationen verfügen, für die zu aktualisierenden Mitglieder über:  
  
-   Die Dimension, in der die vorhandenen Elemente aktualisiert werden sollen.  
  
-   Die Dimensionsattribute, in denen die vorhandenen Elemente aktualisiert werden sollen.  
  
-   Die Schlüssel der vorhandenen Elemente. Wenn ein Attribut einen zusammengesetzten Schlüssel verwendet, erfordert der Schlüssel möglicherweise mehrere Werte.  
  
-   Werte für alle entsprechenden Attributeigenschaften, die nicht als andere Attribute innerhalb der Dimension implementiert wurden. Derartige Attributeigenschaften umfassen unäre Operationen, Übersetzungen, benutzerdefinierte Rollups, benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen.  
  
 Die **Update** -Befehl unterstützt nur drei erforderliche Eigenschaften:  
  
-   Die **Objekt** -Eigenschaft, die einen Objektverweis für die Dimension enthält, in dem die Elemente aktualisiert werden. Der Objektverweis enthält den Datenbankbezeichner, den Cubebezeichner sowie den Dimensionsbezeichner für die Dimension.  
  
-   Die **Attribute** -Eigenschaft, die einer mehreren oder **Attribut** Elemente die Attribute zu identifizieren, in dem Elemente aktualisiert werden. Die **Attribut** -Element identifiziert ein Attribut enthält Name, Wert, Übersetzungen, unäroperator, benutzerdefinierte Rollups, Benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen für ein einzelnes Element, das für das identifizierte Attribut aktualisiert.  
  
    > [!NOTE]  
    >  Alle Eigenschaften für die **Attribut** -Element müssen eingefügt werden. Andernfalls tritt möglicherweise ein Fehler auf.  
  
-   Die [, in denen](../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md) -Eigenschaft, die einer mehreren oder **Attribut** Elemente, die die Attribute zu beschränken, in denen Elemente aktualisiert werden. Die **, in denen** Eigenschaft ist wichtig für die Beschränkung ein **Update** -Befehls auf bestimmte Instanzen eines Elements. Wenn die **, in denen** Eigenschaft nicht angegeben ist, werden alle Instanzen eines bestimmten Elements aktualisiert. Angenommen, Sie möchten den Stadtnamen für drei Kunden von Redmond zu Bellevue ändern. Um den Stadtnamen zu ändern, geben Sie einen **, in denen** Eigenschaft identifiziert die drei Elemente im Customer-Attribut für die die Elemente der City-Attribut geändert werden soll. Wenn Sie keine, dass dies ergeben **, in denen** -Eigenschaft, würde jeder Kunde, dessen Stadtname zurzeit Redmond ist. der Name der Stadt Bellevue nach haben die **Update** -Befehl ausgeführt wird.  
  
    > [!NOTE]  
    >  Davon ausgenommen sind die neuen Mitglieder der **aktualisieren** aktualisiert Befehl kann nur attributschlüsselwerte für Attribute, die nicht in der **, in dem** Klausel. Der Stadtname kann beispielsweise nicht aktualisiert werden, wenn ein Kunde aktualisiert wird, andernfalls wird der Stadtname für alle Kunden geändert.  
  
### <a name="updating-members-in-parent-attributes"></a>Aktualisieren von Elementen in übergeordneten Attributen  
 Zur Unterstützung von übergeordneten Attributen, die **Update** -Befehl die optionalen [MoveWithDescendants](../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md)sollte Eigenschaften. Festlegen der **MoveWithDescendants** Eigenschaft auf "true" gibt an, dass die Nachfolger des übergeordneten Elements auch mit dem übergeordneten Element verschoben werden soll, wenn der Bezeichner des übergeordneten Elements ändert. Wenn dieser Wert auf „False“ festgelegt wird, werden die unmittelbaren Nachfolger eines übergeordneten Elements zu der Ebene höhergestuft, auf der sich das übergeordnete Element zuvor befand, wenn dieses übergeordnete Element verschoben wird.  
  
 Beim Aktualisieren von Elementen in ein übergeordnetes Attribut, das **aktualisieren** Befehl Member in anderen Attributen kann nicht aktualisiert werden.  
  
## <a name="dropping-existing-members"></a>Löschen von vorhandenen Elementen  
 Vor der Erstellung der **löschen** -Befehls sollten Sie folgende Informationen verfügen, für die zu löschenden Mitglieder über:  
  
-   Die Dimension, in der die vorhandenen Elemente gelöscht werden sollen.  
  
-   Die Dimensionsattribute, in denen die vorhandenen Elemente gelöscht werden sollen.  
  
-   Die Schlüssel der zu löschenden vorhandenen Elemente. Wenn ein Attribut einen zusammengesetzten Schlüssel verwendet, erfordert der Schlüssel möglicherweise mehrere Werte.  
  
 Die **löschen** -Befehl unterstützt nur zwei erforderliche Eigenschaften:  
  
-   Die **Objekt** -Eigenschaft, die einen Objektverweis für die Dimension, in dem die Elemente enthält gelöscht werden sollen. Der Objektverweis enthält den Datenbankbezeichner, den Cubebezeichner sowie den Dimensionsbezeichner für die Dimension.  
  
-   Die **, in denen** -Eigenschaft, die einer mehreren oder **Attribut** Elemente, die die Attribute zu beschränken, in dem Elemente gelöscht werden soll. Die **, in denen** Eigenschaft ist wichtig für die Beschränkung ein **löschen** -Befehls auf bestimmte Instanzen eines Elements. Wenn die **, in denen** Befehl nicht angegeben wird, werden alle Instanzen eines bestimmten Elements gelöscht. Angenommen, Sie möchten in Redmond drei Kunden löschen. Um diese Kunden zu löschen, geben Sie einen **, in denen** Eigenschaft identifiziert, die die drei Elemente im Customer-Attribut, das entfernt werden und das Element "Redmond" des City-Attributs, das über das sind die drei Kunden entfernt werden soll. Wenn die **, in denen** Eigenschaft gibt nur das Element "Redmond" des City-Attributs, jeder Kunde zugeordnet würde gelöscht werden, indem die **löschen** Befehl. Wenn die **, in denen** Eigenschaft gibt nur die drei Elemente im Customer-Attribut, die drei Kunden werden vollständig über gelöscht, die **löschen** Befehl.  
  
    > [!NOTE]  
    >  Die **Attribut** Elemente in einem **löschen** Befehl darf nur die **AttributeName** und **Schlüssel** Eigenschaften. Andernfalls tritt möglicherweise ein Fehler auf.  
  
### <a name="dropping-members-in-parent-attributes"></a>Löschen von Elementen in übergeordneten Attributen  
 Festlegen der [DeleteWithDescendants](../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) Eigenschaft gibt an, dass die Nachfolger eines übergeordneten Elements mit dem übergeordneten Element ebenfalls gelöscht werden soll. Wenn dieser Wert auf „False“ festgelegt wird, werden die unmittelbaren Nachfolger eines übergeordneten Elements zu der Ebene höhergestuft, auf der sich das übergeordnete Element zuvor befand.  
  
> [!IMPORTANT]  
>  Ein Benutzer muss lediglich über Löschberechtigungen für das übergeordnete Element verfügen, um sowohl das übergeordnete Element als auch die Nachfolger zu löschen. Ein Benutzer benötigt keine Löschberechtigungen für die Nachfolger.  
  
## <a name="see-also"></a>Siehe auch  
 [Drop-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [INSERT-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Update-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Definieren und Identifizieren von Objekten &#40; XMLA &#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

