---
title: Rangfolgeneinschränkungen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.precedenceconstraint.f1
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- control flow [Integration Services], precedence constraints
- precedence constraints [Integration Services]
- constraints [Integration Services]
- sequence execution options [Integration Services]
- containers [Integration Services], precedence constraints
ms.assetid: c5ce5435-fd89-4156-a11f-68470a69aa9f
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7083cfe62823e790d51b323af4b50c1c31a22f85
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="precedence-constraints"></a>Rangfolgeneinschränkungen
  Rangfolgeneinschränkungen verknüpfen ausführbare Dateien, Container und Tasks in Paketen in einer Ablaufsteuerung und geben Bedingungen an, die bestimmen, ob ausführbare Dateien ausgeführt werden. Bei einer ausführbaren Datei kann es sich um einen For-Schleifencontainer, einen Foreach-Schleifencontainer, einen Task oder einen Ereignishandler handeln. Ereignishandler verwenden Rangfolgeneinschränkungen zum Verlinken der ausführbaren Dateien zu einer Ablaufsteuerung.  
  
 Eine Rangfolgeneinschränkung verlinkt zwei ausführbare Dateien: die ausführbare Datei der Rangfolge und die eingeschränkte ausführbare Datei. Die ausführbare Datei der Rangfolge wird vor der eingeschränkten ausführbaren Datei ausgeführt, und das Ausführungsergebnis der ausführbaren Datei der Rangfolge kann bestimmen, ob die eingeschränkte ausführbare Datei ausgeführt wird. Im folgenden Diagramm werden zwei ausführbare Dateien dargestellt, die durch eine Rangfolgeneinschränkung verlinkt sind.  
  
 ![Ausführbare Dateien, die durch eine Rangfolgeneinschränkung verlinkt sind](../../integration-services/control-flow/media/ssis-pcsimple.gif "Ausführbare Dateien, die durch eine Rangfolgeneinschränkung verlinkt sind")  
  
 Bei einer linearen Ablaufsteuerung, also einer Ablaufsteuerung ohne Verzweigungen, bestimmen Rangfolgeneinschränkungen alleine die Reihenfolge, in der Tasks ausgeführt werden. Falls sich eine Ablaufsteuerung verzweigt, bestimmt das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Laufzeitmodul die Ausführungsreihenfolge für die Tasks und Container, die unmittelbar auf die Verzweigung folgen. Das Laufzeitmodul bestimmt außerdem die Ausführungsreihenfolge für nicht verbundene Workflows in einer Ablaufsteuerung.  
  
 Die geschachtelte Containerarchitektur von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ermöglicht allen Containern (mit Ausnahme des Taskhostcontainers, der nur einen einzelnen Task kapselt), andere Container mit jeweils eigener Ablaufsteuerung einzuschließen. Der For-Schleifencontainer, der Foreach-Schleifencontainer und der Sequenzcontainer können mehrere Tasks und andere Container, die wiederum mehrere Tasks und Container enthalten können, einschließen. Angenommen, ein Paket mit einem Skripttask und einem Sequenzcontainer weist eine Rangfolgeneinschränkung auf, die den Skripttask und den Sequenzcontainer verlinkt. Der Sequenzcontainer schließt drei Skripttasks ein, und die Rangfolgeneinschränkungen verlinken die drei Skripttasks zu einer Ablaufsteuerung. Im folgenden Diagramm werden die Rangfolgeneinschränkungen in einem Paket mit zwei Schachtelungsebenen dargestellt.  
  
 ![Rangfolgeneinschränkungen in einem Paket](../../integration-services/control-flow/media/mw-dts-12.gif "Rangfolgeneinschränkungen in einem Paket")  
  
 Das Paket befindet sich ganz oben in der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Containerhierarchie. Deshalb können mehrere Pakete nicht durch Rangfolgeneinschränkungen verlinkt werden. Sie können jedoch einem Paket einen Task Paket ausführen hinzufügen und indirekt ein anderes Paket mit der Ablaufsteuerung verlinken.  
  
 Es gibt folgende Möglichkeiten, um Rangfolgeneinschränkungen zu konfigurieren:  
  
-   Geben Sie einen Auswertungsvorgang an. Die Rangfolgeneinschränkung verwendet einen Einschränkungswert und/oder einen Ausdruck, um zu bestimmen, ob die eingeschränkte ausführbare Datei ausgeführt wird.  
  
-   Falls die Rangfolgeneinschränkung ein Ausführungsergebnis verwendet, können Sie als Ausführungsergebnis Erfolg, Fehler oder Beendigung angeben.  
  
-   Falls die Rangfolgeneinschränkung ein Auswertungsergebnis verwendet, können Sie einen Ausdruck angeben, der zu einem booleschen Wert ausgewertet wird.  
  
-   Geben Sie an, ob die Rangfolgeneinschränkung einzeln oder zusammen mit anderen Einschränkungen, die auf die eingeschränkte ausführbare Datei zutreffen, ausgewertet wird.  
  
## <a name="evaluation-operations"></a>Auswertungsvorgänge  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt die folgenden Auswertungsvorgänge bereit:  
  
-   Eine Einschränkung, die nur mithilfe des Ausführungsergebnisses der ausführbaren Datei der Rangfolge bestimmt, ob die eingeschränkte ausführbare Datei ausgeführt wird. Das Ausführungsergebnis der ausführbaren Datei der Rangfolge kann Beendigung, Erfolg oder Fehler sein. Dies ist der Standardvorgang.  
  
-   Einen Ausdruck, der ausgewertet wird, um zu bestimmen, ob die eingeschränkte ausführbare Datei ausgeführt wird. Falls der Ausdruck zu True ausgewertet wird, wird die eingeschränkte ausführbare Datei ausgeführt.  
  
-   Einen Ausdruck und eine Einschränkung, die die Anforderungen von Ausführungsergebnissen der ausführbaren Datei der Rangfolge mit den zurückgegebenen Ergebnisse aus der Auswertung des Ausdrucks kombiniert.  
  
-   Einen Ausdruck oder eine Einschränkung, der bzw. die die Ausführungsergebnisse der ausführbaren Datei der Rangfolge oder die zurückgegebenen Ergebnisse aus der Auswertung des Ausdrucks verwendet.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer identifiziert mithilfe einer Farbcodierung den Typ der Rangfolgeneinschränkung. Die Success-Einschränkung ist grün, die Failure-Einschränkung ist rot und die Completion-Einschränkung ist blau. Zum Anzeigen von Beschriftungen im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer, die den Typ der Einschränkung anzeigen, müssen Sie die Barrierefreiheitsfunktionen des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers konfigurieren.  
  
 Der Ausdruck muss ein gültiger [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Ausdruck sein, der Funktionen, Operatoren sowie Systemvariablen und benutzerdefinierte Variablen einschließen kann. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) und [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="execution-results"></a>Ausführungsergebnisse  
 Die Rangfolgeneinschränkung kann die folgenden Ausführungsergebnisse separat oder in Kombination mit einem Ausdruck verwenden.  
  
-   Für die Beendigung muss die ausführbare Datei der Rangfolge ungeachtet des Ergebnisses abgeschlossen worden sein, damit die eingeschränkte ausführbare Datei ausgeführt wird.  
  
-   Für Erfolg muss die ausführbare Datei der Rangfolge erfolgreich abgeschlossen worden sein, damit die eingeschränkte ausführbare Datei ausgeführt wird.  
  
-   Für Fehler muss bei der ausführbaren Datei der Rangfolge ein Fehler auftreten, damit die eingeschränkte ausführbare Datei ausgeführt wird.  
  
> [!NOTE]  
>  Nur Rangfolgeneinschränkungen, die Elemente derselben **Precedence Constraint** -Auflistung sind, können mit einer logischen AND-Bedingung gruppiert werden. Beispielsweise können Rangfolgeneinschränkungen aus zwei Foreach-Schleifencontainern nicht kombiniert werden.  
  
## <a name="set-the-properties-of-a-precedence-constraint-with-the-precedence-constraint-editor"></a>Festlegen der Eigenschaften von Rangfolgeneinschränkungen mithilfe des Rangfolgeneinschränkungs-Editors  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Doppelklicken Sie auf die Rangfolgeneinschränkung.  
  
     Das Dialogfeld **Rangfolgeneinschränkungs-Editor** wird geöffnet.  
  
5.  Wählen Sie in der Dropdownliste **Auswertungsvorgang** einen Auswertungsvorgang aus.  
  
6.  Wählen Sie in der Dropdownliste **Wert** das Ausführungsergebnis der ausführbaren Datei der Rangfolge aus.  
  
7.  Wenn der Auswertungsvorgang einen Ausdruck verwendet, geben Sie in das Feld **Ausdruck** einen Ausdruck ein, und klicken Sie auf **Testen** , um den Ausdruck auszuwerten.  
  
    > [!NOTE]  
    >  Bei Variablennamen wird nach Groß-/Kleinschreibung unterschieden.  
  
8.  Falls mehrere Tasks oder Container mit der eingeschränkten ausführbaren Datei verbunden sind, wählen Sie **Logisches AND** aus, um anzugeben, dass die Ausführungsergebnisse aller vorherigen ausführbaren Dateien zu **true**ausgewertet werden müssen. Wählen Sie **Logisches OR** aus, um anzugeben, dass nur ein Ausführungsergebnis zu **true**ausgewertet werden muss.  
  
9. Klicken Sie auf **OK** , um das Dialogfeld **Rangfolgeneinschränkungs-Editor**zu schließen.  
  
10. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="precedence-constraint-editor"></a>Rangfolgeneinschränkungs-Editor
Verwenden Sie das Dialogfeld **Rangfolgeneinschränkungs-Editor** , um Rangfolgeneinschränkungen zu konfigurieren.  
  
### <a name="options"></a>Tastatur  
 **Auswertungsvorgang**  
 Geben Sie den Auswertungsvorgang an, den die Rangfolgeneinschränkung verwendet. Dazu zählen die folgenden Vorgänge: **Einschränkung**, **Ausdruck**, **Ausdruck und Einschränkung**und **Ausdruck oder Einschränkung**.  
  
 **ReplTest1**  
 Geben Sie den Einschränkungswert an: **Erfolg**, **Fehler**oder **Beendigung**.  
  
> [!NOTE]  
>  Die Rangfolgeneinschränkungslinie wird bei **Erfolg**grün, bei einem **Fehler**hervorgehoben und bei **Beendigung**blau dargestellt.  
  
 **Ausdruck**  
 Wenn Sie den Vorgang **Ausdruck**, **Ausdruck und Einschränkung**oder **Ausdruck oder Einschränkung**verwenden, geben Sie einen Ausdruck ein, oder starten Sie den Ausdrucks-Generator, um einen Ausdruck zu erstellen. Der Ausdruck muss zu einem booleschen Wert ausgewertet werden.  
  
 **Testen**  
 Überprüfen Sie den Ausdruck.  
  
 **Logisches AND**  
 Damit geben Sie an, dass für die ausführbare Datei mehrere Rangfolgeneinschränkungen gemeinsam überprüft werden müssen. Sämtliche Einschränkungen müssen mit **True**ausgewertet werden.  
  
> [!NOTE]  
>  Dieser Typ der Rangfolgeneinschränkung wird als durchgehende grüne, hervorgehobene oder blaue Linie dargestellt.  
  
 **Logisches OR**  
 Damit geben Sie an, dass für die ausführbare Datei mehrere Rangfolgeneinschränkungen gemeinsam überprüft werden müssen. Mindestens eine Einschränkung muss mit **True**ausgewertet werden.  
  
> [!NOTE]  
>  Dieser Typ der Rangfolgeneinschränkung wird als gepunktete grüne, hervorgehobene oder blaue Linie dargestellt.  
  
## <a name="set-the-properties-of-a-precedence-constraint-in-properties-window"></a>Festlegen der Eigenschaften von Rangfolgeneinschränkungen mithilfe des Eigenschaftenfensters  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem Paket, das Sie ändern möchten.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** . Klicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf Rangfolgeneinschränkung, und klicken Sie auf **Eigenschaften**. Ändern Sie im Fenster Eigenschaften die Eigenschaftswerte.  
  
4.  Legen Sie im Fenster **Eigenschaften** die folgenden Lese-/Schreibeigenschaften der Rangfolgeneinschränkung fest:  
  
    |Lese/Schreibeigenschaft|Konfigurationsaktion|  
    |--------------------------|--------------------------|  
    |Description|Bereitstellen einer Beschreibung.|  
    |EvalOp|Auswählen eines Auswertungsvorgangs. Wenn die Vorgänge **Expression**, **ExpressionAndConstant**oder **ExpressionOrConstant** ausgewählt sind, können Sie einen Ausdruck angeben.|  
    |Ausdruck|Wenn der Auswertungsvorgang einen Ausdruck einschließt, wird ein Ausdruck bereitgestellt. Der Ausdruck muss zu einem booleschen Wert ausgewertet werden. Weitere Informationen zur Ausdruckssprache finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).|  
    |LogicalAnd|Legen Sie **LogicalAnd** fest, um anzugeben, ob die Rangfolgeneinschränkung zusammen mit anderen Rangfolgeneinschränkungen ausgewertet wird, wenn mehrere ausführbare Dateien vorausgehen und mit der eingeschränkten ausführbaren Datei verlinkt sind.|  
    |Name|Aktualisieren des Namens der Rangfolgeneinschränkung.|  
    |ShowAnnotation|Geben Sie den Typ der zu verwendenden Anmerkung ein. Wählen Sie **Never** aus, um Anmerkungen zu deaktivieren, **AsNeeded** , um Anmerkungen bei Bedarf zu aktivieren, **ConstraintName** , um automatisch den Wert mithilfe der Name-Eigenschaft anzumerken, **ConstraintDescription** , um automatisch den Wert mithilfe der Description-Eigenschaft anzumerken, und **ConstraintOptions** , um automatisch den Wert mithilfe der Eigenschaften Value und Expression anzumerken.|  
    |value|Wenn der Auswertungsvorgang in der EvalOP-Eigenschaft eine Einschränkung enthält, wählen Sie das Ausführungsergebnis der eingeschränkten ausführbaren Datei aus.|  
  
5.  Schließen Sie das Fenster Eigenschaften.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="set-the-value-of-a-precedence-constraint-with-the-shortcut-menu"></a>Festlegen des Werts einer Rangfolgeneinschränkung mithilfe des Kontextmenüs  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf die Rangfolgeneinschränkung, und klicken Sie dann auf **Erfolg**, **Fehler**oder **Beendigung**.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="add-expressions-to-precedence-constraints"></a>Hinzufügen von Ausdrücken zu Rangfolgeneinschränkungen
 Eine Rangfolgeneinschränkung kann mithilfe eines Ausdrucks die Einschränkung zwischen zwei ausführbaren Dateien definieren, nämlich der ausführbaren Datei der Rangfolge und der eingeschränkten ausführbaren Datei. Bei den ausführbaren Dateien kann es sich um Tasks oder Container handeln. Der Ausdruck kann separat oder in Kombination mit dem Ausführungsergebnis der ausführbaren Datei der Rangfolge verwendet werden. Das Ausführungsergebnis einer ausführbaren Datei ist Erfolg oder Fehler. Wenn Sie das Ausführungsergebnis einer Rangfolgeneinschränkung konfigurieren, können Sie das Ausführungsergebnis auf **Success**, **Failure**oder **Completion**festlegen. Für**Success** muss die ausführbare Datei der Rangfolge erfolgreich ausgeführt werden, für **Failure** muss die ausführbare Datei der Rangfolge mit einem Fehler ausgeführt werden. **Completion** zeigt an, dass die eingeschränkte ausführbare Datei unabhängig von einer erfolgreichen Ausführung des Rangfolgentasks ausgeführt werden sollte. Weitere Informationen finden Sie unter [Rangfolgeneinschränkungen](../../integration-services/control-flow/precedence-constraints.md).  
  
 Der Ausdruck muss zu **Wahr** oder **Falsch** ausgewertet werden, und er muss ein gültiger [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Ausdruck sein. Für diesen Ausdruck sind Literale, Systemvariablen und benutzerdefinierte Variablen sowie die Funktionen und Operatoren zulässig, die von der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Ausdrucksgrammatik bereitgestellt werden. Beispielsweise verwendet der Ausdruck `@Count == SQRT(144) + 10` die **Count**-Variable, die SQRT-Funktion und die Operatoren „equal“ (==) und „add“ (+) . Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)ausgewertet wird.  
  
 In der folgenden Abbildung sind Task A und Task B durch eine Rangfolgeneinschränkung miteinander verlinkt, die ein Ausführungsergebnis und einen Ausdruck verwendet. Der Einschränkungswert ist auf **Success** festgelegt, und der Ausdruck lautet  `@X >== @Z`. Task B, der eingeschränkte Task, wird nur ausgeführt, wenn Task A erfolgreich abgeschlossen wird und der Wert der **X** -Variablen größer oder gleich dem Wert der **Z**-Variablen ist.  
  
 ![Rangfolgeneinschränkung zwischen zwei Tasks](../../integration-services/control-flow/media/mw-dts-03.gif "Rangfolgeneinschränkung zwischen zwei Tasks")  
  
 Ausführbare Dateien können auch mithilfe mehrerer Rangfolgeneinschränkungen miteinander verlinkt werden, die unterschiedliche Ausdrücke enthalten. Beispielsweise sind in der folgenden Abbildung Task B und Task C mit Task A durch Rangfolgeneinschränkungen verlinkt, die Ausführungsergebnisse und Ausdrücke verwenden. Beide Einschränkungswerte sind auf **Success**festgelegt. festgelegt. Eine Rangfolgeneinschränkung enthält den Ausdruck `@X >== @Z`, und die andere Rangfolgeneinschränkung den Ausdruck `@X < @Z`. In Abhängigkeit von den Werten der **X** -Variablen und der **Z**-Variablen wird Task C oder Task B ausgeführt.  
  
 ![Ausdrücke für Rangfolgeneinschränkungen](../../integration-services/control-flow/media/mw-dts-04.gif "Ausdrücke für Rangfolgeneinschränkungen")  
  
 Mit dem **Rangfolgeneinschränkungs-Editor** im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer und im Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] können Sie einen Ausdruck hinzufügen oder ändern. Das Eigenschaftenfenster ermöglicht jedoch keine Überprüfung der Ausdruckssyntax.  
  
 Wenn eine Rangfolgeneinschränkung einen Ausdruck einschließt, wird auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** neben der Rangfolgeneinschränkung ein Symbol angezeigt, und die QuickInfo auf dem Symbol zeigt den Ausdruck an.  

### <a name="add-an-expression-to-a-precedence-constraint"></a>Hinzufügen einer Rangfolgeneinschränkung zu einem Ausdruck  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Doppelklicken Sie auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** auf die Rangfolgeneinschränkung. Das Dialogfeld **Rangfolgeneinschränkungs-Editor** wird geöffnet.  
  
5.  Wählen Sie **Ausdruck**, **Ausdruck und Einschränkung**oder **Ausdruck oder Einschränkung** in der Liste **Auswertungsvorgang** aus.  
  
6.  Geben Sie in das Textfeld **Ausdruck** einen Ausdruck ein, oder starten Sie den Ausdrucks-Generator, um einen Ausdruck zu erstellen.  
  
7.  Klicken Sie auf **Testen**, um die Ausdruckssyntax zu überprüfen.  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
 
### <a name="combine-execution-values-and-expressions"></a>Kombinieren von Ausführungswerten und Ausdrücken  
 In der folgenden Tabelle werden die Auswirkung durch das Kombinieren einer Ausführungswerteinschränkung und eines Ausdrucks in einer Rangfolgeneinschränkung beschrieben.  
  
|Auswertungsvorgang|Einschränkung wird ausgewertet zu|Ausdruck wird ausgewertet zu|Eingeschränkte ausführbare Datei wird ausgeführt|  
|--------------------------|-----------------------------|-----------------------------|---------------------------------|  
|Einschränkung|Wahr|–|Wahr|  
|Einschränkung|False|–|False|  
|expression|–|Wahr|Wahr|  
|expression|–|False|False|  
|Einschränkung und Ausdruck|Wahr|Wahr|Wahr|  
|Einschränkung und Ausdruck|Wahr|Falsch|False|  
|Einschränkung und Ausdruck|False|Wahr|False|  
|Einschränkung und Ausdruck|False|False|False|  
|Einschränkung oder Ausdruck|Wahr|Wahr|Wahr|  
|Einschränkung oder Ausdruck|Wahr|False|Wahr|  
|Einschränkung oder Ausdruck|False|Wahr|Wahr|  
|Einschränkung oder Ausdruck|False|False|False|  


## <a name="complex-constraint-scenarios-with-multiple-precedence-constraints"></a>Komplexe Einschränkungsszenarien mit mehreren Rangfolgeneinschränkungen 
Eine Rangfolgeneinschränkung verbindet zwei ausführbare Dateien: zwei Tasks, zwei Container oder einen Task und einen Container. Sie werden als ausführbare Datei der Rangfolge und als eingeschränkte ausführbare Datei bezeichnet. Eine eingeschränkte ausführbare Datei kann mehrere Rangfolgeneinschränkungen haben. Weitere Informationen finden Sie unter [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md).  
  
 Wenn Sie komplexe Einschränkungsszenarien durch Gruppieren von Einschränkungen zusammenfassen, können Sie eine komplexe Ablaufsteuerung in Paketen implementieren. Beispielsweise ist in der folgenden Abbildung der Task D mit dem Task A durch eine **Success** -Einschränkung verlinkt, der Task D ist mit dem Task B durch eine **Failure** -Einschränkung verlinkt, und der Task D ist mit dem Task C durch eine **Success** -Einschränkung verlinkt. Die Rangfolgeneinschränkungen zwischen Task D und Task A, zwischen Task D und Task B sowie zwischen Task D und Task C nehmen an einer logischen *AND* -Beziehung teil. Damit Task D ausgeführt wird, muss Task A erfolgreich ausgeführt werden, bei Task B muss ein Fehler auftreten, und Task C muss erfolgreich ausgeführt werden.  
  
 ![Durch Rangfolgeneinschränkungen verknüpfte Tasks](../../integration-services/control-flow/media/precedenceconstraints.gif "Durch Rangfolgeneinschränkungen verknüpfte Tasks")  
  
### <a name="logicaland-property"></a>LogicalAnd-Eigenschaft  
 Falls ein Task oder ein Container mehrere Einschränkungen aufweist, gibt die **LogicalAnd** -Eigenschaft an, ob eine Rangfolgeneinschränkung einzeln oder zusammen mit anderen Einschränkungen ausgewertet wird.  
  
 Sie können die **LogicalAnd**-Eigenschaft mithilfe des **Rangfolgeneinschränkungs-Editors** im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer oder im Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] festlegen.  

## <a name="set-the-default-value-for-precedence-constraints"></a>Festlegen des Standardwerts für Rangfolgeneinschränkungen  
Wenn Sie den [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zum ersten Mal verwenden, lautet der Standardwert einer Rangfolgeneinschränkung **Erfolg**. Führen Sie die folgenden Schritte aus, um für den [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer einen anderen Standardwert für Rangfolgeneinschränkungen zu konfigurieren.
  
1.  Öffnen Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
3.  Erweitern Sie im Dialogfeld **Optionen** den Ordner **Business Intelligence-Designer** , und erweitern Sie dann **Integration Services-Designer**.  
  
4.  Klicken Sie auf **Automatische Ablaufsteuerungsverbindung** , und aktivieren Sie das Kontrollkästchen **Neue Form standardmäßig mit der ausgewählten Form verbinden**.  
  
5.  Wählen Sie in der Dropdownliste **Failure-Einschränkung für die neue Form verwenden** oder **Completion-Einschränkung für die neue Form verwenden**aus.  
  
6.  Klicken Sie auf **OK**.  
  
## <a name="create-a-default-precedence-constraint"></a>Erstellen einer Standard-Rangfolgeneinschränkung  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** .  
  
4.  Klicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** auf den Task oder Container, und ziehen Sie dessen Konnektor auf die ausführbare Datei, auf die Sie die Rangfolgeneinschränkung anwenden möchten.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
