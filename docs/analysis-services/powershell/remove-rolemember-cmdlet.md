---
title: Remove-RoleMember-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c093787d86398acaaeaca8f282e1f588c3e726d7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="remove-rolemember-cmdlet"></a>Remove-RoleMember-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Entfernt ein Mitglied aus der angegebenen Rolle einer Analysis Services-Datenbank.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
## <a name="syntax"></a>Syntax  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Das Remove-RoleMember-Cmdlet entfernt ein vorhandenes Mitglied aus einer Rolle einer Analysis Services-Datenbank.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-membername-string"></a>-MemberName \<Zeichenfolge >  
 Gibt den Windows-Benutzer oder die Windows-Gruppe an, der bzw. die aus der Rolle entfernt werden soll.  
  
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
 Gibt die Rolle an, aus der Sie Mitglieder entfernen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databaserole-string"></a>DatabaseRole - \<Zeichenfolge >  
 Gibt das Microsoft.AnalysisServices.Role-Objekt an, aus dem das Mitglied entfernt wird. Verwenden Sie diesen Parameter als Alternative zum –Database-Parameter und dem –RoleName-Parameter, wenn Sie die Datenbankrolle über Pipeline zur Verfügung stellen möchten.  
  
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
 Keine.  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Dieser Befehl entfernt aus der Leserrolle für die AdventureWorks-Datenbank, die auf einer lokalen Standardinstanz ausgeführt wird, ein Windows-Domänenbenutzerkonto.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 Zeile 1 fügt der Pipeline alle Datenbankrollen der AWTEST-Datenbank hinzu. In Zeile 2, in die Sie "$roles" an der Eingabeaufforderung eingeben, wird das Rollen-Array angezeigt. Zeile 3 entfernt den Windows-Benutzer "adventure-works\bobh-adventure-works\bobh" aus der ersten Rolle im Array.  
  
## <a name="example-3"></a>Beispiel 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 Dieser Befehl entfernt aus der ersten Rolle in einem Array ein Windows-Domänenbenutzerkonto. Dabei wird das Array durch Auflisten der untergeordneten Elemente des Ordners "Roles" im Kontext einer bestimmten Datenbank (AWTEST) erstellt.  
  

  
  

