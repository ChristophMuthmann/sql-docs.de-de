---
title: Erstellen und Verwalten von Tabellenmodellpartitionen | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 10c539b5d30d5c1acca4e21b07ddaf9761833818
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-tabular-model-partitions"></a>Erstellen und Verwalten von tabellenmodellpartitionen
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Durch Partitionen wird eine Tabelle logisch unterteilt. Jede Partition kann unabhängig von anderen Partitionen verarbeitet (aktualisiert) werden. Während der Modellerstellung werden die für ein Modell definierten Partitionen in ein bereitgestelltes Modell dupliziert. Nach der Bereitstellung können Sie diese Partitionen mit dem Dialogfeld **Partitionen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder mithilfe eines Skripts verwalten. In den Tasks in diesem Thema wird beschrieben, wie Partitionen für ein bereitgestelltes Modell erstellt und verwaltet werden.  
  
  > [!NOTE]  
>  Partitionen in tabellarischen Modellen mit Kompatibilitätsgrad 1400 erstellt werden mit einer M-Abfrage-Anweisung definiert. Weitere Informationen finden Sie unter [M Verweis](https://msdn.microsoft.com/library/mt211003.aspx). 
>
  
## <a name="tasks"></a>Aufgaben  
 Um Partitionen für die bereitgestellte Datenbank eines tabellarischen Modells zu erstellen und zu verwalten, verwenden Sie das Dialogfeld **Partitionen** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Um das Dialogfeld **Partitionen** anzuzeigen, klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]mit der rechten Maustaste auf eine Tabelle und klicken dann auf **Partitionen**.  
  
###  <a name="bkmk_create_new"></a> So erstellen Sie eine neue Partition  
  
1.  Klicken Sie im Dialogfeld **Partitionen** auf die Schaltfläche **Neu** .  
  
2.  Geben Sie in **Partitionsname**einen Namen für die Partition ein. Der Name der Standardpartition wird für jede neue Partition inkrementell erhöht.  
  
3.  In **Abfrageanweisung**, geben oder fügen Sie eine SQL- oder M-Abfrage-Anweisung, die definiert, die Spalten und Klauseln in der Partition in das Abfragefenster ein enthalten sein sollen.  
  
4.  Um die Anweisung zu überprüfen, klicken Sie auf **Syntax überprüfen**.  
  
###  <a name="bkmk_copy"></a> So kopieren Sie eine Partition  
  
1.  Wählen Sie im Dialogfeld **Partitionen** in der Liste **Partitionen** die Partition aus, die Sie kopieren möchten, und klicken Sie dann auf die Schaltfläche **Kopieren** .  
  
2.  Geben Sie in **Partitionsname**einen neuen Namen für die Partition ein.  
  
3.  In **Abfrageanweisung**, die abfrageanweisung bearbeiten.  
  
###  <a name="bkmk_merge"></a> So führen Sie Partitionen zusammen  
  
-   Wählen Sie im Dialogfeld **Partitionen** in der Liste **Partitionen** mithilfe von STRG-Klicken die Partitionen aus, die Sie zusammenführen möchten, und klicken Sie dann auf die Schaltfläche **Zusammenführen** .  
  
> [!IMPORTANT]  
>  Beim Zusammenführen von Partitionen werden die Partitionsmetadaten nicht aktualisiert. Bearbeiten Sie die SQL- oder M-Anweisung für die resultierende Partition aus, um sicherzustellen, dass die Verarbeitung von Vorgängen auf alle Daten in der zusammengeführten Partition verarbeitet.  
  
###  <a name="bkmk_delete"></a> So löschen Sie eine Partition  
  
-   Wählen Sie im Dialogfeld **Partitionen** in der Liste **Partitionen** die Partition aus, die Sie löschen möchten, und klicken Sie dann auf die Schaltfläche **Löschen** .  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenmodellpartitionen](../../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)   
 [Verarbeiten von tabellenmodellpartitionen](../../analysis-services/tabular-models/process-tabular-model-partitions-ssas-tabular.md)  
  
  
