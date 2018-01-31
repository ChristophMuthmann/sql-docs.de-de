---
title: Entwickeln von Datenflusskomponenten mit mehreren Eingaben | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects-data-flow-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d4fae151d8feb9753eca9704b1b58f6ab7c609cf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>Entwickeln von Datenflusskomponenten mit mehreren Eingaben
  Eine Datenflusskomponente mit mehreren Eingaben verbraucht möglicherweise übermäßig viel Arbeitsspeicher, wenn die Eingaben unregelmäßig Daten erzeugen. Wenn Sie eine benutzerdefinierte Datenflusskomponente entwickeln, die mindestens zwei Eingaben unterstützt, können Sie diese hohe Speicherauslastung verwalten, indem Sie die folgenden Elemente im Namespace „Microsoft.SqlServer.Dts.Pipeline“ verwenden:  
  
-   Die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft der <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>-Klasse. Legen Sie den Wert dieser Eigenschaft auf **true** fest, um den Code zu implementieren, der erforderlich ist, damit die benutzerdefinierte Datenflusskomponente unregelmäßige Datenflüsse verwaltet.  
  
-   Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse. Sie müssen eine Implementierung dieser Methode bereitstellen, wenn Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft auf **TRUE** festlegen. Wenn Sie keine Implementierung bereitstellen, löst das Datenflussmodul zur Laufzeit eine Ausnahme aus.  
  
-   Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse. Sie müssen auch eine Implementierung dieser Methode bereitstellen, wenn Sie die <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft auf **TRUE** festlegen und die benutzerdefinierte Komponente mehr als zwei Eingaben unterstützt. Wenn Sie keine Implementierung bereitstellen, löst das Datenflussmodul zur Laufzeit eine Ausnahme aus, wenn der Benutzer mehr als zwei Eingaben anfügt.  
  
 Zusammen ermöglichen diese Elemente es Ihnen, eine Lösung für hohe Speicherauslastungen zu entwickeln, die der von Microsoft entwickelten Lösung für die Transformationen für Zusammenführen und Zusammenführungsjoin ähnelt.  
  
## <a name="setting-the-supportsbackpressure-property"></a>Festlegen der SupportsBackPressure-Eigenschaft  
 Der erste Schritt beim Implementieren einer besseren Speicherverwaltung für eine benutzerdefinierte Datenflusskomponente, die mehrere Eingaben unterstützt, besteht darin, den Wert der <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft im <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> auf **TRUE** festzulegen. Wenn der Wert von <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> **TRUE** ist, ruft das Datenflussmodul die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode auf. Bei mehr als zwei Eingaben wird außerdem die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode zur Laufzeit aufgerufen.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel legt die Implementierung von <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> den Wert von <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> auf **TRUE** fest.  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>Implementieren der IsInputReady-Methode  
 Wenn Sie den Wert der <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A>-Eigenschaft im <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>-Objekt auf **TRUE** festlegen, müssen Sie auch eine Implementierung für die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse bereitstellen.  
  
> [!NOTE]  
>  Die Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode sollte nicht die Implementierungen in der Basisklasse aufrufen. Die Standardimplementierung dieser Methode in der Basisklasse löst lediglich eine **NotImplementedException**aus.  
  
 Wenn Sie diese Methode implementieren, legen Sie den Status eines Elements im booleschen *canProcess* -Array für jede Eingabe der Komponente fest. (Die Eingaben werden von ihren ID-Werten im *inputIDs*-Array identifiziert.) Wenn Sie den Wert eines Elements im *canProcess*-Array für eine Eingabe auf **TRUE** festlegen, ruft das Datenflussmodul die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>-Methode der Komponente auf und stellt für die angegebene Eingabe mehr Daten bereit.  
  
 Es sind mehr Upstreamdaten verfügbar, und der Wert des *canProcess* -Arrayelements muss für mindestens eine Eingabe immer **true**sein. Andernfalls wird die Verarbeitung angehalten.  
  
 Das Datenflussmodul ruft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode vor dem Senden der einzelnen Datenpuffer auf, um zu bestimmen, welche Eingaben auf den Empfang weiterer Daten warten. Wenn der Rückgabewert angibt, dass eine Eingabe blockiert wird, speichert das Datenflussmodul vorübergehend zusätzliche Datenpuffer für diese Eingabe, statt sie an die Komponente zu senden.  
  
> [!NOTE]  
>  Sie rufen die Methode <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> oder <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> nicht in eigenem Code auf. Das Datenflussmodul ruft diese Methoden und die anderen Methoden der **PipelineComponent** -Klasse auf, die Sie überschreiben, wenn das Datenflussmodul die Komponente ausführt.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel gibt die Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode an, dass eine Eingabe auf den Empfang weiterer Daten wartet, wenn die folgenden Voraussetzungen erfüllt sind:  
  
-   Mehr Upstreamdaten sind für die Eingabe verfügbar (`!inputEOR`).  
  
-   Die Komponente verfügt derzeit nicht über Daten, die für die Eingabe in den Puffern verarbeitet werden können, die die Komponente bereits empfangen hat (`inputBuffers[inputIndex].CurrentRow() == null`).  
  
 Wenn eine Eingabe auf den Empfang weiterer Daten wartet, gibt die Datenflusskomponente dieses an, indem der Wert des Elements im **canProcess** -Array, das dieser Eingabe entspricht, auf *true* festgelegt wird.  
  
 Wenn die Komponente hingegen weiterhin verfügbare Daten aufweist, die für die Eingabe verarbeitet können, wird im Beispiel die Verarbeitung der Eingabe angehalten. Hierfür wird im Beispiel der Wert des Elements im **canProcess** -Array, das dieser Eingabe entspricht, auf *false* festgelegt.  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 Im vorangehenden Beispiel wird das boolesche `inputEOR` -Array verwendet, um anzugeben, ob für die jeweiligen Eingaben weitere Upstreamdaten verfügbar sind. `EOR` im Namen des Arrays steht für "Ende des Rowsets" und bezieht sich auf die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A>-Eigenschaft von Datenflusspuffern. In einem Teil des Beispiels, der hier nicht enthalten ist, überprüft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>-Methode den Wert der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A>-Eigenschaft für jeden empfangenen Datenpuffer. Wenn durch den Wert **TRUE** angegeben wird, dass für eine Eingabe keine Upstreamdaten mehr verfügbar sind, wird im Beispiel der Wert des `inputEOR`-Arrayelements für diese Eingabe auf **TRUE** festgelegt. In diesem Beispiel für die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode wird der Wert des entsprechenden Elements im *canProcess*-Array für eine Eingabe auf **TRUE** festgelegt, wenn der Wert des `inputEOR`-Arrayelements angibt, dass für die Eingabe keine Upstreamdaten mehr verfügbar sind.  
  
## <a name="implementing-the-getdependentinputs-method"></a>Implementieren der GetDependentInputs-Methode  
 Wenn die benutzerdefinierte Datenflusskomponente mehr als zwei Eingaben unterstützt, müssen Sie auch eine Implementierung für die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Klasse bereitstellen.  
  
> [!NOTE]  
>  Die Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode sollte nicht die Implementierungen in der Basisklasse aufrufen. Die Standardimplementierung dieser Methode in der Basisklasse löst lediglich eine **NotImplementedException**aus.  
  
 Das Datenflussmodul ruft die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode nur auf, wenn der Benutzer mehr als zwei Eingaben an die Komponente anfügt. Wenn eine Komponente nur über zwei Eingaben verfügt und die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode angibt, dass eine Eingabe blockiert ist (*canProcess* = **FALSE**), erkennt das Datenflussmodul, dass die andere Eingabe auf den Empfang weiterer Daten wartet. Wenn jedoch mehr als zwei Eingaben vorhanden sind und die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>-Methode angibt, dass eine Eingabe blockiert ist, identifiziert der zusätzliche Code in <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>, welche Eingaben auf den Empfang weiterer Daten warten.  
  
> [!NOTE]  
>  Sie rufen die Methode <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> oder <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> nicht in eigenem Code auf. Das Datenflussmodul ruft diese Methoden und die anderen Methoden der **PipelineComponent** -Klasse auf, die Sie überschreiben, wenn das Datenflussmodul die Komponente ausführt.  
  
### <a name="example"></a>Beispiel  
 Wenn eine bestimmte Eingabe blockiert ist, gibt die folgende Implementierung der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode eine Auflistung der Eingaben zurück, die auf den Empfang weiterer Daten warten und daher die betreffende Eingabe blockieren. Die Komponente identifiziert die blockierenden Eingaben, indem überprüft wird, ob außer der blockierten Eingabe andere Eingaben derzeit in den Puffern, die die Komponente bereits empfangen hat, nicht über Daten verfügen, die verarbeitet werden können (`inputBuffers[i].CurrentRow() == null`). Die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A>-Methode gibt dann die Auflistung der blockierenden Eingaben als Auflistung von Eingabe-IDs zurück.  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
