---
title: MSSQLSERVER_1807 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6042f6788352b1dae1e7922c9e3e3ba59eefb91f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1807|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|CANNOT_EX_LOCK|  
|Meldungstext|Es konnte keine exklusive Sperre für die '%.*ls'-Datenbank erhalten werden. Wiederholen Sie den Vorgang zu einem späteren Zeitpunkt.|  
  
## <a name="explanation"></a>Erklärung  
Ein Vorgang, für den ein exklusiver Zugriff auf die Datenbank erforderlich war, konnte ihn nicht erhalten.  
  
## <a name="user-action"></a>Benutzeraktion  
Trennen Sie alle Verbindungen mit der entsprechenden Datenbank, oder versuchen Sie die Abfrage zu einem späteren Zeitpunkt erneut.  
  
