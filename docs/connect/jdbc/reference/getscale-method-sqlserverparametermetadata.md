---
title: GetScale-Methode (SQLServerParameterMetaData) | Microsoft Docs
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
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e77c6dcfd46b6fbb522312738bd24c9f4ac94fe0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="getscale-method-sqlserverparametermetadata"></a>getScale-Methode (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft für den angegebenen Parameter die Anzahl von Stellen hinter dem Dezimalzeichen ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public int getScale(int param)  
```  
  
#### <a name="parameters"></a>Parameter  
 *param*  
  
 Ein **Int** , der Parameter-Index angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 In **Int** , der die Dezimalstellen des angegebenen Parameters angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetScale-Methode wird von der GetScale-Methode in der java.sql.ParameterMetaData-Schnittstelle angegeben.  
  
 Von dieser Methode werden Spaltendezimalstellen abgerufen. Bei Typen ohne Dezimalzeichen wird "0" zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerParameterMetaData-Methoden](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData-Elemente](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData-Klasse](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
