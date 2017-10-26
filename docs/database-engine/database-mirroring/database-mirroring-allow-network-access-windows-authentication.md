---
title: "Datenbankspiegelung – Netzwerkzugriff zulassen – Windows-Authentifizierung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c7b4dae208e71cb7773fa1ca21227193e3c448e9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="database-mirroring---allow-network-access---windows-authentication"></a>Datenbankspiegelung – Netzwerkzugriff zulassen – Windows-Authentifizierung
  Die Verwendung der Windows-Authentifizierung für die Verbindung der Datenbank, wodurch Endpunkte auf zwei Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespiegelt werden, erfordert unter den folgenden Bedingungen eine manuelle Konfiguration der Anmeldekonten:  
  
-   Wenn die Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als Dienste unter unterschiedlichen Domänenkonten ausgeführt werden (in der gleichen oder einer vertrauenswürdigen Domäne), müssen die Anmeldeinformationen jedes Kontos in **master** auf jeder der Remoteserverinstanzen erstellt werden. Dieser Anmeldung müssen CONNECT-Berechtigungen für den Endpunkt gewährt werden.  
  
-   Wenn die Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als Netzwerkdienstkonto ausgeführt werden, muss die Anmeldung zu jedem Hostcomputer-Konto (*DomainName***\\***ComputerName$*) in **master** auf jeder Remoteserverinstanz erstellt werden. Dieser Anmeldung müssen CONNECT-Berechtigungen für den Endpunkt gewährt werden. Das liegt daran, dass eine Serverinstanz, die unter dem Netzwerkdienstkonto ausgeführt wird, mit dem Domänenkonto des Hostcomputers authentifiziert wird.  
  
> [!NOTE]  
>  Stellen Sie sicher, dass für jede dieser Serverinstanzen ein Endpunkt vorliegt. Weitere Informationen finden Sie unter [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
### <a name="to-configure-logins-for-windows-authentication"></a>So konfigurieren Sie Anmeldenamen für die Windows-Authentifizierung  
  
1.  Erstellen Sie auf den anderen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine Anmeldung für das Benutzerkonto jeder Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie eine [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) -Anweisung mit der FROM WINDOWS-Klausel.  
  
     Weitere Informationen finden Sie unter [Erstellen eines Anmeldenamens](../../relational-databases/security/authentication-access/create-a-login.md).  
  
2.  Erteilen Sie für die Anmeldung die Berechtigung für eine Verbindung zum Endpunkt unter Verwendung der [GRANT](../../t-sql/statements/grant-transact-sql.md) -Anweisung, damit der angemeldete Benutzer auf den Endpunkt zugreifen kann. Wenn es sich beim Benutzer um den Administrator handelt, ist keine Berechtigung für eine Verbindung zum Endpunkt erforderlich.  
  
     Weitere Informationen finden Sie unter [Grant a Permission to a Principal](../../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Beispiel wird ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename für ein Benutzerkonto namens `Otheruser` erstellt, das der Domäne `Adomain`angehört. Anschließend erteilt das Beispiel diesem Benutzer die Berechtigungen zum Verbindungsaufbau mit einem bereits vorhandenen Datenbank-Spiegelungsendpunkt mit dem Namen `Mirroring_Endpoint`.  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Transportsicherheit für Datenbankspiegelung und Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  

