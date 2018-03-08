---
title: "Angeben der Seite „Optionen der Verfügbarkeitsgruppe“ (Assistent für neue Verfügbarkeitsgruppen/Assistent zum Hinzufügen von Datenbanken) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c12b2607c1f1ecd50d61e2b73646b040a2bbc338
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="specify-availability-group-options-page"></a>Angeben der Seite „Optionen der Verfügbarkeitsgruppe“
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema werden die Optionen der Seite **Namen der Verfügbarkeitsgruppe angeben** beschrieben. Dieses Thema wird sowohl von [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] als auch von [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]verwendet.  
  
##  <a name="PageOptions"></a> Angeben der Optionen für Verfügbarkeitsgruppen  
 **Name der Verfügbarkeitsgruppe**  
 Geben Sie den Namen der Verfügbarkeitsgruppe an. Geben Sie für eine neue Verfügbarkeitsgruppe einen gültigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Bezeichner an, der in allen Verfügbarkeitsgruppen im Windows Server-Failovercluster (WSFC) eindeutig ist. Die maximale Länge eines Verfügbarkeitsgruppennamens beträgt 128 Zeichen.  

 **Clustertyp** Geben Sie als nächstes den Clustertyp an. Die möglichen Clustertypen hängen von der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Version und dem Betriebssystem ab. Wählen Sie einen aus der folgenden Liste aus:

   * **Windows Server-Failoverclustering**
   
      Verwenden Sie diesen Clustertyp, wenn die Verfügbarkeitsgruppe auf einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gehostet ist, die zu einem Windows Server-Failovercluster für Hochverfügbarkeit und Notfallwiederherstellung gehört. Gilt für alle unterstützten Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 

   * **EXTERNAL**
      
      Verwenden Sie diesen Clustertyp, wenn die Verfügbarkeitsgruppe auf einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gehostet ist, die von einer externen Clustertechnologie für Hochverfügbarkeit und Notfallwiederherstellung verwaltet wird, z.B. Pacemaker unter Linux. Gilt für [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] und höher.

   * **NONE**
      
      Verwenden Sie diesen Clustertyp, wenn die Verfügbarkeitsgruppe auf einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gehostet ist, die nicht von einer Clustertechnologie für Leseskalierung und Lastenausgleich verwaltet wird. Gilt für [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] und höher. 
 
   **Integritätserkennung auf Datenbankebene** Aktivieren Sie dieses Kontrollkästchen, um die Option „Integritätserkennung auf Datenbankebene“ (DB_FAILOVER) für die Verfügbarkeitsgruppe zu aktivieren. Die Datenbank-Integritätserkennung erkennt, wenn eine Datenbank sich nicht mehr im Onlinestatus befindet oder ein Fehler auftritt und löst ein automatisches Failover der Verfügbarkeitsgruppe aus. Siehe [SQL Server Always On Database Health Detection Failover Option (SQL Server Always On-Failoveroption zur Datenbank-Integritätserkennung)](sql-server-always-on-database-health-detection-failover-option.md).


Select Databases Page (New Availability Group Wizard and Add Database Wizard)  
  
##  <a name="LaunchWiz"></a> Verwandte Aufgaben  
  
-   [Verwenden des Dialogfelds Neue Verfügbarkeitsgruppe &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
