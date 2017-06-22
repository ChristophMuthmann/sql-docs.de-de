---
title: "Überwachen der CPU-Auslastung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- monitoring performance [SQL Server], CPU usage
- tuning databases [SQL Server], CPU usage
- processors [SQL Server], monitoring usage
- database performance [SQL Server], CPU usage
- monitoring CPU usage [SQL Server]
- server performance [SQL Server], CPU usage
- database monitoring [SQL Server], CPU usage
- monitoring [SQL Server], CPU usage
- processors [SQL Server]
- CPU [SQL Server], monitoring
- monitoring server performance [SQL Server], CPU usage
ms.assetid: 2a02a3b6-07b2-4ad0-8a24-670414d19812
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 53ee7928baad42733f9b9cfaaf699153b993a287
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="monitor-cpu-usage"></a>Überwachen der CPU-Auslastung
  Überwachen Sie eine Instanz von Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in regelmäßigen Abständen, um sicherzustellen, dass sich die CPU-Nutzungsraten im Normalbereich bewegen. Eine konstant hohe CPU-Nutzungsrate kann ein Anzeichen dafür sein, dass die CPU aktualisiert werden muss oder weitere Prozessoren hinzugefügt werden müssen. Darüber hinaus kann eine hohe CPU-Nutzungsrate auf eine schlecht angepasste oder entwickelte Anwendung hinweisen. Eine Optimierung der Anwendung kann die CPU-Nutzung senken.  
  
 Um die CPU-Nutzungsrate festzustellen, rufen Sie am besten im Systemmonitor den Leistungsindikator **Prozessor: Prozessorzeit (%)** auf. Dieser Leistungsindikator überwacht die Zeit, die die CPU zur Verarbeitung eines Threads benötigt, der sich nicht im Leerlauf befindet. Ein konstanter Status von 80-90 % kann darauf hinweisen, dass ein CPU-Upgrade notwendig ist oder weitere Prozessoren hinzugefügt werden müssen. Bei Multiprozessorsystemen sollte für jeden Prozessor eine separate Instanz dieses Leistungsindikators überwacht werden. Dieser Wert stellt die Summe der Prozessorzeit für einen bestimmten Prozessor dar. Um den Durchschnitt für alle Prozessoren zu ermitteln, müssen Sie dagegen den Leistungsindikator **System: Gesamtprozessorzeit (%)** aufrufen.  
  
 Darüber hinaus können Sie die Prozessornutzung aber auch über die folgenden Leistungsindikatoren überwachen:  
  
-   **Prozessor: Privilegierte Zeit (%)**  
  
     Gibt den prozentualen Zeitanteil an der Gesamtzeit an, die der Prozessor benötigt, um Microsoft Windows-Kernelbefehle, wie die Verarbeitung von E/A-Anforderungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , auszuführen. Sollte dieser Leistungsindikator bei hohen Werten für die Leistungsindikatoren **Physischer Datenträger** gleich bleibend hoch sein, sollten Sie die Installation eines schnelleren oder effizienteren Datenträgersubsystems in Erwägung ziehen.  
  
    > [!NOTE]  
    >  Unterschiedliche Datenträgercontroller und -treiber benötigen unterschiedlich viel Zeit für die Kernelverarbeitung. Effiziente Controller und Treiber beanspruchen weniger privilegierte Zeit und überlassen Benutzeranwendungen so mehr Verarbeitungszeit, wodurch der Durchsatz insgesamt steigt.  
  
-   **Prozessor: Benutzerzeit (%)**  
  
     Gibt den prozentualen Zeitanteil an der Gesamtzeit an, die der Prozessor benötigt, um Benutzerprozesse wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]auszuführen.  
  
-   **System: Prozessor-Warteschlangenlänge**  
  
     Gibt die Anzahl der Threads an, die auf Prozessorzeit warten. Ein Prozessorengpass entsteht, wenn die Threads eines Prozesses mehr Prozessorzyklen benötigen, als zur Verfügung stehen. Wenn viele Prozesse versuchen, Prozessorzeit zu beanspruchen, müssen Sie ggf. einen schnelleren Prozessor installieren. Bei einem Multiprozessorsystem könnten Sie auch einen Prozessor hinzufügen.  
  
 Bei der Überprüfung der Prozessornutzung müssen Sie auch die Art der Vorgänge berücksichtigen, die durch die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden. Wenn in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viele Berechnungen ausgeführt werden, wie etwa Abfragen, die Aggregate enthalten, oder arbeitsspeichergestützte Abfragen, bei denen keine Datenträger-E/A notwendig ist, können durchaus 100 % der Prozessorzeit beansprucht werden. Wenn dies bewirkt, dass die Leistung anderer Anwendungen leidet, versuchen Sie, die Arbeitsauslastung zu ändern. Reservieren Sie beispielsweise den Computer für das Ausführen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nutzungsraten um 100 %, wenn viele Clientanforderungen verarbeitet werden, können darauf hinweisen, dass Prozesse in Warteschlangen angeordnet werden, auf Prozessorzeit warten und einen Engpass verursachen. Lösen Sie das Problem, indem Sie das System durch leistungsstärkere Prozessoren ergänzen.  
  
  
