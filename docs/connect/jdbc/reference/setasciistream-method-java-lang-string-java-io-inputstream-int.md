---
title: "SetAsciiStream-Methode für die Eingabe von Dateidatenstrom-Bytes - Int | Microsoft Docs"
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
apiname: SQLServerCallableStatement.setAsciiStream
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6ea23386-201f-41af-8232-225de3476765
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b78e40532bcca783859592823ac192a5ab176fca
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="setasciistream-method--javalangstring-javaioinputstream-int"></a>setAsciiStream-Methode (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter auf den angegebenen Eingabedatenstrom, der die angegebene Anzahl von Bytes verfügt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public void setAsciiStream(java.lang.String parameterName,  
                           java.io.InputStream value,  
                           int length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterName*  
  
 Ein **Zeichenfolge** , die den Namen des Parameters enthält.  
  
 *value*  
  
 Ein InputStream-Objekt.  
  
 *length*  
  
 Ein **Int** , der die Länge in Anzahl von Bytes angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetAsciiStream-Methode wird von der SetAsciiStream-Methode in der java.sql.CallableStatement-Schnittstelle angegeben.  
  
 Wenn die Länge des Datenstroms, angegeben unterscheidet die *Länge* Parameter, der JDBC-Treiber löst eine Ausnahme aus, wenn die Zeile aktualisiert oder eingefügt wird.  
  
 Wenn die Länge des Datenstroms unbekannt ist, ist die *Länge* Parameter kann auf-1 festgelegt werden, um anzugeben, dass der Treiber den Datenstrom unabhängig von seiner Länge akzeptiert werden sollen. Bei "sqljdbc4.jar", empfehlen wir, dass Sie die JDBC 4.0-Methode verwenden [SetAsciiStream-Methode (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setasciistream-method-java-lang-string-java-io-inputstream.md) bei die Anwendung möchte, um die Spalte aus einem Stream zu aktualisieren, deren Länge unbekannt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement-Klasse](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
