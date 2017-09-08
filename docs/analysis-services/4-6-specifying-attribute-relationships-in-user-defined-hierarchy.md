---
title: 4-6-angeben von Attributbeziehungen in eine benutzerdefinierte Hierarchie | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d68e4caadf4e19582fb5ccd767535baee1001762
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="4-6-specifying-attribute-relationships-in-user-defined-hierarchy"></a>4-6-angeben von Attributbeziehungen in eine benutzerdefinierte Hierarchie
Wie Sie bereits in diesem Lernprogramm erfahren haben, können Sie Attributhierarchien in Ebenen innerhalb von Benutzerhierarchien organisieren, um Navigationspfade für Benutzer in einem Cube zur Verfügung zu stellen. Eine Benutzerhierarchie kann eine natürliche Hierarchie wie beispielsweise Ort, Land/Region und Staat repräsentieren oder nur einen Navigationspfad wie beispielsweise Angestelltenname, Titel und Abteilungsname. Für den Benutzer, der in einer Hierarchie navigiert, stellen sich diese beiden Hierarchietypen gleich dar.  
  
Wenn Sie Attributbeziehungen zwischen den Attributen definieren, die die Ebenen bilden, kann von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] mithilfe einer natürlichen Hierarchie eine Aggregation von einem Attribut verwendet werden, um die Ergebnisse von einem verknüpften Attribut zu erhalten. Wenn keine Beziehungen zwischen Attributen definiert sind, werden von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] alle Nicht-Schlüssel-Attribute vom Schlüsselattribut aggregiert. Sofern die zugrunde liegenden Daten dies unterstützen, sollten Sie daher auch Attributbeziehungen zwischen Attributen definieren. Durch Definieren von Attributbeziehungen wird die Dimensions-, Partitions- und Abfrageverarbeitung verbessert. Weitere Informationen finden Sie unter [Definieren von Attributbeziehungen](../analysis-services/multidimensional-models/attribute-relationships-define.md) und [Attributbeziehungen](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
Wenn Sie Attributbeziehungen definieren, können Sie angeben, ob die Beziehung flexibel oder fest ist. Wenn Sie eine Beziehung als fest definieren, werden von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Aggregationen beim Aktualisieren der Dimension beibehalten. Wenn sich eine als fest definierte Beziehung tatsächlich ändert, wird von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ein Fehler während der Verarbeitung generiert, außer wenn die Dimension vollständig verarbeitet wurde. Durch das Angeben der entsprechenden Beziehungen und Beziehungseigenschaften wird die Abfrage- und Verarbeitungsleistung erhöht. Weitere Informationen finden Sie unter [Definieren von Attributbeziehungen](../analysis-services/multidimensional-models/attribute-relationships-define.md)und [Eigenschaften der Benutzerhierarchie](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md).  
  
In den Aufgaben in diesem Thema definieren Sie Attributbeziehungen für die Attribute in den natürlichen Benutzerhierarchien im [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial-Projekt. Dazu gehören die Hierarchie **Customer Geography** in der **Customer**-Dimension, die Hierarchie **Sales Territory** in der Dimension **Vertriebsgebiet** , die Hierarchie **Product Model Lines** in der **Product** -Dimension und die Hierarchien **Fiscal Date** und **Calendar Date** in der **Date** -Dimension. Diese Benutzerhierarchien sind alle natürliche Hierarchien.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Definieren von Attributbeziehungen für Attribute in der Customer Geography-Hierarchie  
  
1.  Wechseln Sie zum Dimensions-Designer für die Customer-Dimension, und klicken Sie anschließend auf die Registerkarte **Dimensionsstruktur** .  
  
    Beachten Sie im Bereich **Hierarchien** die Ebenen in der benutzerdefinierten Hierarchie **Customer Geography** . Diese Hierarchie ist zurzeit nur ein Drilldownpfad für Benutzer, da keine Beziehungen zwischen Ebenen oder Attributen definiert wurden.  
  
2.  Klicken Sie auf die Registerkarte **Attributbeziehungen** .  
  
    Beachten Sie die vier Attributbeziehungen, die die Nichtschlüsselattribute aus der **Geography** -Tabelle mit dem Schlüsselattribut aus der **Geography** -Tabelle verknüpfen. Das **Geography** -Attribut ist mit dem **Full Name** -Attribut verknüpft. Das **Postal Code** -Attribut ist über das **Geography** -Attribut indirekt mit dem **Full Name** -Attribut verknüpft, da das **Postal Code** -Attribut mit dem **Geography** -Attribut und das **Geography** -Attribut mit dem **Full Name** -Attribut verknüpft ist. Danach werden die Attributbeziehungen geändert, damit sie das **Geography** -Attribut nicht verwenden.  
  
3.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Full Name** -Attribut, und wählen Sie anschließend **Neue Attributbeziehung**aus.  
  
4.  Im Dialogfeld **Attributbeziehung erstellen** ist das **Quellattribut** **Full Name**. Legen Sie den Wert für **Verknüpftes Attribut** auf **Postal Code**fest. Belassen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Flexibel** , da sich Beziehungen zwischen den Elementen im Laufe der Zeit ändern können.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Ein Warnsymbol wird im Diagramm angezeigt, da die Beziehung redundant ist. Die Beziehung **Full Name**  ->  **Geography** ->  **Postal Code** war bereits vorhanden, und Sie haben nur die Beziehung **Full Name**  ->  **Postal Code** erstellt. Die Beziehung **Geography** ->  **Postal Code** ist jetzt redundant. Daher wird sie entfernt.  
  
6.  Klicken Sie im Bereich **Attributbeziehungen** mit der rechten Maustaste auf **Geography** ->  **Postal Code**, und klicken Sie anschließend auf **Löschen**.  
  
7.  Das Dialogfeld **Objekte löschen** wird geöffnet. Klicken Sie auf **OK**.  
  
8.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Postal Code** -Attribut, und wählen Sie anschließend **Neue Attributbeziehung**.  
  
9. Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Postal Code**. Legen Sie den Wert **Verknüpftes Attribut** auf **City**fest. Belassen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Flexibel**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Die Beziehung **Geography** ->  **City** ist jetzt redundant. Daher wird sie entfernt.  
  
11. Klicken Sie im Bereich „Attributbeziehungen“ mit der rechten Maustaste auf **Geography** ->  **City**, und klicken Sie anschließend auf **Löschen**.  
  
12. Das Dialogfeld **Objekte löschen** wird geöffnet. Klicken Sie auf **OK**.  
  
13. Klicken Sie im Diagramm mit der rechten Maustaste auf das **City** -Attribut, und wählen Sie anschließend **Neue Attributbeziehung**aus.  
  
14. Im Dialogfeld **Attributbeziehung erstellen** ist das **Quellattribut** **City**. Legen Sie den Wert **Verknüpftes Attribut** auf **State-Province**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest** ein, da sich Beziehungen zwischen einem Ort und einem Bundesland bzw. Kanton im Laufe der Zeit nicht ändern.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Klicken Sie mit der rechten Maustaste auf den Pfeil zwischen **Geography** und **State-Province** , und klicken Sie anschließend auf **Löschen**.  
  
17. Das Dialogfeld **Objekte löschen** wird geöffnet. Klicken Sie auf **OK**.  
  
18. Klicken Sie im Diagramm mit der rechten Maustaste auf das Attribut **State-Province** , und wählen Sie anschließend **Neue Attributbeziehung**aus.  
  
19. Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **State-Province**. Legen Sie als **Verknüpftes Attribut** **Country-Region**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest** ein, da sich Beziehungen zwischen einem Bundesland bzw. Kanton und einem Land bzw. einer Region im Laufe der Zeit nicht ändern.  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. Klicken Sie im Bereich Attributbeziehungen mit der rechten Maustaste auf **Geography** ->  **Country-Region**, und klicken Sie anschließend auf **Löschen**.  
  
22. Das Dialogfeld **Objekte löschen** wird geöffnet. Klicken Sie auf **OK**.  
  
23. Klicken Sie auf die Registerkarte **Dimensionsstruktur** .  
  
    Wenn Sie die letzte Attributbeziehung zwischen **Geography** und anderen Attributen löschen, wird auch das **Geography** -Attribut selbst gelöscht. Das liegt daran, dass das Attribut nicht mehr verwendet wird.  
  
24. Klicken Sie im Menü Datei auf **Alle speichern**.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Definieren von Attributbeziehungen für Attribute in der Sales Territory-Hierarchie  
  
1.  Öffnen Sie den Dimensions-Designer für die **Sales Territory** -Dimension, und klicken Sie auf die Registerkarte **Attributbeziehungen** .  
  
2.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Sales Territory Country** -Attribut, und wählen Sie **Neue Attributbeziehung**aus.  
  
3.  Im Dialogfeld **Attributbeziehung erstellen** ist das **Quellattribut** **Sales Territory Country**. Legen Sie den Wert **Verknüpftes Attribut** auf **Sales Territory Group**fest. Belassen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Flexibel**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    **Sales Territory Group** ist jetzt mit **Sales Territory Country**verknüpft, und **Sales Territory Country** ist jetzt mit **Sales Territory Region**verknüpft. Die **RelationshipType** -Eigenschaft ist für jede dieser Beziehungen auf **Flexibel** festgelegt, da sich die Gruppierungen von Regionen innerhalb eines Landes mit der Zeit ändern können und weil sich die Gruppierungen von Ländern in Gruppen mit der Zeit ändern können.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Definieren von Attributbeziehungen für Attribute in der Product Model Lines-Hierarchie  
  
1.  Öffnen Sie den Dimensions-Designer für die **Product** -Dimension, und klicken Sie anschließend auf die Registerkarte **Attributbeziehungen** .  
  
2.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Model Name** -Attribut, und wählen Sie anschließend **Neue Attributbeziehung**aus.  
  
3.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Model Name**. Legen Sie für **Verknüpftes Attribut** die Einstellung **Produktgruppe**fest. Belassen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Flexibel**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Definieren von Attributbeziehungen für Attribute in der Fiscal Date-Hierarchie  
  
1.  Wechseln Sie zum Dimensions-Designer für die **Date** -Dimension, und klicken Sie anschließend auf die Registerkarte **Attributbeziehungen** .  
  
2.  Klicken Sie im Diagramm mit der rechten Maustaste auf das Attribut **Month Name** und wählen Sie **Neue Attributbeziehung**aus.  
  
3.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Month Name**. Legen Sie den Wert **Verknüpftes Attribut** auf **Fiscal Quarter**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Fiscal Quarter** -Attribut, und wählen Sie **Neue Attributbeziehung**aus.  
  
6.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Fiscal Quarter**. Legen Sie den Wert **Verknüpftes Attribut** auf **Fiscal Semester**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Fiscal Semester** -Attribut, und wählen Sie **Neue Attributbeziehung**aus.  
  
9. Im Dialogfeld **Attributbeziehung erstellen** ist das **Quellattribut** **Fiscal Semester**. Legen Sie den Wert für **Verknüpftes Attribut** auf **Fiscal Year**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Definieren von Attributbeziehungen für Attribute in der Calendar Date-Hierarchie  
  
1.  Klicken Sie im Diagramm mit der rechten Maustaste auf das Attribut **Month Name** und wählen Sie **Neue Attributbeziehung**aus.  
  
2.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Month Name**. Legen Sie den Wert für **Verknüpftes Attribut** auf **Calendar Quarter**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Klicken Sie im Diagramm mit der rechten Maustaste auf das Attribut **Calendar Quarter** , und wählen Sie **Neue Attributbeziehung**aus.  
  
5.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Calendar Quarter**. Legen Sie den Wert für **Verknüpftes Attribut** auf **Calendar Semester**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Calendar Semester** -Attribut, und wählen Sie **Neue Attributbeziehung**aus.  
  
8.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Calendar Semester**. Legen Sie den Wert für **Verknüpftes Attribut** auf **Calendar Year**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Definieren von Attributbeziehungen für Attribute in der Geography-Hierarchie  
  
1.  Öffnen Sie den Dimensions-Designer für die Geography-Dimension, und klicken Sie auf die Registerkarte **Attributbeziehungen** .  
  
2.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **Postal Code** -Attribut, und wählen Sie anschließend **Neue Attributbeziehung**.  
  
3.  Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **Postal Code**. Legen Sie den Wert **Verknüpftes Attribut** auf **City**fest. Legen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Flexibel**fest.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Klicken Sie im Diagramm mit der rechten Maustaste auf das **City** -Attribut, und wählen Sie anschließend **Neue Attributbeziehung**aus.  
  
6.  Im Dialogfeld **Attributbeziehung erstellen** ist das **Quellattribut** **City**. Legen Sie den Wert **Verknüpftes Attribut** auf **State-Province**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Klicken Sie im Diagramm mit der rechten Maustaste auf das Attribut **State-Province** , und wählen Sie anschließend **Neue Attributbeziehung**aus.  
  
9. Im Dialogfeld **Attributbeziehung erstellen** lautet das **Quellattribut** **State-Province**. Legen Sie als **Verknüpftes Attribut** **Country-Region**fest. Stellen Sie in der Liste **Beziehungstyp** den Beziehungstyp auf **Fest**ein.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Klicken Sie im Diagramm mit der rechten Maustaste auf das **Geography Key** -Attribut, und wählen Sie **Eigenschaften**aus.  
  
12. Legen Sie die **AttributeHierarchyOptimizedState** -Eigenschaft auf **NotOptimized**fest, legen Sie die **AttributeHierarchyOrdered** -Eigenschaft auf **FALSE**und die **AttributeHierarchyVisible** -Eigenschaft ebenfalls auf **FALSE**fest.  
  
13. Klicken Sie im Menü **Datei** auf **Alle speichern**.  
  
14. Klicken Sie im Menü **Erstellen** von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]auf **Analysis Services Tutorial bereitstellen**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Definieren von unbekannten Elementen und Eigenschaften für das Verarbeiten von NULL-Werten](../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>Siehe auch  
[Definieren von Attributbeziehungen](../analysis-services/multidimensional-models/attribute-relationships-define.md)  
[Eigenschaften der Benutzerhierarchie](../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
  

