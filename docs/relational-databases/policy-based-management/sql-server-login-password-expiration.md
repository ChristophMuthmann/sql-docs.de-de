---
title: Ablauf des SQL Server-Anmeldekennworts | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9725e3e0e00e22515b5a347a4a5267c78d6f2ec8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-login-password-expiration"></a>Ablauf des SQL Server-Anmeldekennworts
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Diese Regel überprüft, ob der Ablauf des Kennworts für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung aktiviert ist. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung aktiviert ist und die Betriebssystemversion älter ist als [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], könnte ein Angreifer ein bekanntes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldekennwort wiederholt nutzen.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Es wird empfohlen, das Betriebssystem auf [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]zu aktualisieren.  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung in Ihrer Umgebung nicht erforderlich ist, verwenden Sie die Windows-Authentifizierung. Weitere Informationen finden Sie unter [Auswählen eines Authentifizierungsmodus](../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Aktivieren Sie den Ablauf des Kennworts für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen. Verwenden Sie [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) , um die Kennwortrichtlinie für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung zu konfigurieren.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Kennwortrichtlinie](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
