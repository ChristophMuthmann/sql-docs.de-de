---
title: GetParameterClassName-Methode (SQLServerParameterMetaData) | Microsoft Docs
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
- SQLServerParameterMetaData.getParameterClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 545634d8-f06b-429a-9293-0087d758f359
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53d055fe1ddfc16e688c9277fc643d95a282b604
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getparameterclassname-method-sqlserverparametermetadata"></a>getParameterClassName-Methode (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den vollqualifizierten Namen der Java-Klasse, mit deren Instanzen sollte, um übergeben werden, die [SetObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) Methode der [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public java.lang.String getParameterClassName(int param)  
```  
  
#### <a name="parameters"></a>Parameter  
 *param*  
  
 Ein **Int** , der Parameter-Index angibt.  
  
## <a name="return-value"></a>Rückgabewert  
 Ein **Zeichenfolge** , die den vollqualifizierten Klassennamen enthält.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese GetParameterClassName-Methode wird von der GetParameterClassName-Methode in der java.sql.ParameterMetaData-Schnittstelle angegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerParameterMetaData-Methoden](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData-Elemente](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData-Klasse](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

