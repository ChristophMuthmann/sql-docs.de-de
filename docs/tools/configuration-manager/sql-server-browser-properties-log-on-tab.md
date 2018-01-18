---
title: "Eigenschaften für die SQL Server-Browser (Registerkarte Anmelden) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c77871ec-c2f4-4e4a-9a10-5aeb4ae70507
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 688b87426feba4128e1c2d8708d0de94a102d94f
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="sql-server-browser-properties-log-on-tab"></a>Eigenschaften von SQL Server-Browser (Registerkarte Anmelden)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browserprogramm wird als Dienst auf dem Server ausgeführt. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser achtet auf eingehende Anforderungen für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcen und stellt Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen zur Verfügung, die auf dem Computer installiert sind.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Browser lauscht an einem UDP-Port; nicht authentifizierte Anforderungen werden mithilfe von SSRP ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol) akzeptiert.  
  
 Das Ändern eines Kennworts für ein Konto wird sofort wirksam. Es ist kein Neustart des Dienstes erforderlich.  
  
## <a name="options"></a>enthalten  
 **Lokales System**  
 Führen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst im Sicherheitskontext des lokalen Systemkontos aus. Verwenden Sie nach Möglichkeit ein Konto mit geringen Berechtigungen.  
  
 **Dieses Konto**  
 Geben Sie ein lokales oder ein Domänenbenutzerkonto an, das die Windows-Authentifizierung verwendet. Das Verwenden eines Domänenbenutzerkontos mit minimalen Berechtigungen für Dienste wird empfohlen. Informationen zum Auswählen eines Kontos finden Sie unter "Einrichten von Windows-Dienstkonten" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
 **Durchsuchen**  
 Suchen Sie nach einem Benutzer oder einem integriertem Sicherheitsprinzipal.  
  
> [!IMPORTANT]  
>  Verwenden Sie ein Konto mit geringen Berechtigungen. Informationen zu den Berechtigungen, die für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst erforderlich sind, finden Sie im Abschnitt „Sicherheit“ von [SQL Server-Browserdienst](../../tools/configuration-manager/sql-server-browser-service.md).  
  
 **Kennwort**  
 Geben Sie das Kennwort des Sicherheitsprinzipals ein.  
  
 **Kennwort bestätigen**  
 Bestätigen Sie das Kennwort des Sicherheitsprinzipals.  
  
 **Dienststatus**  
 Zeigt an, ob dieser Dienst ausgeführt wird, angehalten oder deaktiviert ist. "**…**" gibt einen ausstehenden Statuswechsel an.  
  
 **Start**  
 Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst.  
  
 **Beenden**  
 Beenden Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst.  
  
 **Anhalten**  
 Halten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst an.  
  
 **Fortsetzen**  
 Setzen Sie die Ausführung eines angehaltenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdiensts fort.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Browserdienst](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
