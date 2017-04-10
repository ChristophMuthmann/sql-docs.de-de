---
title: "Protokolldateien f&#252;r Standardablaufverfolgung deaktiviert | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Best Practices [Datenbankmodul]"
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Protokolldateien f&#252;r Standardablaufverfolgung deaktiviert
  Diese Regel überprüft den Wert der Option Standardablaufverfolgung aktiviert der gespeicherten Prozedur sp_configure, um festzustellen, ob die Standardablaufverfolgung auf ON (1) oder OFF (0) festgelegt ist. Wenn diese Option aktiviert ist, stellt die Standardablaufverfolgung Informationen über Konfigurations- und DDL-Änderungen an [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] bereit. In manchen Fällen sind diese Informationen für Kunden sowie den Kundendienst- und Support von [!INCLUDE[msCoName](../../includes/msconame-md.md)] bei der Behebung von Fehlern bei [!INCLUDE[ssDE](../../includes/ssde-md.md)]hilfreich.  
  
## Empfehlungen zu Best Practices  
 Aktivieren Sie die Ablaufverfolgung mit der gespeicherten Prozedur sp_configure, indem Sie den Wert von "Standardablaufverfolgung aktiviert" auf 1 festlegen.  
  
## Weitere Informationen  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## Siehe auch  
 [Überwachen und Erzwingen von Best Practices mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  