---
title: 'Schritt 2: Erstellen des Bereitstellungsprojekts | Microsoft-Dokumentation'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: da96393429cf37224ef609b1ed1de52f41704015
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-1-2---creating-the-deployment-project"></a>Lektion 1-2: Erstellen des Bereitstellungsprojekts
In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]ist die bereitstellbare Einheit ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt. Bevor Sie Pakete bereitstellen können, müssen Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt erstellen und diesem Projekt alle Pakete und Hilfsdateien hinzufügen, die mit den Paketen bereitgestellt werden sollen.  
  
### <a name="to-create-the-integration-services-project"></a>So erstellen Sie das Integration Services-Projekt  
  
1.  Klicken Sie auf **Start**und zeigen sie auf **Alle Programme**. Klicken Sie nun auf **Microsoft SQL Server**und anschließend auf **SQL Server Data Tools**.  
  
2.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie anschließend auf **Projekt** , um ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt zu erstellen.  
  
3.  Wählen Sie im Bereich **Vorlagen** des Dialogfelds **Neues Projekt** die Option **Integration Services-Projekt** aus.  
  
4.  Ändern Sie im Feld **Name** den Standardnamen in **Deployment Tutorial**. Deaktivieren Sie optional das Kontrollkästchen **Projektmappenverzeichnis erstellen** .  
  
5.  Übernehmen Sie den Standardspeicherort, oder klicken Sie auf **Durchsuchen** , um nach dem gewünschten Ordner zu suchen.  
  
6.  Klicken Sie im Dialogfeld **Projektspeicherort** auf den Ordner und anschließend auf **Öffnen**.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Standardmäßig wird ein leeres Paket mit dem Namen Package.dtsx erstellt und dem Projekt hinzugefügt. Sie verwenden dieses Paket jedoch nicht, sondern fügen dem Projekt vorhandene Pakete hinzu. Da alle Pakete in einem Projekt bei der Bereitstellung berücksichtigt werden, sollten Sie Package.dtsx löschen. Klicken Sie dazu mit der rechten Maustaste auf das Paket und anschließend auf **Löschen**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 3: Hinzufügen von Paketen und weiteren Dateien](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
## <a name="see-also"></a>Siehe auch  
[Integration Services-Projekte &#40;SSIS&#41;](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  

