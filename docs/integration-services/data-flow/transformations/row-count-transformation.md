---
title: "Transformation für Zeilenanzahl | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0eb554132024c6169f45fb24d739cb8f9f9d8caf
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="row-count-transformation"></a>Transformation für Zeilenanzahl
  Die Transformation für Zeilenanzahl zählt die Zeilen in einem Datenfluss und speichert die endgültige Anzahl in einer Variablen.  
  
 A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Paket können mithilfe der Zeilenanzahl die in Skripts, Ausdrücken und Eigenschaftsausdrücken verwendeten Variablen aktualisiert werden. (Beispielsweise kann mit der Variablen, die die Zeilenanzahl speichert, der Nachrichtentext in einer E-Mail-Nachricht aktualisiert und um die Zeilenanzahl ergänzt werden.) Die von der Transformation für Zeilenanzahl verwendete Variable muss bereits vorhanden sein, und zwar im Bereich des Datenflusstasks, zu dem der Datenfluss mit der Transformation für Zeilenanzahl gehört.  
  
 Die Transformation speichert den Zeilenanzahlwert erst dann in der Variablen, nachdem die letzte Zeile die Transformation durchlaufen hat. Daher wird der Wert der Variablen nicht rechtzeitig aktualisiert, um den aktualisierten Wert im Datenfluss zu verwenden, der die Transformation für die Zeilenanzahl enthält. Sie können die aktualisierte Variable in einem separaten Datenfluss verwenden.  
  
 Diese Transformation weist je eine Eingabe und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="configuration-of-the-row-count-transformation"></a>Konfiguration der Transformation für Zeilenanzahl  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Informationen zum Festlegen der Eigenschaften dieser Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Variablen &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-variables.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

