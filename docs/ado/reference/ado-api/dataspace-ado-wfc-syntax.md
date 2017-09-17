---
title: Datenspeicher (ADO - WFC-Syntax) | Microsoft Docs
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
helpviewer_keywords:
- DataSpace collection [ADO], ADO/WFC syntax
ms.assetid: 950d45d8-07de-467b-b255-f9a7b997204c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0344190472a9548880e828786bd252bdb17de29b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
