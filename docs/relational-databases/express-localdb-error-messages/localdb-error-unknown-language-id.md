---
title: LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: fa082dca-bf88-46e7-b61e-7ac8835a3493
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5048e40018234568a2da0319cb1e0f3226715a4f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="localdberrorunknownlanguageid"></a>LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|270|  
|Ereignisquelle|Lokale SQL Server-Datenbanklaufzeit 12.0|  
|Komponente|Laufzeit-API der lokalen Datenbank|  
|Meldungstext|Fehler beim Abrufen der lokalisierten Fehlermeldung. Die im LanguageID-Parameter angegebene Sprache ist unbekannt.|  
  
## <a name="explanation"></a>Erklärung  
 Die angeforderte Sprache für die Laufzeitfehlermeldung der lokalen Datenbank ist unbekannt oder wird nicht unterstützt.  
  
## <a name="user-action"></a>Benutzeraktion  
 Versuchen Sie, eine der unterstützten Sprachen für Laufzeitfehlermeldungen der lokalen Datenbank oder eine Standardsprache anzufordern.  
  
  
