---
title: GetScale-Methode (SQLServerParameterMetaData) | Microsoft Docs
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
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be05360747e2b67de20d6e93823b77629b5bbbac
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
  
  

