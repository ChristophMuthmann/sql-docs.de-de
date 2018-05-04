---
title: New-PowerPivotSystemServiceInstance-Cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b5d24b48d2c7b68f7408b5a3ad1da224cc992c3e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-powerpivotsystemserviceinstance-cmdlet"></a>New-PowerPivotSystemServiceInstance-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Fügt einem Anwendungsserver eine neue Instanz des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts hinzu.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das New-PowerPivotSystemServiceInstance-Cmdlet stellt ein neues PowerPivotSystemService-Objekt auf der Farmebene bereit, nachdem Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint mithilfe des SQL Server-Setups auf dem lokalen Anwendungsserver installiert haben. Sie können auf jedem Anwendungsserver nur eine Dienstinstanz bereitstellen.  Wenn der Dienst bereits bereitgestellt wurde, können Sie dieses Cmdlet nicht ausführen.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-parentservice-powerpivotmidtierservicepipebind"></a>-ParentService \<PowerPivotMidTierServicePipeBind >  
 Gibt die GUID des übergeordneten Objekts für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst in der Farm an. Unter dieser Version ist nur ein übergeordnetes Objekt zulässig. Sie können Get-PowerPivotSystemService verwenden, um das Dienstobjekt oder seine GUID zurückgeben.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|true|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-systemserviceinstancename-string"></a>-SystemServiceInstanceName \<Zeichenfolge >  
 Gibt einen Namen an, der dieses Objekt identifiziert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="provision-switchparameter"></a>Bereitstellen [\<Switch-Parameter >]  
 Macht den Dienst unter SharePoint verfügbar. Gültige Werte sind $true oder $false.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## <a name="example-1"></a>Beispiel 1  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 In diesem Beispiel wird die am häufigsten verwendete Form des Cmdlets veranschaulicht. Das Cmdlet registriert den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst auf dem lokalen Anwendungsserver für die Farm.  
  
## <a name="example-2"></a>Beispiel 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 In diesem Beispiel wird die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienstinstanz benannt, aber nicht bereitgestellt. Wenn Sie keinen Namen angeben, wird stattdessen der Standardname Instanz des SQL Server Analysis Services-Systemdiensts verwendet. Das Erstellen eines benutzerdefinierten Namens für den Dienst ist optional. Sie können den Dienst z. B. benennen, um Testszenarien zu unterstützen, oder wenn Sie über ein benutzerdefiniertes Tool oder ein Skript verfügen, mit dem die Instanz in einem späteren Schritt bereitgestellt wird.  
  
  
