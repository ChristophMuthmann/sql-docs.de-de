---
title: Gruppieren von Komponenten oder Aufheben der Gruppierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fd4deab1f2dde19f6d5ec91fe72f10a2e71135d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="group-or-ungroup-components"></a>Gruppieren von Komponenten oder Aufheben der Gruppierung
  Die Registerkarten **Ablaufsteuerung**, **Datenfluss**und **Ereignishandler** im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer unterstützen die reduzierbare Gruppierung. Wenn ein Paket viele Komponenten enthält, kann dies zu einer Überlastung der Registerkarten führen. In diesem Fall ist es schwierig, alle Komponenten gleichzeitig anzuzeigen und das gewünschte Element zu finden. Mit der Funktion für reduzierbare Gruppierung kann Platz auf der Arbeitsoberfläche gespart und die Arbeit mit großen Paketen erleichtert werden.  
  
 Sie wählen die Komponenten aus, die Sie gruppieren möchten, gruppieren sie und erweitern bzw. reduzieren dann die Gruppen entsprechend Ihren Anforderungen. Das Erweitern einer Gruppe ermöglicht den Zugriff auf die Eigenschaften der Komponenten in der Gruppe. Die Rangfolgeneinschränkungen, die Tasks und Container verbinden, werden automatisch in die Gruppe eingeschlossen.  
  
 Folgende Überlegungen gelten im Zusammenhang mit dem Gruppieren von Komponenten.  
  
-   Um Komponenten gruppieren zu können, muss die Ablaufsteuerung, der Datenfluss oder der Ereignishandler mehrere Komponenten enthalten.  
  
-   Gruppen können auch geschachtelt werden, wodurch Gruppen innerhalb von Gruppen erstellt werden können. Die Entwurfsoberfläche kann mehrere nicht geschachtelte Gruppen implementieren, eine Komponente kann aber nur einer Gruppe angehören, sofern die Gruppen nicht geschachtelt sind.  
  
-   Wenn ein Paket gespeichert wird, speichert der [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer die Gruppierung, diese hat jedoch keine Auswirkung auf die Paketausführung. Die Möglichkeit der Gruppierung von Komponenten ist eine Entwurfszeitfunktion. Das Laufzeitverhalten des Pakets ist nicht davon betroffen.  
  
### <a name="to-group-components"></a>So gruppieren Sie Komponenten  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** .  
  
4.  Wählen Sie auf der Entwurfsoberfläche der Registerkarte die Komponenten aus, die Sie gruppieren möchten, klicken Sie mit der rechten Maustaste auf eine ausgewählte Komponente, und klicken Sie anschließend auf **Gruppieren**.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
### <a name="to-ungroup-components"></a>So heben Sie die Gruppierung von Komponenten auf  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung**, **Datenfluss**oder **Ereignishandler** .  
  
4.  Wählen Sie auf der Entwurfsoberfläche der Registerkarte die Gruppe mit der Komponente aus, deren Gruppierung Sie aufheben möchten, führen Sie einen Rechtsklick aus, und klicken Sie anschließend auf **Gruppierung aufheben**.  
  
5.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung](../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Verbinden von Tasks und Containern mithilfe einer Standardrangfolgen-Einschränkung](http://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75)  
  
  
