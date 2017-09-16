---
title: SetResponseBuffering-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerDataSource.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: c9e43ff2-8117-4dca-982d-83c863d0c8e1
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 88cfa89a30461ba3013c7b227651d5d0292c77b2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setresponsebuffering-method-sqlserverdatasource"></a>setResponseBuffering-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den antwortpuffermodus für Verbindungen mit diesem erstellt [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) Objekt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameter  
 *value*  
  
 Ein **Zeichenfolge** , die den Puffer- und Streamingmodus Modus enthält. Gültige Modi kann eine der folgenden Zeichenfolgen Groß-/Kleinschreibung: **vollständige** oder **adaptive**.  
  
## <a name="remarks"></a>Hinweise  
 Die **vollständige** Wert gibt an, das gesamte Ergebnis vom Server gelesen, zur Laufzeit.  
  
 Die **adaptive** Wert gibt die Pufferung wenig Daten wie möglichen bei Bedarf an. Die **adaptive** Wert ist der standardpuffermodus.  
  
 Weitere Informationen zur Verwendung der antwortpuffermodus finden Sie unter [mithilfe der adaptiven Pufferung](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
