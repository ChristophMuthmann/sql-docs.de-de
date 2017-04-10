---
title: "Integration Services-Variablen (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Variablen [Integration Services], Übergeben zwischen Paketen"
  - "Benutzerdefinierte Variablen [Integration Services]"
  - "Bereich [Integration Services]"
  - "Systemvariablen [Integration Services]"
  - "Variablen [Integration Services]"
  - "Variablen [Integration Services], Informationen zu Variablen"
  - "Werte [Integration Services]"
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
caps.latest.revision: 60
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 59
---
# Integration Services-Variablen (SSIS)
  Variablen speichern Werte, die von einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Paket und dessen Containern, Tasks und Ereignishandlern zur Laufzeit verwendet werden können. Die Skripts im Skripttask und die Skriptkomponente können ebenfalls Variablen verwenden. Die Rangfolgeneinschränkungen, mit denen Tasks und Container zu einem Workflow zusammengestellt werden, können Variablen verwenden, wenn ihre Einschränkungsdefinitionen Ausdrücke einschließen.  
  
 Variablen in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Paketen können für folgende Zwecke verwendet werden:  
  
-   Aktualisieren der Eigenschaften von Paketelementen zur Laufzeit. Beispielsweise können Sie die von einem Foreach-Schleifencontainer zulässige Anzahl von gleichzeitig ausführbaren Dateien dynamisch festlegen.  
  
-   Einschließen einer Nachschlagetabelle im Arbeitsspeicher. Beispielsweise kann von einem Paket ein Task SQL ausführen ausgeführt werden, der eine Variable mit Datenwerten lädt.  
  
-   Laden von Variablen mit Datenwerten und anschließend mit deren Hilfe Angeben einer Suchbedingung in einer WHERE-Klausel. Beispielsweise kann das Skript eines Skripttasks den Wert einer Variablen aktualisieren, die von einer Transact-SQL-Anweisung in einem Task SQL ausführen verwendet wird.  
  
-   Laden einer Variablen mit einer ganzen Zahl und anschließend Steuern der Schleifen in einer Paketablaufsteuerung mithilfe dieses Werts. Beispielsweise können Sie im Auswertungsausdruck eines For-Schleifencontainers die Iteration mithilfe einer Variablen steuern.  
  
-   Auffüllen von Parameterwerten für Transact-SQL-Anweisungen zur Laufzeit. Beispielsweise kann ein Paket einen Task SQL ausführen ausführen und anschließend die Parameter einer Transact-SQL-Anweisung mithilfe von Variablen dynamisch festlegen.  
  
-   Erstellen von Ausdrücken, die Variablenwerte einschließen. Beispielsweise kann die Transformation für abgeleitete Spalten eine Spalte mit dem Ergebnis aus dem Multiplizieren eines Variablenwerts mit einem Spaltenwert auffüllen.  
  
## Systemvariablen und benutzerdefinierte Variablen  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] unterstützt zwei Arten von Variablen: Benutzerdefinierte Variablen und Systemvariablen. Benutzerdefinierte Variablen werden von Paketentwicklern definiert, und Systemvariablen werden von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] definiert. Sie können so viele benutzerdefinierte Variablen erstellen, wie für das Paket erforderlich sind. Zusätzliche Systemvariablen können jedoch nicht erstellt werden.  
  
 Alle Variablen, seien es Systemvariablen oder benutzerdefinierte Variablen, können in den Parameterbindungen verwendet werden, die der Task SQL ausführen zum Zuordnen von Variablen zu Parametern in SQL-Anweisungen verwendet. Weitere Informationen finden Sie unter [SQL ausführen (Task)](../integration-services/control-flow/execute-sql-task.md) und [Parameter und Rückgabecodes im Task „SQL ausführen“](../Topic/Parameters%20and%20Return%20Codes%20in%20the%20Execute%20SQL%20Task.md).  
  
> [!NOTE]  
>  Bei den Namen von benutzerdefinierten und Systemvariablen wird nach Groß-/Kleinschreibung unterschieden.  
  
 Sie können benutzerdefinierte Variablen für alle [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Containertypen erstellen: Pakete, Foreach-Schleifencontainer, For-Schleifencontainer, Sequenzcontainer, Tasks und Ereignishandler. Bei benutzerdefinierten Variablen handelt es sich um Elemente der Variables-Auflistung des Containers.  
  
 Wenn Sie das Paket mit dem [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer erstellen, können Sie die Elemente der **Variables**-Auflistung im Ordner Variablen auf der Registerkarte **Paket-Explorer** des [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designers anzeigen. Die Ordner listen benutzerdefinierte Variablen und Systemvariablen auf.  
  
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
  
 Weitere Informationen zu Szenarien für die Verwendung von Variablen in der Praxis finden Sie unter [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md).  
  
## Variableneigenschaften  
 Sie können benutzerdefinierte Variablen konfigurieren, indem Sie die folgenden Eigenschaften im Fenster **Variablen** oder im Fenster **Eigenschaften** festlegen. Bestimmte Eigenschaften sind nur im Eigenschaftenfenster verfügbar.  
  
> [!NOTE]  
>  Die einzige konfigurierbare Option für Systemvariablen ist das Angeben, ob sie ein Ereignis auslösen, wenn sich der Wert ändert.  
  
 Description  
 Gibt die Beschreibung der Variablen an.  
  
 EvaluateAsExpression  
 Wenn die Eigenschaft auf **True** festgelegt wird, wird der bereitgestellte Ausdruck zum Festlegen des Variablenwerts verwendet.  
  
 expression  
 Gibt den der Variablen zugeordneten Ausdruck an.  
  
 Name  
 Gibt den Variablennamen an.  
  
 Namespace  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt zwei Namespaces bereit: **User** und **System**. Standardmäßig gehören benutzerdefinierte Variablen zum Namespace **User** und Systemvariablen zum Namespace **System**. Sie können zusätzliche Namespaces für benutzerdefinierte Variablen erstellen und den Namen des **User**-Namespaces ändern. Es ist jedoch nicht möglich, den Namen des **System**-Namespaces zu ändern, dem **System**-Namespace Variablen hinzuzufügen oder Systemvariablen einem anderen Namespace zuzuweisen.  
  
 RaiseChangedEvent  
 Wenn die Eigenschaft auf **True** festgelegt wird, wird das **OnVariableValueChanged**-Ereignis bei einer Änderung des Variablenwerts ausgelöst.  
  
 ReadOnly  
 Wenn die Eigenschaft auf **False** festgelegt wird, besteht ein Lese- und Schreibzugriff auf die Variable.  
  
 Scope  
 > [!NOTE]  
>  Sie können diese Eigenschafteneinstellung nur ändern, indem Sie im Fenster **Variablen** auf **Variable verschieben** klicken.  
  
 Eine Variable wird im Bereich eines Pakets oder im Bereich eines Containers, Tasks oder Ereignishandlers im Paket erstellt. Der Paketcontainer befindet sich ganz oben in der Containerhierarchie. Deshalb verhalten sich Variablen mit Paketbereichsfunktion wie globale Variablen und können von allen Containern im Paket verwendet werden. Entsprechend können Variablen, die im Bereich eines Containers definiert sind, wie z. B. eines For-Schleifencontainers, von allen Tasks oder Containern innerhalb des For-Schleifencontainers verwendet werden.  
  
 Falls ein Paket mithilfe des Tasks Paket ausführen andere Pakete ausführt, können die Variablen, die im Bereich des aufrufenden Pakets oder des Tasks Paket ausführen definiert sind, dem aufgerufenen Paket mithilfe des Konfigurationstyps Variable für das übergeordnete Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Package Configurations](../integration-services/packages/package-configurations.md).  
  
 IncludeInDebugDump  
 Geben Sie an, ob der Variablenwert in den Debugdumpdateien enthalten ist.  
  
 Für benutzerdefinierte Variablen und Systemvariablen ist **true** der Standardwert für die Option **InclueInDebugDump**.  
  
 Für benutzerdefinierte Variablen setzt das System die **IncludeInDebugDump**-Option jedoch auf **false** zurück, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Wenn die **EvaluateAsExpression**-Variableneigenschaft auf **true** festgelegt ist, setzt das System die **IncludeInDebugDump**-Option auf **false** zurück.  
  
     Um den Text des Ausdrucks als Variablenwert in die Debugdumpdatei einzuschließen, legen Sie die **IncludeInDebugDump**-Option auf **true** fest.  
  
-   Wenn der Datentyp der Variablen in eine Zeichenfolge umgewandelt wird, setzt das System die **IncludeInDebugDump**-Option auf **false** zurück.  
  
 Wenn das System die **IncludeInDebugDump**-Option auf **false** zurücksetzt, wird möglicherweise der vom Benutzer gewählte Wert überschrieben.  
  
 Wert  
 Der Wert einer benutzerdefinierten Variable kann ein Literal oder ein Ausdruck sein. Eine Variable enthält Optionen zum Festlegen des Variablenwerts und des Datentyps des Werts. Die beiden Eigenschaften müssen kompatibel sein. Beispielsweise ist das Verwenden eines string-Werts zusammen mit einem integer-Datentyp ungültig.  
  
 Falls die Variable so konfiguriert ist, dass sie als Ausdruck ausgewertet wird, müssen Sie einen Ausdruck angeben. Zur Laufzeit wird der Ausdruck ausgewertet, und die Variable wird auf das Auswertungsergebnis festgelegt. Wenn z. B. eine Variable den Ausdruck `DATEPART("month", GETDATE())` verwendet, entspricht der Wert der Variablen der Zahl des Monats im aktuellen Datum. Der Ausdruck muss ein gültiger Ausdruck sein, der die [!INCLUDE[ssIS](../includes/ssis-md.md)]-Ausdrucksgrammatiksyntax verwendet. Wenn ein Ausdruck mit Variablen verwendet wird, kann der Ausdruck Literale sowie die Operatoren und Funktionen der Ausdrucksgrammatik verwenden. Der Ausdruck kann jedoch nicht auf die Spalten in einem Datenfluss des Pakets verweisen. Die maximale Länge eines Ausdrucks beträgt 4000 Zeichen. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 ValueType  
 > [!NOTE]  
>  Der Eigenschaftswert wird in der Spalte **Datentyp** im Fenster **Variablen** angezeigt.  
  
 Gibt den Datentyp des Variablenwerts an.  
  
## Konfigurieren von Variablen  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer festlegen können, finden Sie unter [Fenster „Variablen“](../integration-services/variables-window.md).  
  
 Weitere Informationen zu Variableneigenschaften und zum programmgesteuerten Festlegen dieser Eigenschaften finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.Variable>.  
  
## Verwandte Aufgaben  
 [Hinzufügen, Löschen, Ändern des Bereichs von benutzerdefinierten Variablen in einem Paket](../Topic/Add,%20Delete,%20Change%20Scope%20of%20User-Defined%20Variable%20in%20a%20Package.md)  
  
 [Festlegen der Eigenschaften von benutzerdefinierten Variablen](../Topic/Set%20the%20Properties%20of%20a%20User-Defined%20Variable.md)  
  
 [Verwenden der Werte von Variablen und Parametern in einem untergeordneten Paket](../integration-services/packages/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [Zuordnen von Abfrageparametern zu Variablen in einer Datenflusskomponente](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  