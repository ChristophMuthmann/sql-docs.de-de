---
title: 'Schritt 1: Kopieren des Pakets aus Lektion 1 | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b3b601049b8904d439136a1fdc9af7cd84a86b5b
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-2-1---copying-the-lesson-1-package"></a>Lektion 2-1: Kopieren des Pakets aus Lektion 1
In dieser Aufgabe erstellen Sie eine Kopie des in Lektion 1 erstellten Pakets Lesson 1.dtsx. Falls Sie Lektion 1 nicht abgeschlossen haben, können Sie stattdessen das vollständige Lektion 1-Paket, das im Tutorial des Projekts enthalten ist, hinzufügen und anschließend kopieren. Sie verwenden diese neue Kopie im gesamten Rest der Lektion 2.  
  
### <a name="to-create-the-lesson-2-package"></a>So erstellen Sie das Lektion 2-Paket  
  
1.  Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools noch nicht geöffnet ist, klicken Sie auf **Start**und zeigen Sie auf **Alle Programme**. Klicken Sie anschließend auf **Microsoft SQL Server 2012**und danach auf **SQL Server Data Tools**.  
  
2.  Klicken Sie im Menü **Datei** auf **Öffnen**, klicken Sie auf **Projekt/Projektmappe**, klicken Sie auf **SSIS Tutorial** , klicken Sie auf **Öffnen**, und doppelklicken Sie anschließend auf **SSIS Tutorial.sln**.  
  
3.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Lesson 1.dtsx**, und klicken Sie anschließend auf **Kopieren**.  
  
4.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **SSIS-Pakete**und anschließend auf **Einfügen**.  
  
    Standardmäßig wird das kopierte Paket Lesson 2.dtsx genannt.  
  
5.  Doppelklicken Sie im Projektmappen-Explorer auf **Lesson 2.dtsx** , um das Paket zu öffnen.  
  
6.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im Hintergrund der Entwurfsoberfläche **Ablaufsteuerung** , und klicken Sie auf **Eigenschaften**.  
  
7.  Aktualisieren Sie im Eigenschaftenfenster die **Name** -Eigenschaft in **Lesson 2**.  
  
8.  Klicken Sie in das Feld für die **ID** -Eigenschaft, klicken Sie auf den Dropdownpfeil und anschließend auf **<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-1-package"></a>So fügen Sie das abgeschlossene Lektion 1-Paket hinzu  
  
1.  Öffnen Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools und das SSIS-Lernprogrammprojekt.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **SSIS-Pakete**, und klicken Sie auf **Vorhandenes Paket hinzufügen**.  
  
3.  Wählen Sie im Dialogfeld **Kopie des vorhandenen Pakets hinzufügen** unter **Paketspeicherort**die Option **Dateisystem**aus.  
  
4.  Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , navigieren Sie zu **Lesson 1.dtsx** auf Ihrem Computer, und klicken Sie anschließend auf **Öffnen**.  
  
    Um alle Lektionspakete für dieses Lernprogramm herunterzuladen, gehen Sie wie folgt vor.  
  
    1.  Klicken Sie [hier](http://go.microsoft.com/fwlink/?LinkId=275027), um zur Seite Integration Services Product Samples zu gelangen  
  
    2.  Klicken Sie auf die Registerkarte **DOWNLOADS** .  
  
    3.  Klicken Sie auf die Datei SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Kopieren Sie das Paket aus Lektion 1, und fügen Sie es wie in den Schritten 3 bis 8 der vorherigen Prozedur beschrieben ein.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 2: Hinzufügen und Konfigurieren des Foreach-Schleifencontainers](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  

