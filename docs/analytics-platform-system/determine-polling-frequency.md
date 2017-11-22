---
title: Bestimmen Sie das Abrufintervall (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: "7"
ms.openlocfilehash: fb32abc38a90cd7450dc310a9f73eb7a5d72b5fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="determine-polling-frequency"></a>Bestimmen der Abrufintervalle
In diesem Thema wird erläutert, wie das Abrufintervall für SQL Server PDW Appliance Warnungen bestimmt werden.  
  
## <a name="to-determine-the-polling-frequency"></a>Um zu bestimmen, das Abrufintervall  
Da PDW derzeit proaktive Benachrichtigungen nicht unterstützt beim Auftreten von Warnungen, muss der überwachungslösung die Appliance DLLs fortlaufend abzurufen.  Intern fragt PDW die Komponenten an verschiedene Intervalle:  
  
-   Cluster – 60 Sekunden  
  
-   Taktfehler – 60 Sekunden  
  
-   Alle anderen Komponenten – 5 Minuten  
  
-   Leistungsindikatoren – 3 Sekunden  
  
Ein bestimmtes Intervall des Abrufens von Warnungen, die auch von System Center verwendet wird, ist **alle 15 Minuten**.  Natürlich können Sie mehr oder weniger häufig Abfragen, aber es wird nicht empfohlen, kleiner als alle 6 Stunden abrufen.  
  
Häufigeres akzeptabel ist, aber zu häufig abrufen überlasten kann die [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV.  Dies erschwert Benutzern Abfrage Leistungsprobleme zu diagnostizieren, wenn es schnell Abfragen wird nicht aus der Sicht ein.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Überwachen der Appliance &#40; Analyseplattformsystem &#41;](appliance-monitoring.md)  
  
