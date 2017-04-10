---
title: "SMO and DMO XPs (Serverkonfigurationsoption) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 15
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 15
---
# SMO and DMO XPs (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option SMO and DMO XPs, um erweiterte gespeicherte Prozeduren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object (SMO) auf diesem Server zu aktivieren.  
  
 Beachten Sie, dass DMO beginnend mit [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt wurde.  
  
 Eine Beschreibung der möglichen Werte finden Sie in der folgenden Tabelle:  
  
|Wert|Bedeutung|  
|-----------|-------------|  
|0|SMO-XPs sind nicht verfügbar.|  
|1|SMO-XPS sind verfügbar. Dies ist die Standardeinstellung.|  
  
 Diese Einstellung wird sofort wirksam.  
  
## Beispiele  
 Im folgenden Beispiel werden die erweiterten gespeicherten Prozeduren von SMO aktiviert.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## Siehe auch  
 [Programmierungshandbuch für SQL Server Management Objects &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  