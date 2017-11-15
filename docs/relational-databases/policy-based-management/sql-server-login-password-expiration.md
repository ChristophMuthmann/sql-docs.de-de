---
title: Ablauf des SQL Server-Anmeldekennworts | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
ms.openlocfilehash: 5700b0391c00f9743f7885b16be0d8bf7c33055d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-login-password-expiration"></a>Ablauf des SQL Server-Anmeldekennworts
  Diese Regel überprüft, ob der Ablauf des Kennworts für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung aktiviert ist. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung aktiviert ist und die Betriebssystemversion älter ist als [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], könnte ein Angreifer ein bekanntes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldekennwort wiederholt nutzen.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 Es wird empfohlen, das Betriebssystem auf [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]zu aktualisieren.  
  
 Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung in Ihrer Umgebung nicht erforderlich ist, verwenden Sie die Windows-Authentifizierung. Weitere Informationen finden Sie unter [Auswählen eines Authentifizierungsmodus](../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Aktivieren Sie den Ablauf des Kennworts für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen. Verwenden Sie [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) , um die Kennwortrichtlinie für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung zu konfigurieren.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Kennwortrichtlinie](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
