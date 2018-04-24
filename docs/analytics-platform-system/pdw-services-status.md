---
title: PDW-Status - Dienste Analytics Platform System | Microsoft Docs
description: Parallel Data Warehouse (PDW)-Dienststatus für Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e2252bb821f9522515f1625b0fc118323cb50d1f
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Parallel Data Warehouse-Dienststatus für Analytics Platform System
Die Parallel Data Warehouse **Dienststatus** Seite im Microsoft Analytics Platform System Konfigurations-Manager zeigt den aktuellen Status aller SQL Server PDW-Dienste, und bietet die Möglichkeit, die PDW-Dienste beenden und starten. Dies ist die einzige unterstützte Methode für die PDW-Dienste starten und beenden. Beachten Sie, dass die einzelnen Komponenten oder Dienste unabhängig voneinander gestartet werden können.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>So starten oder beenden die Appliance-Dienste  
  
1.  Um die Anwendung Dienste zu starten, klicken Sie auf **starten Appliance**.  
  
2.  Um die Anwendung Dienste zu beenden, klicken Sie auf **beenden Appliance**.  
  
Es ist nicht erforderlich, klicken Sie auf **übernehmen** beim Starten und beenden die Anwendung Dienste mit **starten Appliance** und **beenden Appliance**.  
  
![DWConfig-Anwendung PDW-Dienste](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Beenden die PDW-Region beendet wird, wird damit auch die PDW-Agent (Sqldwagent) auf den Knoten des HDInsight-Region. Der HDInsight-Region beträgt noch funktionsfähig, jedoch Systemüberwachung nicht zur Verfügung stehen. (Der PDW-Agent erfordert den Steuerelementknoten PDW Systemüberwachung gemeldet.)  
  
## <a name="see-also"></a>Siehe auch  
[Schalten Sie ein- oder ausschalten die APS-Appliance &#40;Analyseplattformsystem&#41;](power-the-aps-appliance-on-or-off.md)  
  
