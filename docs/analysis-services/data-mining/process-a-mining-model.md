---
title: Verarbeiten eines Miningmodells | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: mining models [Analysis Services], processing
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5bf9d1f64c100a69411b54efc7b371fc327f12cb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="process-a-mining-model"></a>Verarbeiten eines Miningmodells
  Auf der Registerkarte Miningmodelle im Data Mining-Designer von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]können Sie ein bestimmtes Miningmodell verarbeiten, das einer Miningstruktur zugeordnet ist. Sie können auch alle Modelle verarbeiten, die der Struktur zugeordnet sind.  
  
 Sie können ein Miningmodell mit den folgenden Tools verarbeiten:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 Sie können auch einen XMLA Process-Befehl verwenden. Weitere Informationen finden Sie unter [Tools und Ansätze für die Verarbeitung &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md).  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>Verarbeiten eines einzelnen Miningmodells mit SQL Server-Datentools  
  
1.  Wählen Sie auf der Registerkarte **Miningmodelle** des Data Mining-Designers ein Miningmodell aus einer oder mehreren Spalten der Modelle im Raster aus.  
  
2.  Klicken Sie im Menü **Miningmodell** auf **Modell verarbeiten**.  
  
     Falls Sie Änderungen an der Miningstruktur vorgenommen haben, werden Sie aufgefordert, die Struktur erneut bereitzustellen, bevor Sie das Modell verarbeiten. Klicken Sie auf **Ja**.  
  
3.  In der **Verarbeiten des Miningmodells - \<Modell >** (Dialogfeld), klicken Sie auf **ausführen**.  
  
     Das Dialogfeld **Verarbeitungsstatus** wird geöffnet und zeigt Informationen zur Verarbeitung des Modells an.  
  
4.  Nachdem die Modellverarbeitung erfolgreich abgeschlossen ist, klicken Sie im Dialogfeld **Verarbeitungsstatus** auf **Schließen** .  
  
5.  Klicken Sie auf **schließen** in der **Verarbeiten des Miningmodells - \<Modell >** (Dialogfeld).  
  
 Es wurden lediglich die Miningstruktur und das ausgewählte Miningmodell verarbeitet.  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>Verarbeiten aller Miningmodelle, die einer Miningstruktur zugeordnet sind  
  
1.  Wählen Sie auf der Registerkarte **Miningmodelle** im Data Mining-Designer aus dem Menü **Miningmodell** die Option **Miningstruktur und alle Modelle verarbeiten** aus.  
  
2.  Falls Sie Änderungen an der Miningstruktur vorgenommen haben, werden Sie aufgefordert, die Struktur erneut bereitzustellen, bevor Sie die Modelle verarbeiten. Klicken Sie auf **Ja**.  
  
3.  In der **Miningstruktur verarbeiten - \<Struktur >** (Dialogfeld), klicken Sie auf **ausführen**.  
  
4.  Das Dialogfeld **Verarbeitungsstatus** wird geöffnet und zeigt Informationen zur Verarbeitung des Modells an.  
  
5.  Nachdem die Modellverarbeitung erfolgreich abgeschlossen ist, klicken Sie im Dialogfeld **Verarbeitungsstatus** auf **Schließen** .  
  
6.  Klicken Sie auf **schließen** in der **Verarbeitung \<Modell >** (Dialogfeld).  
  
 Die Miningstruktur und alle zugeordneten Miningmodelle wurden verarbeitet.  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
