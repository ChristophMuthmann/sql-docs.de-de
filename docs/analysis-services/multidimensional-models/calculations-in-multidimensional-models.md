---
title: Berechnungen in mehrdimensionalen Modellen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 897eae64c89203a7d0e507862866d95a8bfe530d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="calculations-in-multidimensional-models"></a>Berechnungen in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Mithilfe der Registerkarte **Berechnungen** des Cube-Designers können Sie berechnete Elemente, benannte Mengen sowie andere MDX-Berechnungen (Multidimensional Expressions) erstellen.  
  
 Die Registerkarte **Berechnungen** setzt sich aus den folgenden drei Bereichen zusammen:  
  
-   Im **Skriptplaner** -Bereich werden die Berechnungen in einem Cube aufgelistet. Mit diesem Bereich können Sie Berechnungen erstellen, strukturieren und für die Bearbeitung auswählen.  
  
-   Im **Berechnungstools** -Bereich werden Metadaten, Funktionen und Vorlagen zum Erstellen von Berechnungen bereitgestellt.  
  
-   Der Berechnungsausdrücke-Bereich unterstützt eine Formularansicht und eine Skriptansicht.  
  
> [!NOTE]  
>  Weitere Informationen zur MDX-Skripterstellung finden Sie unter [Introduction to MDX Scripting in Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892)(in Englisch) sowie im Abschnitt Additional Resources auf der Seite [SQL Server 2005 – Analysis Services](http://go.microsoft.com/fwlink/?LinkId=80853) der Microsoft TechNet-Website. Weitere Informationen zu Leistungsproblemen im Zusammenhang mit dem Cubedesign finden Sie unter [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="creating-a-new-calculation"></a>Erstellen einer neuen Berechnung  
 Zum Erstellen einer neuen Berechnung klicken Sie im Menü **Cube** auf der Registerkarte **Berechnungen** des Cube-Designers auf eine der Optionen **Neues berechnetes Element**, **Neue benannte Menge**oder **Neuer Skriptbefehl**, abhängig von der Art der Berechnung, die Sie erstellen möchten. Sie können auch auf eine der entsprechenden Schaltflächen auf der Symbolleiste oder mit der rechten Maustaste auf eine beliebige Stelle innerhalb des Bereichs **Skriptplaner** und dann auf einen der Befehle im Kontextmenü klicken. Durch diese Aktion wird dem **Skriptplaner** -Bereich eine neue Berechnung hinzugefügt, und im Berechnungsformular des Berechnungsausdrücke-Bereichs werden entsprechende Felder angezeigt. Wenn Sie ein neues Skript erstellen, wird durch diese Aktion die Skriptansicht im Berechnungsausdrücke-Bereich geöffnet. Weitere Informationen zu den drei Arten von Berechnungen finden Sie unter [Erstellen von berechneten Elementen](../../analysis-services/multidimensional-models/create-calculated-members.md), [Erstellen von benannten Mengen](../../analysis-services/multidimensional-models/create-named-sets.md)und [Definieren von Zuweisungen und anderen Skriptbefehlen](../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md).  
  
## <a name="editing-scripts"></a>Bearbeiten von Skripts  
 Skripts werden im Berechnungsausdrücke-Bereich auf der Registerkarte **Berechnungen** bearbeitet. Der Berechnungsausdrücke-Bereich verfügt über zwei Ansichten, die Skriptansicht und die Formularansicht. In der Formularansicht werden die Ausdrücke und Eigenschaften eines einzelnen Befehls angezeigt. Beim Bearbeiten eines MDX-Skripts nimmt ein Ausdrucksfeld die gesamte Formularansicht ein.  
  
 Die Skriptansicht stellt einen Code-Editor für die Bearbeitung der Skripts bereit. Wird der Berechnungsausdrücke-Bereich in der Skriptansicht angezeigt, ist der **Skriptplaner** -Bereich ausgeblendet. In der Skriptansicht stehen Farbcodierung, Vervollständigen von Klammern, automatische Vervollständigung und MDX-Codebereiche zur Verfügung. Die MDX-Codebereiche können zum Vereinfachen der Bearbeitung reduziert oder erweitert werden.  
  
 Sie können zwischen der Formular- und der Skriptansicht hin- und herwechseln, indem Sie im Menü **Cube** auf **Berechnungen anzeigen in**zeigen und dann auf **Skript** oder **Formular**klicken. Sie können auch auf der Symbolleiste entweder auf **Formularansicht** oder **Skriptansicht** klicken.  
  
## <a name="changing-solve-order"></a>Ändern der Lösungsreihenfolge  
 Berechnungen werden in der Reihenfolge aufgelöst, in der sie im **Skriptplaner** -Bereich aufgelistet sind. Indem Sie mit der rechten Maustaste auf eine beliebige Berechnung klicken und anschließend im Kontextmenü auf **Nach oben** oder **Nach unten** klicken, können Sie die Reihenfolge der Berechnungen ändern. Alternativ können Sie auf eine Berechnung klicken und dann auf der Symbolleiste auf die Schaltfläche **Nach oben** oder **Nach unten** klicken.  
  
 Für berechnete Zellen und berechnete Elemente kann die Reihenfolge manuell überschrieben werden. Weitere Informationen zur Durchlauf- und Lösungsreihenfolge finden Sie unter [Grundlegendes zu Durchlauf- und Lösungsreihenfolge &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
## <a name="deleting-a-calculation"></a>Löschen einer Berechnung  
 Wenn Sie eine vorhandene Berechnung löschen möchten, wählen Sie auf der Registerkarte **Berechnungen** im **Skriptplaner** -Bereich die zu löschende Berechnung aus, und klicken Sie dann im Menü **Bearbeiten** auf **Löschen** , oder klicken Sie auf der Symbolleiste auf **Löschen** . Sie können auch im Bereich **Skriptplaner** mit der rechten Maustaste auf die Berechnung klicken und im Kontextmenü die Option **Löschen** auswählen.  
  
  
