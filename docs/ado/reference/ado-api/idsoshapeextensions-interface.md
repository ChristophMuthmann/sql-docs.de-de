---
title: IDSOShapeExtensions Schnittstelle | Microsoft Docs
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
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 454dc39046b33e2b621f77ea2a31bddc16b742ea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="idsoshapeextensions-interface"></a>IDSOShapeExtensions-Schnittstelle
Ruft das zugrunde liegende Objekt für den OLE DB-Datenquelle für das SHAPE-Anbieters ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>Methoden  
  
|||  
|-|-|  
|[GetDataProviderDSO-Methode](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Ruft das zugrunde liegende Objekt für den OLE DB-Datenquelle aus der Shape-Anbieters ab.|  
  
## <a name="requirements"></a>Anforderungen  
 **Version:** ADO 2.0 und höher  
  
 **Bibliothek:** "MSADO15.dll"  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
