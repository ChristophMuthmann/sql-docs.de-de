---
title: "Filter für Miningmodelle (Analysis Services – Datamining) | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [data mining]
- filter syntax [data mining]
- models [Analysis Services], filtering
- filters [data mining]
- filtering data [Analysis Services]
ms.assetid: 0f29c19c-4be3-4bc7-ab60-f4130a10d59c
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 83c491408707f1a7107a3bb6d485418189d9eb1c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>Filter für Miningmodelle (Analysis Services – Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Datenbasierte modellfilterung können Sie Miningmodelle erstellen, die Teilmengen von Daten in einer Miningstruktur verwenden. Die Filterung ermöglicht Flexibilität bei der Entwicklung der Miningstrukturen und der Datenquellen, da Sie eine einzelne Miningstruktur auf der Grundlage einer umfassenden Datenquellensicht erstellen können. Anschließend können Sie Filter erstellen, um nur einen Teil dieser Daten zu verwenden und mehrere Modelle zu trainieren und zu testen, anstatt für jede Teilmenge der Daten eine andere Struktur und ein zugehöriges Modell zu erstellen.  
  
 Zum Beispiel definieren Sie die Datenquellensicht für die Tabelle "Kunden" und verknüpfte Tabellen. Anschließend definieren Sie eine einzelne Miningstruktur, die alle Felder enthält, die Sie benötigen. Schließlich erstellen Sie ein Modell, das nach einem bestimmten Kundenattribut gefiltert wird, z. B. "Region". Sie können einfach eine Kopie dieses Modells erstellen und nur die Filterbedingungen ändern, um ein neues Modell auf der Grundlage einer anderen Region zu erzeugen.  
  
 Die folgenden realistischen Szenarien sind einige Beispiele, in denen diese Funktion hilfreich sein kann:  
  
-   Das Erstellen von separaten Modellen für diskrete Werte wie z. B. Geschlecht, Regionen usw. Ein Bekleidungsgeschäft könnte beispielsweise demografische Kundendaten verwenden, um unterschiedliche Modelle nach Geschlecht zu erstellen, auch wenn die Verkaufsdaten aus einer einzigen Datenquelle für alle Kunden stammen.  
  
-   Man könnte mit Modellen experimentieren, indem man unterschiedliche Gruppierungen der gleichen Daten erstellt, beispielsweise die Altersgruppen 20-30, 20-40 oder 20-25.  
  
-   Man könnte komplexe Filter für geschachtelte Tabelleninhalte erstellen, beispielsweise, dass ein Fall nur in einem Modell enthalten ist, wenn ein Kunde mindestens zwei Exemplare eines bestimmten Artikels gekauft hat.  
  
 Dieser Abschnitt erläutert, wie Filter für Miningmodelle erstellt, verwendet und verwaltet werden.  
  
## <a name="creating-model-filters"></a>Erstellen von Modellfiltern  
 Es gibt folgende Möglichkeiten, um Filter zu erstellen und anzuwenden:  
  
-   Verwenden Sie die Registerkarte **Miningmodelle** im Data Mining-Designer, um mithilfe von Dialogfeldern des Filter-Editors Bedingungen zu erstellen.  
  
-   Geben Sie einen Filterausdruck direkt in die **Filter** -Eigenschaft des Miningmodells ein.  
  
-   Legen Sie mit AMO programmgesteuerte Filterbedingungen für ein Modell fest.  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>Erstellen von Modellfiltern unter Verwendung des Data Mining-Designers  
 Sie filtern ein Modell im Data Mining-Designer, indem Sie die **Filter** -Eigenschaft des Miningmodells ändern. Sie können einen Filterausdruck entweder direkt im Bereich **Eigenschaften** eingeben, oder Sie öffnen ein Filterdialogfeld, um Bedingungen zu erstellen.  
  
 Es gibt zwei Filterdialogfelder. Mit dem ersten können Sie Bedingungen erstellen, die auf die Falltabelle angewendet werden. Wenn die Datenquelle mehrere Tabellen enthält, wählen Sie zuerst eine Tabelle und dann eine Spalte aus und legen die Operatoren und Bedingungen fest, die für die Spalte gelten sollen. Mithilfe der Operatoren **AND**/**OR** können Sie mehrere Bedingungen verknüpfen. Welche Operatoren für die Definition von Werten verfügbar sind, ist davon abhängig, ob die Spalte diskrete oder fortlaufende Werte enthält. Zum Beispiel können Sie mit fortlaufenden Werten die Operatoren **greater than** und **less than** verwenden. Für diskrete Werte können Sie allerdings nur die Operatoren **= (gleich)**, **!= (ungleich)**und **ist NULL** verwenden.  
  
> [!NOTE]  
>  Das Schlüsselwort **LIKE** wird nicht unterstützt. Wenn Sie mehrere diskrete Attribute einfügen möchten, müssen Sie einzelne Bedingungen erstellen und diese mithilfe des Operators **OR** verknüpfen.  
  
 Wenn die Bedingungen komplex sind, können Sie das zweite Filterdialogfeld verwenden, um mit einer Tabelle gleichzeitig zu arbeiten. Wenn Sie das zweite Filterdialogfeld schließen, wird der Ausdruck ausgewertet und anschließend mit Filterbedingungen, die für andere Spalten in der gleichen Falltabelle festgelegt wurden, kombiniert.  
  
### <a name="creating-filters-on-nested-tables"></a>Erstellen von Filtern für geschachtelte Tabellen  
 Wenn die Datenquellensicht geschachtelte Tabellen enthält, können Sie das zweite Filterdialogfeld verwenden, um Bedingungen für die Zeilen in den geschachtelten Tabellen zu erstellen.  
  
 Wenn sich beispielsweise Ihre Falltabelle auf Kunden bezieht und die geschachtelte Tabelle die Produkte zeigt, die der Kunde gekauft hat, können Sie einen Filter für Kunden erstellen, die bestimmte Artikel gekauft haben, indem Sie im Filter der geschachtelten Tabelle die folgende Syntax verwenden: `[ProductName]=’Water Bottle’ OR ProductName=’Water Bottle Cage'`.  
  
 Sie können auch auf das Vorhandensein eines bestimmten Werts in der geschachtelten Tabelle filtern, indem Sie die Schlüsselwörter **EXISTS** oder **NOT EXISTS** und eine Unterabfrage verwenden. Auf diese Weise können Sie Bedingungen wie `EXISTS (SELECT * FROM Products WHERE ProductName=’Water Bottle’)`erstellen. Die `EXISTS SELECT(<subquery>)` gibt **TRUE** zurück, wenn die geschachtelte Tabelle mindestens eine Zeile enthält, die den Wert `Water Bottle`enthält.  
  
 Sie können Bedingungen für die Falltabelle mit Bedingungen für die geschachtelte Tabelle kombinieren. Beispielsweise fügt die folgende Syntax eine Bedingung für die Falltabelle ein (`Age > 30` ), eine Unterabfrage für die geschachtelte Tabelle (`EXISTS (SELECT * FROM Products)`) und mehrere Bedingungen für die geschachtelte Tabelle (`WHERE ProductName=’Milk’  AND Quantity>2`) ).  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity>2) )  
```  
  
 Wenn Sie den Filter fertig gestellt haben, wird der Filtertext von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ausgewertet, in einen DMX-Ausdruck übersetzt und mit dem Modell gespeichert.  
  
 Anweisungen zur Verwendung der Dialogfelder „Filter“ in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]finden Sie unter [Anwenden eines Filters auf ein Miningmodell](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
## <a name="managing-mining-model-filters"></a>Verwalten von Miningmodellfiltern  
 Durch datenbasierte Modellfilterung wird die Verwaltung der Miningstruktur und der Miningmodelle stark vereinfacht, da Sie leicht mehrere Modelle erstellen können, die auf der gleichen Struktur basieren. Sie können auch schnell Kopien vorhandener Miningmodelle erstellen und dann nur die Filterbedingung ändern. Filter können jedoch zu einer gewissen Verwirrung führen.  
  
 Die folgenden häufig gestellten Fragen beziehen sich darauf, wie Sie Filter für Miningmodelle verwalten und interpretieren:  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>Wie stelle ich fest, ob ein Filter verwendet wird?  
 Sie können auf verschiedene Weisen feststellen, ob auf ein Modell ein Filter angewendet wurde:  
  
-   Klicken Sie im Designer auf die Registerkarte **Miningmodelle** , öffnen Sie **Eigenschaften**, und zeigen Sie die **Filter** -Eigenschaft des Miningmodells an.  
  
-   In der DMV mit dem Namen DMSCHEMA_MINING_MODELS wird eine Spalte ausgegeben, die den Text des Filters enthält. Sie können die folgende Abfrage für eine DMV verwenden, um die Namen der Modelle und ihre Filter zurückzugeben:  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   Sie können den Wert der Filter-Eigenschaft des MiningModel-Objekts in AMO abrufen oder das Filter-Element in XMLA untersuchen.  
  
 Darüber hinaus können Sie eine Benennungskonvention für Modelle festlegen, um den Inhalt des Filters wiederzugeben. Dies kann die Unterscheidung verwandter Modelle erleichtern.  
  
### <a name="how-can-i-save-a-filter"></a>Wie kann ich einen Filter speichern?  
 Der Filterausdruck wird als Skript gespeichert, das zusammen mit dem zugehörigen Miningmodell oder der verschachtelten Tabelle gespeichert wird. Wenn Sie den Filtertext löschen, kann dieser nur durch die manuelle Neuerstellung des Filterausdrucks wiederhergestellt werden. Wenn Sie komplexe Filterausdrücke erstellen, sollten Sie daher eine Sicherungskopie des Filtertexts erstellen.  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>Warum sehe ich keine Auswirkungen des Filters?  
 Immer wenn Sie einen Filterausdruck ändern oder hinzufügen, müssen Sie die Struktur und das Modell neu verarbeiten, bevor Sie die Auswirkungen des Filters sehen können.  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>Warum sehe ich gefilterte Attribute in den Ergebnissen von Vorhersageabfragen?  
 Wenn Sie einen Filter auf ein Modell anwenden, wirkt sich dieser nur auf die Auswahl der Fälle aus, die zum Trainieren des Modells verwendet werden. Der Filter wirkt sich nicht auf die Attribute aus, die dem Modell bekannt sind, und ändert oder unterdrückt auch keine Daten, die in der Datenquelle vorhanden sind. Folglich können Abfragen des Modells Vorhersagen für andere Falltypen zurückgeben, und Dropdownlisten mit den vom Modell verwendeten Werten enthalten möglicherweise Attributwerte, die vom Filter ausgeschlossen werden.  
  
 Beispiel: Sie trainieren das [Bike Buyer]-Modell ausschließlich anhand von Fällen, die sich auf Frauen im Alter von 20 bis 30 Jahren beziehen. Sie können trotzdem eine Vorhersageabfrage ausführen, durch die die Wahrscheinlichkeit vorhergesagt wird, mit der ein Mann ein Fahrrad kaufen wird. Alternativ können Sie auch eine Vorhersage für Frauen in der Altersgruppe von 30 bis 40 Jahren ausführen. Dies liegt daran, dass die Attribute und Werte in der Datenquelle definieren, was theoretisch möglich ist, während die Fälle definieren, welche Vorkommen zu Trainingszwecken verwendet werden. Diese Abfragen würden jedoch nur sehr geringe Wahrscheinlichkeiten zurückgeben, weil die Trainingsdaten keine Fälle mit den Zielwerten erhalten.  
  
 Wenn Sie Attributwerte im Modell vollständig ausblenden oder anonymisieren möchten, stehen Ihnen mehrere Optionen zur Verfügung:  
  
-   Filtern der eingehenden Daten als Teil der Definition der Datenquellensicht oder in der relationalen Datenquelle  
  
-   Maskieren oder Codieren des Attributwerts  
  
-   Reduzieren ausgeschlossener Werte in einer Kategorie als Teil der Miningstrukturdefinition  
  
## <a name="related-resources"></a>Verwandte Ressourcen  
 Weitere Informationen zur Filtersyntax und Beispiele für Filterausdrücke finden Sie unter [Modellfiltersyntax und Beispiele &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
 Informationen zur Verwendung von Modellfiltern beim Testen eines Miningmodells finden Sie unter [Auswählen eines Genauigkeitsdiagrammtyps und Festlegen von Diagrammoptionen](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Modellfiltersyntax und Beispiele &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [Tests und Überprüfung &#40;Data Mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
