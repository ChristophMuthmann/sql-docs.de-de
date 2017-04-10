---
title: "Invoke-PolicyEvaluation-Cmdlet | Microsoft Docs"
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
  - "Richtlinienbasierte Verwaltung, Invoke-PolicyEvaluation"
  - "Richtlinienbasierte Verwaltung, PowerShell"
  - "Invoke-PolicyEvaluation-Cmdlet"
  - "Cmdlets [SQL Server], Invoke-PolicyEvaluation"
  - "PowerShell [SQL Server], Invoke-PolicyEvaluation"
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# Invoke-PolicyEvaluation-Cmdlet
  **Invoke_PolicyEvaluation** ist ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Cmdlet, das meldet, ob ein Zielsatz von SQL Server-Objekten den Bedingungen entspricht, die in ein oder mehreren richtlinienbasierten Verwaltungsrichtlinien angegeben sind.  
  
## Verwenden von Invoke-PolicyEvaluation  
 **Invoke-PolicyEvaluation** wertet ein oder mehrere Richtlinien für einen Satz von SQL Server-Objekten aus, der Zielsatz genannt wird. Der Satz von Zielobjekten stammt von einem Zielserver. Jede Richtlinie definiert Bedingungen, die die zulässigen Zustände für die Zielobjekte angeben. Beispielsweise legt die Richtlinie **Vertrauenswürdige Datenbank** fest, dass die Datenbankeigenschaft TRUSTWORTHY auf OFF festgelegt werden muss.  
  
 Der Parameter **-AdHocPolicyEvaluationMode** gibt die Aktionen an:  
  
 Check  
 Berichtet den Kompatibilitätsstatus der Zielobjekte unter Verwendung der Anmeldeinformationen Ihres aktuellen Anmeldenamens. Führt keine Neukonfiguration von Objekten aus. Dies ist die Standardeinstellung.  
  
 CheckSqlScriptAsProxy  
 Meldet den Kompatibilitätsstatus der Zielobjekte unter Verwendung der Anmeldeinformationen des Proxyanmeldenamens **##MS_PolicyTSQLExecutionLogin##**. Führt keine Neukonfiguration von Objekten aus.  
  
 Konfigurieren  
 Berichtet den Kompatibilitätsstatus der Zielobjekte unter Verwendung der Anmeldeinformationen Ihres aktuellen Anmeldenamens. Konfiguriert alle festlegbaren und deterministischen Optionen neu, die nicht in Übereinstimmung mit den Richtlinien sind.  
  
## Angeben von Richtlinien  
 Wie Sie eine Richtlinie angeben, hängt davon ab, wo die Richtlinie gespeichert ist. Richtlinien können in zwei Formaten gespeichert werden:  
  
-   Sie können als Objekte in einem Richtlinienspeicher gespeichert sein, wie z. B. eine Instanz des Datenbankmoduls. Sie können den Ordner SQLSERVER:\SQLPolicy verwenden, um den Speicherort von Richtlinien in einem Richtlinienspeicher anzugeben. Sie können Windows PowerShell-Cmdlets verwenden, um die Eingaberichtlinien basierend auf ihren Eigenschaften zu filtern. Beispielsweise können Sie Where-Object verwenden, um nach der Richtlinienkategorie zu filtern, oder Get-Item, um nach dem Richtliniennamen zu filtern.  
  
-   Sie können als XML-Dateien exportiert werden. Sie können ein Dateisystemlaufwerk verwenden, wie z. B. D:, um den Speicherort der XML-Dateien anzugeben. Sie können Windows PowerShell-Cmdlets verwenden, wie z. B. Where-Object, um die Richtlinien nach ihren Dateieigenschaften zu filtern, wie z. B. nach dem Dateinamen.  
  
 Wenn die Richtlinien in einem Richtlinienspeicher gespeichert sind, müssen Sie einen Satz von PSObjects übergeben, der auf die auszuwertenden Richtlinien zeigt. Hierzu wird in der Regel die Ausgabe eines Cmdlets, wie z.B. Get-Item, an **Invoke-PolicyEvaluation** weitergeleitet. Es ist nicht erforderlich, dass Sie den Parameter **-Policy** angeben. Wenn Sie beispielsweise die Microsoft Best Practices-Richtlinien in Ihre Instanz des Datenbankmoduls importiert haben, wertet dieser Befehl die Richtlinie **Datenbankstatus** aus:  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 Dieses Beispiel zeigt, wie mit „Where-Object“ mehrere Richtlinien basierend auf ihrer **PolicyCategory**-Eigenschaft aus einem Richtlinienspeicher gefiltert werden. Die Objekte aus der weitergereichten Ausgabe von **Where-Object** werden von **Invoke-PolicyEvaluation** genutzt.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 Wenn die Richtlinien als XML-Dateien gespeichert werden, müssen Sie den **-Policy**-Parameter verwenden, um für jede Richtlinie den Pfad und den Namen bereitzustellen. Wenn Sie keinen Pfad im Parameter **-Policy** angeben, verwendet **Invoke-PolicyEvaluation** die aktuelle Einstellung des **sqlps**-Pfads. Beispielsweise wertet dieser Befehl eine der Microsoft Best Practice-Richtlinien, die mit SQL Server installiert wurden, anhand der Standarddatenbank für Ihren Anmeldenamen aus:  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Dieser Befehl bewirkt dasselbe, verwendet jedoch den aktuellen **sqlps** -Pfad, um den Speicherort der XML-Richtliniendatei einzurichten:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Dieses Beispiel zeigt die Verwendung des Cmdlets **PolicyCategory**, um mehrere XML-Richtliniendateien abzurufen und die Objekte an **Invoke-PolicyEvaluation** weiterzureichen:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## Angeben des Zielsatzes  
 Mithilfe von drei Parametern können Sie den Satz der Zielobjekte angeben:  
  
-   **-TargetServerName** gibt die Instanz von SQL Server an, die die Zielobjekte enthält. Sie können die Informationen in einer Zeichenfolge angeben, die das für die ConnectionString-Eigenschaft der <xref:System.Data.SqlClient.SQLConnection> -Klasse definierte Format verwendet. Sie können die <xref:System.Data.SqlClient.SqlConnectionStringBuilder>-Klasse verwenden, um eine ordnungsgemäß formatierte Verbindungszeichenfolge zu erstellen. Sie können auch ein <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection>-Objekt erstellen und an **-TargetServer** übergeben. Wenn Sie eine Zeichenfolge angeben, die nur den Namen des Servers enthält, verwendet **Invoke-PolicyEvaluation** die Windows-Authentifizierung, um eine Verbindung mit dem Server herzustellen.  
  
-   **-TargetObjects** nimmt ein Objekt oder ein Array von Objekten entgegen, das die SQL Server-Objekte im Zielsatz darstellt. Beispielsweise könnten Sie ein Array von <xref:Microsoft.SqlServer.Management.Smo.Database>-Klassenobjekten erstellen, um es an **-TargetObjects** zu übergeben.  
  
-   **-TargetExpressions** nimmt eine Zeichenfolge mit einem Abfrageausdruck entgegen, der die Objekte im Zielsatz angibt. Der Abfrageausdruck liegt in Form von Knoten vor, die durch das Zeichen '/' getrennt sind. Jeder Knoten hat das Format ObjectType [Filter]. ObjectType ist eines der Objekte in einer SMO-Objekthierarchie (SQL Server Management Object). "Filter" ist ein Ausdruck, der bei diesem Knoten nach Objekten filtert. Weitere Informationen finden Sie unter [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
 Geben Sie entweder **-TargetObjects** oder **-TargetExpression**, aber nicht beides an.  
  
 In diesem Beispiel wird ein Sfc.SqlStoreConnection-Objekt verwendet, um den Zielserver anzugeben:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 In diesem Beispiel wird **-TargetExpression** verwendet, um eine bestimmte auszuwertende Datenbank anzugeben:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## Auswerten von Analysis Services-Richtlinien  
 Um Richtlinien anhand einer Instanz von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] auszuwerten, müssen Sie eine Assembly in PowerShell laden und registrieren, eine Variable mit einem Analysis Services-Verbindungsobjekt erstellen und die Variable an den Parameter **-TargetObject** übergeben. Dieses Beispiel zeigt das Auswerten der Best Practices-Oberflächenkonfigurationsrichtlinie für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## Auswerten von Reporting Services-Richtlinien  
 Um [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Richtlinien auszuwerten, müssen Sie eine Assembly in PowerShell laden und registrieren, eine Variable mit einem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Verbindungsobjekt erstellen und die Variable an den Parameter **-TargetObject** übergeben. Dieses Beispiel zeigt das Auswerten der Best Practices-Oberflächenkonfigurationsrichtlinie für [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## Formatieren der Ausgabe  
 Standardmäßig wird die Ausgabe von **Invoke-PolicyEvaluation** im Eingabeaufforderungsfenster als Kurzbericht in Klartextform angezeigt. Sie können den Parameter **-OutputXML** verwenden, um festzulegen, dass das Cmdlet stattdessen einen detaillierten Bericht als XML-Datei erstellt. **Invoke-PolicyEvaluation** verwendet das SML-IF-Schema (Systems Modeling Language Interchange Format), sodass die Datei von SML-IF-Readern gelesen werden kann.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## Siehe auch  
 [Verwenden der Datenbankmodul-Cmdlets](../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
  
  