---
title: ObjectProxy (ADO - WFC-Syntax) | Microsoft Docs
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
helpviewer_keywords:
- ObjectProxy collection [ADO]
ms.assetid: f68f58bc-ad28-46cc-9fb3-099e1a678397
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5923cb3907f62e0910ab4aebbcf79f2ba97e5db5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="objectproxy-ado---wfc-syntax"></a>ObjectProxy (ADO - WFC-Syntax)
Ein **ObjectProxy** -Objekt stellt einen Server und wird zurückgegeben, durch die **CreateObject** Methode der [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) Objekt. Die ObjectProxy-Klasse verfügt über eine Methode, **Aufrufen**, rufen Sie eine Methode auf dem Server und ein Objekt, das aus diesem Aufruf resultierendes zurückgeben können.  
  
 **Paket com.ms.wfc.data**  
  
## <a name="methods"></a>Methoden  
  
### <a name="call-method-adowfc-syntax"></a>Call-Methode (ADO/WFC-Syntax)  
 Ruft eine Methode auf dem Server, die durch die ObjectProxy dargestellt. Methodenargumente können optional als ein Array von Objekten übergeben werden.  
  
#### <a name="syntax"></a>Syntax  
  
```  
public Object ObjectProxy.( String method )  
public Object ObjectProxy.( String method, Object[] args)  
```  
  
#### <a name="returns"></a>Rückgabewert  
 Objekt  
 Ein Objekt, das durch Aufrufen der Methode.  
  
#### <a name="parameters"></a>Parameter  
 *ObjectProxy*  
 Ein **ObjectProxy** -Objekt, das den Server darstellt.  
  
 *-Methode*  
 Eine Zeichenfolge mit dem Namen der Methode, die auf dem Server aufrufen.  
  
 *args*  
 Optional. Ein Array von Objekten, die Argumente der Methode auf dem Server sind. Java-Datentypen werden automatisch in Datentypen, die für die Verwendung auf dem Server geeignet konvertiert.
