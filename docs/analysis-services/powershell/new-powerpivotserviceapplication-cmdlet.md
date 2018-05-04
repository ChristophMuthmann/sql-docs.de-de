---
title: New-PowerPivotServiceApplication-Cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e36e6b170a141c7611c5eb246fd999beee970bf8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="new-powerpivotserviceapplication-cmdlet"></a>New-PowerPivotServiceApplication-Cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Erstellt eine neue [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung.  

>[!NOTE] 
>In diesem Artikel möglicherweise veraltete Informationen und Beispiele enthalten. Verwenden Sie das Cmdlet "Get-Help", für die aktuelle.
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## <a name="syntax"></a>Syntax  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Mit dem New-PowerPivotServiceApplication-Cmdlet wird in der Farm eine neue [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung erstellt. Sie müssen mindestens eine Dienstanwendung definieren, und diese muss Mitglied der Standardproxy-Dienstgruppe sein. Optional können Sie zusätzliche Dienstanwendungen erstellen, wenn Sie Eigenschaften oder Konfigurationseinstellungen ändern müssen. Zusätzlichen Dienstanwendungen muss die Mitgliedschaft in benutzerdefinierten Dienstverbindungsgruppen zugewiesen werden. Nur eine einzige [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung kann Mitglied der Standardproxygruppe sein.  
  
 Eine neue Dienstanwendung wird unter Verwendung einer Standardkonfiguration erstellt. Verwenden Sie das Set-PowerPivotServiceApplication-Cmdlet, um die Konfigurationseigenschaften anzupassen.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-serviceapplicationname-string"></a>-ServiceApplicationName \<Zeichenfolge >  
 Legt den Anzeigenamen der Dienstanwendung fest.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databaseservername-string"></a>-Wert "DatabaseServerName" \<Zeichenfolge >  
 Gibt eine Instanz eines relationalen SQL Server-Datenbankmoduls an, auf der die Anwendungsdatenbank gehostet wird. Standardmäßig können Sie den Datenbankserver der Farm verwenden oder einen anderen Datenbankserver auswählen, für den Sie Rechte zum Erstellen von Datenbanken besitzen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-databasename-string"></a>DatabaseName - \<Zeichenfolge >  
 Gibt den Namen einer relationalen SQL Server-Datenbank an, in der Anwendungsdaten gespeichert werden. Es ist ratsam, der Anwendung einen aussagekräftigen Namen zu geben, damit ihr Zweck leicht erkennbar ist. Sie können eine neue Datenbank erstellen oder eine vorhandene [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungsdatenbank für die neue Anwendung angeben, die Sie erstellen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-addtodefaultproxygroup-switch"></a>-AddToDefaultProxyGroup \<wechseln >  
 Erstellt in der Standard-Dienstverbindungsgruppe eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstverbindung. Zuordnungen zwischen Webanwendungen und Dienstanwendungen werden von der Mitgliedschaft in dieser Gruppe bestimmt. Alle Webanwendungen, die die Standard-Dienstverbindungsgruppe abonnieren, können die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung verwenden, die Sie der Gruppe hinzufügen. Obwohl Sie in einer Farm mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen verwenden können, kann nur eine Dienstanwendung Mitglied der Standard-Dienstverbindungsgruppe sein.  
  
 Wenn Sie bereits eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung verwenden, die Mitglied der Standardproxygruppe ist, müssen Sie für die neu zu erstellende Anwendung AddToDefaultProxyGroup:$false festlegen. Sie müssen die neue Dienstanwendung einer benutzerdefinierten Dienstverbindungsgruppe hinzufügen.  Sie können zu diesem Zweck integrierte SharePoint-Cmdlets verwenden.  Get-SPServiceApplicationProxyGroup gibt die Liste der Dienstverbindungsgruppen zurück, die in der Farm definiert sind.  
  
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
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 In diesem Beispiel wird eine neue Dienstanwendung erstellt. Die Dienstanwendungsdatenbank wird auf einem Datenbankserver mit dem Namen AdvWorks-SRV01 erstellt, der als benannte [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Instanz installiert wurde. Dies ist eine gängige Konfiguration für viele [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installationen. Sie müssen für die SQL Server-Instanz über dbcreator-Berechtigungen verfügen, um die Datenbank erstellen zu können. Sie müssen db_owner für die SharePoint-Konfigurationsdatenbank sein. Da dies die erste [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in der Farm ist, muss sie Mitglied der Standardproxygruppe sein.  
  
  
