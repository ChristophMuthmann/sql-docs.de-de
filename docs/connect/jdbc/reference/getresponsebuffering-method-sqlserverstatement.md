---
title: GetResponseBuffering-Methode (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64ad84e838e64c0e4bd148705e2753277f908a3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>getResponseBuffering-Methode (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den antwortpuffermodus für dieses [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** Kleinbuchstaben enthält **vollständige** oder **adaptive**.  
  
## <a name="remarks"></a>Hinweise  
 **Adaptive** gibt die Pufferung der Daten wie möglichen bei Bedarf an.  
  
 **vollständige** gibt an, das gesamte Ergebnis vom Server gelesen, zur Laufzeit.  
  
 **Adaptive** ist der Standardwert in JDBC Driver, Version 2.0 und 3.0. **vollständige** war der Standardwert in Versionen vor JDBC Driver, Version 2.0.  
  
 Weitere Informationen zur Verwendung der antwortpuffermodus finden Sie unter [mithilfe der adaptiven Pufferung](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SetResponseBuffering-Methode &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [SQLServerStatement-Elemente](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement-Klasse](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
