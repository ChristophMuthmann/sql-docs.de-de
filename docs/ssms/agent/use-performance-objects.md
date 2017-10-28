---
title: Verwenden von Leistungsobjekten | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5197a38da57e041039dab93d037064bba79db7ff
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="use-performance-objects"></a>Verwenden von Leistungsobjekten
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent umfasst Leistungsobjekte und -indikatoren zum Überwachen der Leistung des Diensts. Mithilfe dieser Leistungsobjekte können Sie das Windows-Tool Systemmonitor verwenden, um festzustellen, welche Vorgänge vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst im Hintergrund ausgeführt werden. Sie können beispielsweise die Anzahl der aktiven Aufträge feststellen, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst aktuell ausgeführt werden, um blockierte Aufträge zu identifizieren.  
  
Die Leistungsobjekte und Leistungsindikatoren des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Diensts sind für jede Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] vorhanden, die auf einem Computer installiert ist. Leistungsobjekte sind nach der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] benannt, die jedes Objekt repräsentiert.  
  
Die folgende Tabelle veranschaulicht, wie die Leistungsobjekte des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Diensts benannt werden:  
  
|Instanztyp|Objektname|  
|-----------------|---------------|  
|Default|**SQLAgent:***Objekt*:*Indikator*|  
|Benannt|**SQLAgent$**<br /> **&#42;Instanzname&#42; :***Objekt*:*Indikator*|  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] beinhaltet die folgenden Leistungsobjekte für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent.  
  
|Objektname|Description|  
|---------------|---------------|  
|[SQLAgent:Aufträge](http://msdn.microsoft.com/en-us/225b5e2d-4a78-4178-b2b6-b419df83c4aa)|Leistungsinformationen zu gestarteten Aufträgen, Erfolgsrate und aktuellem Status|  
|[SQLAgent:Auftragsschritte](http://msdn.microsoft.com/en-us/44f9983c-1753-4fe0-8475-973aa2460b3a)|Statusinformationen zu Auftragsschritten|  
|[SQLAgent:Warnungen](http://msdn.microsoft.com/en-us/e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a)|Informationen zur Anzahl der Warnungen und Benachrichtigungen|  
|[SQLAgent:Statistik](http://msdn.microsoft.com/en-us/ebe92bfa-0721-48aa-9ba6-e7904ad265a1)|Allgemeine Leistungsinformationen|  
  
## <a name="see-also"></a>Siehe auch  
[Überwachen und Optimieren der Leistung](http://msdn.microsoft.com/en-us/87f23f03-0f19-4b2e-bfae-efa378f7a0d4)  
[Vorgehensweise: Starten des Systemmonitors (Windows)](http://msdn.microsoft.com/en-us/5e51bb79-5737-470b-9c47-fac330c001c5)  
  

