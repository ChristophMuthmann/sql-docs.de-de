---
title: Datenspeicher (ADO - WFC-Syntax) | Microsoft Docs
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
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a393ae11d8248bc10c7d9831743426e2687ae76
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="dataspace-ado---wfc-syntax"></a>Datenspeicher (ADO - WFC-Syntax)
Die **CreateObject** Methode der **DataSpace** Klasse gibt sowohl ein Geschäftsobjekt zum Verarbeiten von Clientanforderungen für die Anwendung (*progid*) und das Kommunikationsprotokoll und Server (*Verbindung*). **CreateObject** gibt eine [ObjectProxy](../../../ado/reference/ado-api/objectproxy-ado-wfc-syntax.md) -Objekt, das den Server darstellt.  
  
## <a name="package-commswfcdata"></a>Paket com.ms.wfc.data  
  
### <a name="constructor"></a>Konstruktor  
  
```  
public DataSpace()  
```  
  
### <a name="methods"></a>Methoden  
  
```  
public static ObjectProxy DataSpace.createObject(String  
    progid, String connection)  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
public static int getInternetTimeout()  
public static void setInternetTimeout(int plInetTimeout)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DataSpace-Objekt (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)
