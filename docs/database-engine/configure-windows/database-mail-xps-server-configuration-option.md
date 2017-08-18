---
title: Database Mail XPs (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 989df51eeeb19f45e1c515637cce16783e5227a1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="database-mail-xps-server-configuration-option"></a>Database Mail XPs (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option **DatabaseMail XPs** , um Datenbank-E-Mail auf diesem Server zu aktivieren. Die folgenden Werte sind möglich:  
  
-   **0** gibt an, dass Datenbank-E-Mail nicht verfügbar ist (Standard).  
  
-   **1** gibt an, dass Datenbank-E-Mail verfügbar ist.  
  
 Die Einstellung tritt ohne Beenden und Neustarten des Servers sofort in Kraft.  
  
 Nachdem Sie Datenbank-E-Mail aktiviert haben, müssen Sie zum Verwenden von Datenbank-E-Mail eine Hostdatenbank für Datenbank-E-Mail konfigurieren.  
  
 Durch das Konfigurieren von Datenbank-E-Mail mithilfe des Assistenten zum Konfigurieren von Datenbank-E-Mail **** werden die erweiterten gespeicherten Prozeduren von Datenbank-E-Mail in der **msdb** -Datenbank aktiviert. Wenn Sie den **Assistenten zum Konfigurieren von Datenbank-E-Mail**verwenden, müssen Sie das unten angeführte **sp_configure** -Beispiel nicht verwenden.  
  
 Das festlegen der Option **Database Mail XPs** auf 0 verhindert das Starten von Datenbank-E-Mail. Wird Datenbank-E-Mail mit dem Wert 0 ausgeführt, wird die Ausführung und das Senden von E-Mails bis zur in der Option **DatabaseMailExeMinimumLifeTime** konfigurierten Leerlaufzeit fortgesetzt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die erweiterten gespeicherten Prozeduren von Datenbank-E-Mail aktiviert.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)  
  
  

