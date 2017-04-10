---
title: "Ausf&#252;hren eines Pakets in SQL Server-Datentools | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services-Pakete, Ausführen"
  - "SSIS-Pakete, ausführen"
  - "Pakete [Integration Services], ausführen"
  - "SQL Server Integration Services-Pakete, ausführen"
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Ausf&#252;hren eines Pakets in SQL Server-Datentools
  Das Ausführen von Paketen in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erfolgt zumeist beim Entwickeln, Debuggen und Testen von Paketen. Wenn Sie ein Paket im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer ausführen, wird das Paket immer sofort ausgeführt.  
  
 Während ein Paket ausgeführt wird, zeigt der [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer den Fortschritt der Paketausführung auf der **Status** -Registerkarte an. Sie können den Start- und Endzeitpunkt des Pakets sowie seine Tasks und Container sehen. Außerdem werden Informationen über Tasks und Container im Paket angezeigt, deren Ausführung fehlerhaft ist. Wenn die Ausführung des Pakets beendet wurde, sind die Laufzeitinformationen weiterhin auf der Registerkarte **Ausführungsergebnisse** verfügbar. Weitere Informationen finden Sie im Abschnitt "Fortschrittsberichte" im Thema [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Entwurfszeitbereitstellung**. Wenn Sie ein Paket in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]ausführen, wird das Paket erstellt und dann in einem Ordner bereitgestellt. Vor dem Ausführen des Pakets können Sie den Ordner angeben, in dem das Paket bereitgestellt wird. Wenn Sie keinen Ordner angeben, wird standardmäßig der Ordner **bin** verwendet. Dieser Bereitstellungstyp wird als Entwurfszeitbereitstellung bezeichnet.  
  
### So führen Sie ein Paket in SQL Server-Datentools aus  
  
1.  Wenn die Projektmappe mehrere Projekte enthält, klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekt mit dem Paket, und klicken Sie anschließend auf **Als Startobjekt festlegen**, um das Startprojekt festzulegen.  
  
2.  Wenn das Projekt mehrere Pakete enthält, klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, und klicken Sie anschließend auf **Als Startobjekt** festlegen, um das Startpaket festzulegen.  
  
3.  Sie können ein Paket mit einem der folgenden Schritte ausführen:  
  
    -   Öffnen Sie das Paket, das Sie ausführen möchten, und klicken Sie auf der Menüleiste auf **Debuggen starten** , oder drücken Sie F5. Nachdem das Paket ausgeführt wurde, drücken Sie UMSCHALT+F5, um zum Entwurfsmodus zurückzukehren.  
  
    -   Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Paket, und klicken Sie anschließend auf **Paket ausführen**.  
  
### So geben Sie einen anderen Ordner für die Entwurfszeitbereitstellung an  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projektordner, der das auszuführende Paket enthält. Klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **\<Projektname>-Eigenschaftenseiten** auf **Erstellen**.  
  
3.  Aktualisieren Sie den Wert der OutputPath-Eigenschaft, und geben Sie den Ordner an, den Sie für die Entwurfszeitbereitstellung verwenden möchten. Klicken Sie anschließend auf **OK**.  
  
## Siehe auch  
 [Ausführung von Projekten und Paketen](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Integration Services-Pakete (SSIS)](https://msdn.microsoft.com/library/ms141134.aspx)  
  
  