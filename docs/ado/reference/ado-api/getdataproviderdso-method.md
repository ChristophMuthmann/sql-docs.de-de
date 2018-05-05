---
title: GetDataProviderDSO Methode | Microsoft Docs
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
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 687ba2301edfbd944bc9feafdbce2c528b26b58c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO-Methode
Ruft das zugrunde liegende Objekt für den OLE DB-Datenquelle aus der Shape-Anbieters ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 *ppDataProviderDSOIUnknown*  
 [out]  Ein Zeiger auf einen Zeiger, der das IUnknown des zugrunde liegenden Objekts der OLE DB-Datenquelle zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode hat keine Addref den Schnittstellenzeiger auf. Wenn der Aufrufer plant, die Zeiger enthalten, müssen der Aufrufer erforderlich Addref und release.  
  
## <a name="applies-to"></a>Gilt für  
 [IDSOShapeExtensions-Schnittstelle](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
