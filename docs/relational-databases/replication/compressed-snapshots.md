---
title: Komprimierte Momentaufnahmen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], compressed
- snapshot replication [SQL Server], compressed snapshots
- compressed snapshots [SQL Server replication]
ms.assetid: 979ffa7c-3a88-4e70-8cf2-b8d452fd7a7f
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 661a5051ea2377c42394ba20da2bf5f4cdb2817b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="compressed-snapshots"></a>Komprimierte Momentaufnahmen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Das Komprimieren von Momentaufnahmedateien empfiehlt sich, wenn Sie Momentaufnahmen in einem langsamen Netzwerk übertragen, oder wenn Sie große Momentaufnahmen auf einem Wechseldatenträger speichern möchten, die sonst keinen Platz darauf hätten. Das Komprimieren von Momentaufnahmedateien ist in diesen Fällen zwar hilfreich, durch die Komprimierung dauert das Generieren und Anwenden der Momentaufnahme jedoch länger.  
  
 Komprimierte Momentaufnahmedateien werden im [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB-Dateiformat geschrieben, mit dem Dateien von bis zu 2 GB komprimiert werden können (Momentaufnahmedateien mit über 2 GB können nicht komprimiert werden). Dateien müssen zum Komprimieren in einen alternativen Momentaufnahmeordner geschrieben werden (in den Standardmomentaufnahmeordner geschriebene Dateien können nicht komprimiert werden). Weitere Informationen zu alternativen Momentaufnahmeordnern finden Sie unter [Alternative Speicherorte für Momentaufnahmeordner](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
 Dateien werden dort dekomprimiert, wo der Verteilungs-Agent oder der Merge-Agent ausgeführt wird; in der Regel werden Pullabonnements mit komprimierten Momentaufnahme verwendet, sodass Dateien auf dem Abonnenten dekomprimiert werden. Wenn der Abonnent eine komprimierte Datei empfängt, wird die Datei zunächst an einem temporären Speicherort abgelegt. Nachdem die komprimierte Datei auf den Abonnenten kopiert wurde, werden die Momentaufnahmedateien in der Datei jeweils nacheinander vom CAB-Hilfsprogramm dekomprimiert. Der auf dem Abonnenten benötigte Speicherplatz entspricht der Größe der komprimierten Datei plus der größten dekomprimierten Datei.  
  
> [!NOTE]  
>  Komprimierte Momentaufnahmen können in einigen Fällen die Leistung beim Übertragen der Momentaufnahmedateien im Netzwerk verbessern. Beim Komprimieren der Momentaufnahme fällt jedoch zusätzlicher Verarbeitungsaufwand für den Momentaufnahme-Agent an, wenn die Momentaufnahmedateien erstellt werden, sowie für den Verteilungs-Agent oder den Merge-Agent, wenn die Momentaufnahmedateien angewendet werden. Dies könnte das Erstellen von Momentaufnahmen verlangsamen und den Zeitaufwand für das Anwenden einer Momentaufnahme in manchen Fällen erhöhen. Darüber hinaus kann das Übertragen komprimierter Momentaufnahmen bei einem Netzwerkausfall nicht wieder aufgenommen werden, weshalb sie sich nicht für unzuverlässige Netzwerke eignen. Wägen Sie die Vor- und Nachteile sorgfältig ab, wenn Sie komprimierte Momentaufnahmen in einem Netzwerk verwenden.  
  
 **So komprimieren und übermitteln Sie Momentaufnahmedateien**  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Komprimieren von Momentaufnahmedateien &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   Replikation [!INCLUDE[tsql](../../includes/tsql-md.md)] Programmierung: [Konfigurieren von Momentaufnahmeeigenschaften &#40;Replication Transact-SQL Programming&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Initialisieren eines Abonnements mit einer Momentaufnahme](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Momentaufnahmeoptionen](../../relational-databases/replication/snapshot-options.md)  
  
  
