---
title: ExecuteOptions und FetchOptions Eigenschaften Beispiel (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- FetchOptions property [ADO], VBScript example
- ExecuteOptions property [ADO]
ms.assetid: 753a4a3d-0fba-40b8-86e7-50b34182ca69
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f35f6b4c00b33eeea463a99540eba40abf76ebe
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="executeoptions-and-fetchoptions-properties-example-vbscript"></a>ExecuteOptions und FetchOptions Eigenschaften Beispiel (VBScript)
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Der folgende Code veranschaulicht das Festlegen der [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) und [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) Eigenschaften zur Entwurfszeit. Wenn nicht festgelegt ist, bleibt **ExecuteOptions** standardmäßig **AdcExecSync**. Diese Einstellung gibt an, dass die **RDS. Aktualisieren Sie** -Methode aufgerufen wird, für den aktuellen aufrufenden Thread ausgeführt wird – d. h., synchron. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor, und speichern Sie diese als **ExecuteOptionsDesignVBS.asp**.  
  
```  
<!-- BeginExecuteOptionsDesignVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Design-time ExecuteOptions and FetchOptions Properties Example</title>  
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
<h2>Design-time <br> ExecuteOptions and FetchOptions Properties Example</h2>  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS height=1 width=1>  
<PARAM NAME="SQL" VALUE="SELECT FirstName, LastName FROM Employees ORDER BY LastName">  
<PARAM NAME="Connect" VALUE="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Integrated Security='SSPI';Initial Catalog='Northwind'">  
<PARAM NAME="Server" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
<PARAM NAME="ExecuteOptions" VALUE="1">  
<PARAM NAME="FetchOptions" VALUE="3">  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR class="thead2">  
      <TH>First Name</TH>  
      <TH>Last Name</TH>  
   </TR>  
   <TR class="tbody">  
     <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
     <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
  
</body>  
</html>  
<!-- EndExecuteOptionsDesignVBS -->  
```  
  
 Im folgende Beispiel wird gezeigt, wie zum Festlegen der **ExecuteOptions** und **FetchOptions** Eigenschaften zur Laufzeit in VBScript-Code. Finden Sie unter der [aktualisieren](../../../ado/reference/rds-api/refresh-method-rds.md) Methode ein funktionsfähiges Beispiel dieser Eigenschaften. Ausschneiden und fügen Sie den folgenden Code in Editor oder einem anderen Texteditor, und speichern Sie diese als **ExecuteOptionsRuntimeVBS.asp**.  
  
```  
<!-- BeginExecuteOptionsRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Run-time ExecuteOptions and FetchOptions Properties Example</title>  
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
<h2>Run-time <br> ExecuteOptions and FetchOptions Properties Example</h2>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS height=1 width=1>  
<PARAM NAME="SQL" VALUE="SELECT FirstName, LastName FROM Employees ORDER BY LastName">  
<PARAM NAME="Connect" VALUE="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Integrated Security='SSPI';Initial Catalog='Northwind'">  
<PARAM NAME="Server" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR class="thead2">  
      <TH>First Name</TH>  
      <TH>Last Name</TH>  
   </TR>  
   <TR class="tbody">  
     <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
     <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
<Script Language="VBScript">  
Const adcExecSync = 1  
Const adcFetchAsynch = 3  
  
Sub ExecuteHow  
  ' set RDS properties at run-time  
  RDS1.ExecuteOptions = adcExecSync  
  RDS1.FetchOptions = adcFetchAsynch  
  RDS.Refresh  
End Sub  
</Script>  
</body>  
</html>  
<!-- EndExecuteOptionsRuntimeVBS -->  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ExecuteOptions-Eigenschaft (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)   
 [FetchOptions-Eigenschaft (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)



