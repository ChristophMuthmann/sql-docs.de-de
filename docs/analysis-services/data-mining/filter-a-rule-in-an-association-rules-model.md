---
title: "Filtern einer Regel in einem Zuordnungsregelmodell | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Filtern von Regeln [Analysis Services]"
  - "Miningmodell-Viewer [Analysis Services], Regeln"
  - "Regeln-Viewer"
ms.assetid: 26cdba5b-5bf1-439e-80a3-8759774e918b
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 28
---
# Filtern einer Regel in einem Zuordnungsregelmodell
  Sie können Filterung mit Zuordnungsmodellen verwenden, um die Ergebnisse auf die Zuordnungen zu beschränken, die für Sie von Interesse sind. Zum Beispiel können Sie die Regeln filtern, damit nur die Ergebnisse angezeigt werden, die ein bestimmtes Produkt enthalten.  
  
 Im Data Mining-Designer verwenden Sie die Steuerelemente auf der Registerkarte **Regeln** des [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Zuordnungsregeln-Viewers, um die angezeigten Regeln zu filtern.  Sie können auch eine Abfrage für das Modell erstellen, um nur Itemsets anzuzeigen, die einen bestimmten Wert enthalten.  
  
> [!NOTE]  
>  Diese Option ist nur für Miningmodelle verfügbar, die mit dem Microsoft Association-Algorithmus erstellt wurden.  
  
### Filtern einer Regel in einem Zuordnungsmodell  
  
1.  Öffnen Sie das Miningmodell mit dem **Zuordnungsregeln-Viewer**. In SQL Server Management Studio müssen Sie hierzu mit der rechten Maustaste auf den Modellnamen klicken und **Durchsuchen**auswählen. Doppelklicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] auf die Miningstruktur, die das Modell enthält, und klicken Sie anschließend auf die Registerkarte **Miningmodell-Viewer** im **Data Mining-Designer**.  
  
2.  Klicken Sie im **Zuordnungsregeln-Viewer** auf die Registerkarte **Regeln**.  
  
3.  Geben Sie in das Feld **Filterregel** eine Regelbedingung ein. Eine Regelbedingung könnte z. B. "Bike Stand" sein, die auch "Bike Stands" zurückgibt.  
  
     Das Textfeld **Filterregel** unterstützt reguläre Ausdrücke, wie diese von der .NET-Sprache definiert werden. Daher können Sie z. B. folgende Ausdrücke verwenden: `((.Helmets.*Fenders.*)|(.*Fenders.*Helmets.*))`. Dieser Ausdruck gibt alle Itemsets zurück, die Attribute mit den Wörtern Helmets und Fenders in beliebiger Reihenfolge enthalten.  
  
4.  Erhöhen Sie unter **Minimale Wahrscheinlichkeit**den Wert für die Wahrscheinlichkeit, um mehr Regeln anzuzeigen, und verringern Sie den Wert, um weniger Regeln anzuzeigen.  
  
5.  Erhöhen Sie unter **Minimale Wichtigkeit**den Wert für die Wichtigkeit, um mehr Regeln anzuzeigen, und verringern Sie den Wert, um weniger Regeln anzuzeigen.  
  
6.  Wählen Sie für **Anzeigen**eine der folgenden Optionen aus: **Attributnamen und Wert anzeigen**, **Nur Attributnamen anzeigen**oder **Nur Attributwert anzeigen**.  
  
7.  Erhöhen Sie den Wert für **Maximale Zeilenanzahl**, um die Gesamtzahl von Regeln zu erhöhen, die die angegebenen Bedingungen erfüllen, oder verringern Sie den Wert, um die Anzahl der zurückgegebenen Regeln zu beschränken. Regeln werden nach Wahrscheinlichkeit sortiert. Daher können Sie zusätzliche Regeln ausschließen, die die angegebenen Bedingungen für Wahrscheinlichkeit oder Wichtigkeit erfüllen.  
  
8.  Aktivieren oder deaktivieren Sie das Kontrollkästchen **Langen Namen anzeigen** , um umzuschalten, wie die Namen der Regeln angezeigt werden.  
  
     Die Regeln werden daraufhin gefiltert und es werden nur Regeln angezeigt, die das angegebene Element enthalten. Die Filterbedingung gilt für Attributwerte, die entweder vor oder nach dem Regeltrennzeichen "->" stehen.  
  
    > [!NOTE]  
    >  Der Viewer speichert die ursprüngliche Liste der Regeln basierend auf einer Abfrage des Miningmodells und aktualisiert die Liste der Regeln nur, wenn Sie die Bedingungen für die Abfrage ändern, indem Sie die maximale Zeilenanzahl, die Wahrscheinlichkeit, die Wichtigkeit oder die Anzeige langer Namen festlegen. Wenn Sie eine Bedingung eingeben und die Anzeige nicht sofort aktualisiert wird, können Sie im Viewer daher eine Aktualisierung der Daten erzwingen, indem Sie das Kontrollkästchen **Langen Namen anzeigen** aktivieren und anschließend wieder deaktivieren.  
  
### Erstellen einer Abfrage in den Itemsets in einem Zuordnungsmodell  
  
-   [Beispiele für Zuordnungsmodellabfragen](../../analysis-services/data-mining/association-model-query-examples.md)  
  
## Siehe auch  
 [Tasks und Anweisungen für Miningmodell-Viewer](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Modell mit dem Microsoft-Viewer für Zuordnungsregeln durchsuchen](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)   
 [Lektion 3: Erstellen eines Warenkorbszenarios &#40;Data Mining-Tutorial für Fortgeschrittene&#41;](../Topic/Lesson%203:%20Building%20a%20Market%20Basket%20Scenario%20\(Intermediate%20Data%20Mining%20Tutorial\).md)  
  
  