---
title: "Dienstkonten (Assistent zum Konfigurieren der Sicherheit für die Datenbankspiegelung) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.configdbmsecurwiz.serviceaccounts.f1
ms.assetid: d58d8f93-7888-4d66-af4d-969ef6a2dbee
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 65f16e29d01348e8158c99b53a87ab9d27e31b62
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="service-accounts-configure-database-mirroring-security-wizard"></a>Dienstkonten (Assistent zum Konfigurieren der Sicherheit für die Datenbankspiegelung)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Geben Sie bei Verwendung der Windows-Authentifizierung die Dienstkonten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an, wenn die Serverinstanzen verschiedene Konten verwenden. Diese Dienstkonten müssen alle Domänenkonten (in derselben oder vertrauenswürdigen Domäne) sein.  
  
 Wenn alle Serverinstanzen das gleiche Domänenkonto oder die zertifikatbasierte Authentifizierung verwenden, lassen Sie die Felder leer. Klicken Sie einfach auf **Fertig stellen**, und der Assistent konfiguriert automatisch die Konten auf Basis des Kontos des aktuellen Assistenten.  
  
> [!IMPORTANT]  
>  Wenn die Endpunkte für die Datenbankspiegelung der Serverinstanzen für die Verwendung von Zertifikaten konfiguriert sind, müssen Sie die Felder für die Dienstkonten leer lassen.  
  
 **So konfigurieren Sie die Datenbankspiegelung mithilfe von SQL Server Management Studio**  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Starten des Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Tastatur  
 **Prinzipal**  
 Geben Sie das Dienstkonto der Prinzipalserverinstanz an. Geben Sie den Domänennamen in Großbuchstaben ein:  
  
 *DOMÄNENNAME*\\*Benutzername*  
  
 **Spiegel**  
 Geben Sie das Dienstkonto der Spiegelserverinstanz an. Geben Sie den Domänennamen in Großbuchstaben ein:  
  
 *DOMÄNENNAME*\\*Benutzername*  
  
 **Zeuge**  
 Geben Sie das Dienstkonto der Zeugenserverinstanz an. Geben Sie den Domänennamen in Großbuchstaben ein:  
  
 *DOMÄNENNAME*\\*Benutzername*  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankeigenschaften &#40;Seite „Wird gespiegelt“&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Einrichten von Anmeldekonten für die Datenbankspiegelung oder Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
  
