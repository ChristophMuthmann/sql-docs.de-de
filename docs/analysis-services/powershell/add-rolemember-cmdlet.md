---
title: Add-RoleMember-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d10c7c9db41ec9e6f6f6e779b12e62f62e3b3b36
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="add-rolemember-cmdlet"></a>Add-RoleMember-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Fügen Sie der angegebenen Rolle einer Analysis Services-Tabelle oder einer multidimensionalen Datenbank ein Element hinzu.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Das Add-RoleMember-Cmdlet fügt einer vorhandenen Datenbankrolle ein gültiges Mitglied hinzu. Nur Datenbankrollen sind zulässig. Sie können dieses Cmdlet nicht verwenden, um einer Serverrolle Mitglieder hinzuzufügen.  
  
 Sie können jeweils nur ein Mitglied hinzufügen, das entweder ein Benutzer- oder ein Gruppenkonto sein kann.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-membername-string"></a>-MemberName \<Zeichenfolge >  
 Gibt den Windows-Benutzer oder die Windows-Gruppe an, der bzw. die der Rolle hinzugefügt werden soll.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-database-string"></a>-Datenbank \<Zeichenfolge >  
 Gibt die Datenbank an, zu der die Rolle gehört.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-rolename-string"></a>-RoleName \<Zeichenfolge >  
 Gibt die Rolle an, der Sie Mitglieder hinzufügen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databaserole-string"></a>DatabaseRole - \<Zeichenfolge >  
 Gibt das Microsoft.AnalysisServices.Role-Objekt an, dem das Mitglied hinzugefügt werden soll. Verwenden Sie diesen Parameter als Alternative zum –Database-Parameter und dem –RoleName-Parameter, wenn Sie die Datenbankrolle über Pipeline zur Verfügung stellen möchten.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true (ByPropertyName)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|InclusionThresholdSetting|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Dieser Befehl fügt der Leserrolle für die AdventureWorks-Datenbank, die auf einer lokalen Standardinstanz ausgeführt wird, ein Windows-Domänenbenutzerkonto hinzu.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 Zeile 1 fügt der Pipeline alle Datenbankrollen der AWTEST-Datenbank hinzu. In Zeile 2, in die Sie "$roles" an der Eingabeaufforderung eingeben, wird das Rollen-Array angezeigt. Zeile 3 fügt den Windows-Benutzer "adventure-works\bobh" als Mitglied der ersten Rolle im Array hinzu.  
  
## <a name="example-3"></a>Beispiel 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 Dieser Befehl fügt der ersten Rolle in einem Array ein Windows-Domänenbenutzerkonto hinzu. Dabei wird das Array durch Auflisten der untergeordneten Elemente des Ordners "Roles" im Kontext einer bestimmten Datenbank (AWTEST) erstellt.  
  

  
  
