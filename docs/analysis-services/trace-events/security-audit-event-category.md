---
title: Sicherheitsüberwachung-Ereigniskategorie | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [Analysis Services], security audit
- security events [Analysis Services]
ms.assetid: 9686a495-68d7-4137-8e30-2655aa519f6c
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e4973e777105531b63fb5aacdae298e57f6f9e40
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="security-audit-event-category"></a>Sicherheitsüberwachung-Ereigniskategorie
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Die Security Audit-Ereigniskategorie enthält die in der folgenden Tabelle beschriebenen Ereignisklassen.  
  
|Ereignisklasse|Ereignis-ID|Description|  
|-----------------|--------------|-----------------|  
|Audit Login|1|Zeichnet alle neuen Verbindungsereignisse seit dem Start der Ablaufverfolgung auf (z. B. wenn ein Client eine Verbindung mit einem Server anfordert, auf dem eine Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]ausgeführt wird).|  
|Audit Logout|2|Zeichnet alle neuen Ereignisse zum Trennen einer Verbindung auf, die seit dem Start der Ablaufverfolgung eingetreten sind, z. B. wenn ein Client einen Befehl zum Trennen der Verbindung ausgibt.|  
|Audit Server Starts and Stops|4|Zeichnet das Starten, Beenden und Anhalten für Dienste auf.|  
|Audit Object Permission Event|18|Zeichnet alle Änderungen von Objektberechtigungen auf.|  
|Audit Admin Operations-Ereignis|19|Zeichnet Servervorgänge für die Sicherung, Wiederherstellung, Synchronisierung, für das Anfügen und Trennen sowie für das Laden und Speichern von Images auf.|  
  
 Informationen zu den Spalten, die den einzelnen Security Audit-Ereignisklassen zugeordnet sind, finden Sie unter [Security Audit Data Columns](../../analysis-services/trace-events/security-audit-data-columns.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
