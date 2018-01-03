---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords: ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d030fa1643cbf836a7380dd3113236ec7961b8d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
Gibt an, ob die [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode einen impliziten gefolgt [Resync](../../../ado/reference/ado-api/resync-method.md) Methodenvorgangs und wenn dies der Fall ist, den Bereich dieses Vorgangs.  
  
|Konstante|value|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Ruft **Resync** mit der kombinierte Wert aller anderen ADCPROP_UPDATERESYNC_ENUM-Elemente.|  
|**adResyncAutoIncrement**|1|Standard. Versucht, den neuen Identitätswert für Spalten abzurufen, die automatisch erhöht oder von der Datenquelle, z. B. Microsoft Jet AutoWert-Felder oder Microsoft SQL Server-Identitätsspalten generiert werden.|  
|**adResyncConflicts**|2|Ruft **Resync** für alle Zeilen in der Update- oder Delete aufgrund eines Parallelitätskonflikts Vorgangsfehler.|  
|**adResyncInserts**|8|Ruft **Resync** für alle erfolgreich eingefügten Zeilen. AutoIncrement-Spaltenwerte sind allerdings nicht neu synchronisiert. Stattdessen werden der Inhalt der neu eingefügten Zeilen basierend auf dem vorhandenen Primärschlüsselwert neu synchronisiert. Wenn der Primärschlüssel einen Wert, der automatisch inkrementieren ist **Resync** wird nicht Abrufen des Inhalts der gewünschten Zeile. Rufen Sie für die Primärschlüsselwerte AutoIncrement automatisch inkrementiert, **UpdateBatch** mit der kombinierte Wert **AdResyncAutoIncrement** + **AdResyncInserts**.|  
|**adResyncNone**|0|Keine aufgerufen **Resync**.|  
|**adResyncUpdates**|4|Ruft **Resync** für alle erfolgreich aktualisierten Zeilen.|  
  
## <a name="applies-to"></a>Gilt für  
 [Dynamische Eigenschaft Update Resync (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
