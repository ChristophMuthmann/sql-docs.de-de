---
title: 'Schritt 1: Kopieren des Pakets aus Lektion 4 | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ecaf6b4d68c7e588abe499564f97a867db29e03a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="lesson-5-1---copying-the-lesson-4-package"></a>Lektion 5-1: Kopieren des Pakets aus Lektion 4
In dieser Aufgabe erstellen Sie eine Kopie des in Lektion 4 erstellten Pakets namens „Lesson 4.dtsx“. Alternativ können Sie dem Projekt auch das im Tutorial enthaltene, abgeschlossene Paket aus Lektion 4 hinzufügen und anschließend eine Kopie dieses Pakets erstellen. Sie werden diese neue Kopie in der gesamten Lektion 5 verwenden.  
  
### <a name="to-copy-the-lesson-4-package"></a>So kopieren Sie das Paket aus Lektion 4  
  
1.  Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools noch nicht geöffnet ist, klicken Sie auf **Start**und zeigen Sie auf **Alle Programme**. Klicken Sie anschließend auf **Microsoft SQL Server 2012**und danach auf **SQL Server Data Tools**.  
  
2.  Klicken Sie im Menü **Datei** auf **Öffnen**&gt; **Projekt/Projektmappe**. Wählen Sie **SSIS Tutorial** aus, klicken Sie auf **Öffnen**und anschließend auf **SSIS Tutorial.sln**.  
  
3.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Lesson 4.dtsx**, und klicken Sie anschließend auf **Kopieren**.  
  
4.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **SSIS-Pakete**und anschließend auf **Einfügen**.  
  
    Standardmäßig wird das kopierte Paket „Lesson 5.dtsx“ benannt.  
  
5.  Doppelklicken Sie im Projektmappen-Explorer auf **Lesson 5.dtsx** , um das Paket zu öffnen.  
  
6.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im Hintergrund der Registerkarte **Ablaufsteuerung** und anschließend auf **Eigenschaften**.  
  
7.  Aktualisieren Sie im Eigenschaftenfenster die **Name** -Eigenschaft auf **Lektion 5**.  
  
8.  Klicken Sie in das Feld für die **ID** -Eigenschaft, klicken Sie auf den Dropdownpfeil, und klicken Sie zuletzt auf **<Generate New ID>**.  
  
### <a name="to-add-the-completed-lesson-4-package"></a>So fügen Sie das abgeschlossene Paket aus Lektion 4 hinzu  
  
1.  Öffnen Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools und das SSIS-Lernprogrammprojekt.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **SSIS-Pakete**, und klicken Sie auf **Vorhandenes Paket hinzufügen**.  
  
3.  Wählen Sie im Dialogfeld **Kopie des vorhandenen Pakets hinzufügen** unter **Paketspeicherort**die Option **Dateisystem**aus.  
  
4.  Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , navigieren Sie zu **Lesson 4.dtsx** auf Ihrem Computer, und klicken Sie anschließend auf **Öffnen**.  
  
    Um alle Lektionspakete für dieses Lernprogramm herunterzuladen, gehen Sie wie folgt vor.  
  
    1.  Klicken Sie [hier](http://go.microsoft.com/fwlink/?LinkId=275027), um zur Seite Integration Services Product Samples zu gelangen  
  
    2.  Klicken Sie auf die Registerkarte **DOWNLOADS** .  
  
    3.  Klicken Sie auf die Datei SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
5.  Kopieren Sie das Paket aus Lektion 4, und fügen Sie es gemäß den Schritten 3 bis 8 der vorherigen Prozedur ein.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Schritt 2: Aktivieren und Konfigurieren von Paketkonfigurationen](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
