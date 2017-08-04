---
title: "Data Quality-Abgleich Spalten (MDS-Add-in für Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 9
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4ce8ddcdbf8c29663640025ad40b4e01e44d99c1
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>Spalten für Data Quality-Abgleich (MDS-Add-In für Excel)
  In der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]nach dem Abgleichen von Daten in der **Datenqualität** Gruppe klicken Sie auf dem Menüband können auf **Details anzeigen** auf Spalten mit übereinstimmenden Details anzuzeigen.  
  
 In der folgenden Tabelle sind die Spalten aufgeführt, die beim Abgleichen von Daten angezeigt werden.  
  
|Name|Description|  
|----------|-----------------|  
|**CLUSTER_ID**|Ein eindeutiger Bezeichner, der zum Gruppieren ähnlicher Datensätze verwendet wird. Alle Zeilen, die einander ähnlich sind, haben die gleiche **CLUSTER_ID**. Wenn für eine Zeile keine **CLUSTER_ID** angezeigt wird, wurden keine ähnlichen Datensätze gefunden.|  
|**RECORD_ID**|Ein eindeutiger Bezeichner, der zum Identifizieren verwendet wird. Dies ist ein Wert, der zum Identifizieren eines Datensatzes verwendet wird und dem im MDS-Repository gespeicherten Codewert ähnelt. Er wird jeweils automatisch generiert, wenn ein Abgleich durchgeführt wird.|  
|**PIVOT_MARK**|Ein beliebiger Datensatz, mit dem andere Datensätze verglichen werden. Er verfügt nicht über einen Ergebniswert.|  
|**SCORE**|Gibt an, welchen Grad an Ähnlichkeit die Datensätze in der Gruppe mit dem Pivotdatensatz aufweisen. Dieses Ergebnis wird mithilfe von DQS bestimmt. Wenn kein Ergebnis angezeigt wird, ist der Datensatz der Pivotdatensatz für andere Datensätze, oder es wurden keine Übereinstimmungen gefunden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Data Quality-Abgleich im MDS-Add-in für Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Übereinstimmen Sie, ähnliche Daten &#40; MDS-Add-in für Excel &#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)   
 [Datenabgleich](../../data-quality-services/data-matching.md)  
  
  
