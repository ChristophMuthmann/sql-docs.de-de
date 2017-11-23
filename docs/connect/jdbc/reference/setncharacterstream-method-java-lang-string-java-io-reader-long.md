---
title: SetNCharacterStream-Methode auf Leserobjekt - lang | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: af9a1ba8-7980-43fa-88e5-14f6cc5e897c
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 291c94f63ebc86869682e769ef93b93c86f60ffc
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setncharacterstream-method-javalangstring-javaioreader-long"></a>setNCharacterStream-Methode (java.lang.String, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter auf den angegebenen Reader-Objekt, das die angegebene Anzahl von Zeichen lang ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                     java.io.Reader value,  
                     long length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterName*  
  
 Ein **Zeichenfolge** , der den Namen des Parameters angibt.  
  
 *value*  
  
 Ein Readerobjekt.  
  
 *length*  
  
 Ein **lang** , der die Anzahl der Zeichen im Datenstrom angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetNCharacterStream-Methode wird von der SetNCharacterStream-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Diese Methode sollte verwendet werden, für die **NCHAR**, **NVARCHAR**, **NTEXT**, und **XML** -Datentypen.  
  
 Wenn die Länge des Datenstroms unterscheidet sich von der Angabe in der *Länge* Parameter, der JDBC-Treiber löst eine Ausnahme aus, wenn die Zeile aktualisiert oder eingefügt wird.  
  
 Wenn die Länge des Datenstroms unbekannt ist, ist die *Länge* Parameter kann auf-1 festgelegt werden, um anzugeben, dass der Treiber den Datenstrom unabhängig von seiner Länge akzeptiert werden sollen. Bei "sqljdbc4.jar", empfehlen wir, dass Sie die JDBC 4.0-Methode verwenden [SetNCharacterStream-Methode &#40;java.lang.String, java.io.Reader &#41;](../../../connect/jdbc/reference/setncharacterstream-method-java-lang-string-java-io-reader.md) Wenn die Anwendung die Spalte aus einem Datenstrom Länge zu aktualisieren möchte unbekannt.  
  
## <a name="see-also"></a>Siehe auch  
 [SetNCharacterStream-Methode &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
