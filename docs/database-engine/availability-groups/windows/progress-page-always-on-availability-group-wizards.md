---
title: "Seite „Status“ (Always On-Verfügbarkeitsgruppen-Assistenten) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.adddatabasewizard.progress.f1
- sql13.swb.addreplicawizard.progress.f1
- sql13.swb.newagwizard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 78fd0315e1f58eef1dbc5d8c41f6254817879d8c
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="progress-page-always-on-availability-group-wizards"></a>Seite „Status“ (Always On-Verfügbarkeitsgruppen-Assistenten)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Mithilfe dieses Dialogfelds können Sie den Status eines [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Assistenten anzuzeigen, den Sie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]ausführen. Die Statusanzeige gibt den relativen Status der Schritte an, die der Assistent ausführt.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Weitere Informationen**  
 Klicken Sie auf den Pfeil nach unten, um ein Statusraster anzuzeigen, in der alle ausgeführten Schritte in der entsprechenden Reihenfolge aufgeführt sind, gefolgt vom derzeit laufenden Vorgang. Das Raster enthält die folgenden Spalten:  
  
 **Name**  
 Zeigt einen Ausdruck an, der einen bestimmten Schritt beschreibt.  
  
 **Status**  
 Gibt das Ergebnis ausgeführter Schritte und den Prozentsatz des Abschlusses des aktuellen Schritts wie folgt an:  
  
|Ergebnis|Beschreibung|  
|------------|-----------------|  
|**Fehler**|Gibt an, dass beim Vorgang für diesen Schritt ein Fehler aufgetreten ist. Klicken Sie auf den Link, um ein Meldungsdialogfeld anzuzeigen, das den Fehler beschreibt.|  
|**In Bearbeitung (** *Prozent abgeschlossen* **)**|Gibt an, dass der Vorgang jetzt auftritt, und schätzt den Prozentsatz dieses Schritts, der abgeschlossen wurde.|  
|**Success**|Gibt an, dass der Vorgang für diesen Schritt erfolgreich abgeschlossen wurde.|  
  
 **Weniger Details**  
 Klicken Sie, um das Statusraster auszublenden.  
  
 **Abbrechen**  
 Klicken Sie, um verbleibende Vorgänge zu überspringen, und beenden Sie dann den Assistenten.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [Verwenden des Assistenten für Failover-Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

