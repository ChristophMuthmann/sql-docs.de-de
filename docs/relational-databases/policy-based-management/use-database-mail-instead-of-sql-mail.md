---
title: Verwenden von Datenbank-E-Mail anstelle von SQL Mail | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: db3b564cf3e89460ee24ad0a1ed0828c1eb37a99
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="use-database-mail-instead-of-sql-mail"></a>Verwenden von Datenbank-E-Mail anstelle von SQL Mail
  Diese Regel überprüft die sys.configurations-Katalogsicht, um zu bestimmen, ob die serverweite Konfigurationoption von SQL Mail XPs auf ON festgelegt ist.  
  
## <a name="best-practices-recommendations"></a>Empfehlungen zu Best Practices  
 SQL Mail wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie zum Versenden von E-Mail-Nachrichten Datenbank-E-Mail.  
  
 SQL Mail wird prozessintern zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt. Wenn SQL Mail beendet wird, wird der Server ebenfalls beendet. Datenbank-E-Mail wird in einem separaten Prozess außerhalb von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt. Sie ist skalierbar und benötigt keine Extended MAPI-Clientkomponenten auf dem Produktionsserver.  
  
## <a name="for-more-information"></a>Weitere Informationen  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
