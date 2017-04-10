---
title: "Aufrufen der SQL Server PowerShell-Hilfe | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Hilfe [PowerShell]"
  - "Hilfe [SQL Server], PowerShell"
  - "PowerShell [SQL Server], Hilfe"
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Aufrufen der SQL Server PowerShell-Hilfe
  Es stehen mehrere Informationsquellen zur Verwendung des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anbieters für Windows PowerShell und Cmdlets zur Verfügung. Dazu gehört auch die Hilfe, die in der Windows PowerShell-Umgebung verfügbar ist.  
  
## Vorbereitungen  
 Informationen zu Windows PowerShell finden Sie unter [Erste Schritte mit Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=217083).  
  
 Eine Übersicht über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Cmdlets und -Anbieter finden Sie unter [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
### Hilfe in der Windows PowerShell-Umgebung  
 Verwenden Sie das Cmdlet **Get-Help**, um Hilfe in der Windows PowerShell-Umgebung aufzurufen. **Get-Help** stellt grundlegende Hilfe zur Windows PowerShell-Sprache und den verschiedenen in Windows PowerShell verfügbaren Cmdlets und Anbietern bereit.  
  
 Weitere Informationen zur Verwendung von **Get-Help** finden Sie unter [Abrufen von Hilfeinformationen: Get-Help](http://go.microsoft.com/fwlink/?LinkId=102136).  
  
### SQL Server PowerShell-Anbieterhilfe  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Anbieter implementiert mehrere Ordner auf einem virtuellen SQLSERVER-Laufwerk, z. B. die Ordner SQLSERVER:\SQL und SQLSERVER:\DAC. Jeder Ordner ist einem der SQL Server-Verwaltbarkeitsobjektmodelle zugeordnet. Während Sie die jedem Knoten zugeordneten Methoden und Eigenschaften in einem SQL Server-Pfad auflisten können, können Sie dafür keine Hilfe in der PowerShell-Umgebung abrufen. Eine Tabelle mit den Ordnern mit Links zur zugeordneten Referenzdokumentation zur Programmierung finden Sie unter [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md).  
  
### Invoke-Sqlcmd-Hilfe  
 Das Cmdlet **Invoke-Sqlcmd** akzeptiert alle Abfragen oder Skriptdateien als Eingabe, die vom **sqlcmd**-Hilfsprogramm ausgeführt werden können. Sie können mit **Get-Help** Informationen zu **Invoke-Sqlcmd** und den zugehörigen Parametern abrufen. **Get-Help** kann jedoch nicht für die **sqlcmd**-Abfragen verwendet werden.  
  
 Die Eingaben *-Query* oder *-QueryFromFile* können Folgendes enthalten:  
  
-   **sqlcmd**-Variablen und -Befehle. Informationen zu diesen Variablen und Befehlen finden Sie unter [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md) im Abschnitt „Hinweise“.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen verwendet werden. Weitere Informationen über die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sprache finden Sie unter [Transact-SQL-Referenz &#40;Datenbankmodul&#41;](../../t-sql/transact-sql-reference-database-engine.md).  
  
-   XQuery-Anweisungen. Weitere Informationen zu der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützten XQuery-Sprache finden Sie unter [XQuery-Sprachreferenz &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md).  
  
## Aufrufen von Hilfe für ein SQL Server-Cmdlet  
 **So rufen Sie Hilfe für ein Cmdlet auf**  
  
-   Führen Sie "Get-Help" aus, und geben Sie dabei den Namen des Cmdlet und die Ebene der Hilfe an, die zurückgegeben werden soll.  
  
### Beispiel: Cmdlet Get-Help  
 In den folgenden Beispielen werden verschiedene Ebenen der Hilfe für **Invoke-Sqlcmd** zurückgegeben:  
  
```  
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd –Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd –Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd –Syntax  
```  
  
## Abrufen einer Liste von Anbietern  
 **So rufen Sie eine Liste aktiver Anbieter ab**  
  
1.  Führen Sie "Get-Help" aus, und geben Sie dabei die Anbieterkategorie an.  
  
 Weitere Informationen darüber, wie Sie in Windows PowerShell Hilfe zu den Anbietern erhalten können, finden Sie unter [Laufwerke und Anbieter](http://go.microsoft.com/fwlink/?LinkId=102137).  
  
### Beispiel: Abrufen einer Liste von Anbietern  
 Mit diesem Code wird eine Liste der Anbieter, die gerade in der Windows PowerShell-Sitzung aktiviert sind, zurückgegeben:  
  
```  
Get-Help -Category provider  
```  
  
## Aufrufen von Hilfe zum SQL Server-Anbieter  
 **So rufen Sie Hilfe zum Anbieter auf**  
  
1.  Ausführen von "Get-Help" mit Angabe des Namens "SQLServer"  
  
### Beispiel: Aufrufen von Hilfe zum SQL Server-Anbieter  
 In diesem Beispiel werden grundlegende Informationen zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anbieter zurückgegeben:  
  
```  
Get-Help SQLServer  
```  
  
## Auflisten von Methoden und Eigenschaften  
 **So listen Sie die Methoden und die Eigenschaften für einen Knoten in einem SQL Server-Anbieterpfad auf**  
  
1.  Verweisen Sie mit CD auf einen Knoten im SQL Server-Pfad, oder erstellen Sie einen Variablensatz zu diesem Speicherort.  
  
2.  Ausführen des **Get-Member**-Cmdlets, wobei der –Type-Parameter auf „Methoden“ oder „Eigenschaften“ festgelegt ist  
  
### Beispiele: Auflisten von Methoden und Eigenschaften  
 In diesem Beispiel sind die für den Datenbankknoten unterstützten Methoden aufgeführt:  
  
```  
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 In diesem Beispiel werden die Eigenschaften für eine Variable aufgelistet, die auf ein SMO-Tabellenobjekt festgelegt wurde:  
  
```  
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## Siehe auch  
 [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Verwenden der Datenbankmodul-Cmdlets](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
  
  