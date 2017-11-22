---
title: "Verschlüsselte Datenbanken bei Always On-Verfügbarkeitsgruppen (SQL Server) | Microsoft-Dokumentation"
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
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
caps.latest.revision: "10"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d728a5e275b2c037392dd2a8134f1180e6e0fed9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="encrypted-databases-with-always-on-availability-groups-sql-server"></a>Verschlüsselte Datenbanken bei Always On-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Dieses Thema enthält Informationen zur Verwendung aktuell verschlüsselter oder vor kurzem entschlüsselter Datenbanken mit [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 **In diesem Thema:**  
  
-   [Einschränkungen](#Restrictions)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="Restrictions"></a> Einschränkungen  
  
-   Wenn eine Datenbank verschlüsselt ist oder sogar einen Datenbankverschlüsselungs-Schlüssel (DEK) enthält, können Sie die Datenbank nicht mithilfe von [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] oder [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] einer Verfügbarkeitsgruppe hinzufügen. Selbst wenn eine verschlüsselte Datenbank entschlüsselt wurde, enthalten ihre Protokollsicherungen möglicherweise verschlüsselte Daten. In diesem Fall ist es unter Umständen nicht möglich, die anfängliche Datensynchronisierung vollständig auf der Datenbank durchzuführen. Grund hierfür ist die Tatsache, dass für den Wiederherstellungsprotokollvorgang eventuell das Zertifikat erforderlich ist, das von den Datenbank-Verschlüsselungsschlüsseln (DEKs) verwendet wurde, und dieses Zertifikat möglicherweise nicht verfügbar ist.  
  
     So machen Sie eine entschlüsselte Datenbank verfügbar für das Hinzufügen zu einer Verfügbarkeitsgruppe mithilfe des Assistenten:  
  
    1.  Erstellen Sie eine Protokollsicherung von der primären Datenbank.  
  
    2.  Erstellen Sie eine vollständige Datenbanksicherung der primären Datenbank.  
  
    3.  Stellen Sie die Datenbanksicherung auf der Serverinstanz wieder her, die das sekundäre Replikat hostet.  
  
    4.  Erstellen Sie eine neue Protokollsicherung aus der primären Datenbank.  
  
    5.  Stellen Sie diese Protokollsicherung in der sekundären Datenbank wieder her.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Verwenden des Assistenten für Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Verwenden des Assistenten zum Hinzufügen von Datenbanken zu Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
