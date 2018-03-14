---
title: Definieren von Filtern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4baa09c02936eb9e67bbcbcbf2b69d70253a4111
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="define-filters"></a>Filter definieren
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Im Dialogfeld **Filter definieren** können Sie Filter definieren, die Sie anschließend bei Datenkonflikten anwenden, um eine Untermenge der Konflikte im Raster anzuzeigen. Um einen Filter zu definieren, wählen Sie im Dropdownlistenfeld **Operator** einen Operator aus, und geben Sie dann einen Wert ein. Um beispielsweise nur die Konflikte anzuzeigen, in welchen Server **ReplTest1**der Konfliktverlierer ist, wählen Sie im Dropdown-Listenfeld **Operator** die Option **Gleich** aus, und geben Sie in die erste **Value** -Spalte den Wert **ReplTest1** ein.  
  
## <a name="options"></a>Tastatur  
 **Ist gleich**  
 Wählen Sie für den Filter einen Operator wie **Kleiner als oder gleich**aus.  
  
 **ReplTest1**  
 Geben Sie einen Wert für den Filter ein. Für die meisten Operatoren muss nur in der ersten **Value** -Spalte ein Wert eingegeben werden. Für die Operatoren **Zwischen** und **Nicht zwischen** muss jedoch in beide **Value** -Spalten ein Wert eingegeben werden.  
  
 **Löschen**  
 Klicken Sie auf diese Schaltfläche, um alle zuvor definierten Filter zu löschen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Replikationskonflikt-Viewer von Microsoft &#40;Mergereplikation&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Replikationskonflikt-Viewer von Microsoft &#40;Transaktionsreplikation&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
