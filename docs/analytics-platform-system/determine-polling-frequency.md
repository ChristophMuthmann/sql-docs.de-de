---
title: Bestimmen Abrufintervalle - Analytics Platform System | Microsoft Docs
description: In diesem Artikel wird erläutert, wie das Abrufintervall für Analytics Platform System Appliance Warnungen bestimmt wird.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e8e2a1ccf469e6c587870c0d5921014d797f87d1
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="determine-polling-frequency"></a>Bestimmen der Abrufintervalle
In diesem Artikel wird erläutert, wie das Abrufintervall für Analytics Platform System Appliance Warnungen bestimmt wird.  
  
## <a name="to-determine-the-polling-frequency"></a>Um zu bestimmen, das Abrufintervall  
Da PDW derzeit proaktive Benachrichtigungen nicht unterstützt beim Auftreten von Warnungen, muss der überwachungslösung die Appliance DLLs fortlaufend abzurufen.  Intern fragt PDW die Komponenten an verschiedene Intervalle:  
  
-   Cluster – 60 Sekunden  
  
-   Taktfehler – 60 Sekunden  
  
-   Alle anderen Komponenten – fünf Minuten  
  
-   Leistungsindikatoren – drei Sekunden  
  
Ein bestimmtes Intervall des Abrufens von Warnungen, die auch von System Center verwendet wird, ist **alle 15 Minuten**.  Natürlich können Sie mehr oder weniger häufig Abfragen, aber es wird nicht empfohlen, kleiner als alle sechs Stunden abrufen.  
  
Häufigeres akzeptabel ist, aber zu häufig abrufen überlasten kann die [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV.  Zu häufig abrufen lassen es schwierig für Benutzer, um die abfrageleistung zu diagnostizieren Probleme bei deren schnell aus der Sicht wird ein.  
  
## <a name="see-also"></a>Siehe auch  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Überwachen der Appliance &#40;Analyseplattformsystem&#41;](appliance-monitoring.md)  
  
