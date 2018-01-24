---
title: Konfigurieren von Datenbankmodulinstanzen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
caps.latest.revision: "6"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f245606ea20d419098b919019e7854546fdc7208
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="configure-database-engine-instances-sql-server"></a>Konfigurieren von Datenbankmodulinstanzen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Jede Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] muss so konfiguriert werden, dass sie die für die Datenbanken, die von der Instanz gehostet werden, definierten Anforderungen in Bezug auf Leistung und Verfügbarkeit erfüllt. [!INCLUDE[ssDE](../../includes/ssde-md.md)] enthält Konfigurationsoptionen, die Verhaltensweisen wie Ressourcenauslastung und Verfügbarkeit von Funktionen, z. B. Überwachung oder Triggerrekursion, steuern.  
  
## <a name="instance-configuration"></a>Instanzkonfiguration  
 Wenn eine Datenbank in der Produktionsumgebung bereitgestellt wird, gibt es oft eine Vereinbarung zum Servicelevel (SLA), in der Bereiche wie die erforderlichen Leistungsstufen der Datenbank und die erforderliche Verfügbarkeitsstufe der Datenbank festgelegt sind. Die Konfigurationsanforderungen für die Instanz orientieren sich in der Regel an den SLA-Bedingungen.  
  
 Eine Instanz wird normalerweise sofort nach ihrer Installation konfiguriert. Die Erstkonfiguration wird normalerweise von den SLA-Anforderungen der Typen von Datenbanken bestimmt, die auf der Instanz bereitgestellt werden sollen. Nach der Bereitstellung der Datenbanken überwachen die Datenbankadministratoren die Leistung der Instanz und passen die Konfigurationseinstellungen ggf. an, wenn die Leistungsmetrik anzeigt, dass SAL-Anforderungen nicht von der Instanz erfüllt werden.  
  
## <a name="configuration-tasks"></a>Konfigurationstasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt die verschiedenen Optionen zur Instanzkonfiguration und das Anzeigen oder Ändern dieser Optionen.|[Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
|Beschreibt, wie Sie die Standardspeicherorte von neuen Daten- und Protokolldateien in der Instanz anzeigen und konfigurieren.|[Anzeigen oder Ändern der Standardspeicherorte für Daten- und Protokolldateien &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|Beschreibt, wie Sie SQL Server für die Verwendung von Soft-NUMA konfigurieren.|[Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)|  
|Beschreibt, wie ein TCP/IP-Port einer Affinität von TCP/IP-Ports zu NUMA-Knoten (Non-Uniform Memory Access) zugeordnet wird.|[Zuordnen von TCP/IP-Ports zu NUMA-Knoten &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Beschreibt, wie Sie die Windows-Richtlinie Lock Pages In Memory aktivieren. Mit dieser Richtlinie werden die Konten bestimmt, die einen Prozess zum Speichern von Daten im physischen Speicher verwenden können, um das systemgesteuerte Auslagern der Daten in den virtuellen Arbeitsspeicher zu vermeiden.|[Aktivieren der Option Sperren von Seiten im Speicher &#40;Windows&#41;](../../database-engine/configure-windows/enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankmodulinstanzen &#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
