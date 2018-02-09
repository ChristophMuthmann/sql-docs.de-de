---
title: MoveRecordOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d42dbc66f84a3b087401063ee3a53a00f2f37105
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Gibt das Verhalten der [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) Methode.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Standard. Führt der Standardvorgang verschieben: der Vorgang fehlschlägt, wenn die Zieldatei oder das Verzeichnis bereits vorhanden ist, und der Vorgang Hypertextlinks aktualisiert.|  
|**adMoveOverWrite**|1|Überschreibt die Zieldatei oder das Verzeichnis, an, auch wenn er bereits vorhanden ist.|  
|**adMoveDontUpdateLinks**|2|Ändert das Standardverhalten des **MoveRecord** Methode durch die Aktualisierung nicht Hypertextlinks der Quelle **Datensatz**. Das Standardverhalten hängt von den Funktionen des Anbieters ab. Verschiebevorgang aktualisiert Links aus, wenn der Anbieter kann. Wenn der Anbieter Links nicht beheben kann, oder wenn dieser Wert nicht angegeben wird, erfolgreich verschieben, selbst wenn Links nicht behoben wurden.|  
|**adMoveAllowEmulation**|4|Fordert an, dass der Anbieter versuchen, um das Verschieben (mit herunterladen, hochladen und Löschvorgänge) zu simulieren. Wenn beim Versuch, Verschieben der **Datensatz** schlägt fehl, da der Ziel-URL auf einem anderen Server wird oder von einem anderen Anbieter als die Quelle bedient, wird daher möglicherweise höhere Latenz oder Datenverlust aufgrund verschiedener Anbieterfunktionen beim Verschieben von Ressourcen zwischen Anbietern.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [MoveRecord-Methode (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
