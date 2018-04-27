---
title: Programmgesteuertes Auflisten verfügbarer Pakete | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: run-manage-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programmatically enumerate packages [SSIS]
- existence testing [Integration Services]
- enumerating packages [Integration Services]
ms.assetid: 254ec7ee-d3ff-4361-8995-46e9b9c4dc95
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dc06d8d80ea5ef5034735f953491d38ee3ce903
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="enumerating-available-packages-programmatically"></a>Enumerating Available Packages Programmatically
  <a name="top"></a> Wenn Sie programmgesteuert mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen arbeiten, möchten Sie vielleicht bestimmen, ob ein einzelnes Paket oder ein einzelner Ordner vorhanden ist, oder die gespeicherten Pakete auflisten, die zum Laden und Ausführen verfügbar sind. Die <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse des <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace stellt eine Reihe von Methoden bereit, die diese Anforderungen erfüllen.    
    
##  <a name="exists"></a> Bestimmen, ob ein Paket oder ein Ordner vorhanden ist    
 Um programmgesteuert zu ermitteln, ob ein gespeichertes Paket vorhanden ist, rufen Sie eine der folgenden Methoden auf, bevor Sie versuchen, es zu laden und auszuführen:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Um programmgesteuert zu ermitteln, ob ein Ordner vorhanden ist, rufen Sie eine der folgenden Methoden auf, bevor Sie versuchen, die darin gespeicherten Pakete aufzulisten:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Zurück zum Anfang](#top)    
    
##  <a name="listing"></a> Auflisten verfügbarer Pakete    
 Rufen Sie eine der folgenden Methoden auf, um eine Liste von gespeicherten Paketen programmgesteuert abzurufen:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerPackageInfos%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageInfos%2A>|    
    
 Die folgenden Beispiele sind Konsolenanwendungen, die die Verwendung dieser Methoden veranschaulichen.    
    
###  <a name="listing_store"></a> Beispiel (SSIS-Paketspeicher)    
 Verwenden Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerPackageInfos%2A>-Methode, um im SSIS-Paketspeicher gespeicherte Pakete aufzulisten. Die Standardspeicherorte, die vom SSIS-Paketspeicher verwaltet werden, sind "Dateisystem" und "MSDB". Sie können zusätzliche logische Ordner innerhalb dieser Speicherorte erstellen.    
    
```vb    
Imports Microsoft.SqlServer.Dts.Runtime    
    
Module Module1    
    
  Sub Main()    
    
    Dim sqlFolder As String    
    Dim sqlServer As String    
    
    Dim ssisApplication As Application    
    Dim sqlPackages As PackageInfos    
    Dim sqlPackage As PackageInfo    
    
    sqlServer = "."    
    
    ssisApplication = New Application()    
    
    ' Get packages stored in MSDB.    
    sqlFolder = "MSDB"    
    sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer)    
    If sqlPackages.Count > 0 Then    
      Console.WriteLine("Packages stored in MSDB:")    
      For Each sqlPackage In sqlPackages    
        Console.WriteLine(sqlPackage.Name)    
      Next    
      Console.WriteLine()    
    End If    
    
    ' Get packages stored in the File System.    
    sqlFolder = "File System"    
    sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer)    
    If sqlPackages.Count > 0 Then    
      Console.WriteLine("Packages stored in the File System:")    
      For Each sqlPackage In sqlPackages    
        Console.WriteLine(sqlPackage.Name)    
      Next    
    End If    
    
    Console.Read()    
    
  End Sub    
    
End Module    
```    
    
```csharp    
using System;    
using Microsoft.SqlServer.Dts.Runtime;    
    
namespace EnumeratePackagesSSIS_CS    
{    
  class Program    
  {    
    static void Main(string[] args)    
    {    
    
      string sqlFolder;    
      string sqlServer;    
    
      Application ssisApplication;    
      PackageInfos sqlPackages;    
    
      sqlServer = ".";    
    
      ssisApplication = new Application();    
    
      // Get packages stored in MSDB.    
      sqlFolder = "MSDB";    
      sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer);    
      if (sqlPackages.Count > 0)    
      {    
        Console.WriteLine("Packages stored in MSDB:");    
        foreach (PackageInfo sqlPackage in sqlPackages)    
        {    
          Console.WriteLine(sqlPackage.Name);    
        }    
        Console.WriteLine();    
      }    
    
      // Get packages stored in the File System.    
      sqlFolder = "File System";    
      sqlPackages = ssisApplication.GetDtsServerPackageInfos(sqlFolder, sqlServer);    
      if (sqlPackages.Count > 0)    
      {    
        Console.WriteLine("Packages stored in the File System:");    
        foreach (PackageInfo sqlPackage in sqlPackages)    
        {    
          Console.WriteLine(sqlPackage.Name);    
        }    
      }    
    
      Console.Read();    
    
    }    
    
  }    
    
}    
```    
    
 [Zurück zum Anfang](#top)    
    
###  <a name="listing_sql"></a> Beispiel (SQL Server)    
 Verwenden Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageInfos%2A>-Methode, um [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Pakete aufzulisten, die in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert sind.    
    
```vb    
Imports Microsoft.SqlServer.Dts.Runtime    
    
Module Module1    
    
  Sub Main()    
    
    Dim sqlFolder As String    
    Dim sqlServer As String    
    Dim sqlUser As String    
    Dim sqlPassword As String    
    
    Dim ssisApplication As Application    
    Dim sqlPackages As PackageInfos    
    Dim sqlPackage As PackageInfo    
    
    sqlFolder = String.Empty    
    sqlServer = "(local)"    
    sqlUser = String.Empty    
    sqlPassword = String.Empty    
    
    ssisApplication = New Application()    
    
    sqlPackages = ssisApplication.GetPackageInfos(sqlFolder, sqlServer, sqlUser, sqlPassword)    
    
    For Each sqlPackage In sqlPackages    
      Console.WriteLine(sqlPackage.Name)    
    Next    
    
    Console.Read()    
    
  End Sub    
    
End Module    
```    
    
```csharp    
using System;    
using Microsoft.SqlServer.Dts.Runtime;    
    
namespace EnumeratePackagesSql_CS    
{    
  class Program    
  {    
    static void Main(string[] args)    
    {    
    
      string sqlFolder;    
      string sqlServer;    
      string sqlUser;    
      string sqlPassword;    
    
      Application ssisApplication;    
      PackageInfos sqlPackages;    
    
      sqlFolder = String.Empty;    
      sqlServer = "(local)";    
      sqlUser = String.Empty;    
      sqlPassword = String.Empty;    
    
      ssisApplication = new Application();    
    
      sqlPackages = ssisApplication.GetPackageInfos(sqlFolder, sqlServer, sqlUser, sqlPassword);    
    
      foreach (PackageInfo sqlPackage in sqlPackages)    
      {    
        Console.WriteLine(sqlPackage.Name);    
      }    
    
      Console.Read();    
    
    }    
  }    
}    
```    
    
 [Zurück zum Anfang](#top)    
   
## <a name="see-also"></a>Weitere Informationen finden Sie unter    
 [Paketverwaltung &#40;SSIS-Dienst&#41;](../../integration-services/service/package-management-ssis-service.md)    
    
  
