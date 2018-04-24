---
title: MSSQLSERVER_17053 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fa2aabfa00f75a7abb4407dcb88cb2b75f41d69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver17053"></a>MSSQLSERVER_17053
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|17053|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|OS_ERROR|  
|Meldungstext|%ls: Betriebssystemfehler %ls.|  
  
## <a name="explanation"></a>Erklärung  
Ein allgemeiner Betriebssystemfehler ist aufgetreten.  Der resultierende Status ist unbekannt.  
  
## <a name="user-action"></a>Benutzeraktion  
Normalerweise tritt dies in Verbindung mit einem anderen Fehler auf und sollte dazu verwendet werden, eine Diagnose für diesen Fehler zu erstellen. Zu den Beispielen gehören fehlerhafte Lese- oder Schreibvorgänge für Daten und Protokolldateien, Lese-/Schreibvorgänge für die Registrierung oder unerwartete Win32API-Fehler.  
  
