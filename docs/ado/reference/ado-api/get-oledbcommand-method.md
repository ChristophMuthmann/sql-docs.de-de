---
title: Get_OLEDBCommand Methode | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c78a0b7bd79da2bc75c3bcccbcb2bc9acbde8e35
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getoledbcommand-method"></a>Get_OLEDBCommand-Methode
Gibt den zugrunde liegenden OLE DB-Befehl, weitergeben zuerst alle Parameterinformationen für den ADO-Befehl an den OLE DB-Befehl festgelegt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 *ppOLEDBCommand*  
 [out] Ein Zeiger auf einen Zeiger Speicherort, in dem der IUnknown-Zeiger für den zugrunde liegenden OLE DB-Befehl geschrieben wird.  
  
## <a name="applies-to"></a>Gilt für  
 [IADOCommandConstruction](http://msdn.microsoft.com/en-us/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)

