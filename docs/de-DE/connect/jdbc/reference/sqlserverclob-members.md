---
title: SQLServerClob-Elemente | Microsoft Docs
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
apitype: Assembly
ms.assetid: 7db785ca-edd5-4833-8053-17fdbf87279a
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d0c1db09adaa23a9f1ac1309cce91e4cf087437
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverclob-members"></a>SQLServerClob-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  In den folgenden Tabellen enthalten die Elemente, die verfügbar gemacht werden, indem Sie die [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
  
|Name|Description|  
|----------|-----------------|  
|[SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-constructor-sqlserverconnection-java-lang-string.md)|Initialisiert eine neue Instanz der SQLServerClob-Klasse.|  
  
## <a name="fields"></a>Felder  
 Keine.  
  
## <a name="inherited-fields"></a>Geerbte Felder  
 Keine.  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[Frei](../../../connect/jdbc/reference/free-method-sqlserverclob.md)|Mit dieser Methode werden das CLOB sowie die von diesem verwendeten Ressourcen freigegeben.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverclob.md)|Materialisiert das CLOB als ASCII-Datenstrom.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverclob.md)|Gibt die CLOB-Daten als java.io.Reader-Objekt oder als Zeichendatenstrom zurück.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlserverclob.md)|Gibt eine Kopie der angegebenen Teilzeichenfolge im CLOB auf der Grundlage der angegebenen Startposition und der Anzahl der zu kopierenden Zeichen zurück.|  
|[length](../../../connect/jdbc/reference/length-method-sqlserverclob.md)|Gibt die Anzahl von Zeichen im CLOB zurück.|  
|[position](../../../connect/jdbc/reference/position-method-sqlserverclob.md)|Gibt die Zeichenposition des angegebenen CLOBs oder der Zeichenfolge im CLOB auf der Grundlage der angegebenen Startposition zurück.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverclob.md)|Gibt einen Datenstrom zurück, der verwendet wird, um ab der angegebenen Position ASCII-Zeichen in das CLOB zu schreiben.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverclob.md)|Gibt einen Datenstrom zurück, der verwendet wird, um ab der angegebenen Position einen Unicode-Zeichendatenstrom in das CLOB zu schreiben.|  
|[SetString](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)|Schreibt die angegebene Zeichenfolge ab der angegebenen Position in das CLOB.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlserverclob.md)|Kürzt das Clob auf die angegebene Länge.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von|Methoden|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerClob-Klasse](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
