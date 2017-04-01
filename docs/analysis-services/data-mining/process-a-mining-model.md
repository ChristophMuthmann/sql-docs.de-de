---
title: "Verarbeiten eines Miningmodells | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Miningmodelle [Analysis Services], verarbeiten"
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 32
---
# Verarbeiten eines Miningmodells
  Auf der Registerkarte Miningmodelle im Data Mining-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können Sie ein bestimmtes Miningmodell verarbeiten, das einer Miningstruktur zugeordnet ist. Sie können auch alle Modelle verarbeiten, die der Struktur zugeordnet sind.  
  
 Sie können ein Miningmodell mit den folgenden Tools verarbeiten:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Sie können auch einen XMLA Process-Befehl verwenden. Weitere Informationen finden Sie unter [Tools und Ansätze für die Verarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### Verarbeiten eines einzelnen Miningmodells mit SQL Server-Datentools  
  
1.  Wählen Sie auf der Registerkarte **Miningmodelle** des Data Mining-Designers ein Miningmodell aus einer oder mehreren Spalten der Modelle im Raster aus.  
  
2.  Klicken Sie im Menü **Miningmodell** auf **Modell verarbeiten**.  
  
     Falls Sie Änderungen an der Miningstruktur vorgenommen haben, werden Sie aufgefordert, die Struktur erneut bereitzustellen, bevor Sie das Modell verarbeiten. Klicken Sie auf **Ja**.  
  
3.  Klicken Sie im Dialogfeld zum **Verarbeiten des Miningmodells- \<Modell>** auf **Ausführen**.  
  
     Das Dialogfeld **Verarbeitungsstatus** wird geöffnet und zeigt Informationen zur Verarbeitung des Modells an.  
  
4.  Nachdem die Modellverarbeitung erfolgreich abgeschlossen ist, klicken Sie im Dialogfeld **Verarbeitungsstatus** auf **Schließen** .  
  
5.  Klicken Sie im Dialogfeld zum **Verarbeiten des Miningmodells- \<Model**** auf >Schließen**.  
  
 Es wurden lediglich die Miningstruktur und das ausgewählte Miningmodell verarbeitet.  
  
### Verarbeiten aller Miningmodelle, die einer Miningstruktur zugeordnet sind  
  
1.  Wählen Sie auf der Registerkarte **Miningmodelle** im Data Mining-Designer aus dem Menü **Miningmodell** die Option **Miningstruktur und alle Modelle verarbeiten** aus.  
  
2.  Falls Sie Änderungen an der Miningstruktur vorgenommen haben, werden Sie aufgefordert, die Struktur erneut bereitzustellen, bevor Sie die Modelle verarbeiten. Klicken Sie auf **Ja**.  
  
3.  Klicken Sie im Dialogfeld zum **Verarbeiten der Miningstruktur - \<Struktur>**auf **Ausführen**.  
  
4.  Das Dialogfeld **Verarbeitungsstatus** wird geöffnet und zeigt Informationen zur Verarbeitung des Modells an.  
  
5.  Nachdem die Modellverarbeitung erfolgreich abgeschlossen ist, klicken Sie im Dialogfeld **Verarbeitungsstatus** auf **Schließen** .  
  
6.  Klicken Sie im Dialogfeld zur **Verarbeitung des \<Modells>** auf **Schließen**.  
  
 Die Miningstruktur und alle zugeordneten Miningmodelle wurden verarbeitet.  
  
## Siehe auch  
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  