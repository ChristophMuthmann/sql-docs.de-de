---
title: "Erstellen und Verwalten von Partitionen in der Arbeitsbereichsdatenbank (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.partitionmgr.f1
ms.assetid: 0b3027d6-652b-4eb3-a197-58b25df65218
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 094dc11c2d13ec23575a40ce41c1369080f11d40
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="create-and-manage-partitions-in-the-workspace-database-ssas-tabular"></a>Erstellen und Verwalten von Partitionen in der Arbeitsbereichsdatenbank (SSAS – tabellarisch)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Partitionen unterteilt eine Tabelle logisch. Die einzelnen Partitionen können dann unabhängig voneinander oder parallel mit anderen Partitionen verarbeitet (aktualisiert) werden. Durch Partitionen kann sich die Skalierbarkeit und Verwaltbarkeit großer Datenbanken verbessern. Standardmäßig verfügt jede Tabelle über eine Partition, die alle Spalten einschließt. In diesem Thema wird beschrieben, wie Partitionen in der Arbeitsbereichsdatenbank des Modells unter Verwendung des Dialogfelds **Partitions-Manager** in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
 Nachdem ein Modell für eine andere Analysis Services-Instanz bereitgestellt wurde, können Datenbankadministratoren Partitionen im (bereitgestellten) Modell mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen und verwalten. Weitere Informationen finden Sie unter [Erstellen und Verwalten von Tabellenmodellpartitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
 Dieses Thema umfasst folgende Aufgaben:  
  
-   [So erstellen Sie eine neue Partition](#bkmk_create_new)  
  
-   [So kopieren Sie eine Partition](#bkmk_copy)  
  
-   [So löschen Sie eine Partition](#bkmk_delete)  
  
> [!NOTE]  
>  Partitionen in der Arbeitsbereichsdatenbank des Modells können nicht mithilfe des Dialogfelds Partitions-Manager zusammengeführt werden. Partitionen können in einem bereitgestellten Modell nur mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zusammengeführt werden.  
  
## <a name="tasks"></a>Aufgaben  
 Um Partitionen zu erstellen und zu verwalten, verwenden Sie das Dialogfeld **Partitions-Manager** . Sie öffnen das Dialogfeld **Partitions-Manager** , indem Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Tabelle** und dann auf **Partitionen**klicken.  
  
###  <a name="bkmk_create_new"></a> So erstellen Sie eine neue Partition  
  
1.  Wählen Sie im Modell-Designer die Tabelle aus, für die Sie eine Partition definieren möchten.  
  
2.  Klicken Sie auf das Menü **Tabelle** und dann auf **Partitionen**.  
  
3.  Überprüfen Sie, ob im **Partitions-Manager**im Listenfeld **Tabelle** die richtige Tabelle angezeigt wird, oder wählen Sie die zu partitionierende Tabelle aus, und klicken Sie auf **Neu**.  
  
4.  Geben Sie in **Partitionsname**einen Namen für die Partition ein. Der Name der Standardpartition wird für jede neue Partition inkrementell erhöht.  
  
5.  Sie können die in die Partition einzufügenden Zeilen und Spalten auswählen, indem Sie den Tabellenvorschaumodus oder eine SQL-Abfrage verwenden, die im Abfrage-Editor-Modus erstellt wurde.  
  
     Klicken Sie nahe der oberen rechten Ecke des Vorschaufensters auf die Schaltfläche **Tabellenvorschau** , um den Tabellenvorschaumodus (Standard) zu verwenden. Wählen Sie die in die Partition einzuschließenden Spalten aus, indem Sie das Kontrollkästchen neben dem Spaltennamen aktivieren. Um Zeilen zu filtern, klicken Sie mit der rechten Maustaste auf einen Zellenwert, und klicken Sie auf **Nach dem Wert der ausgewählten Zelle filtern**.  
  
     Klicken Sie nahe der oberen rechten Ecke des Vorschaufensters auf die Schaltfläche **Abfrage-Editor** , um eine SQL-Anweisung zu verwenden. Geben Sie anschließend im Abfragefenster eine SQL-Abfrage-Anweisung ein (oder kopieren und fügen Sie die Anweisung aus einem anderen Text ein). Um die Anweisung zu überprüfen, klicken Sie auf **Überprüfen**. Um den Abfrage-Designer zu verwenden, klicken Sie auf **Entwurf**.  
  
###  <a name="bkmk_copy"></a> So kopieren Sie eine Partition  
  
1.  Überprüfen Sie, ob im **Partitions-Manager**im Listenfeld **Tabelle** die richtige Tabelle angezeigt wird, oder wählen Sie die Tabelle mit der zu kopierenden Partition aus.  
  
2.  Wählen Sie in der Liste **Partitionen** die zu kopierende Partition aus, und klicken Sie auf **Kopieren**.  
  
3.  Geben Sie in **Partitionsname**einen neuen Namen für die Partition ein.  
  
###  <a name="bkmk_delete"></a> So löschen Sie eine Partition  
  
1.  Überprüfen Sie, ob im **Partitions-Manager**im Listenfeld **Tabelle** die richtige Tabelle angezeigt wird, oder wählen Sie die zu löschende Partition aus.  
  
2.  Wählen Sie in der Liste **Partitionen** die zu löschende Partition aus, und klicken Sie auf **Löschen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [Verarbeiten von Partitionen in der Arbeitsbereichsdatenbank &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)  
  
  
