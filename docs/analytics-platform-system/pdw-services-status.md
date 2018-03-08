---
title: PDW-Dienststatus (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fc9bee2-c372-4c4a-956c-fb54215d8918
caps.latest.revision: "14"
ms.openlocfilehash: 7a6b1a1f9a6ef922833930abf00ca10482648141
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-services-status"></a>PDW-Dienststatus
Die Parallel Data Warehouse **Dienststatus** Seite im Microsoft Analytics Platform System Konfigurations-Manager zeigt den aktuellen Status aller SQL Server PDW-Dienste, und bietet die Möglichkeit, die PDW-Dienste beenden und starten. Dies ist die einzige unterstützte Methode für die PDW-Dienste starten und beenden. Beachten Sie, dass die einzelnen Komponenten oder Dienste unabhängig voneinander gestartet werden können.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>So starten oder beenden die Appliance-Dienste  
  
1.  Um die Anwendung Dienste zu starten, klicken Sie auf **starten Appliance**.  
  
2.  Um die Anwendung Dienste zu beenden, klicken Sie auf **beenden Appliance**.  
  
Es ist nicht erforderlich, klicken Sie auf **übernehmen** beim Starten und beenden die Anwendung Dienste mit **starten Appliance** und **beenden Appliance**.  
  
![DWConfig-Anwendung PDW-Dienste](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Beenden die PDW-Region beendet wird, wird damit auch die PDW-Agent (Sqldwagent) auf den Knoten des HDInsight-Region. Der HDInsight-Region beträgt noch funktionsfähig, jedoch Systemüberwachung nicht zur Verfügung stehen. (Der PDW-Agent erfordert den Steuerelementknoten PDW Systemüberwachung gemeldet.)  
  
## <a name="see-also"></a>Siehe auch  
[Schalten Sie die Appliance APS ein- oder ausschalten &#40; Analyseplattformsystem &#41;](power-the-aps-appliance-on-or-off.md)  
  
