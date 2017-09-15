---
title: Die Eigenschaft PageSize (ADO) | Microsoft Docs
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
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fde7e53b844ece01f85b7ecba7e309a71107029d
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="pagesize-property-ado"></a>Die Eigenschaft PageSize (ADO)
Gibt an, wie viele Datensätze bilden eine Seite in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **lange** Wert, der angibt, wie viele Datensätze auf einer Seite befinden. Die Standardeinstellung ist **10**.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **PageSize** -Eigenschaft können Sie bestimmen, wie viele Datensätze eine logische Seite der Daten bilden. Einrichten einer Seitengröße können Sie mit der [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) Eigenschaft auf den ersten Eintrag in einer bestimmten Seite verschoben. Dies ist nützlich in Szenarien, Webserver, soll, wenn der Benutzer seitenweise durch Daten, kann eine bestimmte Anzahl von Datensätzen zu einem Zeitpunkt anzuzeigen.  
  
 Diese Eigenschaft kann zu einem beliebigen Zeitpunkt festgelegt werden, und sein Wert wird zum Berechnen der Position des ersten Datensatzes, der eine bestimmte Seite verwendet werden.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePage "PageCount" und PageSize Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage "PageCount" und PageSize Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage-Eigenschaft (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 ["PageCount"-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)

