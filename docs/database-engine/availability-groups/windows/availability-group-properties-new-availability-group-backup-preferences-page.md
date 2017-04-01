---
title: "Eigenschaften der Verf&#252;gbarkeitsgruppe: Neue Verf&#252;gbarkeitsgruppe (Seite Sicherungseinstellungen) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.availabilitygroupproperties.backuppreferences.f1"
helpviewer_keywords: 
  - "Schreibgeschütztes Routing"
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
caps.latest.revision: 7
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 7
---
# Eigenschaften der Verf&#252;gbarkeitsgruppe: Neue Verf&#252;gbarkeitsgruppe (Seite Sicherungseinstellungen)
  Verwenden Sie dieses Dialogfeld, um die Sicherungseinstellungen der ausgewählten Verfügbarkeitsgruppe anzuzeigen und zu ändern.  
  
 **So zeigen Sie Verfügbarkeitsgruppeneigenschaften an**  
  
-   [Anzeigen von Verfügbarkeitsgruppeneigenschaften &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../Topic/Use%20the%20Always On%20Dashboard%20\(SQL%20Server%20Management%20Studio\).md)  
  
## Wo sollten Sicherungen erfolgen?  
 **Sekundär bevorzugen**  
 Gibt an, dass Sicherungen auf einem sekundären Replikat erfolgen müssen, außer wenn es sich beim primären Replikat um das einzige Onlinereplikat handelt. In diesem Fall muss die Sicherung auf dem primären Replikat erfolgen. Diese Option ist die Standardeinstellung.  
  
 **Nur sekundär**  
 Gibt an, dass Sicherungen nie auf dem primären Replikat ausgeführt werden dürfen. Wenn es sich beim primären Replikat um das einzige Onlinereplikat handelt, darf keine Sicherung erfolgen.  
  
 **Primär**  
 Gibt an, dass die Sicherungen immer auf dem primären Replikat erfolgen müssen. Diese Option ist hilfreich, wenn Sie Sicherungsfunktionen benötigen, z. B. das Erstellen differenzieller Sicherungen, die nicht unterstützt werden, wenn die Sicherung auf einem sekundären Replikat ausgeführt wird.  
  
 **Beliebiges Replikat**  
 Gibt an, dass Sicherungsaufträge die Rolle der Verfügbarkeitsreplikate ignorieren sollen, wenn sie das Replikat zum Durchführen der Sicherungen auswählen. Sicherungsaufträge können andere Faktoren auswerten, wie z. B. die Sicherungspriorität jedes Verfügbarkeitsreplikats in Verbindung mit seinem Betriebszustand und Verbindungsstatus.  
  
> [!IMPORTANT]  
>  Die Einstellung "backup-preference" wird nicht erzwungen. Die Interpretation dieser Einstellung hängt von der Logik ab, die Sie ggf. per Skript in Sicherungsaufträge für die Datenbanken in einer angegebenen Verfügbarkeitsgruppe integriert haben. Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../Topic/Active%20Secondaries:%20Backup%20on%20Secondary%20Replicas%20\(Always On%20Availability%20Groups\).md).  
  
## Replikatssicherungsprioritäten  
 Dieses Raster enthält die aktuelle Sicherungspriorität aller Serverinstanzen, die ein Replikat für die Verfügbarkeitsgruppe hosten. Verwenden Sie dieses Raster, um die Sicherungspriorität von Verfügbarkeitsreplikaten zu ändern.  
  
 **Serverinstanz**  
 Der Name der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], die das Verfügbarkeitsreplikat hostet.  
  
 **Sicherungspriorität (niedrigste = 1, höchste = 100)**  
 Gibt die Priorität für die Ausführung von Sicherungen auf diesem Replikat in Relation zu den anderen Replikaten in derselben Verfügbarkeitsgruppe an. Der Wert liegt im Bereich von 0 bis 100 und ist eine ganze Zahl. 1 gibt die niedrigste Priorität und 100 die höchste Priorität an. Wenn **BACKUP_PRIORITY** 1 ist, würde das Verfügbarkeitsreplikat nur zum Ausführen von Sicherungen ausgewählt werden, wenn gerade keine höheren Prioritätsverfügbarkeitsreplikate verfügbar sind.  
  
 **Replikat ausschließen**  
 Wählen Sie diese Option, wenn dieses Verfügbarkeitsreplikat nie zum Ausführen von Sicherungen ausgewählt werden soll. Dies ist zum Beispiel für ein Remoteverfügbarkeitsreplikat hilfreich, für das keine Failover bei Sicherungen auftreten sollen.  
  
## Siehe auch  
 [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../Topic/Active%20Secondaries:%20Backup%20on%20Secondary%20Replicas%20\(Always On%20Availability%20Groups\).md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  