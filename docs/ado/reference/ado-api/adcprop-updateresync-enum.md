---
title: ADCPROP_UPDATERESYNC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADCPROP_UPDATERESYNC_ENUM
helpviewer_keywords:
- ADCPROP_UPDATERESYNC_ENUM [ADO]
ms.assetid: bc9e1a37-e969-47e9-8382-0bbfffa2034f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e5c25ab6802b6a99902c9e52990be80ff14ed6d5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="adcpropupdateresyncenum"></a>ADCPROP_UPDATERESYNC_ENUM
Gibt an, ob die [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) Methode einen impliziten gefolgt [Resync](../../../ado/reference/ado-api/resync-method.md) Methodenvorgangs und wenn dies der Fall ist, den Bereich dieses Vorgangs.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adResyncAll**|15|Ruft **Resync** mit der kombinierte Wert aller anderen ADCPROP_UPDATERESYNC_ENUM-Elemente.|  
|**adResyncAutoIncrement**|1|Standard. Versucht, den neuen Identitätswert für Spalten abzurufen, die automatisch erhöht oder von der Datenquelle, z. B. Microsoft Jet AutoWert-Felder oder Microsoft SQL Server-Identitätsspalten generiert werden.|  
|**adResyncConflicts**|2|Ruft **Resync** für alle Zeilen in der Update- oder Delete aufgrund eines Parallelitätskonflikts Vorgangsfehler.|  
|**adResyncInserts**|8|Ruft **Resync** für alle erfolgreich eingefügten Zeilen. AutoIncrement-Spaltenwerte sind allerdings nicht neu synchronisiert. Stattdessen werden der Inhalt der neu eingefügten Zeilen basierend auf dem vorhandenen Primärschlüsselwert neu synchronisiert. Wenn der Primärschlüssel einen Wert, der automatisch inkrementieren ist **Resync** wird nicht Abrufen des Inhalts der gewünschten Zeile. Rufen Sie für die Primärschlüsselwerte AutoIncrement automatisch inkrementiert, **UpdateBatch** mit der kombinierte Wert **AdResyncAutoIncrement** + **AdResyncInserts**.|  
|**adResyncNone**|0|Keine aufgerufen **Resync**.|  
|**adResyncUpdates**|4|Ruft **Resync** für alle erfolgreich aktualisierten Zeilen.|  
  
## <a name="applies-to"></a>Gilt für  
 [Aktualisieren Sie die Resync Eigenschaft dynamisch (ADO)](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)
