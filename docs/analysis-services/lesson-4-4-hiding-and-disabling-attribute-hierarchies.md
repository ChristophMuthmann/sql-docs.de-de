---
title: Ausblenden und Deaktivieren von Attributhierarchien | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 095039c2-7104-414c-a9a6-327b03ce79df
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b1ae1a57e05d8953c4bd5f93b9e247419ee986c0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-4-4---hiding-and-disabling-attribute-hierarchies"></a>Lektion 4-4-ausblenden und Deaktivieren von Attributhierarchien
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]Standardmäßig wird eine Attributhierarchie für jedes Attribut in einer Dimension erstellt, und jede Hierarchie ist für die Dimensionierung von Faktendaten verfügbar. Diese Hierarchie setzt sich aus einer Gesamtergebnisebene und einer Detailebene mit allen Elementen der Hierarchie zusammen. Ihnen ist bereits bekannt, dass Sie Attribute in benutzerdefinierten Hierarchien organisieren können, um Navigationspfade in einem Cube bereitzustellen. Unter bestimmten Umständen möchten Sie möglicherweise einige Attribute und deren Hierarchien deaktivieren oder ausblenden. Bestimmte Attribute wie Sozialversicherungs- oder Personalausweisnummer, Lohnsatz, Geburtsdatum und Anmeldeinformationen sind beispielsweise keine Attribute, mit denen Benutzer Cubeinformationen dimensionieren. Stattdessen werden diese Informationen nur als Details eines bestimmten Attributelements angezeigt. Diese Attributhierarchien können von Ihnen ausgeblendet werden, sodass die Attribute nur als Elementeigenschaften eines bestimmten Attributs angezeigt werden. Sie möchten Elemente anderer Attribute, beispielsweise Kundennamen oder Postleitzahlen, möglicherweise nur anzeigen lassen, wenn sie durch eine Benutzerhierarchie und nicht unabhängig durch eine Attributhierarchie angezeigt werden. Ein Grund dafür kann in der schieren Anzahl verschiedener Elemente in der Attributhierarchie liegen. Zur Steigerung der Verarbeitungsleistung sollten Sie schließlich Attributhierarchien deaktivieren, die nicht von Benutzern zum Durchsuchen verwendet werden.  
  
Der Wert der **AttributeHierarchyEnabled** -Eigenschaft bestimmt, ob eine Attributhierarchie erstellt wird. Wenn diese Eigenschaft auf **False**festgelegt ist, wird die Attributhierarchie nicht erstellt, und das Attribut kann nicht als Ebene in einer Benutzerhierarchie verwendet werden. Die Attributhierarchie ist nur als Elementeigenschaft vorhanden. Allerdings kann eine deaktivierte Attributhierarchie weiterhin verwendet werden, um die Elemente eines anderen Attributs zu bestellen. Wenn der Wert der **AttributeHierarchyEnabled** -Eigenschaft auf **TRUE**festgelegt ist, wird mit dem Wert der **AttributeHierarchyVisible** -Eigenschaft bestimmt, ob die Attributhierarchie angezeigt wird, unabhängig von ihrer Verwendung in einer benutzerdefinierten Hierarchie.  
  
Wenn eine Attributhierarchie aktiviert ist, möchten Sie möglicherweise Werte für die folgenden drei zusätzlichen Eigenschaften angeben:  
  
-   **IsAggregatable**  
  
    Standardmäßig ist für alle Attributhierarchien eine Gesamtergebnisebene definiert. Zum Deaktivieren der Gesamtergebnisebene für eine aktivierte Attributhierarchie legen Sie den Wert für diese Eigenschaft auf **FALSE**fest.  
  
    > [!NOTE]  
    > Ein Attribut, dessen **IsAggregatable** -Eigenschaft auf False festgelegt ist, kann nur als Stamm einer benutzerdefinierten Hierarchie verwendet werden und muss ein angegebenes Standardelement haben (andernfalls wird vom [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Modul ein Standardelement für Sie ausgewählt).  
  
-   **AttributeHierarchyOrdered**  
  
    Standardmäßig werden von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] die Elemente von aktivierten Attributhierarchien während der Verarbeitung bestellt und dann nach dem Wert der **OrderBy** -Eigenschaft gespeichert, beispielsweise nach Name oder Schlüssel. Wenn die Bestellung für Sie uninteressant ist, können Sie die Verarbeitungsleistung steigern, indem Sie den Wert dieser Eigenschaft auf **False**festlegen.  
  
-   **AttributeHierarchyOptimizedState**  
  
    Standardmäßig wird von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ein Index für jede aktivierte Attributhierarchie während der Verarbeitung erstellt, um die Abfrageleistung zu verbessern. Wenn Sie keine Attributhierarchie zum Durchsuchen verwenden möchten, können Sie die Verarbeitungsleistung steigern, indem Sie den Wert dieser Eigenschaft auf **NotOptimized**festlegen. Wenn Sie eine ausgeblendete Hierarchie als das Schlüsselattribut für die Dimension verwenden, wird durch das Erstellen der Attributelemente weiterhin die Leistung verbessert.  
  
Diese Eigenschaften werden nicht angewendet, wenn eine Attributhierarchie deaktiviert ist.  
  
Mithilfe der Aufgaben in diesem Thema werden Sie Sozialversicherungsnummern und andere Attribute in der Employee-Dimension deaktivieren, die nicht zum Durchsuchen verwendet werden. Sie werden dann die Kundennamen- und Postleitzahl-Attributhierarchien in der Customer-Dimension ausblenden. Die große Anzahl der Attributelemente in diesen Hierarchien gestaltet das Durchsuchen dieser Hierarchien unabhängig von einer Benutzerhierarchie äußerst langsam.  
  
## <a name="setting-attribute-hierarchy-properties-in-the-employee-dimension"></a>Festlegen von Attributhierarchieeigenschaften in der Employee-Dimension  
  
1.  Wechseln Sie zum Dimensions-Designer für die Employee-Dimension, und klicken Sie dann auf die Registerkarte **Browser** .  
  
2.  Überprüfen Sie, ob die folgenden Attributhierarchien in der **Hierarchie** -Liste vorhanden sind:  
  
    -   **Base Rate**  
  
    -   **Birth Date**  
  
    -   **Login ID**  
  
    -   **Manager SSN**  
  
    -   **SSN**  
  
3.  Wechseln Sie auf die Registerkarte **Dimensionsstruktur** , und wählen Sie dann die folgenden Attribute im Bereich **Attribute** aus. Um mehrere Measures auszuwählen, halten Sie beim Klicken die STRG-TASTE gedrückt:  
  
    -   **Base Rate**  
  
    -   **Birth Date**  
  
    -   **Login ID**  
  
    -   **Manager SSN**  
  
    -   **SSN**  
  
4.  Legen Sie im Eigenschaftenfenster den Wert der **AttributeHierarchyEnabled** -Eigenschaft auf **False** für die ausgewählten Attribute fest.  
  
    Beachten Sie im Bereich **Attribute** , dass sich das Symbol für jedes Attribut geändert hat, um den deaktivierten Zustand des Attributs anzuzeigen.  
  
    Die folgende Abbildung zeigt die **AttributeHierarchyEnabled** -Eigenschaft mit dem Wert False für die ausgewählten Attribute.  
  
    ![AttributeHierarchyEnabled-Eigenschaft auf "false"](../analysis-services/media/l4-hierarchyenabled-1.gif "AttributeHierarchyEnabled-Eigenschaft auf "false"")  
  
5.  Klicken Sie im Menü **Erstellen** auf **Analysis Services Tutorial bereitstellen**.  
  
6.  Wechseln Sie nach erfolgreichem Abschluss der Verarbeitung zur Registerkarte **Browser** , klicken Sie auf **Verbindung wiederherstellen**, und versuchen Sie dann, jede der geänderten Attributhierarchien anzuzeigen.  
  
    Beachten Sie, dass die Elemente der geänderten Attribute nicht zum Durchsuchen als Attributhierarchien in der Liste **Hierarchie** zur Verfügung stehen. Wenn Sie versuchen, eine der deaktivierten Attributhierarchien als Ebene in einer Benutzerhierarchie hinzuzufügen, erhalten Sie eine Fehlermeldung dahingehend, dass die Attributhierarchie aktiviert sein muss, um an einer benutzerdefinierten Hierarchie teilnehmen zu können.  
  
## <a name="setting-attribute-hierarchy-properties-in-the-customer-dimension"></a>Festlegen von Attributhierarchieeigenschaften in der Customer-Dimension  
  
1.  Wechseln Sie zum Dimensions-Designer für die Customer-Dimension, und klicken Sie dann auf die Registerkarte **Browser** .  
  
2.  Überprüfen Sie, ob die folgenden Attributhierarchien in der **Hierarchie** -Liste vorhanden sind:  
  
    -   **Full Name**  
  
    -   **Postal Code**  
  
3.  Wechseln Sie zur Registerkarte **Dimensionsstruktur** , und wählen Sie die folgenden Attribute im Bereich **Attribute** aus, indem Sie die STRG-Taste zur Auswahl mehrerer Attribute gleichzeitig verwenden:  
  
    -   **Full Name**  
  
    -   **Postal Code**  
  
4.  Legen Sie im Eigenschaftenfenster den Wert der **AttributeHierarchyVisible** -Eigenschaft auf **False** für die ausgewählten Attribute fest.  
  
    Weil die Elemente dieser Attributhierarchien für die Dimensionierung von Faktendaten verwendet werden, wird durch die Bestellung und Optimierung dieser Attributhierarchien die Leistung verbessert. Darum sollten die Eigenschaften dieser Attribute nicht geändert werden.  
  
    Im folgenden Bild wird die **AttributeHierarchyVisible** -Eigenschaft mit dem Wert False gezeigt.  
  
    ![AttributeHierarchyVisible-Eigenschaft auf "false" festgelegt](../analysis-services/media/l4-hierarchyvisible-1.gif "AttributeHierarchyVisible-Eigenschaft auf "false" festgelegt")  
  
5.  Ziehen Sie das **Postal Code** -Attribut aus dem Bereich **Attribute** in die **Customer Geography** -Benutzerhierarchie im Bereich **Hierarchien und Ebenen** direkt unter der **City** -Ebene.  
  
    Beachten Sie, dass aus einem ausgeblendeten Attribut weiterhin eine Ebene in einer Benutzerhierarchie werden kann.  
  
6.  Klicken Sie im Menü **Erstellen** auf **Analysis Services Tutorial bereitstellen**.  
  
7.  Wechseln Sie nach erfolgreichem Abschluss der Bereitstellung zur Registerkarte **Browser** für die Customer-Dimension, und klicken Sie dann auf **Verbindung wiederherstellen**.  
  
8.  Versuchen Sie, eine der beiden geänderten Attributhierarchien aus der Liste **Hierarchie** auszuwählen.  
  
    Beachten Sie, dass keine der geänderten Attributhierarchien in der **Hierarchie** -Liste angezeigt wird.  
  
9. Wählen Sie in der **Hierarchie** -Liste die Option **Customer Geography**aus, und durchsuchen Sie dann jede Ebene im Browserbereich.  
  
    Beachten Sie, dass die ausgeblendeten Ebenen **Postal Code** und **Full Name**in der benutzerdefinierten Hierarchie sichtbar sind.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Sortieren von Attributelementen basierend auf einem sekundären Attribut](../analysis-services/lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md)  
  
  
  
