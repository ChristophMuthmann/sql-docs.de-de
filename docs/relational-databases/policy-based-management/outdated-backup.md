---
title: Veraltete Sicherung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de64b70cfad30e223bcec8da9025aaa0843752ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="outdated-backup"></a>Obsolete Sicherung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Diese Regel überprüft, ob aktuelle Sicherungen einer Datenbank existieren. Die Planung regelmäßiger Sicherungen ist wichtig, um die Datenbanken vor Datenverlust aufgrund vieler verschiedener Fehler zu schützen. Die geeignete Häufigkeit der Datensicherung hängt vom Wiederherstellungsmodell der Datenbank und von den Unternehmensrichtlinien hinsichtlich potenziellen Datenverlusts ab sowie davon, wie oft die Datenbank aktualisiert wird. Wird die Datenbank häufig aktualisiert, steigt die Gefahr des Datenverlusts zwischen den Sicherungsvorgängen stark an.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Wir empfehlen, dass Sie Sicherungen häufig genug ausführen, um Datenbanken vor Datenverlust zu schützen.  
  
 Sowohl das einfache als auch das vollständige Wiederherstellungsmodell erfordern Datensicherungen. In beiden Wiederherstellungsmodellen können Sie jede vollständige Sicherung mit differenziellen Sicherungen ergänzen, um das Risiko eines Datenverlusts zu verringern.  
  
 Für Datenbanken, die das vollständige Wiederherstellungsmodell verwenden, empfehlen wir häufige Protokollsicherungen. Von einer Produktionsdatenbank mit sehr wichtigen Daten sollten Protokollsicherungen in der Regel alle 1 bis 15 Minuten erstellt werden.  
  
> [!NOTE]  
>  Die empfohlene Methode zur Planung von Sicherungen ist ein Datenbankwartungsplan.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Sichern und Wiederherstellen von Systemdatenbanken &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Wiederherstellungsmodelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
 [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
 [Transaktionsprotokollsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
