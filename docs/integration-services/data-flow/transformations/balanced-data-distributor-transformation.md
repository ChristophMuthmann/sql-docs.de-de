---
title: Balanced Data Distributor-Transformation | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.balanceddatadistributor.f1
ms.assetid: ae0b33dd-f44b-42df-b6f6-69861770ce10
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7a148470ac38ee6168d5c6a245899d629a0e3250
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="balanced-data-distributor-transformation"></a>Balanced Data Distributor (BDD)-Transformation
  Die BDD (Balanced Data Distributor)-Transformation profitiert von der Fähigkeit moderner CPUs, eine parallele Verarbeitung durchzuführen. Sie verteilt Puffer mit eingehenden Zeilen gleichmäßig auf Ausgaben für separate Threads. Indem für jeden Ausgabepfad separate Threads verwendet werden, verbessert die BDD-Komponente die Leistung eines SSIS-Pakets auf Mehrkern- oder Mehrprozessorcomputern.  
  
 Das folgende Diagramm zeigt ein einfaches Verwendungsbeispiel für die BDD-Transformation. In diesem Beispiel wählt die BDD-Transformation jeweils einen Pipelinepuffer aus den Eingabedaten einer Flatfilequelle aus und sendet ihn nach dem Roundrobin-Prinzip an einen der drei Ausgabepfade. In den SQL Server Data Tools können Sie die Werte von <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.DefaultBufferSize%2A>(Standardgröße des Pipelinepuffers) und <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.DefaultBufferMaxRows%2A>(maximale Zeilenanzahl in einem Pipelinepuffer) im Fenster **Eigenschaften** überprüfen, das die Eigenschaften eines Datenflusstasks enthält.  
  
 ![Ausgeglichener Datenverteiler](../../../integration-services/data-flow/transformations/media/balanceddatadistributor.JPG "ausgeglichener Datenverteiler")  
  
 Die BDD (Balanced Data Distributor)-Transformation verbessert die Paketausführungsleistung in einem Szenario, das die folgenden Bedingungen erfüllt:  
  
1.  Eine große Datenmenge wird an die BDD-Transformation übermittelt. Bei einer geringen Datenmenge und nur einem Puffer, der die Daten aufnehmen kann, ergibt die Verwendung der BDD-Transformation keinen Sinn. Bei einer großen Datenmenge und mehreren Puffern zum Speichern der Daten kann BDD die Pufferdaten jedoch effizient parallel in separaten Threads verarbeiten.  
  
2.  Die Daten werden schneller gelesen, als sie im weiteren Datenfluss verarbeitet werden. In diesem Szenario werden die für die Daten ausgeführten Transformationen im Vergleich zur Eingangsgeschwindigkeit der Daten langsam ausgeführt. Wenn sich der Engpass am Ziel befindet, muss das Ziel eine ausreichende Parallelität aufweisen.  
  
3.  Die Daten müssen keine bestimmte Reihenfolge einhalten. Wenn Sie jedoch eine bestimmte Reihenfolge beibehalten müssen, sollten Sie die Daten nicht mithilfe der BDD-Transformation unterteilen.  
  
 Wenn der Engpass bei einem SSIS-Paket auf die Geschwindigkeit zurückzuführen ist, mit der Daten aus der Quelle gelesen werden können, kann die Leistung mittels der BDD-Komponente nicht verbessert werden. Liegt der Engpass des SSIS-Pakets daran, dass das Ziel keine Parallelität unterstützt, ist BDD ebenfalls nicht die richtige Lösung. In einem passenden Szenario können Sie mit BDD jedoch alle Transformationen parallel ausführen und die Ausgabedaten, die aus den verschiedenen Ausgabepfaden der BDD-Transformation stammen, mithilfe der UNION ALL-Transformation kombinieren, bevor Sie die Daten an das Ziel senden.  
  
> [!IMPORTANT]  
>  Ein Verwendungsbeispiel dieser Transformation finden Sie im [BDD-Video (Balanced Data Distributor)](http://go.microsoft.com/fwlink/?LinkID=226278) in der TechNet Library.  
  
  

