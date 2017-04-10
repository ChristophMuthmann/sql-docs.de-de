---
title: "Verbinden von Komponenten in einem Datenfluss | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Komponenten [Integration Services], Verbindungen"
  - "Verbindungen [Integration Services], Datenflusskomponenten"
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Verbinden von Komponenten in einem Datenfluss
  In diesem Verfahren wird das Verbinden der Ausgabe von Komponenten in einem Datenfluss mit anderen Komponenten innerhalb desselben Datenflusses beschrieben.  
  
### So verbinden Sie Komponenten in einem Datenfluss  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Ablaufsteuerung**, und doppelklicken Sie anschließend auf den Datenflusstask, der den Datenfluss enthält, in dem Sie Komponenten verbinden möchten.  
  
4.  Wählen Sie auf der Entwurfsoberfläche der Registerkarte **Datenfluss** die Transformation oder Quelle aus, die Sie verbinden möchten.  
  
5.  Ziehen Sie den grünen Ausgabepfeil einer Transformation oder Quelle auf eine Transformation oder ein Ziel. Manche Datenflusskomponenten weisen Fehlerausgaben auf, die Sie auf die gleiche Weise verbinden können.  
  
    > [!NOTE]  
    >  Für manche Datenflusskomponenten sind mehrere Ausgaben möglich, und Sie können jede Ausgabe mit einer anderen Transformation oder einem anderen Ziel verbinden.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Hinzufügen oder Löschen einer Komponente im Datenfluss](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [Konfigurieren einer Fehlerausgabe in einer Datenflusskomponente](../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  