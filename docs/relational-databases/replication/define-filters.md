---
title: "Filter definieren | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.definefilters.f1"
helpviewer_keywords: 
  - "Filter definieren (Dialogfeld)"
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Filter definieren
  Im Dialogfeld **Filter definieren** können Sie Filter definieren, die Sie anschließend bei Datenkonflikten anwenden, um eine Untermenge der Konflikte im Raster anzuzeigen. Um einen Filter zu definieren, wählen Sie einen Operator aus der **Operator** Dropdown-Liste aus und geben Sie einen Wert. Beispielsweise, um nur die Konflikte anzuzeigen, ist der Verlierer des Konflikts Server **ReplTest1**, auf **gleich** aus der **Operator** Dropdown-Liste ein, und geben Sie **ReplTest1** in der ersten **Wert** Spalte.  
  
## Optionen  
 **Operator**  
 Wählen Sie einen Operator für den Filter ein, z. B. **kleiner als oder gleich**.  
  
 **Wert**  
 Geben Sie einen Wert für den Filter ein. Für die meisten Operatoren muss nur in der ersten **Value** -Spalte ein Wert eingegeben werden. Für die Operatoren **Zwischen** und **Nicht zwischen** muss jedoch in beide **Value** -Spalten ein Wert eingegeben werden.  
  
 **Löschen**  
 Klicken Sie auf diese Schaltfläche, um alle zuvor definierten Filter zu löschen.  
  
## Siehe auch  
 [Replikationskonflikt-Viewer von Microsoft & #40; Mergereplikation & #41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Replikationskonflikt-Viewer von Microsoft & #40; Transaktionsreplikation & #41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  