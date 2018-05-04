---
title: CopyRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 835af17e654e6f248b9e6390251e280fdb6ef0ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
Gibt das Verhalten der [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) Methode.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|Gibt an, dass die *Quelle* -Anbieter versucht, simulieren Kopie, die mithilfe von Download- und Uploadvorgängen aus, wenn aufgrund dieser Methode ein Fehler *Ziel*befindet er sich auf einem anderen Server oder von einem anderen bearbeitet wird Anbieter als *Quelle*. Beachten Sie, dass unterschiedliche Funktionen des Anbieters Leistung behindern können, oder gehen Daten verloren.|  
|**adCopyNonRecursive**|2|Kopiert das aktuelle Verzeichnis, jedoch keiner seiner Unterverzeichnisse an das Ziel an. Der Kopiervorgang ist nicht rekursiv.|  
|**adCopyOverWrite**|1|Überschreibt die Datei oder das Verzeichnis, wenn die *Ziel* verweist auf eine vorhandene Datei oder ein Verzeichnis.|  
|**adCopyUnspecified**|-1|Standard. Führt die Standard-Kopiervorgang: der Vorgang fehl, wenn die Zieldatei oder das Verzeichnis bereits vorhanden ist und der Vorgang rekursiv kopiert.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Diese Konstanten keine ADO/WFC-Entsprechungen.  
  
## <a name="applies-to"></a>Gilt für  
 [CopyRecord-Methode (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
