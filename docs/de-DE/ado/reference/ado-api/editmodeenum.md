---
title: EditModeEnum | Microsoft Docs
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
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3702e111333194804f3c0bd7335e4403f4bfddd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="editmodeenum"></a>EditModeEnum
Gibt den Bearbeitungsstatus eines Datensatzes.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Gibt an, dass kein Bearbeitungsvorgang ausgeführt wird.|  
|**adEditInProgress**|1|Gibt an, dass die Daten im aktuellen Datensatz geändert, aber nicht gespeichert wurden.|  
|**adEditAdd**|2|Gibt an, dass die [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) -Methode aufgerufen wurde, und der aktuelle Datensatz im Kopierpuffer ist ein neuer Datensatz, der nicht in der Datenbank gespeichert wurde.|  
|**adEditDelete**|4|Gibt an, dass der aktuelle Datensatz gelöscht wurde.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>Gilt für  
 [EditMode-Eigenschaft](../../../ado/reference/ado-api/editmode-property.md)
