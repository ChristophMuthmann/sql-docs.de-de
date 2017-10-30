---
title: Entwickeln bestimmter Arten von Skriptkomponenten | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 458ba4be689ed976a5948380d35f38020f7dd4dd
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="developing-specific-types-of-script-components"></a>Entwickeln bestimmter Arten von Skriptkomponenten
  Bei der Skriptkomponente handelt es sich um ein konfigurierbares Tool, das Sie im Datenfluss eines Pakets verwenden können, um nahezu allen Anforderungen gerecht zu werden, die von den Quellen, Transformationen und Zielen nicht erfüllt werden, die in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthalten sind. Dieser Abschnitt enthält Codebeispiele für Skriptkomponenten, in denen die vier Optionen zum Konfigurieren der Skriptkomponente veranschaulicht werden:  
  
-   Als Quelle.  
  
-   Als Transformation mit synchronen Ausgaben.  
  
-   Als Transformation mit asynchronen Ausgaben.  
  
-   Als Ziel.  
  
 Weitere Beispiele von der Skriptkomponente finden Sie unter [Additional Script Component Examples](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Erstellen einer Quelle mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
 Erläutert und veranschaulicht, wie eine Datenflussquelle mithilfe der Skriptkomponente erstellt wird.  
  
 [Erstellen einer synchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 Erläutert und veranschaulicht, wie eine Datenflusstransformation mit synchronen Ausgaben mithilfe der Skriptkomponente erstellt wird. Durch diese Art von Transformation werden Datenzeilen an Ort und Stelle beim Durchlaufen der Komponente geändert.  
  
 [Erstellen einer asynchronen Transformation mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 Erläutert und veranschaulicht, wie eine Datenflusstransformation mit asynchronen Ausgaben mithilfe der Skriptkomponente erstellt wird. Bei dieser Art von Transformation müssen alle Datenzeilen gelesen werden, bevor den Daten, die die Komponente durchlaufen, weitere Informationen, z. B. berechnete Aggregate, hinzugefügt werden können.  
  
 [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 Erläutert und veranschaulicht, wie ein Datenflussziel mithilfe der Skriptkomponente erstellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Vergleichen von Skriptlösungen und benutzerdefinierten Objekten](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Entwickeln bestimmte Arten von Daten von Datenflusskomponenten](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  

