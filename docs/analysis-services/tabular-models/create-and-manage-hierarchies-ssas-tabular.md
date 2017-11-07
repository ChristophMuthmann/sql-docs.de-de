---
title: "Erstellen und Verwalten von Hierarchien (SSAS – tabellarisch) | Microsoft Docs"
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
ms.assetid: 8dd30cd0-a831-4d25-b577-648d7f3c7fa6
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 63c10ca6e8486e67db96d7fe4d1e6afe76133ef8
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-manage-hierarchies-ssas-tabular"></a>Erstellen und Verwalten von Hierarchien (SSAS – tabellarisch)
  Hierarchien können in der Diagrammsicht des Modell-Designers erstellt und verwaltet werden. Um den Modell-Designer in der Diagrammsicht in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]anzuzeigen, klicken Sie auf das Menü **Modell** , zeigen Sie dann auf **Modellansicht**, und klicken Sie dann auf **Diagrammsicht**.  
  
 Dieses Thema umfasst folgende Aufgaben:  
  
-   [Erstellen einer Hierarchie](#bkmk_create)  
  
-   [Bearbeiten einer Hierarchie](#bkmk_edit)  
  
-   [Löschen einer Hierarchie](#bkmk_delete)  
  
##  <a name="bkmk_create"></a> Erstellen einer Hierarchie  
 Sie können eine Hierarchie mithilfe der Kontextmenüs für Spalten und Tabellen erstellen. Wenn Sie eine Hierarchie erstellen, wird eine neue übergeordnete Ebene mit den ausgewählten Spalten als untergeordnete Ebenen angezeigt.  
  
#### <a name="to-create-a-hierarchy-from-the-context-menu"></a>So erstellen Sie eine Hierarchie über das Kontextmenü  
  
1.  Klicken Sie im Modell-Designer (Diagrammsicht) in einem Tabellenfenster mit der rechten Maustaste auf eine Spalte, und klicken Sie dann auf **Hierarchie erstellen**.  
  
     Um mehrere Spalten auszuwählen, klicken Sie auf jede Spalte, klicken Sie dann mit der rechten Maustaste, um das Kontextmenü zu öffnen, und klicken Sie dann auf **Hierarchie erstellen**.  
  
     Im unteren Bereich des Tabellenfensters wird eine übergeordnete Hierarchieebene erstellt, und die ausgewählten Spalten werden als untergeordnete Ebenen unter die Hierarchie kopiert.  
  
2.  Geben Sie einen Namen für die Hierarchie ein.  
  
 Sie können zusätzliche Spalten in die übergeordnete Ebene der Hierarchie ziehen, wodurch die Spalten kopiert werden. Legen Sie die untergeordnete Ebene an der Stelle ab, an der sie in der Hierarchie angezeigt werden soll.  
  
> [!NOTE]  
>  Wenn Sie ein Measure zusammen mit mindestens einer Spalte auswählen oder Spalten aus mehreren Tabellen auswählen, ist der Befehl Hierarchie erstellen im Kontextmenü deaktiviert.  
  
##  <a name="bkmk_edit"></a> Bearbeiten einer Hierarchie  
 Sie können eine Hierarchie und eine untergeordnete Ebene umbenennen, die Reihenfolge der untergeordneten Ebenen ändern, zusätzliche Spalten als untergeordnete Ebenen hinzufügen, eine untergeordnete Ebene aus einer Hierarchie entfernen, den Quellnamen einer untergeordneten Ebene (Spaltennamen) anzeigen und eine untergeordnete Ebene ausblenden, wenn sie über den gleichen Namen verfügt wie die übergeordnete Hierarchieebene.  
  
#### <a name="to-change-the-name-of-a-hierarchy-or-child-level"></a>So ändern Sie den Namen einer Hierarchie oder untergeordneten Ebene  
  
1.  Klicken Sie mit der rechten Maustaste auf die übergeordnete Hierarchieebene oder eine untergeordnete Ebene, und klicken Sie dann auf **Umbenennen**.  
  
2.  Geben Sie einen neuen Namen ein, oder bearbeiten Sie den vorhandenen Namen.  
  
#### <a name="to-change-the-order-of-a-child-level-in-a-hierarchy"></a>So ändern Sie die Reihenfolge einer untergeordneten Ebene in einer Hierarchie  
  
-   Klicken Sie auf eine untergeordnete Ebene, und ziehen Sie sie auf eine neue Position in der Hierarchie.  
  
-   Alternativ können Sie mit der rechten Maustaste auf eine untergeordnete Ebene der Hierarchie klicken und dann auf Nach oben klicken, um die Ebene in der Liste nach oben zu verschieben, oder klicken Sie auf Nach unten, um die Ebene in der Liste nach unten zu verschieben.  
  
-   Oder klicken Sie auf eine untergeordnete Ebene, um sie auszuwählen, und drücken Sie dann ALT+NACH-OBEN, um die Ebene nach oben zu verschieben, oder drücken Sie ALT+NACH-UNTEN, um die Ebene in der Liste nach unten zu verschieben.  
  
#### <a name="to-add-another-child-level-to-a-hierarchy"></a>So fügen Sie einer Hierarchie eine weitere untergeordnete Ebene hinzu  
  
-   Klicken Sie auf eine Spalte, und ziehen Sie sie auf die übergeordnete Ebene oder auf eine bestimmte Position in der Hierarchie. Die Spalte wird als untergeordnete Ebene der Hierarchie kopiert.  
  
-   Oder klicken Sie mit der rechten Maustaste auf eine Spalte, zeigen Sie auf **Zur Hierarchie hinzufügen**, und klicken Sie dann auf die Hierarchie.  
  
> [!NOTE]  
>  Sie können der Hierarchie eine (in Berichten ausgeblendete) Spalte als untergeordnete Ebene hinzufügen. Die untergeordnete Ebene wird nicht ausgeblendet.  
  
#### <a name="to-remove-a-child-level-from-a-hierarchy"></a>So entfernen Sie eine untergeordnete Ebene aus einer Hierarchie  
  
-   Klicken Sie mit der rechten Maustaste auf eine untergeordnete Ebene, und klicken Sie dann auf **Aus Hierarchie entfernen**.  
  
-   Sie können auch auf eine untergeordnete Ebene klicken und dann **ENTF**drücken.  
  
> [!NOTE]  
>  Wenn Sie eine untergeordnete Hierarchieebene umbenennen, hat sie nicht mehr den gleichen Namen wie die Spalte, von der sie kopiert wurde. Verwenden Sie den Befehl **Quellspaltennamen einblenden** , um die Spalte anzuzeigen, von der sie kopiert wurde.  
  
#### <a name="to-show-a-source-name"></a>So zeigen Sie einen Quellnamen an  
  
-   Klicken Sie mit der rechten Maustaste auf eine untergeordnete Ebene in der Hierarchie, und klicken Sie dann auf **Quellspaltennamen**einblenden. Der Name der Spalte, von der die Spalte kopiert wurde, wird angezeigt.  
  
##  <a name="bkmk_delete"></a> Löschen einer Hierarchie  
  
#### <a name="to-delete-a-hierarchy-and-remove-its-child-levels"></a>So löschen Sie eine Hierarchie und entfernen deren untergeordnete Ebenen  
  
-   Klicken Sie mit der rechten Maustaste auf die übergeordnete Hierarchieebene, und klicken Sie dann auf Hierarchie löschen.  
  
-   Klicken Sie auf die übergeordnete Hierarchieebene, und drücken Sie dann ENTF. Dadurch werden auch alle untergeordneten Ebenen entfernt.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen-Modell-Designer &#40;SSAS&#41;](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [Hierarchien &#40; SSAS – tabellarisch &#41;](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)   
 [Measures &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/measures-ssas-tabular.md)  
  
  

