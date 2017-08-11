---
title: Melden und gruppieren Sie Variablen Sammlungen Verweise (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10404"
- "10083"
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- sql13.rtp.rptdesigner.categorygroupproperties.variables.f1
- sql13.rtp.rptdesigner.reportproperties.variables.f1
- "10292"
- sql13.rtp.rptdesigner.seriesgroupproperties.variables.f1
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 99b5b8ec78220064b79795e51b37b22f18a60886
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="built-in-collections---report-and-group-variables-references-report-builder"></a>Integrierte Auflistungen - Bericht und verweist auf Variablen (Berichts-Generator)
  Bei komplexen Berechnungen, die in Ausdrücken eines Berichts mehrfach verwendet werden, empfiehlt sich das Erstellen einer Variable. Sie können eine Berichtsvariable oder eine Gruppenvariable erstellen. Variablennamen müssen im Bericht eindeutig sein.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>Berichtsvariablen  
 Verwenden Sie eine Berichtsvariable zur Aufnahme eines Werts für zeitabhängige Berechnungen, wie Währungskurse oder Zeitstempel, oder für eine komplexe Berechnung, auf die mehrere Male verwiesen wird. Standardmäßig wird eine Berichtsvariable einmal berechnet und kann in Ausdrücken im gesamten Bericht verwendet werden. Berichtsvariablen sind standardmäßig schreibgeschützt. Sie können die Standardeinstellung ändern, um für eine Berichtsvariable den Lese-/Schreibzugriff zu aktivieren. Der Wert in einer Berichtsvariable wird in der gesamten Sitzung beibehalten, bis der Bericht erneut verarbeitet wird.  
  
 Um eine Berichtsvariable hinzuzufügen, öffnen Sie das Dialogfeld **Berichtseigenschaften** , klicken Sie auf **Variablen**, und geben Sie einen Namen und einen Wert an. Bei Namen ist die Groß-/Kleinschreibung zu beachten. Sie beginnen mit einem Buchstaben und enthalten keine Leerzeichen. Ein Name darf Buchstaben, Zahlen oder Unterstriche (_) enthalten.  
  
 Um auf die Variable in einem Ausdruck zu verweisen, verwenden Sie die globale Auflistungssyntax, z. B. `=Variables!CustomTimeStamp.Value`. Auf der Entwurfsoberfläche wird der Wert in einem Textfeld als `<<Expr>>`angezeigt.  
  
 Es gibt folgende Möglichkeiten für die Verwendung von Berichtsvariablen:  
  
-   **Nur Lesezugriff** Legen Sie einmalig einen Wert fest, um eine Konstante für die Berichtssitzung zu erstellen, z.B. einen Zeitstempel.  
  
     Da Ausdrücke in Textfeldern bedarfsgesteuert ausgewertet werden, wenn ein Benutzer durch einen Bericht blättert, können dynamische Werte (z.B. ein Ausdruck, der `Now()` einschließt, eine Funktion, die die Tageszeit zurückgibt) unterschiedliche Werte zurückgeben, wenn Sie vor und mit der Schaltfläche **Zurück** zurückblättern. Durch Festlegen des Werts einer Berichtsvariablen auf den Ausdruck `=Now()`und anschließendes Hinzufügen der Variablen zum Ausdruck wird gewährleistet, dass während der Berichtsverarbeitung die gleiche Variable verwendet wird.  
  
-   **Lese-/Schreibzugriff** Legen Sie einmalig einen Wert fest, und serialisieren Sie diesen innerhalb einer Berichtssitzung. Die Lese-/Schreiboption für Variablen bietet eine bessere Alternative als die Verwendung einer statischen Variable im Codeblock der Berichtsdefinition.  
  
     Wenn Sie die Option **Schreibgeschützt** für eine Variable deaktivieren, wird die Writable-Eigenschaft der Variable auf **TRUE**festgelegt. Verwenden Sie die SetValue-Methode, z.B. `=Variables!MyVariable.SetValue("123")`, um den Wert mit einem Ausdruck zu aktualisieren.  
  
    > [!NOTE]  
    >  Sie können nicht steuern, wann der Berichtsprozessor eine Variable initialisiert oder einen Ausdruck auswertet, der eine Variable aktualisiert. Der Reihenfolge der Ausführung für die Variableninitialisierung ist nicht definiert.  
  
 Weitere Informationen zu Sitzungen finden Sie unter [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="group-variables"></a>Gruppenvariablen  
 Verwenden Sie eine Gruppenvariable, um einen komplexen Ausdruck im Bereich einer Gruppe einmal zu berechnen. Eine Gruppenvariable ist nur im Bereich der Gruppe und der untergeordneten Gruppen gültig.  
  
 Angenommen, ein Datenbereich zeigt Bestandsdaten für Posten an, die verschiedenen Steuerkategorien angehören, und Sie möchten für jede Kategorie einen anderen Steuersatz anwenden. In diesem Fall gruppieren Sie die Daten in Kategorien und definieren für die übergeordnete Gruppe eine *Tax* -Variable. Anschließend definieren Sie eine Gruppenvariable für *ItemTax* für jede Steuerkategorie und weisen jeder der Kategorieuntergruppen die richtige Gruppenvariable zu. Beispiel:  
  
-   Definieren Sie für die übergeordnete Gruppe auf Grundlage von `[Category]`die Variable *Tax* mit einem Wert `[Tax]`. Angenommen, die Kategoriewerte lauten Nahrungsmittel und Kleidung.  
  
-   Definieren Sie für die untergeordnete Gruppe auf Grundlage von `[Subcategory]`die Variable *ItemsTax* als `=Variables!Tax.Value * Sum(Fields!Price.Value)`. Angenommen, die Unterkategoriewerte für die Kategorie Nahrungsmittel sind Getränke und Brot. Die Unterkategoriewerte für Kleidung lauten Hemden und Hüte.  
  
-   Fügen Sie für ein Textfeld in einer Zeile der untergeordneten Gruppe den Ausdruck `=Variables!ItemsTax.Value`hinzu.  
  
     Das Textfeld zeigt die gesamte Steuer für Getränke und Brot unter Verwendung des Steuersatzes für Nahrungsmittel und für Hemden und Hüte unter Verwendung des Steuersatzes für Kleidung an.  
  
 Um eine Gruppenvariable hinzuzufügen, öffnen Sie das Dialogfeld **Tablix-Gruppeneigenschaften** , klicken Sie auf **Variablen**, und geben Sie einen Namen und einen Wert an. Die Gruppenvariable wird einmal pro eindeutigen Gruppenwert berechnet.  
  
 Um auf die Variable in einem Ausdruck zu verweisen, verwenden Sie die globale Auflistungssyntax, z. B. `=Variables!GroupDescription.Value`. Auf der Entwurfsoberfläche wird der Wert in einem Textfeld als `<<Expr>>`angezeigt.  
  
## <a name="see-also"></a>Siehe auch  
 [Filter, Gruppen, und Sortieren von Daten &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Integrierte Auflistungen in Ausdrücken &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Beispiele für Ausdrücke &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
