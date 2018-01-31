---
title: "Programmgesteuertes Laden und Ausführen eines Remotepakets | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- remote packages [Integration Services]
ms.assetid: 9f6ef376-3408-46bf-b5fa-fc7b18c689c9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1d8a6fabc3b3b8ca1267160c716263b6366e5dcf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="loading-and-running-a-remote-package-programmatically"></a>Programmgesteuertes Laden und Ausführen eines Remotepakets
  Um Remotepakete auf einem lokalen Computer auszuführen, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nicht installiert ist, starten Sie die Pakete, sodass sie auf dem Remotecomputer ausgeführt werden, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert ist. Hierzu muss auf dem lokalen Computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent, ein Webdienst oder eine Remotekomponente zum Starten der Pakete auf dem Remotecomputer verwendet werden. Wenn Sie versuchen, die Remotepakete direkt auf dem lokalen Computer zu starten, werden die Pakete geladen, und es wird versucht, die Pakete auf dem lokalen Computer auszuführen. Wenn [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nicht auf dem lokalen Computer installiert ist, werden die Pakete nicht ausgeführt.  
  
> [!NOTE]  
>  Sie können Pakete außerhalb von [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] nur auf Clientcomputern ausführen, auf denen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert ist, wobei die Bedingungen Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Lizenz möglicherweise die Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf weiteren Computern nicht zulässt. Bei [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] handelt es sich um eine Serverkomponente, die nicht an Clientcomputer weitergegeben werden darf.  
  
 Alternativ können Sie ein Remotepaket auch auf einem lokalen Computer ausführen, auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert ist. Weitere Informationen finden Sie unter [Programmgesteuertes Laden und Ausführen eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md).  
  
##  <a name="top"></a> Ausführen eines Remotepakets auf dem Remotecomputer  
 Wie bereits erwähnt, gibt es mehrere Möglichkeiten, ein Remotepaket auf einem Remoteserver auszuführen:  
  
-   [Verwenden von SQL Server-Agent zum programmgesteuerten Ausführen des Remotepakets](#agent)  
  
-   [Verwenden eines Webdiensts oder einer Remotekomponente zum programmgesteuerten Auszuführen eines Remotepakets](#service)  
  
 Nahezu alle in diesem Thema erläuterten Methoden zum Laden und Speichern von Paketen erfordern einen Verweis auf die **Microsoft.SqlServer.ManagedDTS**-Assembly. Eine Ausnahme stellt der in diesem Thema beschriebene ADO.NET-Ansatz dar, mit dem die gespeicherte Prozedur **sp_start_job** ausgeführt wird, die lediglich einen Verweis auf **System.Data** erfordert. Nachdem Sie den Verweis zur **Microsoft.SqlServer.ManagedDTS**-Assembly in einem neuen Projekt hinzugefügt haben, importieren Sie den <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace mit einer **using**- oder **Imports**-Anweisung.  
  
###  <a name="agent"></a> Verwenden von SQL Server-Agent zum programmgesteuerten Ausführen eines Remotepakets auf dem Server  
 Im folgenden Beispielcode wird die programmgesteuerte Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent zum Ausführen eines Remotepakets auf dem Server veranschaulicht. Im Codebeispiel wird die gespeicherte Systemprozedur **sp_start_job** aufgerufen, die einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Auftrag startet. Der Auftrag, den die Prozedur startet, hat den Namen `RunSSISPackage` und befindet sich auf dem Remotecomputer. Der `RunSSISPackage`-Auftrag führt das Paket auf dem Remotecomputer aus.  
  
> [!NOTE]  
>  Der Rückgabewert der gespeicherten Prozedur **sp_start_job** gibt an, ob die gespeicherte Prozedur den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Auftrag starten konnte. Der Rückgabewert gibt nicht an, ob beim Ausführen des Pakets ein Fehler aufgetreten ist.  
  
 Weitere Informationen zur Problembehandlung bei der Ausführung von Paketen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Aufträgen finden Sie im Microsoft-Artikel [Beim Aufrufen aus einem SQL Server-Agent-Auftragsschritt wird ein SSIS-Paket nicht ausgeführt ](http://support.microsoft.com/kb/918760).  
  
### <a name="sample-code"></a>Beispielcode  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
  
    Dim jobConnection As SqlConnection  
    Dim jobCommand As SqlCommand  
    Dim jobReturnValue As SqlParameter  
    Dim jobParameter As SqlParameter  
    Dim jobResult As Integer  
  
    jobConnection = New SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI")  
    jobCommand = New SqlCommand("sp_start_job", jobConnection)  
    jobCommand.CommandType = CommandType.StoredProcedure  
  
    jobReturnValue = New SqlParameter("@RETURN_VALUE", SqlDbType.Int)  
    jobReturnValue.Direction = ParameterDirection.ReturnValue  
    jobCommand.Parameters.Add(jobReturnValue)  
  
    jobParameter = New SqlParameter("@job_name", SqlDbType.VarChar)  
    jobParameter.Direction = ParameterDirection.Input  
    jobCommand.Parameters.Add(jobParameter)  
    jobParameter.Value = "RunSSISPackage"  
  
    jobConnection.Open()  
    jobCommand.ExecuteNonQuery()  
    jobResult = DirectCast(jobCommand.Parameters("@RETURN_VALUE").Value, Integer)  
    jobConnection.Close()  
  
    Select Case jobResult  
      Case 0  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.")  
      Case Else  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.")  
    End Select  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace LaunchSSISPackageAgent_CS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      SqlConnection jobConnection;  
      SqlCommand jobCommand;  
      SqlParameter jobReturnValue;  
      SqlParameter jobParameter;  
      int jobResult;  
  
      jobConnection = new SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI");  
      jobCommand = new SqlCommand("sp_start_job", jobConnection);  
      jobCommand.CommandType = CommandType.StoredProcedure;  
  
      jobReturnValue = new SqlParameter("@RETURN_VALUE", SqlDbType.Int);  
      jobReturnValue.Direction = ParameterDirection.ReturnValue;  
      jobCommand.Parameters.Add(jobReturnValue);  
  
      jobParameter = new SqlParameter("@job_name", SqlDbType.VarChar);  
      jobParameter.Direction = ParameterDirection.Input;  
      jobCommand.Parameters.Add(jobParameter);  
      jobParameter.Value = "RunSSISPackage";  
  
      jobConnection.Open();  
      jobCommand.ExecuteNonQuery();  
      jobResult = (Int32)jobCommand.Parameters["@RETURN_VALUE"].Value;  
      jobConnection.Close();  
  
      switch (jobResult)  
      {  
        case 0:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.");  
          break;  
        default:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.");  
          break;  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
###  <a name="service"></a> Verwenden eines Webdiensts oder einer Remotekomponente zum programmgesteuerten Auszuführen eines Remotepakets  
 Für die vorherige Lösung zum programmgesteuerten Ausführen von Paketen auf dem Server ist kein benutzerdefinierter Code auf dem Server erforderlich. Möglicherweise bevorzugen Sie jedoch eine Lösung, bei der Pakete ohne SQL Server-Agent ausgeführt werden. Im Folgenden wird ein Beispiel für einen Webdienst, der auf dem Server zum lokalen Starten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen erstellt werden kann, sowie für eine Testanwendung dargestellt, mit deren Hilfe der Webdienst von einem Clientcomputer aus aufgerufen werden kann. Wenn Sie anstelle eines Webdiensts lieber eine Remotekomponente erstellen, können Sie dieselbe Codelogik mit nur wenigen Änderungen für eine Remotekomponente verwenden. Für eine Remotekomponente sind jedoch möglicherweise umfangreichere Konfigurationsschritte erforderlich als für einen Webdienst.  
  
> [!IMPORTANT]  
>  Mit den Standardeinstellungen für die Authentifizierung und Autorisierung verfügt ein Webdienst im Allgemeinen nicht über die erforderlichen Berechtigungen für den Zugriff auf SQL Server oder das Dateisystem, um Pakete zu laden und auszuführen. Daher müssen Sie möglicherweise dem Webdienst die entsprechenden Berechtigungen zuweisen. Konfigurieren Sie hierzu die Einstellungen für die Authentifizierung und Autorisierung in der Datei **Web.config**, und weisen Sie die für Datenbank und Dateisystem erforderlichen Berechtigungen zu. Eine ausführliche Beschreibung von Berechtigungen für Webdienste, Datenbanken und Dateisysteme ist nicht Gegenstand dieses Themas.  
  
> [!IMPORTANT]  
>  Die Methoden der <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse zum Arbeiten mit dem SSIS-Paketspeicher unterstützen nur „.“, localhost oder den Namen des lokalen Servers. Sie können "(local)" nicht verwenden.  
  
### <a name="sample-code"></a>Beispielcode  
 In den folgenden Codebeispielen wird gezeigt, wie der Webdienst erstellt und getestet wird.  
  
#### <a name="creating-the-web-service"></a>Erstellen des Webdiensts  
 Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket kann direkt aus einer Datei, direkt aus SQL Server oder aus dem SSIS-Paketspeicher geladen werden, der die Paketspeicherung sowohl in SQL Server-Ordnern als auch in speziellen Dateisystemordnern verwaltet. Dieses Beispiel unterstützt alle verfügbaren Optionen mithilfe eines **Select Case**- oder eines **switch**-Konstrukts, damit die geeignete Syntax zum Starten des Pakets ausgewählt wird und die Eingabeargumente entsprechend verkettet werden können. Die LaunchPackage-Webdienstmethode gibt das Ergebnis der Paketausführung als ganze Zahl zurück und nicht als <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>-Wert, sodass Clientcomputers keinen Verweis auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Assemblys benötigen.  
  
###### <a name="to-create-a-web-service-to-run-packages-on-the-server-programmatically"></a>So erstellen Sie einen Webdienst zum programmgesteuerten Ausführen von Paketen auf dem Server  
  
1.  Öffnen Sie Visual Studio, und erstellen Sie in der gewünchsten Programmiersprache ein Webdienstprojekt. Im Beispielcode wird der Name "LaunchSSISPackageService" für das Projekt verwendet.  
  
2.  Fügen Sie einen Verweis auf **Microsoft.SqlServer.ManagedDTS** hinzu, und fügen Sie eine **Imports**- oder **using**-Anweisung zur Codedatei für den **Microsoft.SqlServer.Dts.Runtime**-Namespace hinzu.  
  
3.  Fügen Sie den Beispielcode für die LaunchPackage-Webdienstmethode in die Klasse ein. (Im Beispiel ist der gesamte Inhalt des Codefensters dargestellt.)  
  
4.  Erstellen und testen Sie den Webdienst. Stellen Sie hierzu eine Reihe gültiger Werte für die Eingabeargumente der LaunchPackage-Methode bereit, die auf ein vorhandenes Paket zeigen. Beispiel: Wenn package1.dtsx auf dem Server im Verzeichnis C:\My Packages gespeichert ist, übergeben Sie "file" als Wert von sourceType, "C:\My Packages" als Wert von sourceLocation und "package1" (ohne Erweiterung) als Wert von packageName.  
  
```vb  
Imports System.Web  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.IO  
  
<WebService(Namespace:="http://dtsue/")> _  
<WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _  
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _  
Public Class LaunchSSISPackageService  
  Inherits System.Web.Services.WebService  
  
  ' LaunchPackage Method Parameters:  
  ' 1. sourceType: file, sql, dts  
  ' 2. sourceLocation: file system folder, (none), logical folder  
  ' 3. packageName: for file system, ".dtsx" extension is appended  
  
  <WebMethod()> _  
  Public Function LaunchPackage( _  
    ByVal sourceType As String, _  
    ByVal sourceLocation As String, _  
    ByVal packageName As String) As Integer 'DTSExecResult  
  
    Dim packagePath As String  
    Dim myPackage As Package  
    Dim integrationServices As New Application  
  
    ' Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName)  
  
    Select Case sourceType  
      Case "file"  
        ' Package is stored as a file.  
        ' Add extension if not present.  
        If String.IsNullOrEmpty(Path.GetExtension(packagePath)) Then  
          packagePath = String.Concat(packagePath, ".dtsx")  
        End If  
        If File.Exists(packagePath) Then  
          myPackage = integrationServices.LoadPackage(packagePath, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid file location: " & packagePath)  
        End If  
      Case "sql"  
        ' Package is stored in MSDB.  
        ' Combine logical path and package name.  
        If integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty) Then  
          myPackage = integrationServices.LoadFromSqlServer( _  
            packageName, "(local)", String.Empty, String.Empty, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case "dts"  
        ' Package is managed by SSIS Package Store.  
        ' Default logical paths are File System and MSDB.  
        If integrationServices.ExistsOnDtsServer(packagePath, ".") Then  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case Else  
        Throw New ApplicationException( _  
          "Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.")  
    End Select  
  
    Return myPackage.Execute()  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.IO;  
  
[WebService(Namespace = "http://dtsue/")]  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
public class LaunchSSISPackageServiceCS : System.Web.Services.WebService  
{  
  public LaunchSSISPackageServiceCS()  
  {  
    }  
  
  // LaunchPackage Method Parameters:  
  // 1. sourceType: file, sql, dts  
  // 2. sourceLocation: file system folder, (none), logical folder  
  // 3. packageName: for file system, ".dtsx" extension is appended  
  
  [WebMethod]  
  public int LaunchPackage(string sourceType, string sourceLocation, string packageName)  
  {   
  
    string packagePath;  
    Package myPackage;  
    Application integrationServices = new Application();  
  
    // Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName);  
  
    switch(sourceType)  
    {  
      case "file":  
        // Package is stored as a file.  
        // Add extension if not present.  
        if (String.IsNullOrEmpty(Path.GetExtension(packagePath)))  
        {  
          packagePath = String.Concat(packagePath, ".dtsx");  
        }  
        if (File.Exists(packagePath))  
        {  
          myPackage = integrationServices.LoadPackage(packagePath, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid file location: "+packagePath);  
        }  
        break;  
      case "sql":  
        // Package is stored in MSDB.  
        // Combine logical path and package name.  
        if (integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty))  
        {  
          myPackage = integrationServices.LoadFromSqlServer(packageName, "(local)", String.Empty, String.Empty, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      case "dts":  
        // Package is managed by SSIS Package Store.  
        // Default logical paths are File System and MSDB.  
        if (integrationServices.ExistsOnDtsServer(packagePath, "."))  
        {  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      default:  
        throw new ApplicationException("Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.");  
    }  
  
    return (Int32)myPackage.Execute();  
  
  }  
  
}  
```  
  
#### <a name="testing-the-web-service"></a>Testen des Webdiensts  
 Im folgenden Beispiel für eine Konsolenanwendung wird der Webdienst zum Ausführen eines Pakets verwendet. Die LaunchPackage-Methode des Webdiensts gibt das Ergebnis der Paketausführung als ganze Zahl zurück und nicht als <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>-Wert, sodass Clientcomputers keinen Verweis auf [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Assemblys benötigen. Mit dem Beispiel wird zum Melden der Ausführungsergebnisse eine private Enumeration erstellt, deren Werte die <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>-Werte spiegeln.  
  
###### <a name="to-create-a-console-application-to-test-the-web-service"></a>So erstellen Sie eine Konsolenanwendung zum Testen des Webdiensts  
  
1.  Fügen Sie in Visual Studio mithilfe der gewünschten Programmiersprache eine neue Konsolenanwendung zu der Projektmappe hinzu, die das Webdienstprojekt enthält. Im Beispielcode wird der Name LaunchSSISPackageTest für das Projekt verwendet.  
  
2.  Legen Sie die neue Konsolenanwendung als Startprojekt in der Projektmappe fest.  
  
3.  Fügen Sie einen Webverweis für das Webdienstprojekt hinzu. Passen Sie ggf. die Variablendeklaration im Beispielscode für den Namen an, den Sie dem Webdienstproxyobjekt zuweisen.  
  
4.  Fügen Sie den Beispielcode für die Hauptroutine und die private Enumeration in den Code ein. (Im Beispiel ist der gesamte Inhalt des Codefensters dargestellt.)  
  
5.  Bearbeiten Sie die Codezeile, die die LaunchPackage-Methode aufruft, um eine Reihe gültiger Werte für die Eingabeargumente bereitzustellen, die auf ein vorhandenes Paket zeigen. Beispiel: Wenn package1.dtsx auf dem Server im Verzeichnis C:\My Packages gespeichert ist, übergeben Sie "file" als Wert von `sourceType`, "C:\My Packages" als Wert von `sourceLocation` und "package1" (ohne Erweiterung) als Wert von `packageName`.  
  
```vb  
Module LaunchSSISPackageTest  
  
  Sub Main()  
  
    Dim launchPackageService As New LaunchSSISPackageService.LaunchSSISPackageService  
    Dim packageResult As Integer  
  
    Try  
      packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage")  
    Catch ex As Exception  
      ' The type of exception returned by a Web service is:  
      '  System.Web.Services.Protocols.SoapException  
      Console.WriteLine("The following exception occurred: " & ex.Message)  
    End Try  
  
    Console.WriteLine(CType(packageResult, PackageExecutionResult).ToString)  
    Console.ReadKey()  
  
  End Sub  
  
  Private Enum PackageExecutionResult  
    PackageSucceeded  
    PackageFailed  
    PackageCompleted  
    PackageWasCancelled  
  End Enum  
  
End Module  
```  
  
```csharp  
using System;  
  
namespace LaunchSSISPackageSvcTestCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS launchPackageService = new LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS();  
      int packageResult = 0;  
  
      try  
      {  
        packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage");  
      }  
      catch (Exception ex)  
      {  
        // The type of exception returned by a Web service is:  
        //  System.Web.Services.Protocols.SoapException  
        Console.WriteLine("The following exception occurred: " + ex.Message);  
      }  
  
      Console.WriteLine(((PackageExecutionResult)packageResult).ToString());  
      Console.ReadKey();  
  
    }  
  
    private enum PackageExecutionResult  
    {  
      PackageSucceeded,  
      PackageFailed,  
      PackageCompleted,  
      PackageWasCancelled  
    };  
  
  }  
}  
```  
  
## <a name="external-resources"></a>Externe Ressourcen  
  
-   Video [Vorgehensweise: Automatisieren der SSIS-Paketausführung mit dem SQL Server-Agent (SQL Server-Video)](http://technet.microsoft.com/sqlserver/ff686764.aspx) auf technet.microsoft.com  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Grundlegendes zu den Unterschieden zwischen der lokalen und der Remoteausführung](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Programmgesteuertes Laden und Ausführen eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Laden der Ausgabe eines lokalen Pakets](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
