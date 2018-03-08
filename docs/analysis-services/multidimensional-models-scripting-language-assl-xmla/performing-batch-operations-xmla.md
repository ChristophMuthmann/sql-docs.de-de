---
title: "Ausführen von Batchvorgängen (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f2730fb8396f63e123bf8d896ea9a648ad22016d
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="performing-batch-operations-xmla"></a>Ausführen von Batchvorgängen (XMLA)
  Können Sie die [Batch](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) -Befehl in XML for Analysis (XMLA) mehrere XMLA-Befehle, die mit einer einzigen XMLA-ausführen [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) Methode. Sie können mehrere Befehle, die in enthaltenen Ausführen der **Batch** -Befehl entweder als einzelne Transaktion oder als individuelle Transaktionen für jeden Befehl in Serie oder parallel. Sie können auch angeben, Out-of-Line-Bindungen und andere Eigenschaften in der **Batch** Befehl für die Verarbeitung mehrerer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Objekte.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Ausführen von transaktionalen und nicht transaktionalen Batchbefehlen  
 Die **Batch** Befehl führt die Befehle in einer von zwei Methoden:  
  
 **Transaktion**  
 Wenn die **Transaktion** Attribut des der **Batch** Befehlssatz ist auf "true", die **Batch** Befehl führen Sie Befehle alle Befehle innerhalb der **Batch** Befehl in einer einzelnen Transaktion – eine *transaktionale* Batch.  
  
 Schlägt jeder Befehl in einem Transaktionsbatch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Rollback für alle Befehle aus, der **Batch** -Befehl, der vor dem Befehl fehlgeschlagenen ausgeführt wurde, und die **Batch** -Befehl wird unmittelbar beendet. Alle Befehle in der **Batch** -Befehl, der noch nicht ausgeführt wurden, werden nicht ausgeführt. Nach der **Batch** Befehl beendet, die **Batch** Befehl meldet Fehler, die für den fehlgeschlagenen Befehl aufgetreten sind.  
  
 **Nontransactional**  
 Wenn die **Transaktion** -Attribut auf "false" festgelegt ist die **Batch** Befehl ausgeführt wird, jeden Befehl enthalten die **Batch** -Befehl in einer separaten Transaktion – eine  *nicht transaktionale* Batch. Schlägt jeder Befehl in einer nicht transaktionalen Batch die **Batch** -Befehl weiterhin Befehle nach dem Befehl, der Fehler, ausführen. Nach der **Batch** -Befehl versucht hat, führen Sie alle Befehle, die die **Batch** Befehl enthält, die **Batch** Befehl gibt alle aufgetretenen Fehler.  
  
 Alle Ergebnisse zurückgegeben, die in enthaltenen Befehle eine **Batch** -Befehl zurückgegeben werden, in der gleichen Reihenfolge, in dem die Befehle enthalten sind, in, der **Batch** Befehl. Von der zurückgegebenen Ergebnisse eine **Batch** Befehl variieren in Abhängigkeit davon, ob die **Batch** Befehl ist transaktional oder nicht transaktional.  
  
> [!NOTE]  
>  Wenn eine **Batch** -Befehl einen Befehl, der keine Ausgabe, wie z. B. zurückgibt enthält die [Sperre](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) Befehl, und dass der Befehl erfolgreich ausgeführt wurde, die **Batch** Befehl gibt ein leeres [Root](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) Element innerhalb des Elements der Ergebnisse. Die leere **Root** Element wird sichergestellt, dass jeder Befehl in enthaltenen eine **Batch** Befehl abgeglichen werden kann, mit dem entsprechenden **Root** -Element für die Ergebnisse des Befehls.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Zurückgeben von Ergebnissen von transaktionalen Batchergebnissen  
 Ergebnisse von Befehlen in einem transaktionalen Batch ausgeführt werden nicht zurückgegeben, bis die gesamte **Batch** Befehl abgeschlossen ist. Die Ergebnisse werden nicht zurückgegeben werden, nach jedem Befehl wird ausgeführt, da es sich bei einem Befehl, mit dem ein Fehler auftritt, in einem transaktionalen Batch die gesamte würde **Batch** Befehl und alle darin enthaltenen Befehle rückgängig gemacht werden. Wenn alle Befehle erfolgreich gestartet und ausgeführt, der [zurückgeben](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md) Element von der [ExecuteResponse](../../analysis-services/xmla/xml-elements-objects-executeresponse.md) zurückgegebene Element der **Execute** Methode für die **Batch**  Befehl enthält ein [Ergebnisse](../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md) Element, das wiederum ein **Root** -Element für jeden erfolgreich ausgeführten Befehl innerhalb der **Batch** Befehl. Wenn ein Befehl die **Batch** Befehl kann nicht gestartet werden kann oder fehlschlägt, die **Execute** Methodenrückgabe ein SOAP-Fehlers die **Batch** -Befehl, der den Fehler enthält die fehlgeschlagene Befehl.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Zurückgeben von Ergebnissen von nicht transaktionalen Batchergebnissen  
 Ergebnisse von Befehlen, die in einem nicht transaktionalen Batch ausgeführt werden zurückgegeben, in der Reihenfolge, in dem die Befehle, innerhalb enthalten sind, der **Batch** Befehl und wie sie von jedem Befehl zurückgegeben werden. Wenn keiner der in enthaltenen Befehle die **Batch** Befehl erfolgreich gestartet werden kann, die **Execute** Methodenrückgabe einen SOAP-Fehler, die für einen Fehler enthält die **Batch** Befehl. Wenn mindestens ein Befehl wurde erfolgreich gestartet wurde, die **zurückgeben** Element von der **ExecuteResponse** zurückgegebene Element der **Execute** Methode für die **Batch**  Befehl enthält ein **Ergebnisse** Element, das wiederum ein **Root** Element für jeden Befehl in enthalten die **Batch** Befehl . Wenn eine oder mehrere Befehle in einem nicht transaktionalen Batch kann nicht gestartet werden kann oder fehlschlägt, die **Root** -Element für diesen fehlgeschlagenen Befehl enthält ein [Fehler](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) Element, das den Fehler beschreibt.  
  
> [!NOTE]  
>  Solange mindestens ein Befehl in einem nicht transaktionalen Batch gestartet werden kann, nicht transaktionalen Batch gilt erfolgreich ausgeführt haben, auch wenn jeder im nicht transaktionalen Batch enthaltene Befehl einen Fehler, in den Ergebnissen zurückgibt der **Batch**  Befehl.  
  
## <a name="using-serial-and-parallel-execution"></a>Verwenden von serieller und paralleler Ausführung  
 Sie können die **Batch** enthalten auszuführende Befehl Befehle seriell oder parallel. Wenn die Befehle seriell ausgeführt werden, enthalten der nächste Befehl der **Batch** Befehl kann nicht gestartet, bis der aktuell ausgeführten Befehl in der **Batch** Befehl abgeschlossen ist. Wenn die Befehle parallel ausgeführt werden, mehrere Befehle können ausgeführt werden gleichzeitig durch den **Batch** Befehl.  
  
 Um Befehle parallel ausgeführt werden, Sie die Befehle parallel ausgeführt werden Hinzufügen der [parallele](../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) Eigenschaft von der **Batch** Befehl. Derzeit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] kann nur ausgeführt, zusammenhängender, sequenzieller [Prozess](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) Befehle parallel. Alle anderen XMLA-Befehle, wie z. B. [erstellen](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) oder [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), enthalten in der **parallele** Eigenschaft seriell ausgeführt wird.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] versucht, alle auszuführen **Prozess** Befehle enthalten, die der **parallele** Eigenschaft parallel, aber gewährleisten, dass alle enthaltenen kann nicht **Prozess** Befehle parallel ausgeführt werden können. Die Instanz analysiert jeden **Prozess** Befehl und, wenn die Instanz ermittelt, dass der Befehl nicht parallel ausgeführt werden darf nicht der **Prozess** Befehl in Serie ausgeführt wird.  
  
> [!NOTE]  
>  Befehle parallel ausführen der **Transaktion** Attribut des der **Batch** Befehl muss festgelegt werden, da true [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] unterstützt nur eine aktive Transaktion pro Verbindung und nicht transaktionalen Batches jeden Befehl in einer separaten Transaktion ausgeführt. Wenn Sie enthalten die **parallele** -Eigenschaft in einem nicht transaktionalen Batch, ein Fehler auftritt.  
  
### <a name="limiting-parallel-execution"></a>Beschränken paralleler Ausführung  
 Ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Instanz versucht, so viele ausführen **Prozess** Befehle parallel wie möglich bis zu den Grenzwerten des Computers, auf dem die Instanz ausgeführt wird. Sie können die Anzahl der gleichzeitig ausgeführten **Prozess** Befehle durch Festlegen der **MaxParallel** Attribut des der **parallele** -Eigenschaft auf einen Wert, der angibt, die maximale Anzahl von **Prozess** Befehle, die parallel ausgeführt werden können.  
  
 Z. B. eine **parallele** Eigenschaft enthält die folgenden Befehle in der aufgeführten Reihenfolge:  
  
1.  **Create**  
  
2.  **Verarbeiten**  
  
3.  **Alter**  
  
4.  **Verarbeiten**  
  
5.  **Verarbeiten**  
  
6.  **Verarbeiten**  
  
7.  **Delete**  
  
8.  **Verarbeiten**  
  
9. **Verarbeiten**  
  
 Die **MaxParalle**l-Attribut dieses **parallele** -Eigenschaft auf 2 festgelegt ist. Daher führt die Instanz die vorherige Liste der Befehle wie in der folgenden Liste beschrieben aus:  
  
-   Befehl 1 wird seriell ausgeführt, da Befehl 1 ein **erstellen** Befehl und nur **Prozess** Befehle parallel ausgeführt werden können.  
  
-   Befehl 2 wird seriell ausgeführt, nachdem Befehl 1 abgeschlossen wurde.  
  
-   Befehl 3 wird seriell ausgeführt, nachdem Befehl 2 abgeschlossen wurde.  
  
-   Die Befehle 4 und 5, die parallel ausgeführt werden, nachdem Befehl 3 abgeschlossen ist. Obwohl Befehl 6 auch ist ein **Prozess** Befehl 6-Befehl kann nicht parallel mit Befehlen 4 und 5 ausgeführt, weil die **MaxParallel** -Eigenschaft auf 2 festgelegt ist.  
  
-   Befehl 6 wird seriell ausgeführt, nachdem die Befehle 4 und 5 abgeschlossen wurden.  
  
-   Befehl 7 wird seriell ausgeführt, nachdem Befehl 6 abgeschlossen wurde.  
  
-   Die Befehle 8 und 9 werden parallel ausgeführt, nachdem Befehl 7 abgeschlossen wurde.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Verwenden des Batchbefehls für die Verarbeitung von Objekten  
 Die **Batch** -Befehl enthält mehrere optionale Eigenschaften und Attribute, die speziell zur Unterstützung von enthalten Verarbeitung mehrerer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Projekte:  
  
-   Die **ProcessAffectedObjects** Attribut des der **Batch** Befehl gibt an, ob die Instanz ebenfalls Objekte verarbeiten soll, die eine erneute Verarbeitung als Ergebnis des erfordert eine **Prozess** Befehl enthalten der **Batch** -Befehl für die Verarbeitung eines angegebenen Objekts.  
  
-   Die [Bindungen](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) Eigenschaft enthält eine Auflistung von Out-of-Line-Bindungen, die von allen verwendet die **Prozess** Befehle in der **Batch** Befehl.  
  
-   Die [DataSource](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md) Eigenschaft enthält eine Out-of-Line-Bindung für eine Datenquelle, die von allen verwendet die **Prozess** Befehle in der **Batch** Befehl.  
  
-   Die [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) Eigenschaft enthält eine Out-of-Line-Bindung für eine Datenquellensicht, die von allen verwendet die **Prozess** Befehle in der **Batch** Befehl.  
  
-   Die [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) Eigenschaft gibt an, wie in der die **Batch** Befehl behandelt alle aufgetretenen Fehler **Prozess** in der enthaltenenBefehle**Batch** Befehl.  
  
    > [!IMPORTANT]  
    >  Ein **Prozess** -Befehl kann nicht einschließen der **Bindungen**, **DataSource**, **DataSourceView**, oder **ErrorConfiguration**  Eigenschaften, wenn die **Prozess** Befehl befindet sich einem **Batch** Befehl. Wenn Sie diese Eigenschaften angeben, müssen eine **Prozess** Befehl, geben Sie die erforderlichen Informationen in den entsprechenden Eigenschaften der **Batch** Befehl, der die **Prozess** Befehl.  
  
## <a name="see-also"></a>Siehe auch  
 [Batch-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Process-Element &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)   
 [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
