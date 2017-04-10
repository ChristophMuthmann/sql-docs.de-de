---
title: "Add-RoleMember-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Add-RoleMember-Cmdlet
  Fügen Sie der angegebenen Rolle einer Analysis Services-Tabelle oder einer multidimensionalen Datenbank ein Element hinzu.  
  
## Syntax  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## Description  
 Das Add-RoleMember-Cmdlet fügt einer vorhandenen Datenbankrolle ein gültiges Mitglied hinzu. Nur Datenbankrollen sind zulässig. Sie können dieses Cmdlet nicht verwenden, um einer Serverrolle Mitglieder hinzuzufügen.  
  
 Sie können jeweils nur ein Mitglied hinzufügen, das entweder ein Benutzer- oder ein Gruppenkonto sein kann.  
  
## Parameter  
  
### -MemberName \<string>  
 Gibt den Windows-Benutzer oder die Windows-Gruppe an, der bzw. die der Rolle hinzugefügt werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -Database \<string>  
 Gibt die Datenbank an, zu der die Rolle gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -RoleName \<string>  
 Gibt die Rolle an, der Sie Mitglieder hinzufügen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DatabaseRole \<string>  
 Gibt das Microsoft.AnalysisServices.Role-Objekt an, dem das Mitglied hinzugefügt werden soll. Verwenden Sie diesen Parameter als Alternative zum –Database-Parameter und dem –RoleName-Parameter, wenn Sie die Datenbankrolle über Pipeline zur Verfügung stellen möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true (ByPropertyName)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### \<CommonParameters>  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|InclusionThresholdSetting|  
  
## Beispiel 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Dieser Befehl fügt der Leserrolle für die AdventureWorks-Datenbank, die auf einer lokalen Standardinstanz ausgeführt wird, ein Windows-Domänenbenutzerkonto hinzu.  
  
## Beispiel 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 Zeile 1 fügt der Pipeline alle Datenbankrollen der AWTEST-Datenbank hinzu. In Zeile 2, in die Sie "$roles" an der Eingabeaufforderung eingeben, wird das Rollen-Array angezeigt. Zeile 3 fügt den Windows-Benutzer "adventure-works\bobh" als Mitglied der ersten Rolle im Array hinzu.  
  
## Beispiel 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 Dieser Befehl fügt der ersten Rolle in einem Array ein Windows-Domänenbenutzerkonto hinzu. Dabei wird das Array durch Auflisten der untergeordneten Elemente des Ordners "Roles" im Kontext einer bestimmten Datenbank (AWTEST) erstellt.  
  
## Siehe auch  
 [PowerShell-Skripts in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Verwalten von tabellarischen Modellen mit PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  