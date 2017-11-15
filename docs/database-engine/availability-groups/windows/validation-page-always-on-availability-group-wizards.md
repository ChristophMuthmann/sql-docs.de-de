---
title: "Seite „Überprüfung“ (Always On-Verfügbarkeitsgruppen-Assistenten) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.addreplicawizard.validation.f1
- sql13.swb.adddatabasewizard.validation.f1
- sql13.swb.newagwizard.validation.f1
helpviewer_keywords: ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 715d425c6a9a252f9f0d444eb6f51bfdf43122d4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="validation-page-always-on-availability-group-wizards"></a>Seite „Überprüfung“ (Always On-Verfügbarkeitsgruppen-Assistenten)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  
    
  In diesem Hilfethema werden die Optionen der Seite **Überprüfung** beschrieben. Dieses Thema gilt für [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]und [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Verwenden Sie diese Seite, um zu überprüfen, ob die Umgebung alle auf vorherigen Seiten des Assistenten festgelegte Konfigurationsoptionen unterstützt.  
  
##  <a name="PageOptions"></a> Optionen auf der Seite "Überprüfung"  
 **Ergebnisse der Verfügbarkeitsgruppenüberprüfung.**  
 Dieses Raster zeigt die Ergebnisse jedes ausgeführten Überprüfungsschritts an. Es gibt folgende Rasterspalten:  
  
 **Name**  
 Zeigt einen Ausdruck an, der einen bestimmten Schritt beschreibt.  
  
 **Ergebnis**  
 Zeigt einen der folgenden Linktexte an. Klicken Sie auf den Link, um weitere Informationen zum Ergebnis eines bestimmten Überprüfungsschritts anzuzeigen.  
  
|Ergebnis|Beschreibung|  
|------------|-----------------|  
|**Fehler**|Gibt an, dass der Überprüfungsschritt fehlgeschlagen ist. Klicken Sie auf den Link, um die Fehlermeldung anzuzeigen.|  
|**Ausgelassen**|Gibt an, dass der Überprüfungsschritt ausgelassen wurde, da er für die Optionen nicht erforderlich ist. Klicken Sie auf den Link, um die Ursache für das Auslassen eines Schritts anzuzeigen.|  
|**Success**|Gibt an, dass der Überprüfungsschritt erfolgreich abgeschlossen wurde.|  
|**Warnung**|Zeigt ein potenzielles Problem mit der Verfügbarkeitsgruppenkonfiguration an.  Klicken Sie auf den Link, um die Warnmeldung anzuzeigen.|  
  
 **Überprüfung erneut ausführen**  
 Klicken Sie, um die Überprüfungsschritte zu wiederholen, wenn Sie außerhalb des Assistenten als Reaktion auf einen Überprüfungsfehler eine Änderung vornehmen.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Verwenden des Dialogfelds „Neue Verfügbarkeitsgruppe“ &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
