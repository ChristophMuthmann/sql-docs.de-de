---
title: Spalten für Data Quality-Abgleich (MDS-Add-In für Excel) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: microsoft-excel-add-in
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d784a6225cc7d0ff223dd3fd3e9fb4b58ecb02cd
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Spalten für Data Quality-Abgleich (MDS-Add-In für Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]können Sie nach dem Abgleichen von Daten im Menüband in der Gruppe **Data Quality** auf **Details anzeigen** klicken, um Spalten mit übereinstimmenden Details anzuzeigen.  
  
 In der folgenden Tabelle sind die Spalten aufgeführt, die beim Abgleichen von Daten angezeigt werden.  
  
|Name|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|Ein eindeutiger Bezeichner, der zum Gruppieren ähnlicher Datensätze verwendet wird. Alle Zeilen, die einander ähnlich sind, haben die gleiche **CLUSTER_ID**. Wenn für eine Zeile keine **CLUSTER_ID** angezeigt wird, wurden keine ähnlichen Datensätze gefunden.|  
|**RECORD_ID**|Ein eindeutiger Bezeichner, der zum Identifizieren verwendet wird. Dies ist ein Wert, der zum Identifizieren eines Datensatzes verwendet wird und dem im MDS-Repository gespeicherten Codewert ähnelt. Er wird jeweils automatisch generiert, wenn ein Abgleich durchgeführt wird.|  
|**PIVOT_MARK**|Ein beliebiger Datensatz, mit dem andere Datensätze verglichen werden. Er verfügt nicht über einen Ergebniswert.|  
|**SCORE**|Gibt an, welchen Grad an Ähnlichkeit die Datensätze in der Gruppe mit dem Pivotdatensatz aufweisen. Dieses Ergebnis wird mithilfe von DQS bestimmt. Wenn kein Ergebnis angezeigt wird, ist der Datensatz der Pivotdatensatz für andere Datensätze, oder es wurden keine Übereinstimmungen gefunden.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Data Quality-Abgleich im MDS-Add-In für Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Abgleichen ähnlicher Daten (MDS-Add-In für Excel)](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [Datenabgleich](../../data-quality-services/data-matching.md)  
  
  
