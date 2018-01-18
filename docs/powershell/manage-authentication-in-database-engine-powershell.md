---
title: Verwalten der Authentifizierung in PowerShell des Datenbankmoduls | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
caps.latest.revision: "9"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2693e570fd1db9a823cd602c871f699e14c06e6
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2018
---
# <a name="manage-authentication-in-database-engine-powershell"></a>Verwalten der Authentifizierung in PowerShell des Datenbankmoduls
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Standardmäßig wird von den [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell-Komponenten beim Herstellen einer Verbindung mit einer [!INCLUDE[ssDE](../includes/ssde-md.md)]-Instanz die Windows-Authentifizierung verwendet. Sie können die SQL Server-Authentifizierung verwenden, indem Sie entweder ein virtuelles PowerShell-Laufwerk definieren oder die Parameter **–Username** und **–Password** für **Invoke-Sqlcmd**angeben.  
  
> [!NOTE]
> Es gibt zwei SQL Server PowerShell-Module: **SqlServer** und **SQLPS**. Das **SQLPS**-Modul ist zwar in der SQL Server-Installation (für die Abwärtskompatibilität) enthalten, wird jedoch nicht mehr aktualisiert. Das **SqlServer**-Modul ist das aktuellste PowerShell-Modul. Das **SqlServer**-Modul enthält aktualisierte Versionen der Cmdlets in **SQLPS** sowie neue Cmdlets zur Unterstützung der neuesten SQL-Funktionen.  
> Vorherige Versionen des **SqlServer**-Moduls *waren* in SQL Server Management Studio (SSMS) enthalten, allerdings nur in den Versionen 16.x. Das **SqlServer**-Modul muss über den PowerShell-Katalog installiert werden, damit PowerShell mit SSMS 17.0 und höher verwendet werden kann.
> Informationen zur Installation des **SqlServer**-Moduls finden Sie unter [Installieren von SQL Server PowerShell](download-sql-server-ps-module.md).

  
##  <a name="Permissions"></a> Berechtigungen  
 Alle Aktionen, die Sie in einer [!INCLUDE[ssDE](../includes/ssde-md.md)] -Instanz ausführen können, werden über die Berechtigungen gesteuert, die den beim Verbinden mit der Instanz verwendeten Authentifizierungsinformationen erteilt wurden. Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anbieter und Cmdlets verwenden standardmäßig das Windows-Konto, unter dem sie ausgeführt werden, um eine Windows-Authentifizierungsverbindung mit [!INCLUDE[ssDE](../includes/ssde-md.md)]herzustellen.  
  
 Zum Herstellen einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierungsverbindung müssen Sie eine Anmelde-ID und ein Kennwort für die SQL Server-Authentifizierung angeben. Bei Verwendung des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anbieters müssen Sie die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anmeldeinformationen einem virtuellen Laufwerk zuordnen und anschließend mithilfe des Befehls zum Ändern des Verzeichnisses (**cd**) eine Verbindung mit diesem Laufwerk herstellen. In Windows PowerShell können Sicherheitsanmeldeinformationen nur virtuellen Laufwerken zugeordnet werden.  
  
##  <a name="SQLAuthVirtDrv"></a> SQL Server-Authentifizierung mit einem virtuellen Laufwerk  
 **So erstellen Sie ein virtuelles Laufwerk mit Zuordnung zu einer SQL Server-Authentifizierungsanmeldung**  
  
1.  Erstellen Sie eine Funktion, auf die Folgendes zutrifft:  
  
    1.  Sie verfügt über Parameter für den Namen, der dem virtuellen Laufwerk zugeordnet werden soll, für die Anmelde-ID und für den Anbieterpfad, der dem virtuellen Laufwerk zugeordnet werden soll.  
  
    2.  Sie verwendet **read-host** , um den Benutzer zur Eingabe des Kennworts aufzufordern.  
  
    3.  Sie verwendet **new-object** um ein Anmeldeinformationsobjekt zu erstellen.  
  
    4.  Sie verwendet **new-psdrive** , um ein virtuelles Laufwerk mit den angegebenen Anmeldeinformationen zu erstellen.  
  
2.  Rufen Sie die Funktion auf, um ein virtuelles Laufwerk mit den angegebenen Anmeldeinformationen zu erstellen.  
  
### <a name="example-virtual-drive"></a>Beispiel (virtuelles Laufwerk)  
 In diesem Beispiel wird eine Funktion mit dem Namen **sqldrive** erstellt, mit der Sie ein virtuelles Laufwerk erstellen können, das mit dem angegebenen Anmeldenamen für die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung und der angegebenen Instanz verknüpft ist.  
  
 Sie werden von der Funktion **sqldrive** zur Eingabe des Kennworts für Ihren Anmeldenamen aufgefordert. Das Kennwort wird bei der Eingabe maskiert. Wenn Sie anschließend den Befehl zum Ändern eines Verzeichnisses (**cd**) verwenden, um über den Namen des virtuellen Laufwerks eine Verbindung mit einem Pfad herzustellen, werden alle Vorgänge mithilfe der Anmeldeinformationen für die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Authentifizierung ausgeführt, die Sie beim Erstellen des Laufwerks angegeben haben.  
  
```  
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = read-host -AsSecureString -Prompt "Password"  
    $cred = new-object System.Management.Automation.PSCredential -argumentlist $login,$pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> SQL Server-Authentifizierung mit Invoke-Sqlcmd  
 **So verwenden Sie Invoke-Sqlcmd mit der SQL Server-Authentifizierung**  
  
1.  Verwenden Sie den **–Username** -Parameter, um eine Anmelde-ID anzugeben, und den **–Password** -Parameter, um das zugeordnete Kennwort anzugeben.  
  
### <a name="example-invoke-sqlcmd"></a>Beispiel (Invoke-Sqlcmd)  
 In diesem Beispiel wird das "read-host"-Cmdlet verwendet, um den Benutzer zur Eingabe des Kennworts aufzufordern, und dann unter Verwendung der SQL Server-Authentifizierung eine Verbindung hergestellt.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" –Username “MyLogin” –Password $pwd  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server-PowerShell](sql-server-powershell.md)   
 [SQL Server PowerShell-Anbieter](sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd-Cmdlet](invoke-sqlcmd-cmdlet.md)  
  
  
