---
title: IsolationLevelEnum | Microsoft Docs
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
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f6f18a4cd10c70369d2e0aceb226310d7a5f4ae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
Gibt die Ebene der Isolation jeder Transaktion für eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
|Konstante|Wert|Description|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|Gibt an, dass der Anbieter eine andere Isolationsstufe verwendet wird, als angegeben, aber die Ebene nicht bestimmt werden kann.|  
|**adXactChaos**|16|Gibt an, dass die ausstehenden Änderungen durch Transaktionen mehr hoch isolierten nicht überschrieben werden kann.|  
|**adXactBrowse**|256|Gibt an, dass eine Transaktion ausgecheckte Änderungen in anderen Transaktionen anzeigen können.|  
|**adXactReadUncommitted**|256|Identisch mit **AdXactBrowse**.|  
|**adXactCursorStability**|4096|Gibt an, dass von einer Transaktion aus Änderungen in anderen Transaktionen nur, nachdem sie ein Commit ausgeführt wurde.|  
|**adXactReadCommitted**|4096|Identisch mit **AdXactCursorStability**.|  
|**adXactRepeatableRead**|65536|Gibt an, dass Sie nicht aus einer Transaktion in anderen Transaktionen vorgenommene Änderungen sehen, Erneutes Abfragen kann jedoch auch Abrufen neuer **Recordset** Objekte.|  
|**adXactIsolated**|1048576|Gibt an, dass Transaktionen isoliert von anderen Transaktionen durchgeführt werden.|  
|**adXactSerializable**|1048576|Identisch mit **AdXactIsolated**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC-Entsprechung  
 Paket: **com.ms.wfc.data**  
  
|Konstante|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>Gilt für  
 [IsolationLevel-Eigenschaft](../../../ado/reference/ado-api/isolationlevel-property.md)
