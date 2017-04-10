---
title: "Erweitern eines Datasets mithilfe der Transformation f&#252;r Zusammenf&#252;hrungsjoins | Microsoft Docs"
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
  - "Transformation für Zusammenführungsjoin"
  - "Datasets [Integration Services], verknüpfen"
  - "Datasets [Integration Services], erweitern"
  - "Verknüpfen von Datasets [Integration Services]"
ms.assetid: 9e512c3c-f89b-45f3-8281-cdb8f35a2b1f
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Erweitern eines Datasets mithilfe der Transformation f&#252;r Zusammenf&#252;hrungsjoins
  Das Paket muss bereits mindestens einen Datenflusstask und zwei Datenflusskomponenten enthalten, die Eingaben für die Transformation für Zusammenführungsjoins bereitstellen, damit Sie eine Transformation für Zusammenführungsjoins hinzufügen und konfigurieren können.  
  
 Die Transformation für Zusammenführungsjoin erfordert zwei sortierte Eingaben. Weitere Informationen finden Sie unter [Sortieren von Daten für die Transformationen für Zusammenführen und Zusammenführungsjoin](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### So erweitern Sie ein Dataset  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Bereich **Toolbox**die Transformation für Zusammenführungsjoin auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für Zusammenführungsjoins mit dem Datenfluss, indem Sie den Konnektor von einer Datenquelle oder einer vorherigen Transformation auf die Transformation für Zusammenführungsjoins ziehen.  
  
5.  Doppelklicken Sie auf die Transformation für Zusammenführungsjoin.  
  
6.  Wählen Sie im Dialogfeld **Transformations-Editor für Zusammenführungsjoins** den zu verwendenden Jointyp in der Liste **Jointyp** aus.  
  
    > [!NOTE]  
    >  Wenn Sie den Typ **Linker äußerer Join** auswählen, können Sie auf **Eingaben vertauschen** klicken, um die Eingaben zu vertauschen und den linken äußeren Join in einen rechten äußeren Join zu ändern.  
  
7.  Ziehen Sie Spalten in der linken Eingabe auf Spalten in der rechten Eingabe, um die Joinspalten anzugeben. Falls die Spalten denselben Namen haben, können Sie das entsprechende Kontrollkästchen **** aktivieren, damit die Transformation für Zusammenführungsjoin den Join automatisch erstellt.  
  
    > [!NOTE]  
    >  Joins können nur zwischen Spalten mit der gleichen Sortierposition erstellt werden, und die Joins müssen in der von der Sortierposition angegebenen Reihenfolge erstellt werden. Wenn Sie versuchen, die Joins außerhalb der Reihenfolge zu erstellen, werden Sie vom **Transformations-Editor für Zusammenführungsjoin** aufgefordert, zusätzliche Joins für die ausgelassenen Sortierreihenfolgepositionen zu erstellen.  
  
    > [!NOTE]  
    >  Standardmäßig wird die Ausgabe nach den Joinspalten sortiert.  
  
8.  Aktivieren Sie in der linken und rechten Eingabe die Kontrollkästchen zusätzlicher Spalten, die in die Ausgabe eingeschlossen werden sollen. Joinspalten sind standardmäßig eingeschlossen.  
  
9. Aktualisieren Sie optional die Namen von Ausgabespalten in der **Ausgabealias** -Spalte.  
  
10. Klicken Sie auf **OK**.  
  
11. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [SQL Server Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  