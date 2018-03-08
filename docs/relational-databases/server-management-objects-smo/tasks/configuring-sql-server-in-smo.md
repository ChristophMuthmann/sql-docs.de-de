---
title: Konfigurieren von SQLServer in SMO | Microsoft Docs
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
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
caps.latest.revision: "42"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f64bb51a733898d89f4c1cd67c2615fce6266a69
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="configuring-sql-server-in-smo"></a>Konfigurieren von SQL Server in SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In SMO werden die <xref:Microsoft.SqlServer.Management.Smo.Information> -Objekt, das <xref:Microsoft.SqlServer.Management.Smo.Settings> -Objekt, der <xref:Microsoft.SqlServer.Management.Smo.UserOptions> -Objekt, und die <xref:Microsoft.SqlServer.Management.Smo.Configuration> Objekt enthalten, Einstellungen und Informationen für die Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verfügt über zahlreiche Eigenschaften, die das Verhalten der installierten Instanz beschreiben. Die Eigenschaften beschreiben die Startoptionen, die Serverstandardwerte, Dateien und Verzeichnisse, System- und Prozessorinformationen, Produkt und Versionen, Verbindungsinformationen, Speicheroptionen, Sprach- und Sortierungsauswahl und den Authentifizierungsmodus.  
  
## <a name="sql-server-configuration"></a>SQL Server-Konfiguration  
 Die <xref:Microsoft.SqlServer.Management.Smo.Information> -Objekteigenschaften enthalten Informationen über die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], z. B. Prozessor und Plattform.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.Settings> -Objekteigenschaften enthalten Informationen über die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Die Standard-Datenbankdatei und das Standardverzeichnis können zusätzlich zum Mailprofil und Serverkonto geändert werden. Diese Eigenschaften bleiben für die Dauer der Verbindung erhalten.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekteigenschaften enthalten Informationen über das aktuelle Verbindungsverhalten im Zusammenhang mit Arithmetik, ANSI-Standards und Transaktionen.  
  
 Es gibt auch einen Satz an Konfigurationsoptionen, die durch dargestellt wird die <xref:Microsoft.SqlServer.Management.Smo.Configuration> Objekt. Er enthält eine Eigenschaftengruppe, die die Optionen darstellt, die durch die gespeicherte Prozedur **sp_configure** geändert werden können. Optionen wie z. B. **Priority Boost**, **Recovery Interval** und **Network Packet Size**kontrollieren die Leistung der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Viele dieser Optionen können dynamisch geändert werden. In einigen Fällen allerdings wird zunächst der Wert konfiguriert und dann geändert, wenn die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] neu gestartet wird.  
  
 Es ist ein <xref:Microsoft.SqlServer.Management.Smo.Configuration> -Objekteigenschaft für jede Konfigurationsoption. Durch die Verwendung des <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>-Objekts können Sie die globale Konfigurationseinstellung ändern. Viele Eigenschaften verfügen über Maximal- und Minimalwerte, die auch als <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>-Eigenschaften gespeichert werden. Diese Eigenschaften erfordern die <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> Methode, um die Änderung zu übernehmen, mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Alle Konfigurationsoptionen im die <xref:Microsoft.SqlServer.Management.Smo.Configuration> -Objekt müssen vom Systemadministrator geändert werden.  
  
## <a name="examples"></a>Beispiele  
 Für die folgenden Codebeispiele müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>Ändern von SQL Server-Konfigurationsoptionen in Visual Basic  
 Im Codebeispiel wird gezeigt, wie eine Konfigurationsoption in Visual Basic .NET aktualisiert wird. Weiterhin ruft es Informationen über Maximal- und Minimalwerte für die angegebene Konfigurationsoption ab und stellt diese dar. Schließlich informiert das Programm den Benutzer, wenn die Änderung dynamisch vorgenommen wurde oder wenn sie, bis die Instanz von gespeichert wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] neu gestartet wird.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display all the configuration options.
Dim p As ConfigProperty
For Each p In srv.Configuration.Properties
    Console.WriteLine(p.DisplayName)
Next
Console.WriteLine("There are " & srv.Configuration.Properties.Count.ToString & " configuration options.")
'Display the maximum and minimum values for ShowAdvancedOptions.
Dim min As Integer
Dim max As Integer
min = srv.Configuration.ShowAdvancedOptions.Minimum
max = srv.Configuration.ShowAdvancedOptions.Maximum
Console.WriteLine("Minimum and Maximum values are " & min & " and " & max & ".")
'Modify the value of ShowAdvancedOptions and run the Alter method.
srv.Configuration.ShowAdvancedOptions.ConfigValue = 0
srv.Configuration.Alter()
'Display when the change takes place according to the IsDynamic property.
If srv.Configuration.ShowAdvancedOptions.IsDynamic = True Then
    Console.WriteLine("Configuration option has been updated.")
Else
    Console.WriteLine("Configuration option will be updated when SQL Server is restarted.")
End If
``` 
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>Ändern von SQL Server-Einstellungen in Visual Basic  
 Das Codebeispiel zeigt Informationen zu der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in <xref:Microsoft.SqlServer.Management.Smo.Information> und <xref:Microsoft.SqlServer.Management.Smo.Settings>, und ändert Einstellungen in <xref:Microsoft.SqlServer.Management.Smo.Settings> und <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekteigenschaften.  
  
 Im Beispiel verfügen sowohl das <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekt als auch das <xref:Microsoft.SqlServer.Management.Smo.Settings>-Objekt über eine <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>-Methode. Sie können Ausführen der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> -Methoden für diese einzeln.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display information about the instance of SQL Server in Information and Settings.
Console.WriteLine("OS Version = " & srv.Information.OSVersion)
Console.WriteLine("State = " & srv.Settings.State.ToString)
'Display information specific to the current user in UserOptions.
Console.WriteLine("Quoted Identifier support = " & srv.UserOptions.QuotedIdentifier)
'Modify server settings in Settings.

srv.Settings.LoginMode = ServerLoginMode.Integrated
'Modify settings specific to the current connection in UserOptions.
srv.UserOptions.AbortOnArithmeticErrors = True
'Run the Alter method to make the changes on the instance of SQL Server.
srv.Alter()
```
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>Ändern von SQL Server-Einstellungen in Visual C#  
 Das Codebeispiel zeigt Informationen zu der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in <xref:Microsoft.SqlServer.Management.Smo.Information> und <xref:Microsoft.SqlServer.Management.Smo.Settings>, und ändert Einstellungen in <xref:Microsoft.SqlServer.Management.Smo.Settings> und <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekteigenschaften.  
  
 Im Beispiel verfügen sowohl das <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekt als auch das <xref:Microsoft.SqlServer.Management.Smo.Settings>-Objekt über eine <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>-Methode. Sie können Ausführen der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> -Methoden für diese einzeln.  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```csharp  
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>Ändern von SQL Server-Einstellungen in PowerShell  
 Das Codebeispiel zeigt Informationen zu der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in <xref:Microsoft.SqlServer.Management.Smo.Information> und <xref:Microsoft.SqlServer.Management.Smo.Settings>, und ändert Einstellungen in <xref:Microsoft.SqlServer.Management.Smo.Settings> und <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekteigenschaften.  
  
 Im Beispiel verfügen sowohl das <xref:Microsoft.SqlServer.Management.Smo.UserOptions>-Objekt als auch das <xref:Microsoft.SqlServer.Management.Smo.Settings>-Objekt über eine <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>-Methode. Sie können Ausführen der <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> -Methoden für diese einzeln.  
  
```powershell 
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>Ändern von SQL Server-Konfigurationsoptionen in PowerShell  
 Im Codebeispiel wird gezeigt, wie eine Konfigurationsoption in Visual Basic .NET aktualisiert wird. Weiterhin ruft es Informationen über Maximal- und Minimalwerte für die angegebene Konfigurationsoption ab und stellt diese dar. Schließlich informiert das Programm den Benutzer, wenn die Änderung dynamisch vorgenommen wurde oder wenn sie, bis die Instanz von gespeichert wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] neu gestartet wird.  
  
```powershell 
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = get-item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {    
   "Configuration option has been updated."  
 }  
Else  
{  
    "Configuration option will be updated when SQL Server is restarted."  
}  
```  
  
  
