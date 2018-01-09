---
title: Verwenden von Synonymen | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
caps.latest.revision: "49"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf13a234a187b9da168cc77c26794131c8c32222
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="using-synonyms"></a>Verwenden von Synonymen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Ein Synonym ist ein alternativer Name für ein Objekt mit Schemabereich. In SMO werden Synonyme durch dargestellt die <xref:Microsoft.SqlServer.Management.Smo.Synonym> Objekt. Das <xref:Microsoft.SqlServer.Management.Smo.Synonym>-Objekt ist dem <xref:Microsoft.SqlServer.Management.Smo.Database>-Objekt untergeordnet. Dies bedeutet, dass Synonyme nur in dem Kontext der Datenbank gültig sind, in der sie definiert sind. Allerdings kann das Synonym auf Objekte auf einer anderen Datenbank oder auf einer Remoteinstanz von verweisen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Das Objekt, dem ein alternativer Name gegeben wird, wird als Basisobjekt bezeichnet. Die Name-Eigenschaft des <xref:Microsoft.SqlServer.Management.Smo.Synonym>-Objekts ist ein alternativer Name, der an das Basisobjekt vergeben wird.  
  
## <a name="example"></a>Beispiel  
 Für die folgenden Codebeispiele müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-synonym-in-visual-c"></a>Erstellen eines Synonyms in Visual C#  
 Dieses Codebeispiel zeigt, wie ein Synonym oder ein alternativer Name für ein Objekt mit Schemabereich erstellt wird. Clientanwendungen können einen einzelnen Verweis für das Basisobjekt über ein Synonym verwenden, anstatt einen mehrteiligen Namen zu verwenden, der auf das Basisobjekt verweist.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>Erstellen eines Synonyms in PowerShell  
 Dieses Codebeispiel zeigt, wie ein Synonym oder ein alternativer Name für ein Objekt mit Schemabereich erstellt wird. Clientanwendungen können einen einzelnen Verweis für das Basisobjekt über ein Synonym verwenden, anstatt einen mehrteiligen Namen zu verwenden, der auf das Basisobjekt verweist.  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym `  
-argumentlist $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../../t-sql/statements/create-synonym-transact-sql.md)  
  
  
