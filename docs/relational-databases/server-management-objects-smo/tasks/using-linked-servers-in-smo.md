---
title: Verwenden von Verbindungsservern in SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c864271d5ca3d9cfb4155f6b755493432d441110
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-linked-servers-in-smo"></a>Verwenden von Verbindungsservern in SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Ein Verbindungsserver stellt eine OLE DB-Datenquelle auf einem Remoteserver dar. Remote-OLE DB-Datenquellen verknüpft sind, mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe der <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> Objekt.  
  
 Remote-Datenbankserver können verknüpft werden, mit der aktuellen Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe eines OLE DB-Anbieters. In SMO werden Verbindungsserver durch dargestellt die <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> -Eigenschaft verweist auf eine Auflistung von <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> Objekte. Diese speichern die Anmeldeinformationen, die erforderlich sind, um eine Verbindung mit dem Verbindungsserver herzustellen.  
  
## <a name="ole-db-providers"></a>OLE DB-Anbieter  
 In SMO werden installierte OLE-DB-Anbieter durch eine Auflistung von <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings>-Objekten dargestellt.  
  
## <a name="example"></a>Beispiel  
 Für die folgenden Codebeispiele müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C&#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Erstellen eines Links zu einem OLE DB-Anbieterserver in Visual C#  
 Im Codebeispiel wird veranschaulicht, wie eine Verknüpfung zum Erstellen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, heterogene Datenquelle mithilfe der <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> Objekt. Durch Angabe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] der Datenzugriff erfolgt als Produktname, auf dem Verbindungsserver mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB-Anbieter, der der offizielle OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>Erstellen eines Links zu einem OLE DB-Anbieterserver in PowerShell  
 Im Codebeispiel wird veranschaulicht, wie eine Verknüpfung zum Erstellen einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB, heterogene Datenquelle mithilfe der <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> Objekt. Durch Angabe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] der Datenzugriff erfolgt als Produktname, auf dem Verbindungsserver mithilfe der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB-Anbieter, der der offizielle OLE DB-Anbieter für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
