---
title: "&#220;berpr&#252;fen der Einstellung &#39;Max. Anzahl von Arbeitsthreads&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Best Practices [Datenbankmodul]"
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# &#220;berpr&#252;fen der Einstellung &#39;Max. Anzahl von Arbeitsthreads&#39;
  Diese Regel überprüft die Serveroption Max. Anzahl von Arbeitsthreads auf potenziell falsche Einstellungen. Das Festlegen der Option Max. Anzahl von Arbeitsthreads auf einen niedrigen Wert verhindert die prompte Reaktion vieler Threads auf eingehende Clientanforderungen, was dazu führen kann, dass Threads nicht mehr auf die CPU zugreifen können. Legen Sie die Option jedoch auf einen hohen Wert fest, wird möglicherweise Adressraum verschwendet, da jeder aktive Thread auf 64-Bit-Servern bis zu 4 MB Speicherplatz in Anspruch nimmt.  
  
## Empfehlungen zu Best Practices  
 Legen Sie die max. Anzahl von NIB-Arbeitsthreads (Option) auf 0 fest. Dadurch ermittelt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] basierend auf den Benutzeranforderungen automatisch die richtige Anzahl aktiver Arbeitsthreads.  
  
## Weitere Informationen  
 [Konfigurieren der Serverkonfigurationsoption Maximale Anzahl von Arbeitsthreads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  