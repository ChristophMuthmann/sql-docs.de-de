---
title: Verarbeiten einer Miningstruktur | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], processing
ms.assetid: 4162f33e-c23f-4293-8905-271781e45fa4
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2e9c6f31a8701571b2d9be03eecd34050757e7a7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="process-a-mining-structure"></a>Verarbeiten einer Miningstruktur
  Bevor Sie die einer Miningstruktur zugeordneten Miningmodelle durchsuchen und verwenden können, müssen Sie das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt bereitstellen und die Miningstruktur und die Miningmodelle verarbeiten. Wenn Sie eine Änderung an der Miningstruktur oder den Miningmodellen vornehmen, werden Sie zur erneuten Bereitstellung und Verarbeitung aufgefordert. Beim Verarbeiten der Struktur auf der Registerkarte **Miningstruktur** des Data Mining-Designers von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] werden auch alle zugeordneten Modelle verarbeitet.  
  
 Sie können eine Miningstruktur mit den folgenden Tools verarbeiten:  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   XMLA: Process-Befehl  
  
 Informationen zum Verarbeiten einzelner Modelle finden Sie unter [Verarbeiten eines Miningmodells](../../analysis-services/data-mining/process-a-mining-model.md).  
  
### <a name="to-process-a-mining-structure-and-all-associated-mining-models-using-sql-server-data-tools"></a>So verarbeiten Sie eine Miningstruktur und alle zugeordneten Miningmodelle mit SQL Server-Datentools  
  
1.  Wählen Sie in **im Menüelement** Miningmodell **die Option** Miningstruktur und alle Modelle verarbeiten [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]aus.  
  
     Wenn Sie Änderungen an der Struktur vorgenommen haben, werden Sie aufgefordert, die Struktur erneut bereitzustellen, bevor die Modelle verarbeitet werden. Klicken Sie auf **Ja**.  
  
2.  Klicken Sie auf **ausführen** in der **Miningstruktur verarbeiten - \<Struktur >** (Dialogfeld).  
  
     Das Dialogfeld **Verarbeitungsstatus** wird geöffnet und zeigt detaillierte Informationen zur Verarbeitung des Modells an.  
  
3.  Klicken Sie nach Abschluss der Modellverarbeitung im Dialogfeld **Verarbeitungsstatus** auf **Schließen** .  
  
4.  Klicken Sie auf **schließen** in der **Miningstruktur verarbeiten - \<Struktur >** (Dialogfeld).  
  
## <a name="see-also"></a>Siehe auch  
 [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
