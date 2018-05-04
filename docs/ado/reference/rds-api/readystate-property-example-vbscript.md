---
title: Eigenschaft ReadyState-Beispiel (VBScript) | Microsoft Docs
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ReadyState property [ADO], VBScript example
ms.assetid: e3e18da4-0511-4ece-a35d-699978bc28c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0c34362dfec239d7a2f46f2786a8ad7c8b09137
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="readystate-property-example-vbscript"></a>Eigenschaft ReadyState-Beispiel (VBScript)
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Im folgende Beispiel wird gezeigt, wie zum Lesen der [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) Eigenschaft von der [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt zur Laufzeit in VBScript-Code. **ReadyState** ist eine schreibgeschützte Eigenschaft.  
  
 Klicken Sie zum Testen dieses Beispiels ausgeschnitten, und fügen Sie diesen Code zwischen den \<Text > und \</Body > Tags in einer normalen HTML-Dokument, und nennen Sie sie **RDSReadySt.asp**. Verwenden Sie **suchen** suchen Sie die Datei Adovbs.inc und fügen Sie ihn in das Verzeichnis, das Sie verwenden möchten. ASP-Skript identifiziert Ihren Server.  
  
```  
<!-- BeginReadyStateVBS -->  
<%@ Language=VBScript %>  
<!--#include file="adovbs.inc"-->  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>RDS.DataControl ReadyState Property</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body>  
<H1>RDS.DataControl ReadyState Property</H1>  
<H2>RDS API Code Examples </H2>  
<HR>  
<!-- RDS.DataControl with parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS>  
   <PARAM NAME="SQL" VALUE="Select * from Orders">  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=SQLOLEDB;Integrated Security=SSPI;Initial Catalog=Northwind">  
   <PARAM NAME="ExecuteOptions" VALUE="2">   
   <PARAM NAME="FetchOptions" VALUE="3">  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="OrderID"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<Script Language="VBScript">  
  
   Sub Window_OnLoad  
  
      Select Case RDS.ReadyState  
         case 2   'adcReadyStateLoaded  
          MsgBox "Executing Query"  
         case 3   'adcReadyStateInteractive  
          MsgBox "Fetching records in background"  
         case 4   'adcReadyStateComplete  
          MsgBox "All records fetched"  
      End Select  
  
   End Sub  
</Script>  
  
</body>  
</html>  
<!-- EndReadyStateVBS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [ReadyState-Eigenschaft (RDS)](../../../ado/reference/rds-api/readystate-property-rds.md)


