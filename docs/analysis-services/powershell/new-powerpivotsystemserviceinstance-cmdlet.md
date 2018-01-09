---
title: New-PowerPivotSystemServiceInstance-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f2e412047e4d859de637da933d2335232961ee13
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="new-powerpivotsystemserviceinstance-cmdlet"></a>New-PowerPivotSystemServiceInstance-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Fügt eine neue Instanz der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst auf einem Anwendungsserver.  

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
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
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
  
  
