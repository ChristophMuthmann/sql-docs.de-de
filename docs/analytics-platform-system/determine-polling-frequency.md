---
title: Bestimmen Sie das Abrufintervall (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: 7
ms.openlocfilehash: e67ab38c12000f3d78a9179a177ce5f673b8eaa2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
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
[Überwachen der Appliance &#40;Analyseplattformsystem&#41;](appliance-monitoring.md)  
  
