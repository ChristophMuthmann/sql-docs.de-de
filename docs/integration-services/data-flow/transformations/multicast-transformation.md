---
title: "Transformation für Multicast | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8619a0ed02ffc73126eb151f4a83a0b6b24c4be8
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="multicast-transformation"></a>Transformation für Multicast
  Die Multicasttransformation verteilt ihre Eingabe an mindestens eine Ausgabe. Diese Transformation ist mit der Transformation für bedingtes Teilen vergleichbar. Beide Transformationen leiten eine Ausgabe an mehrere Ausgaben weiter. Der Unterschied zwischen den beiden Transformationen besteht darin, dass die Multicasttransformation jede Zeile an jede Ausgabe weiterleitet, während die Transformation für bedingtes Teilen eine Zeile an eine einzelne Ausgabe weiterleitet. Weitere Informationen finden Sie unter [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
 Zum Konfigurieren der Multicasttransformation fügen Sie Ausgaben hinzu.  
  
 Mithilfe der Multicasttransformation kann ein Paket logische Kopien von Daten erstellen. Dies ist hilfreich, wenn das Paket mehrere Transformationen auf dieselben Daten anwenden muss. Angenommen, eine Kopie der Daten wird aggregiert und nur die Zusammenfassungsinformationen werden in das Ziel geladen, während die andere Kopie der Daten mit Nachschlagewerten und abgeleiteten Spalten erweitert wird, bevor sie in das Ziel geladen wird.  
  
 Diese Transformation weist eine Eingabe und mehrere Ausgaben auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="configuration-of-the-multicast-transformation"></a>Konfiguration der Multicasttransformation  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für Multicast** festlegen können, finden Sie unter [Multicast Transformation Editor](../../../integration-services/data-flow/transformations/multicast-transformation-editor.md).  
  
 Weitere Informationen zu den Eigenschaften, die Sie programmgesteuert festlegen können, finden Sie unter [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Informationen zum Festlegen der Eigenschaften dieser Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
