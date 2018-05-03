---
title: Löschen eines Miningmodells aus einer Miningstruktur | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 38d544972849b8de847467f5fa964f34fed3cd57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>Löschen eines Miningmodells aus einer Miningstruktur
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Miningmodelle können mit dem Data Mining-Designer, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]oder DMX-Anweisungen gelöscht werden.  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>Löschen eines Miningmodells mit SQL Server-Datentools  
  
1.  Wählen Sie die Registerkarte **Miningmodelle** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aus.  
  
2.  Klicken Sie mit der rechten Maustaste auf das zu löschende Modell, und anschließend auf **Löschen**.  
  
     Das Dialogfeld **Objekte löschen** wird angezeigt.  
  
3.  Klicken Sie auf **OK**.  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>Löschen eines Miningmodells mit SQL Server Management Studio  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, die das Modell enthält.  
  
2.  Erweitern Sie **Miningstrukturen**und anschließend **Miningmodelle**.  
  
3.  Klicken Sie mit der rechten Maustaste auf das zu löschende Modell, und anschließend auf **Löschen**.  
  
     Durch Löschen des Modells werden nicht die Trainingsdaten, sondern nur die Metadaten und alle Muster gelöscht, die beim Trainieren des Modells erstellt wurden.  
  
### <a name="delete-a-mining-model-using-dmx"></a>Löschen eines Miningmodells mit DMX  
  
-   [DROP MINING MODEL & #40; DMX & #41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
