---
title: XSLT-Transformationen | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18826a213cde63779cbe7b2a625a2de24453dac1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xslt-transformations"></a>XSLT-Transformationen
XSLT kann auf die generierte XML-Datei in ein anderes Format zu transformieren angewendet werden. Grundlegendes zu XML-Format in ADO hilft bei der Entwicklung von XSLT-Vorlagen, die sie in eine benutzerfreundlichere Form transformieren können.  
  
 Beispielsweise wissen Sie, dass jede Zeile des Recordsets als Z: Row-Element innerhalb des Elements Rs: Daten gespeichert wird. Auf ähnliche Weise wird jedes Feld des Recordset-Objekts als ein Attribut / Wert-Paar für dieses Element gespeichert.  
  
## <a name="remarks"></a>Hinweise  
 Das folgende XSLT-Skript kann angewendet werden, dem XML-Code im vorherigen Abschnitt gezeigt, um es in einer HTML-Tabelle zu transformieren, die im Browser angezeigt werden:  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 Die XSLT-Datei konvertiert des XML-Streams, die von der Methode zum Speichern von ADO generiert wird, in eine HTML-Tabelle, die jedes Feld des Recordsets zusammen mit einer Überschrift der Tabelle angezeigt. Tabellenüberschriften und Zeilen werden auch verschiedene Schriftarten und Farben zugewiesen.  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
