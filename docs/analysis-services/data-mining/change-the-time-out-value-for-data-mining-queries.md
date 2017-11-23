---
title: "Ändern des Timeoutwerts für Datamining-Abfragen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: time-out
ms.assetid: f1add4bc-e882-440a-a98b-333cfa274c3e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ed9b0accbd229361d8ff2e559d4a7f367c6072d9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="change-the-time-out-value-for-data-mining-queries"></a>Ändern des Timeoutwerts für Data Mining-Abfragen
  Wenn Sie ein Prognosegütediagramm erstellen oder eine Vorhersageabfrage ausführen, kann es viel Zeit in Anspruch nehmen, alle für die Vorhersage erforderlichen Daten zu generieren. Um ein Timeout der Abfrage zu verhindern, können Sie den Wert ändern, der festlegt, wie lange der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server auf den Abschluss einer Abfrage wartet.  
  
 Der Standardwert ist 15. Wenn Ihre Modelle komplex sind oder die Datenquelle umfangreich ist, reicht dies unter Umständen nicht aus. Bei Bedarf können Sie den Wert heraufsetzen, um genügend Zeit für die Verarbeitung bereitzustellen. Beispiel: wenn Sie **Abfragetimeout** auf 600 setzen, kann die Abfrage bis zu 10 Minuten lang ausgeführt werden.  
  
 Weitere Informationen zu Vorhersageabfragen finden Sie unter [Data Mining-Abfragetasks und Anweisungen](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
### <a name="configure-the-time-out-value-for-data-mining-queries"></a>Konfigurieren des Timeoutwerts für Data Mining-Abfragen  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Menü **Extras** auf **Optionen**.  
  
2.  Erweitern Sie im Bereich **Optionen** **Business Intelligence-Designer**.  
  
3.  Klicken Sie auf das Textfeld **Abfragetimeout** , und geben Sie einen Wert für die Anzahl der Sekunden ein.  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Abfragetasks und Anweisungen](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)   
 [Data Mining-Abfrage](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
