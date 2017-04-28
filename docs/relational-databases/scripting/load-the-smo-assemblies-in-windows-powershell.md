---
title: Laden der SMO-Assemblys in Windows PowerShell | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 149ba0be18c46dbf2171f7a1fac0641ae81d3515
ms.lasthandoff: 04/11/2017

---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>Laden der SMO-Assemblys in Windows PowerShell
  In diesem Thema wird beschrieben, wie die SQL Server Management Object-Assemblys (SMO) in Windows PowerShell-Skripts geladen werden, die nicht den SQL Server PowerShell-Anbieter verwenden.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Der bevorzugte Mechanismus zum Laden der SMO-Assemblys besteht im Laden des **sqlps** -Moduls. Der im Modul enthaltene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieter lädt die SMO-Assemblys automatisch und implementiert außerdem Funktionen, die die Nützlichkeit der SMO-Objekte in PowerShell-Skripts erweitern.  Weitere Informationen finden Sie unter [Importieren des SQLPS-Moduls](../../relational-databases/scripting/import-the-sqlps-module.md).
  
 In zwei Szenarien müssen die SMO-Assemblys direkt geladen werden:  
  
-   Das Skript verweist vor dem ersten Befehl, der auf den Anbieter oder die Cmdlets der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Snap-Ins verweist, auf ein SMO-Objekt.  
  
-   Sie möchten SMO-Code portieren, der in einer anderen Sprache geschrieben wurde, die weder den Anbieter noch Cmdlets verwendet (z. B. C# oder Visual Basic).  
  
## <a name="example-loading-the-sql-server-management-objects"></a>Beispiel: Laden von SQL Server Management Objects  
 Mit folgendem Code werden die SMO-Assemblys geladen:  
  
```  
#  
# Loads the SQL Server Management Objects (SMO)  
#  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg="HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
update-FormatData -prependpath SQLProvider.Format.ps1xml   
Pop-Location  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
