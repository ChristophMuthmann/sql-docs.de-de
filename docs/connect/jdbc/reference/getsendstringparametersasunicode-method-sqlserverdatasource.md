---
title: GetSendStringParametersAsUnicode-Methode (SQLServerDataSource) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getSendStringParametersAsUnicode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3836d0ab-c3fb-41ff-bb89-10389594ae51
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 520e40a43f47536b34ef68ebebde73f199c8e915
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="getsendstringparametersasunicode-method-sqlserverdatasource"></a>getSendStringParametersAsUnicode-Methode (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Gibt eine **booleschen** -Wert, der angibt, ob das Senden von Zeichenfolgenparametern an den Server im Unicode-Format aktiviert ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public boolean getSendStringParametersAsUnicode()  
```  
  
## <a name="return-value"></a>Rückgabewert  
 **"true"** Wenn Zeichenfolgenparameter im Unicode-Format an den Server gesendet werden. Andernfalls lautet der Wert **false**.  
  
## <a name="remarks"></a>Hinweise  
 Wenn die SendStringParametersAsUnicode-Eigenschaft, um festgelegt wird **"true"**, Hierbei handelt es sich um den Standardwert, Zeichenfolgenparameter im Unicode-Format an den Server gesendet werden. Wenn SendStringParametersAsUnicode auf **"false"**, String-Parameter an den Server in einem ASCII/MBCS-Format, nicht im Unicode-Format gesendet werden. Wenn sendstringparametersasunicode-Eigenschaft nicht festgelegt ist, gibt GetSendStringParametersAsUnicode den Standardwert von **"true"**.  
  
 Weitere Informationen zur SendStringParametersAsUnicode-Verbindungseigenschaft finden Sie unter [Festlegen der Verbindungseigenschaften](../../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerDataSource-Elemente](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource-Klasse](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

