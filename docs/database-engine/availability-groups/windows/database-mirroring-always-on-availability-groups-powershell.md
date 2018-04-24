---
title: Datenbankspiegelung – Always On-Verfügbarkeitsgruppe – PowerShell | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
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
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], endpoint
ms.assetid: 6197bbe7-67d4-446d-ba5f-cabfa5df77f1
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f8a7edeef42eff4e67827f8665dda68244ebbe0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-mirroring---always-on-availability-groups--powershell"></a>Datenbankspiegelung – Always On-Verfügbarkeitsgruppe – PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie ein Datenbankspiegelungs-Endpunkt zur Verwendung durch [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit PowerShell erstellt wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  [Sicherheit](#Security)  
  
-   **So erstellen Sie einen Datenbankspiegelungs-Endpunkt mit:**  [PowerShell](#PowerShellProcedure)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
> [!IMPORTANT]  
>  Der RC4-Algorithmus ist veraltet. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] Stattdessen wird die Verwendung von AES empfohlen.  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CREATE ENDPOINT-Berechtigung oder die Mitgliedschaft in der festen Serverrolle "sysadmin". Weitere Informationen finden Sie unter [GRANT (Endpunktberechtigungen) &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-endpoint-permissions-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So erstellen Sie einen Datenbankspiegelungs-Endpunkt**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, für die Sie den Datenbankspiegelungs-Endpunkt erstellen möchten.  
  
2.  Verwenden Sie das Cmdlet **New-SqlHadrEndpoint** , um den Endpunkt zu erstellen und verwenden Sie dann **Set-SqlHadrEndpoint** , um den Endpunkt zu starten.  
  
###  <a name="PShellExample"></a> Beispiel (PowerShell)  
 Mit den folgenden PowerShell-Befehlen wird ein Datenbankspiegelungs-Endpunkt auf einer Instanz von SQL Server erstellt (*Computer*\\*Instanz*). Der Endpunkt verwendet Port 5022.  
  
> [!IMPORTANT]  
>  Dieses Beispiel funktioniert nur auf einer Serverinstanz, die derzeit keinen Datenbankspiegelungs-Endpunkt hat.  
  
```  
# Create the endpoint.  
$endpoint = New-SqlHadrEndpoint MyMirroringEndpoint -Port 5022 -Path SQLSERVER:\SQL\Machine\Instance  
  
# Start the endpoint  
Set-SqlHadrEndpoint -InputObject $endpoint -State "Started"  
  
```  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie einen Datenbankspiegelungs-Endpunkt**  
  
-   [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Verwenden von Zertifikaten für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Ermöglichen des Verwendens von Zertifikaten für ausgehende Verbindungen für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Ermöglichen des Verwendens von Zertifikaten für eingehende Verbindungen für einen Datenbankspiegelungs-Endpunkt &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Angeben einer Servernetzwerkadresse &#40;Datenbankspiegelung&#41;](../../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Angeben der Endpunkt-URL beim Hinzufügen oder Ändern eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **So zeigen Sie Informationen zum Datenbankspiegelungs-Endpunkt an**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)   
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
