---
title: Data Quality-Abgleich im MDS-Add-In für Excel | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
ms.assetid: be78d051-0d56-46d3-bb89-327e218dadd6
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 956ec1ca6d60f867c68fb9f049ddc6201276a0b9
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="data-quality-matching-in-the-mds-add-in-for-excel"></a>Data Quality-Abgleich im MDS-Add-In für Excel

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Es ist möglich, dass Sie dem MDS-Repository im Laufe der Zeit weitere Daten hinzufügen möchten. Vor dem Hinzufügen von Daten kann es hilfreich sein, die neuen Daten mit den bereits in MDS verwalteten Daten zu vergleichen, um sicherzustellen, dass Sie keine doppelten oder ungenauen Daten hinzufügen.  
  
 Unter MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] wird die Data Quality Services-Funktion (DQS) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um ähnliche Daten zu ermitteln. Wenn Sie im Add-In die Abgleichfunktion verwenden, werden ähnliche Datensätze gruppiert, und es wird ein Wert angezeigt, der die Genauigkeit des Ergebnisses angibt. Weitere Informationen zur Abgleichfunktion von DQS finden Sie unter [Data Matching](../../data-quality-services/data-matching.md).  
  
## <a name="workflow-for-data-quality-matching"></a>Workflow für Data Quality-Abgleich  
 Verwenden Sie beim Nutzen von DQS in Verbindung mit MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]den folgenden Workflow:  
  
1.  Rufen Sie eine Liste mit von MDS verwalteten Daten ab, und kombinieren Sie diese mit einer Liste, die nicht unter MDS verwaltet wird. Weitere Informationen finden Sie unter [Kombinieren von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md).  
  
2.  Vergleichen Sie die Daten mithilfe der DQS-Erkenntnisse in der kombinierten Liste. Weitere Informationen finden Sie unter [Abgleichen ähnlicher Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
3.  Zeigen Sie die Detailspalten an, um weitere Details zu den mit DQS ermittelten Ähnlichkeiten anzuzeigen.  
  
4.  Gehen Sie die Ergebnisse durch, und bestimmen Sie, welche Daten dem MDS-Repository hinzugefügt werden sollen und welche Daten doppelt vorhanden sind.  
  
5.  Veröffentlichen Sie die neuen und/oder aktualisierten Daten im MDS-Repository.  
  
## <a name="knowledge-bases"></a>Wissensdatenbanken  
 Die im Add-In angegebenen Abgleichergebnisse basieren auf einer DQS-Wissensdatenbank.  
  
-   Die Standardwissensdatenbank (DQS-Daten) wird bei der Installation von DQS erstellt. Wenn Sie die Standardwissensdatenbank verwenden (ohne eine Abgleichsrichtlinie zur Standardwissensdatenbank im Data Quality Client hinzuzufügen), müssen Sie Spalten im Arbeitsblatt Domänen in der Wissensdatenbank zuordnen und dann den ausgewählten Domänen einen Gewichtungswert zuweisen.  
  
-   Sie können mit dem Data Quality Client eine neue Wissensdatenbank mit einer Abgleichsrichtlinie erstellen oder der Standardwissensdatenbank eine Abgleichsrichtlinie hinzufügen. In diesem Fall werden die Gewichtungswerte von der Abgleichrichtlinie bestimmt, die Sie bereits erstellt haben, und Sie müssen lediglich die Spalten den Domänen zuordnen. Weitere Informationen finden Sie unter [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md).  
  
 Weitere Informationen zu Wissensdatenbanken finden Sie unter [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Kombinieren Sie als Vorbereitung eines Vergleichs externe Daten mit von MDS verwalteten Daten.|[Kombinieren von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  
|Verwenden Sie DQS-Erkenntnisse zum Ermitteln von ähnlichen Elementen in Ihren Daten.|[Abgleichen ähnlicher Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Übersicht: Importieren von Daten aus Excel &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Data Matching](../../data-quality-services/data-matching.md)  
  
  
