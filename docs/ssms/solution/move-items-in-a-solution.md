---
title: Verschieben von Elementen in einer Projektmappe | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-solutions
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e549c4943173ccf23c62c0e12f53cd8203aa064
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="move-items-in-a-solution"></a>Verschieben von Elementen in einer Projektmappe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Projektelemente in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]-Projekten sind Abfragen, Verbindungen und sonstige Dateien. Sie können Abfragen und sonstige Dateien zwischen Projekten im Projektmappen-Explorer verschieben. Verbindungen können aber nicht verschoben werden.  
  
### <a name="to-move-items-in-solution-explorer"></a>So verschieben Sie Elemente im Projektmappen-Explorer  
  
1.  Wählen Sie im Projektmappen-Explorer das Element aus, das Sie verschieben möchten.  
  
2.  Klicken Sie im Menü **Bearbeiten** auf **Ausschneiden**.  
  
3.  Wählen Sie den Zielordner im Projektmappen-Explorer aus.  
  
4.  Klicken Sie im Menü **Bearbeiten** auf **Einfügen**.  
  
Sie können Elemente durch Ziehen von Abfragen und sonstigen Dateien innerhalb des Projektmappen-Explorers verschieben. Beim Ziehen sehen Sie das Ergebnis des Ziehvorgangs. Wenn Abfragen aus einem Projekttyp in einen anderen verschoben werden, können die Abfragen im Zielprojekt möglicherweise als sonstige Dateien betrachtet werden.  
  
> [!NOTE]  
> Wenn eine verbundene Abfrage verschoben wird, wird nicht die Verbindung in das Zielprojekt verschoben. Die Abfrage verliert die Verbindung, nachdem sie in das Zielprojekt verschoben wurde.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Projektmappen-Explorer](../../ssms/solution/solution-explorer.md)  
[Kopieren von Elementen in einer Projektmappe](../../ssms/solution/copy-items-in-a-solution.md)  
  
