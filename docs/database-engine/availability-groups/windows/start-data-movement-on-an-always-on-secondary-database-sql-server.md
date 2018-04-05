---
title: Starten der Datenverschiebung auf einer sekundären Always On-Datenbank (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], databases
ms.assetid: 498eb3fb-6a43-434d-ad95-68a754232c45
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0a2f1e376bb44ba9920edf954c4979a397c7ceb1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="start-data-movement-on-an-always-on-secondary-database-sql-server"></a>Starten der Datenverschiebung auf einer sekundären Always On-Datenbank (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält Informationen zum Starten der Datensynchronisierung, nachdem Sie einer Always On-Verfügbarkeitsgruppe eine Datenbank hinzugefügt haben. Für jedes neue primäre Replikat müssen sekundäre Datenbanken auf den Serverinstanzen vorbereitet werden, die die sekundären Replikate hosten. Dann muss jede dieser sekundären Datenbanken manuell mit der Verfügbarkeitsgruppe verknüpft werden.  
  
> [!NOTE]  
>  Wenn die Dateipfade auf jeder Serverinstanz, die ein Verfügbarkeitsreplikat für eine Verfügbarkeitsgruppe hostet, identisch sind, kann der [Assistent für neue Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md), der [Assistent zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)oder der [Assistent zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md) unter Umständen die Datensynchronisierung automatisch starten.  
  
 Um die Datensynchronisierung manuell zu starten, müssen Sie wiederum eine Verbindung mit jeder Serverinstanz herstellen, die ein sekundäres Replikat für die Verfügbarkeitsgruppe hostet, und die folgenden Schritte ausführen:  
  
1.  Stellen Sie aktuelle Sicherungen jeder primären Datenbank und ihres Transaktionsprotokolls (mithilfe von RESTORE WITH NORECOVERY) wieder her. Sie können einen der folgenden alternativen Ansätze verwenden:  
  
    -   Stellen Sie manuell mit RESTORE WITH NORECOVERY eine aktuelle Datenbanksicherung der primären Datenbank wieder her, und stellen Sie dann jede nachfolgende Protokollsicherung mit RESTORE WITH NORECOVERY wieder her. Führen Sie diese Wiederherstellungssequenz auf jeder Serverinstanz aus, die ein sekundäres Replikat für die Verfügbarkeitsgruppe hostet.  
  
         **Weitere Informationen:**  
  
         [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
    -   Wenn Sie einer Verfügbarkeitsgruppe eine oder mehrere primäre Datenbanken für den Protokollversand hinzufügen, können Sie möglicherweise eine oder mehrere der entsprechenden sekundären Datenbanken für den Protokollversand zu Always On-Verfügbarkeitsgruppen migrieren. Das Migrieren einer sekundären Datenbank für den Protokollversand erfordert, dass sie den gleichen Datenbanknamen wie die primäre Datenbank verwendet und dass sie sich auf einer Serverinstanz befindet, die ein sekundäres Replikat für die Verfügbarkeitsgruppe hostet. Weiterhin muss die Verfügbarkeitsgruppe so konfiguriert sein, dass das primäre Replikat für Sicherungen bevorzugt wird und ein Kandidat zum Ausführen von Sicherungen ist (das heißt, eine Sicherungspriorität, die >0 hat). Nachdem der Sicherungsauftrag auf der primären Datenbank ausgeführt wurde, müssen Sie den Sicherungsauftrag deaktivieren, und sobald der Wiederherstellungsauftrag auf einer angegebenen sekundären Datenbank ausgeführt wurde, müssen Sie den Wiederherstellungsauftrag deaktivieren.  
  
        > [!NOTE]  
        >  Nachdem Sie alle sekundären Datenbanken für die Verfügbarkeitsgruppe erstellt haben, sofern Sie Sicherungen auf sekundären Replikaten ausführen möchten, müssen Sie die Voreinstellung zur automatisierten Sicherung der Verfügbarkeitsgruppe neu konfigurieren.  
  
         **Weitere Informationen:**  
  
         [Voraussetzungen für das Migrieren vom Protokollversand zu Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
         [Konfigurieren der Sicherung auf Verfügbarkeitsreplikaten &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
2.  Verknüpfen Sie jede neu vorbereitete sekundäre Datenbank sofort mit der Verfügbarkeitsgruppe.  
  
     **Weitere Informationen:**  
  
     [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="LaunchWiz"></a> Verwandte Aufgaben  
  
-   [Verwenden des Dialogfelds Neue Verfügbarkeitsgruppe &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Replikaten zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
