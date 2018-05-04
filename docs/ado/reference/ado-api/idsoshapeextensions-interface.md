---
title: IDSOShapeExtensions Schnittstelle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0ab928d6ae248acf7dfeafa95755723474c14b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
