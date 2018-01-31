---
title: Integration Services-Variablen (SSIS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 141b245a49e1d2fa6f83b886c70c159ab089c2fa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-ssis-variables"></a>Integration Services-Variablen (SSIS)
  Variablen speichern Werte, die von einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket und dessen Containern, Tasks und Ereignishandlern zur Laufzeit verwendet werden können. Die Skripts im Skripttask und die Skriptkomponente können ebenfalls Variablen verwenden. Die Rangfolgeneinschränkungen, mit denen Tasks und Container zu einem Workflow zusammengestellt werden, können Variablen verwenden, wenn ihre Einschränkungsdefinitionen Ausdrücke einschließen.  
  
 Variablen in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paketen können für folgende Zwecke verwendet werden:  
  
-   Aktualisieren der Eigenschaften von Paketelementen zur Laufzeit. Beispielsweise können Sie die von einem Foreach-Schleifencontainer zulässige Anzahl von gleichzeitig ausführbaren Dateien dynamisch festlegen.  
  
-   Einschließen einer Nachschlagetabelle im Arbeitsspeicher. Beispielsweise kann von einem Paket ein Task SQL ausführen ausgeführt werden, der eine Variable mit Datenwerten lädt.  
  
-   Laden von Variablen mit Datenwerten und anschließend mit deren Hilfe Angeben einer Suchbedingung in einer WHERE-Klausel. Beispielsweise kann das Skript eines Skripttasks den Wert einer Variablen aktualisieren, die von einer Transact-SQL-Anweisung in einem Task SQL ausführen verwendet wird.  
  
-   Laden einer Variablen mit einer ganzen Zahl und anschließend Steuern der Schleifen in einer Paketablaufsteuerung mithilfe dieses Werts. Beispielsweise können Sie im Auswertungsausdruck eines For-Schleifencontainers die Iteration mithilfe einer Variablen steuern.  
  
-   Auffüllen von Parameterwerten für Transact-SQL-Anweisungen zur Laufzeit. Beispielsweise kann ein Paket einen Task SQL ausführen ausführen und anschließend die Parameter einer Transact-SQL-Anweisung mithilfe von Variablen dynamisch festlegen.  
  
-   Erstellen von Ausdrücken, die Variablenwerte einschließen. Beispielsweise kann die Transformation für abgeleitete Spalten eine Spalte mit dem Ergebnis aus dem Multiplizieren eines Variablenwerts mit einem Spaltenwert auffüllen.  
  
## <a name="system-and-user-defined-variables"></a>Systemvariablen und benutzerdefinierte Variablen  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] unterstützt zwei Arten von Variablen: Benutzerdefinierte Variablen und Systemvariablen. Benutzerdefinierte Variablen werden von Paketentwicklern definiert, und Systemvariablen werden von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]definiert. Sie können so viele benutzerdefinierte Variablen erstellen, wie für das Paket erforderlich sind. Zusätzliche Systemvariablen können jedoch nicht erstellt werden.  
  
 Alle Variablen, seien es Systemvariablen oder benutzerdefinierte Variablen, können in den Parameterbindungen verwendet werden, die der Task SQL ausführen zum Zuordnen von Variablen zu Parametern in SQL-Anweisungen verwendet. Weitere Informationen finden Sie unter [SQL ausführen (Task)](../integration-services/control-flow/execute-sql-task.md) und [Parameter und Rückgabecodes im Task „SQL ausführen“](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
> [!NOTE]  
>  Bei den Namen von benutzerdefinierten und Systemvariablen wird nach Groß-/Kleinschreibung unterschieden.  
  
 Sie können benutzerdefinierte Variablen für alle [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Containertypen erstellen: Pakete, Foreach-Schleifencontainer, For-Schleifencontainer, Sequenzcontainer, Tasks und Ereignishandler. Bei benutzerdefinierten Variablen handelt es sich um Elemente der Variables-Auflistung des Containers.  
  
 Wenn Sie das Paket mit dem [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer erstellen, können Sie die Elemente der **Variables** -Auflistung im Ordner Variablen auf der Registerkarte **Paket-Explorer** des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers anzeigen. Die Ordner listen benutzerdefinierte Variablen und Systemvariablen auf.  
  
 Es gibt folgende Möglichkeiten, um benutzerdefinierte Variablen zu konfigurieren:  
  
-   Geben Sie einen Namen und eine Beschreibung für die Variable an.  
  
-   Geben Sie einen Namespace für die Variable an.  
  
-   Geben Sie an, ob die Variable ein Ereignis auslöst, wenn ihr Wert geändert wird.  
  
-   Geben Sie an, ob die Variable schreibgeschützt ist oder Lese-/Schreibzugriff aufweist.  
  
-   Verwenden Sie das Auswertungsergebnis eines Ausdrucks zum Festlegen des Variablenwerts.  
  
-   Erstellen Sie die Variable im Bereich des Pakets oder eines Paketobjekts, wie z. B. eines Tasks.  
  
-   Geben Sie den Wert und den Datentyp der Variablen an.  
  
 Die einzige konfigurierbare Option für Systemvariablen ist das Angeben, ob sie ein Ereignis auslösen, wenn sich der Wert ändert.  
  
 Ein anderer Systemvariablensatz ist für andere Containertypen verfügbar. Weitere Informationen zu den Systemvariablen, die von Paketen und deren Elementen verwendet werden, finden Sie unter [Systemvariablen](../integration-services/system-variables.md).  
  
 Weitere Informationen zu Szenarien für die Verwendung von Variablen in der Praxis finden Sie unter [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="properties-of-variables"></a>Eigenschaften von Variablen  
 Sie können benutzerdefinierte Variablen konfigurieren, indem Sie die folgenden Eigenschaften im Fenster **Variablen** oder im Fenster **Eigenschaften** festlegen. Bestimmte Eigenschaften sind nur im Eigenschaftenfenster verfügbar.  
  
> [!NOTE]  
>  Die einzige konfigurierbare Option für Systemvariablen ist das Angeben, ob sie ein Ereignis auslösen, wenn sich der Wert ändert.  
  
 **Description**    
 Gibt die Beschreibung der Variablen an.  
  
 **EvaluateAsExpression**    
 Wenn die Eigenschaft auf **True**festgelegt wird, wird der bereitgestellte Ausdruck zum Festlegen des Variablenwerts verwendet.  
  
 **expression**    
 Gibt den der Variablen zugeordneten Ausdruck an.  
  
 **Name**    
 Gibt den Variablennamen an.  
  
 **Namespace**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt zwei Namespaces bereit: **User** und **System**. Standardmäßig gehören benutzerdefinierte Variablen zum Namespace **User** und Systemvariablen zum Namespace **System** . Sie können zusätzliche Namespaces für benutzerdefinierte Variablen erstellen und den Namen des **User** -Namespaces ändern. Es ist jedoch nicht möglich, den Namen des **System** -Namespaces zu ändern, dem **System** -Namespace Variablen hinzuzufügen oder Systemvariablen einem anderen Namespace zuzuweisen.  
  
**RaiseChangedEvent**  
 Wenn die Eigenschaft auf **True**festgelegt wird, wird das **OnVariableValueChanged** -Ereignis bei einer Änderung des Variablenwerts ausgelöst.  
  
 **ReadOnly**  
 Wenn die Eigenschaft auf **False**festgelegt wird, besteht ein Lese- und Schreibzugriff auf die Variable.  
  
**Scope**    
 > [!NOTE]  
>  Sie können diese Eigenschafteneinstellung nur ändern, indem Sie im Fenster **Variablen** auf **Variable verschieben** klicken.  
  
 Eine Variable wird im Bereich eines Pakets oder im Bereich eines Containers, Tasks oder Ereignishandlers im Paket erstellt. Der Paketcontainer befindet sich ganz oben in der Containerhierarchie. Deshalb verhalten sich Variablen mit Paketbereichsfunktion wie globale Variablen und können von allen Containern im Paket verwendet werden. Entsprechend können Variablen, die im Bereich eines Containers definiert sind, wie z. B. eines For-Schleifencontainers, von allen Tasks oder Containern innerhalb des For-Schleifencontainers verwendet werden.  
  
 Falls ein Paket mithilfe des Tasks Paket ausführen andere Pakete ausführt, können die Variablen, die im Bereich des aufrufenden Pakets oder des Tasks Paket ausführen definiert sind, dem aufgerufenen Paket mithilfe des Konfigurationstyps Variable für das übergeordnete Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Package Configurations](../integration-services/packages/package-configurations.md).  
  
**IncludeInDebugDump**  
 Geben Sie an, ob der Variablenwert in den Debugdumpdateien enthalten ist.  
  
 Für benutzerdefinierte Variablen und Systemvariablen ist **true** der Standardwert für die Option **InclueInDebugDump**.  
  
 Für benutzerdefinierte Variablen setzt das System die **IncludeInDebugDump** -Option jedoch auf **false** zurück, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Wenn die **EvaluateAsExpression** -Variableneigenschaft auf **true**festgelegt ist, setzt das System die **IncludeInDebugDump** -Option auf **false**zurück.  
  
     Um den Text des Ausdrucks als Variablenwert in die Debugdumpdatei einzuschließen, legen Sie die **IncludeInDebugDump** -Option auf **true**fest.  
  
-   Wenn der Datentyp der Variablen in eine Zeichenfolge umgewandelt wird, setzt das System die **IncludeInDebugDump** -Option auf **false**zurück.  
  
 Wenn das System die **IncludeInDebugDump** -Option auf **false**zurücksetzt, wird möglicherweise der vom Benutzer gewählte Wert überschrieben.  
  
**Wert**    
Der Wert einer benutzerdefinierten Variable kann ein Literal oder ein Ausdruck sein. Der Wert einer Variable darf nicht NULL sein. Variablen enthalten die folgenden Standardwerte:

| Datentyp | Standardwert |
|---|---|
| Boolean | False |
| numeric- und binary-Datentypen | 0 (Null) |
| Char- und String-Datentypen | (leere Zeichenfolge) |
| Objekt | System.Object |
| | |

Eine Variable enthält Optionen zum Festlegen des Variablenwerts und des Datentyps des Werts. Die beiden Eigenschaften müssen kompatibel sein. Beispielsweise ist das Verwenden eines string-Werts zusammen mit einem integer-Datentyp ungültig.  
  
 Falls die Variable so konfiguriert ist, dass sie als Ausdruck ausgewertet wird, müssen Sie einen Ausdruck angeben. Zur Laufzeit wird der Ausdruck ausgewertet, und die Variable wird auf das Auswertungsergebnis festgelegt. Wenn z. B. eine Variable den Ausdruck `DATEPART("month", GETDATE())` verwendet, entspricht der Wert der Variablen der Zahl des Monats im aktuellen Datum. Der Ausdruck muss ein gültiger Ausdruck sein, der die [!INCLUDE[ssIS](../includes/ssis-md.md)] -Ausdrucksgrammatiksyntax verwendet. Wenn ein Ausdruck mit Variablen verwendet wird, kann der Ausdruck Literale sowie die Operatoren und Funktionen der Ausdrucksgrammatik verwenden. Der Ausdruck kann jedoch nicht auf die Spalten in einem Datenfluss des Pakets verweisen. Die maximale Länge eines Ausdrucks beträgt 4000 Zeichen. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
**ValueType**    
 > [!NOTE]  
>  Der Eigenschaftswert wird in der Spalte **Datentyp** im Fenster **Variablen** angezeigt.  
  
 Gibt den Datentyp des Variablenwerts an.  

## <a name="scenarios-for-using-variables"></a>Szenarien für die Verwendung von Variablen  
 Variablen werden auf verschiedene Weisen in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paketen verwendet. Sie werden möglicherweise der Meinung sein, dass die Paketentwicklung nicht voranschreitet, bis Sie die benutzerdefinierten Variablen einem Paket hinzugefügt haben, um die benötigte Flexibilität und Verwaltbarkeit der Lösung zu implementieren. Abhängig von dem Szenario, werden die Systemvariablen gemeinsam verwendet.  
  
 **Eigenschaftsausdrücke** Verwenden von Variablen zum Bereitstellen von Werten in den Eigenschaftsausdrücken, die die Eigenschaften der Pakete und der Paketobjekte festlegen. Beispielsweise schließt der Ausdruck `SELECT * FROM @varTableName` die `varTableName` -Variable ein, die die SQL-Anweisung aktualisiert, die der Task SQL ausführen ausführt. Der `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`-Ausdruck aktualisiert das Paket, das der Task Paket ausführen ausführt. Dies erfolgt durch Ausführen des angegebenen Pakets in der `varPackageFirst` -Variablen am ersten Tag des Monats, und das angegebene Paket in der `varPackageOther` -Variable wird an anderen Tagen ausgeführt. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 **Datenflussausdrücke** Verwendet Variablen, um Werte in den Ausdrücken bereitzustellen, die die Transformationen Abgeleitete Spalten und Bedingtes Teilen zum Auffüllen der Spalten verwenden, oder um Datenzeilen an verschiedene Transformationsausgaben weiterzuleiten. Beispielsweise verkettet der `@varSalutation + LastName`-Ausdruck den Wert in der `VarSalutation` -Variablen und der `LastName` -Spalte. Der `Income < @HighIncome`-Ausdruck leitet Datenzeilen, in denen der Wert der `Income` -Spalte niedriger ist als der Wert in der `HighIncome` -Variablen an eine Ausgabe weiter. Weitere Informationen finden Sie unter [Transformation für abgeleitete Spalten](../integration-services/data-flow/transformations/derived-column-transformation.md), [Transformation für bedingtes Teilen](../integration-services/data-flow/transformations/conditional-split-transformation.md) und [Integration Services-Ausdrücke &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 **Rangfolgeneinschränkungs-Ausdrücke** Stellen Werte in Rangfolgeneinschränkungen bereit, um zu bestimmen, ob eine ausführbare Datei ausgeführt wird. Die Ausdrücke können entweder gemeinsam mit einem Ausführungsergebnis (Erfolg, Fehler, Beendigung) oder stattdessen mit einem Ausführungsergebnis verwendet werden. Wenn der Ausdruck `@varMax > @varMin`beispielsweise zu **TRUE**ausgewertet wird, werden die ausführbaren Dateien ausgeführt. Weitere Informationen finden Sie unter [Hinzufügen von Ausdrücken zu Rangfolgeneinschränkungen](http://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1).  
  
 **Parameter und Rückgabecode** Stellt Eingabeparametern Werte bereit oder speichert die Ausgabeparameter und den Rückgabecode. Dies erfolgt durch Zuordnen der Variablen zu Parametern und Rückgabewerten. Wenn sie beispielsweise die `varProductId` -Variable auf 23 festlegen und die `SELECT * from Production.Product WHERE ProductID = ?`-SQL-Anweisung ausführen, ruft die Abfrage das Produkt mit einer `ProductID` von 23 ab. Weitere Informationen finden Sie unter [SQL ausführen (Task)](../integration-services/control-flow/execute-sql-task.md) und [Parameter und Rückgabecodes im Task „SQL ausführen“](http://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).  
  
 **For-Schleifenausdrücke** Stellt Werte bereit, die bei der Initialisierung, bei der Auswertung und bei der Zuordnung von Ausdrücken für die For-Schleife verwendet werden. Wenn der Wert für die `varCount` -Variable beispielsweise 2 und der Wert für `varMaxCount` 10, der Initialisierungsausdruck `@varCount`, der Auswertungsausdruck  `@varCount < @varMaxCount`und der Zuordnungsausdruck `@varCount =@varCount +1`lautet, dann wiederholt sich die Schleife acht Mal. Weitere Informationen finden Sie unter [For Loop Container](../integration-services/control-flow/for-loop-container.md).  
  
 **Variablenkonfiguration für übergeordnete Pakete** Übergibt Werte von übergeordneten Paketen an untergeordnete Paketen. Untergeordnete Pakete können auf Variablen in übergeordneten Paketen mithilfe der Variablenkonfiguration für übergeordnete Pakete zugreifen. Wenn beispielsweise ein untergeordnetes Paket die gleichen Daten wie das übergeordnete Paket verwenden muss, kann das untergeordnete Paket eine Variablenkonfiguration definieren, die eine Variable angibt, die durch die GETDATE-Funktion in dem übergeordneten Paket festgelegt wurde. Weitere Informationen finden Sie unter [Execute Package Task](../integration-services/control-flow/execute-package-task.md) und [Package Configurations](../integration-services/packages/package-configurations.md).  
  
 **Skripttasks und Skriptkomponenten** Stellt eine Liste von schreibgeschützten und Lese-/Schreibvariablen für Skripttasks oder Skriptkomponenten bereit, aktualisiert die Lese/Schreibvariablen innerhalb des Skripts und verwendet dann die aktualisierten Werte innerhalb oder außerhalb des Skripts. Beispielsweise im `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`-Code wird die `numberOfCars` -Skriptvariable durch den Wert in der `NumberOfCars`-Variable aktualisiert. Weitere Informationen finden Sie unter [Using Variables in the Script Task](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md).  

## <a name="add-a-variable"></a>Hinzufügen einer Variable  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das gewünschte [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Gehen Sie im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer zum Definieren des Gültigkeitsbereichs der Variablen wie folgt vor:  
  
    -   Um den Gültigkeitsbereich des Pakets festzulegen, klicken Sie an eine beliebige Stelle auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** .  
  
    -   Um den Gültigkeitsbereich auf einen Ereignishandler festzulegen, wählen Sie eine ausführbare Datei und einen Ereignishandler auf der Entwurfsoberfläche der Registerkarte **Ereignishandler** aus.  
  
    -   Um den Gültigkeitsbereich auf einen Task oder Container festzulegen, klicken Sie auf der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** oder **Ereignishandler** auf einen Task oder Container.  
  
4.  Klicken Sie im Menü **SSIS** auf **Variablen**. Sie können das Fenster **Variablen** auch anzeigen, indem Sie im Dialogfeld **Optionen** auf der Seite **Tastatur** den Befehl View.Variables einer beliebigen Tastenkombination zuordnen.  
  
5.  Klicken Sie im Fenster **Variablen** auf das Symbol **Variable hinzufügen** . Die neue Variable wird der Liste hinzugefügt.  
  
6.  Klicken Sie wahlweise auf das Symbol **Rasteroptionen** , wählen Sie zusätzliche Spalten aus, die im Dialogfeld **Variable Rasteroptionen** angezeigt werden sollen, und klicken Sie dann auf **OK**.  
  
7.  Legen Sie optional die Variableneigenschaften fest. Weitere Informationen finden Sie unter [Festlegen der Eigenschaften von benutzerdefinierten Variablen](http://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f).  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

### <a name="add-variable-dialog-box"></a>Variable hinzufügen (Dialogfeld)
Mithilfe des Dialogfelds **Variable hinzufügen** können Sie die Eigenschaften einer neuen Variablen angeben.  
  
#### <a name="options"></a>Tastatur  
 **Container**  
 Wählen Sie in der Liste einen Container aus. Der Container definiert den Gültigkeitsbereich der Variablen. Der Container kann entweder das Paket oder eine im Paket enthaltene ausführbare Datei sein.  
  
 **Name**  
 Geben Sie den Variablennamen ein.  
  
 **Namespace**  
 Geben Sie den Namespace der Variablen an. Benutzerdefinierte Variablen befinden sich standardmäßig im **Benutzer** -Namespace.  
  
 **Werttyp**  
 Wählen Sie einen Datentyp aus.  
  
 **ReplTest1**  
 Geben Sie einen Wert ein. Der Wert muss mit dem unter der Option **Werttyp** angegebenen Datentyp kompatibel sein.  
  
 **Schreibgeschützt**  
 Wählen Sie diese Option aus, wenn die Variable schreibgeschützt sein soll.  
   
## <a name="delete-a-variable"></a>Löschen einer Variable  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im Menü **SSIS** auf **Variablen**. Sie können das Fenster **Variablen** auch anzeigen, indem Sie im Dialogfeld **Optionen** auf der Seite **Tastatur** den Befehl View.Variables einer beliebigen Tastenkombination zuordnen.  
  
4.  Wählen Sie die zu löschende Variable aus, und klicken Sie dann auf **Variable löschen**.  
  
     Wenn die Variable nicht im Fenster Variablen angezeigt wird, klicken Sie auf **Rasteroptionen** , und wählen Sie dann **Variablen aller Bereiche anzeigen**aus.  
  
5.  Wenn das Dialogfeld **Löschen der Variablen bestätigen** aufgerufen wird, klicken Sie zur Bestätigung auf **Ja** .  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="change-the-scope-of-a-variable"></a>Ändern des Bereichs einer Variable  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im Menü **SSIS** auf **Variablen**. Sie können das Fenster **Variablen** auch anzeigen, indem Sie im Dialogfeld **Optionen** auf der Seite **Tastatur** den Befehl View.Variables einer beliebigen Tastenkombination zuordnen.  
  
4.  Wählen Sie die Variable aus, und klicken Sie dann auf **Variable verschieben**.  
  
     Wenn die Variable nicht im Fenster Variablen angezeigt wird, klicken Sie auf **Rasteroptionen** , und wählen Sie dann **Variablen aller Bereiche anzeigen**aus.  
  
5.  Wählen Sie im Dialogfeld **Neuen Bereich auswählen** das Paket oder einen Container, Task oder Ereignishandler im Paket aus, um den Gültigkeitsbereich der Variablen zu ändern.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  

## <a name="set-the-properties-of-a-user-defined-variable"></a>Festlegen der Eigenschaften von benutzerdefinierten Variablen
 Sie können eine der folgenden Funktionen verwenden, um die Eigenschaften einer benutzerdefinierten Variable in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]festzulegen:  
  
-   Fenster "Variablen".  
  
-   Eigenschaftenfenster. Im Fenster **Eigenschaften** werden die Eigenschaften zum Konfigurieren von Variablen aufgelistet, die im Fenster **Variablen** nicht zur Verfügung stehen: Description, EvaluateAsExpression, Expression, ReadOnly, ValueType und IncludeInDebugDump.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt außerdem eine Gruppe von Systemvariablen bereit, deren Eigenschaften, mit Ausnahme der RaiseChangedEvent-Eigenschaft, nicht aktualisiert werden können.  
  
### <a name="set-expressions-on-variables"></a>Festlegen von Ausdrücken für Variablen  
  
 Wenn Sie das Fenster **Eigenschaften** verwenden, um Ausdrücke für eine benutzerdefinierte Variable festzulegen:  
  
-   Der Wert dieser Variablen kann durch die Value-Eigenschaft oder die Expression-Eigenschaft festgelegt werden. Standardmäßig ist die EvaluateAsExpression-Eigenschaft auf **False** festgelegt, und der Wert dieser Variablen wird durch die Value-Eigenschaft festgelegt. Um einen Ausdruck zum Festlegen des Werts zu verwenden, müssen Sie zuerst EvaluateAsExpression auf **True**festlegen und dann einen Ausdruck in der Expression-Eigenschaft bereitstellen. Die Value-Eigenschaft wird automatisch auf das Auswertungsergebnis des Ausdrucks festgelegt.  
  
-   Die ValueType-Eigenschaft enthält den Datentyp des Werts in der Value-Eigenschaft. Wenn Value durch einen Ausdruck festgelegt wird, dann wird ValueType automatisch auf einen Datentyp aktualisiert, der mit dem Auswertungsergebnis des Ausdrucks kompatibel ist. Angenommen, Value enthält 0 und die ValueType-Eigenschaft enthält **Int32** . Nun legen Sie Expression auf GETDATE() fest. Daraufhin enthält Value das aktuelle Datum und die Uhrzeit, und ValueType wird auf **DateTime**festgelegt.  
  
-   Das  **Eigenschaftenfenster** für die Variable stellt den Zugriff auf das Dialogfeld **Ausdrucks-Generator** bereit. Sie können dieses Tool zum Erstellen, Überprüfen und Auswerten von Ausdrücken verwenden. Weitere Informationen finden Sie unter [Ausdrucks-Generator](../integration-services/expressions/expression-builder.md) und [Integration Services-Ausdrücke &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Wenn Sie das Fenster **Variablen** verwenden, um Ausdrücke für eine benutzerdefinierte Variable festzulegen:  
  
-   Wenn Sie den Variablenwert mit einem Ausdruck festlegen möchten, stellen Sie zunächst sicher, dass der Variablendatentyp mit dem Auswertungsergebnis des Ausdrucks kompatibel ist. Stellen Sie dann einen Ausdruck in der Spalte **Ausdruck** im Fenster **Variablen** bereit. Die EvaluateAsExpression-Eigenschaft im Fenster **Eigenschaften** wird automatisch auf **True**festgelegt.  
  
-   Wenn Sie einer Variablen einen Ausdruck zuweisen, wird ein spezieller Symbolmarker neben der Variablen angezeigt. Dieser spezielle Symbolmarker wird auch neben Verbindungs-Managern und Tasks angezeigt, für die Ausdrücke festgelegt wurden.  
  
-   Das Fenster **Variablen** für die Variable stellt den Zugriff auf das Dialogfeld **Ausdrucks-Generator** bereit. Sie können dieses Tool zum Erstellen, Überprüfen und Auswerten von Ausdrücken verwenden. Weitere Informationen finden Sie unter [Ausdrucks-Generator](../integration-services/expressions/expression-builder.md) und [Integration Services-Ausdrücke &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Wenn Sie der Variablen im Fenster **Variablen** oder im **Eigenschaftenfenster** einen Ausdruck zuweisen und **EvaluateAsExpression** auf **True**festgelegt ist, können Sie den Datentyp der Variablen nicht ändern.  
  
### <a name="set-the-namespace-and-name-properties"></a>Festlegen des Namespaces und der Namenseigenschaften
  
 Die Werte der Eigenschaften **Name** und **Namespace** müssen mit einem Buchstaben beginnen, wie in Unicode-Standard 2.0 definiert ist, oder mit einem Unterstrich (_). Bei den nachfolgenden Zeichen kann es sich um Buchstaben oder Zahlen gemäß Unicode-Standard 2.0 oder um einem Unterstrich (\_) handeln.  
  
### <a name="set-variable-properties-in-the-variables-window"></a>Festlegen von Variableneigenschaften im Fenster „Variablen“   
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im Menü **SSIS** auf **Variablen**.  
  
     Sie können das Fenster **Variablen** auch anzeigen, indem Sie im Dialogfeld **Optionen** auf der Seite **Tastatur** den Befehl View.Variables einer beliebigen Tastenkombination zuordnen.  
  
4.  Klicken Sie optional im Fenster **Variablen** auf **Rasteroptionen**, und wählen Sie die Spalten aus, die im Fenster **Variablen** angezeigt werden sollen. Wählen Sie dann die Filter aus, die auf die Liste der Variablen angewendet werden sollen.  
  
5.  Wählen Sie die gewünschte Variable aus der Liste aus, und aktualisieren Sie dann die Werte in den Spalten **Name**, **Datentyp**, **Wert**, **Namespace**, **Änderungsereignis auslösen**, **Beschriftung** und **Ausdruck** .  
  
6.  Wählen Sie die Variable in der Liste aus, und klicken Sie dann auf **Variable verschieben** , um den Bereich zu ändern.  
  
7.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  
  
### <a name="set-variable-properties-in-the-properties-window"></a>Festlegen von Variableneigenschaften im Fenster „Eigenschaften“  

1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im Menü **Ansicht** auf **Eigenschaftenfenster**.  
  
4.  Klicken Sie in [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer auf die Registerkarte **Paket-Explorer** , und erweitern Sie den Paketknoten.  
  
5.  Um Variablen mit Paketbereich zu ändern, erweitern Sie den Variablenknoten. Erweitern Sie anderenfalls den Ereignishandlerknoten oder den Knoten für Ausführbare Dateien, bis Sie den Variablenknoten finden, der die zu ändernde Variable enthält.  
  
6.  Klicken Sie auf die Variable, deren Eigenschaften Sie ändern möchten.  
  
7.  Aktualisieren Sie im Fenster **Eigenschaften** die Variableneigenschaften für den Lese-/Schreibzugriff. Einige Eigenschaften sind für benutzerdefinierte Variablen auf Nur Lesen festgelegt.  
  
     Weitere Informationen zu den Eigenschaften finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  

## <a name="update-a-variable-dynamically-with-configurations"></a>Dynamisches Aktualisieren einer Variable mit Konfigurationen  
 Zum dynamischen Aktualisieren von Variablen können Sie Konfigurationen für die Variablen erstellen, die Konfigurationen zusammen mit dem Paket bereitstellen und dann die Variablenwerte in der Konfigurationsdatei aktualisieren, wenn Sie die Pakete bereitstellen. Zur Laufzeit verwendet das Paket die aktualisierten Variablenwerte. Weitere Informationen finden Sie unter [Erstellen von Paketkonfigurationen](../integration-services/packages/create-package-configurations.md).  

## <a name="related-tasks"></a>Related Tasks  
 [Verwenden der Werte von Variablen und Parametern in einem untergeordneten Paket](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
