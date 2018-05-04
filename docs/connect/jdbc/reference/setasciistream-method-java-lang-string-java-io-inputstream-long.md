---
title: SetAsciiStream-Methode, die Eingabe von stream Byte - long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6bc486cd-e432-4057-8789-9957ba23dd30
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc27260a8052dddbb167eeba110945d00e80a200
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setasciistream-method-javalangstring-javaioinputstream-long"></a>setAsciiStream-Methode (java.lang.String, java.io.InputStream, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebene Parameter auf den angegebenenEingabedatenstrom mit der angegebenen Anzahl von Bytes fest.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x,  
                                long length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterName*  
  
 Ein **Zeichenfolge** , die den Namen des Parameters enthält.  
  
 *x*  
  
 Ein InputStream-Objekt.  
  
 *length*  
  
 Ein **lang** , der die Anzahl von Bytes angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetAsciiStream-Methode wird von der SetAsciiStream-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
 Wenn die Länge des Datenstroms unterscheidet sich von der Angabe in der *Länge* Parameter, der JDBC-Treiber löst eine Ausnahme aus, wenn die Zeile aktualisiert oder eingefügt wird.  
  
 Wenn die Länge des Datenstroms unbekannt ist, ist die *Länge* Parameter kann auf-1 festgelegt werden, um anzugeben, dass der Treiber den Datenstrom unabhängig von seiner Länge akzeptiert werden sollen. Bei "sqljdbc4.jar", empfehlen wir, dass Sie die JDBC 4.0-Methode verwenden [SetAsciiStream-Methode (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setasciistream-method-java-lang-string-java-io-inputstream.md) bei die Anwendung möchte, um die Spalte aus einem Stream zu aktualisieren, deren Länge unbekannt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SetAsciiStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement-Elemente](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
