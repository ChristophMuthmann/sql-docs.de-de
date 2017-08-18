---
title: Konfigurieren von Datenbankmodulinstanzen (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 334a4e5426f501db9987ef0106a3e4f04952a544
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-database-engine-instances-sql-server"></a>Konfigurieren von Datenbankmodulinstanzen (SQL Server)
  Jede Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] muss so konfiguriert werden, dass sie die für die Datenbanken, die von der Instanz gehostet werden, definierten Anforderungen in Bezug auf Leistung und Verfügbarkeit erfüllen. [!INCLUDE[ssDE](../../includes/ssde-md.md)] enthält Konfigurationsoptionen, die Verhaltensweisen wie Ressourcenauslastung und Verfügbarkeit von Funktionen, z. B. Überwachung oder Triggerrekursion, steuern.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Datenbankmodulinstanzen &#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
