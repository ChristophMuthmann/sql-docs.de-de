---
title: "Zusammenführen von Daten mithilfe der Union All-Transformation | Microsoft Docs"
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
helpviewer_keywords:
- merging datasets [Integration Services]
- merging inputs [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 78304403-a81c-4101-b87e-ec80ddfdac98
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b2f9933f48083b0849ba01312979911bacb4fd86
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="merge-data-by-using-the-union-all-transformation"></a>Zusammenführen von Daten mithilfe der Transformation für UNION ALL
  Das Paket muss bereits mindestens einen Datenflusstask und zwei Datenquellen enthalten, damit Sie eine Transformation für UNION ALL hinzufügen und konfigurieren können.  
  
 Die Transformation für UNION ALL kombiniert mehrere Eingaben. Die erste Eingabe, die mit der Transformation verbunden wird, ist die Verweiseingabe, und die nachfolgend verbundenen Eingaben sind die sekundären Eingaben. Die Ausgabe enthält die Spalten in der Verweiseingabe.  
  
### <a name="to-combine-inputs-in-a-data-flow"></a>So kombinieren Sie Eingaben in einem Datenfluss  
  
1.  Doppelklicken Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]im Projektmappen-Explorer auf das Paket, um es im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer zu öffnen, und klicken Sie dann auf die Registerkarte **Datenfluss** .  
  
2.  Ziehen Sie aus **Toolbox**die Transformation für UNION ALL auf die Entwurfsoberfläche der Registerkarte **Datenfluss** .  
  
3.  Verbinden Sie die Transformation für UNION ALL mit dem Datenfluss, indem Sie einen Konnektor von der Datenquelle oder einer vorherigen Transformation auf die Transformation für UNION ALL ziehen.  
  
4.  Doppelklicken Sie auf die Transformation für UNION ALL.  
  
5.  Ordnen Sie im **Transformations-Editor für UNION ALL**eine Spalte aus einer Eingabe einer Spalte in der Liste **Name der Ausgabespalte** zu. Klicken Sie dazu auf eine Zeile, und wählen Sie dann eine Spalte in der Eingabeliste aus. Wählen Sie  **\<ignorieren >** in der Eingabeliste zum Zuordnen der Spalte auszulassen.  
  
    > [!NOTE]  
    >  Für die Zuordnung von zwei Spalten müssen die Metadaten der Spalten übereinstimmen.  
  
    > [!NOTE]  
    >  Für Spalten in einer sekundären Eingabe, die keinen Verweisspalten zugeordnet sind, werden in der Ausgabe NULL-Werte festgelegt.  
  
6.  Ändern Sie optional die Namen von Spalten in der **Name der Ausgabespalte** -Spalte.  
  
7.  Wiederholen Sie die Schritte 5 und 6 für jede Spalte in jeder Eingabe.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Union All-Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  

