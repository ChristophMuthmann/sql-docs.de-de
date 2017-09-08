---
title: Update-PowerPivotSystemService-Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: a90f1158-68d3-4330-98c1-fb0f81e13328
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ac64af222158746d63530f236eeda8cb94f2260
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="update-powerpivotsystemservice-cmdlet"></a>Update-PowerPivotSystemService-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Aktualisiert das übergeordnete Objekt des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts in der Farm.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
Update-PowerPivotSystemService [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Das **Update-PowerPivotSystemService** -Cmdlet führt für das übergeordnete Objekt des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts sowie für zugehörige Instanzen und [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen in der Farm eine Reihe von Upgradeaktionen aus. Alle Dienste und Anwendungen der mittleren Ebene in einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung müssen auf der gleichen Funktionsebene ausgeführt werden. Dieses Cmdlet führt die Upgradeaktionen für alle diese Objekte aus.  
  
 Führen Sie dieses Cmdlet nach dem SQL Server-Setup aus, um eine neuere Version von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint zu installieren, oder wenn auf dem Server ein kumulatives Update ausgeführt wurde. Um festzustellen, ob ein Upgrade erforderlich ist, führen Sie `Get-PowerPivotSystemService` aus, um die **NeedsUpgrade** -Eigenschaft zu überprüfen. Wenn **NeedsUpgrade** den Wert „true“ hat, sollten Sie das Cmdlet ausführen, um die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Objekte der mittleren Ebene in der Farm zu aktualisieren.  
  
 Da eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Bereitstellung Datendienste der mittleren Ebene und Back-End-Datendienste umfasst, müssen Sie bei jeder Ausführung von **Update-PowerPivotSystemService** auch **Update-PowerPivotEngineService** ausführen, um sicherzustellen, dass beide Ebenen in der Farm die gleiche Version aufweisen.  
  
 Nach dem Upgrade kann kein Rollback zur vorherigen Version durchgeführt werden. Wenn Sie eine frühere Version wiederherstellen müssen, sollten Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aus der SharePoint-Farm entfernen und die Software erneut installieren. Wenn Sie überprüfen möchten, ob der Upgradevorgang erfolgreich war, führen Sie `Get-PowerPivotSystemService` aus, um die Versionsinformationen in den globalen Eigenschaften zu überprüfen und um sicherzustellen, dass **NeedsUpgrade** nicht mehr auf „true“ festgelegt ist.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-confirm-switch"></a>-Bestätigen Sie \<wechseln >  
 Fordert eine Bestätigung an, bevor der Befehl ausgeführt wird. Dieser Wert ist standardmäßig aktiviert. Geben Sie Confirm:$false für einen Befehl an, um die Bestätigungsantwort in einem Befehl zu umgehen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die folgenden Parameter:  
  
-   Ausführlich  
  
-   Debuggen  
  
-   ErrorAction  
  
-   ErrorVariable  
  
-   WarningAction  
  
-   WarningVariable  
  
-   OutBuffer  
  
-   OutVariable  
  
 Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
  
