---
title: SetCharacterStream-Methode (Int, java.io.Reader, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cb6ac7f5-81ae-4cb7-87c8-cbee40d278c5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5bcb6f7bd4440001dc5e17765e21cf7c8a408e9c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-int-javaioreader-long"></a>setCharacterStream-Methode (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Legt den angegebenen Parameter auf die java.io.Reader-Objekt, das die angegebene Anzahl von Zeichen lang ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
public final void setCharacterStream(int parameterIndex,  
                                    java.io.Reader reader,  
                                    long length)  
```  
  
#### <a name="parameters"></a>Parameter  
 *parameterIndex*  
  
 Ein **Int** , der die Parameteranzahl angibt.  
  
 *Reader*  
  
 Das java.io.Reader-Objekt, das die Unicode-Daten enthält.  
  
 *length*  
  
 Ein **lang** , der die Anzahl der Zeichen im Datenstrom angibt.  
  
## <a name="exceptions"></a>Ausnahmen  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Hinweise  
 Diese SetCharacterStream-Methode wird von der SetCharacterStream-Methode in der java.sql.PreparedStatement-Schnittstelle angegeben.  
  
 Wenn die Länge des Datenstroms unterscheidet sich von der Angabe in der *Länge* Parameter, der JDBC-Treiber löst eine Ausnahme aus, wenn die Zeile aktualisiert oder eingefügt wird.  
  
 Wenn die Länge des Datenstroms unbekannt ist, ist die *Länge* Parameter kann auf-1 festgelegt werden, um anzugeben, dass der Treiber den Datenstrom unabhängig von seiner Länge akzeptiert werden sollen. Bei "sqljdbc4.jar", empfehlen wir, dass Sie die JDBC 4.0-Methode verwenden [SetCharacterStream-Methode &#40;Int, java.io.Reader&#41; ](../../../connect/jdbc/reference/setcharacterstream-method-int-java-io-reader.md) Wenn die Anwendung möchte, um die Spalte aus einem Stream zu aktualisieren, deren Länge unbekannt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SetCharacterStream-Methode &#40;sqlserverpreparedstatement-Klasse&#41;](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement-Elemente](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
