---
title: "Transformation für bedingtes Teilen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.conditionalsplittrans.f1
- sql13.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 84791cd0513a4da1dae8befe6168180a4b7ce6cd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="conditional-split-transformation"></a>Transformation für bedingtes Teilen
  Die Transformation für bedingtes Teilen kann Datenzeilen je nach Dateninhalt an andere Ausgaben routen. Die Implementierung der Transformation für bedingtes Teilen ist mit einer CASE-Entscheidungsstruktur in einer Programmiersprache zu vergleichen. Diese Transformation wertet Ausdrücke aus und leitet dann basierend auf den Ergebnissen die Datenzeilen an die angegebene Ausgabe weiter. Diese Transformation stellt außerdem eine Standardausgabe bereit, damit eine Zeile, die mit keinem Ausdruck übereinstimmt, an die Standardausgabe weitergeleitet wird.  
  
## <a name="configuration-of-the-conditional-split-transformation"></a>Konfiguration der Transformation für bedingtes Teilen  
 Es gibt folgende Möglichkeiten, um die Transformation für bedingtes Teilen zu konfigurieren:  
  
-   Stellen Sie einen Ausdruck, der in einen booleschen Wert ausgewertet wird, für jede von der Transformation zu testende Bedingung bereit.  
  
-   Geben Sie die Reihenfolge an, in der die Bedingungen ausgewertet werden. Die Reihenfolge ist wichtig, weil eine Zeile entsprechend der ersten Bedingung, die zu true ausgewertet wird, an die Ausgabe gesendet wird.  
  
-   Geben Sie die Standardausgabe für die Transformation an. Für die Transformation muss eine Standardausgabe angegeben werden.  
  
 Jede Eingabezeile kann nur an eine Ausgabe gesendet werden, nämlich an die Ausgabe für die erste Bedingung, die zu true ausgewertet wird. Beispielsweise leiten die folgenden Bedingungen Zeilen in der **FirstName** -Spalte, die mit dem Buchstaben *A* beginnen, an eine bestimmte Ausgabe weiter. Zeilen, die mit dem Buchstaben *B* beginnen, werden an eine andere Ausgabe weitergeleitet. Alle anderen Zeilen werden an die Standardausgabe weitergeleitet.  
  
 Output 1  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 Output 2  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] schließt Funktionen und Operatoren ein, mit denen Sie die Ausdrücke erstellen können, die Eingabedaten auswerten und Ausgabedaten weiterleiten. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
 Die Transformation für bedingtes Teilen schließt die benutzerdefinierte Eigenschaft **FriendlyExpression** ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist eine Eingabe, mindestens eine Ausgabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Teilen eines Datasets mithilfe der Transformation für bedingtes Teilen](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Teilen eines Datasets mithilfe der Transformation für bedingtes Teilen](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
## <a name="conditional-split-transformation-editor"></a>Transformations-Editor für bedingtes Teilen
  Mithilfe des Dialogfelds **Transformations-Editor für bedingtes Teilen** können Sie Ausdrücke erstellen, die Reihenfolge festlegen, in der Ausdrücke ausgewertet werden, und die Ausgaben des bedingten Teilens benennen. Dieses Dialogfeld schließt Funktionen und Operatoren für mathematische Berechnungen, Zeichenfolgen und Datum/Uhrzeit ein, die Sie für das Erstellen von Ausdrücken verwenden können. Die erste Bedingung, bei der die Auswertung den Wert TRUE ergibt, bestimmt die Ausgabe, an die eine Zeile geleitet wird.  
  
> [!NOTE]  
>  Die Transformation für bedingtes Teilen leitet jede Eingabezeile an nur eine Ausgabe. Wenn Sie mehrere Bedingungen eingeben, wird jede Zeile durch die Transformation an die erste Ausgabe gesendet, bei der die Bedingung erfüllt ist (TRUE). Dadurch bleiben alle folgenden Bedingungen für diese Zeile unberücksichtigt. Wenn mehrere Bedingungen aufeinander folgend ausgewertet werden sollen, dann müssen Sie mehrere Transformationen für bedingtes Teilen im Datenfluss miteinander verketten.  
  
### <a name="options"></a>enthalten  
 **Order**  
 Wählen Sie eine Zeile aus, und verwenden Sie die Pfeiltasten auf der rechten Seite, um die Reihenfolge zu ändern, in der die Ausdrücke ausgewertet werden.  
  
 **Ausgabename**  
 Geben Sie einen Ausgabenamen an. Standardwert ist eine nummerierte Liste aus Fällen; Sie können jedoch einen eindeutigen, beschreibenden Namen auswählen.  
  
 **Bedingung**  
 Geben Sie einen Ausdruck ein, oder erstellen Sie einen, indem Sie aus der Liste der verfügbaren Spalten, Variablen, Funktionen und Operatoren die entsprechenden Teile ziehen.  
  
 Der Wert dieser Eigenschaft kann mithilfe eines Eigenschaftsausdrucks angegeben werden.  
  
 **Verwandte Themen:** [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operatoren &#40;SSIS-Ausdruck&#41;](../../../integration-services/expressions/operators-ssis-expression.md) und [Funktionen &#40;SSIS-Ausdruck&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **Standardausgabename**  
 Geben Sie einen Namen für die Standardausgabe ein, oder verwenden Sie den Standardnamen.  
  
 **Fehlerausgabe konfigurieren**  
 Geben Sie mithilfe des Dialogfelds [Fehlerausgabe konfigurieren](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) an, wie Fehler behandelt werden sollen.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
