---
title: "New-PowerPivotServiceApplication-Cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 7bb2a2d2-04c8-43d4-a0fc-e8339ea22138
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# New-PowerPivotServiceApplication-Cmdlet
  Erstellt eine neue [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung.  
  
 **Gilt für:** SharePoint 2010 und SharePoint 2013.  
  
## Syntax  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## Description  
 Mit dem New-PowerPivotServiceApplication-Cmdlet wird in der Farm eine neue [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung erstellt. Sie müssen mindestens eine Dienstanwendung definieren, und diese muss Mitglied der Standardproxy-Dienstgruppe sein. Optional können Sie zusätzliche Dienstanwendungen erstellen, wenn Sie Eigenschaften oder Konfigurationseinstellungen ändern müssen. Zusätzlichen Dienstanwendungen muss die Mitgliedschaft in benutzerdefinierten Dienstverbindungsgruppen zugewiesen werden. Nur eine einzige [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung kann Mitglied der Standardproxygruppe sein.  
  
 Eine neue Dienstanwendung wird unter Verwendung einer Standardkonfiguration erstellt. Verwenden Sie das Set-PowerPivotServiceApplication-Cmdlet, um die Konfigurationseigenschaften anzupassen.  
  
## Parameter  
  
### -ServiceApplicationName \<string>  
 Legt den Anzeigenamen der Dienstanwendung fest.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|0|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DatabaseServerName \<string>  
 Gibt eine Instanz eines relationalen SQL Server-Datenbankmoduls an, auf der die Anwendungsdatenbank gehostet wird. Standardmäßig können Sie den Datenbankserver der Farm verwenden oder einen anderen Datenbankserver auswählen, für den Sie Rechte zum Erstellen von Datenbanken besitzen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|1|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -DatabaseName \<string>  
 Gibt den Namen einer relationalen SQL Server-Datenbank an, in der Anwendungsdaten gespeichert werden. Es ist ratsam, der Anwendung einen aussagekräftigen Namen zu geben, damit ihr Zweck leicht erkennbar ist. Sie können eine neue Datenbank erstellen oder eine vorhandene [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendungsdatenbank für die neue Anwendung angeben, die Sie erstellen.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|2|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### -AddToDefaultProxyGroup \<switch>  
 Erstellt in der Standard-Dienstverbindungsgruppe eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstverbindung. Zuordnungen zwischen Webanwendungen und Dienstanwendungen werden von der Mitgliedschaft in dieser Gruppe bestimmt. Alle Webanwendungen, die die Standard-Dienstverbindungsgruppe abonnieren, können die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung verwenden, die Sie der Gruppe hinzufügen. Obwohl Sie in einer Farm mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendungen verwenden können, kann nur eine Dienstanwendung Mitglied der Standard-Dienstverbindungsgruppe sein.  
  
 Wenn Sie bereits eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung verwenden, die Mitglied der Standardproxygruppe ist, müssen Sie für die neu zu erstellende Anwendung AddToDefaultProxyGroup:$false festlegen. Sie müssen die neue Dienstanwendung einer benutzerdefinierten Dienstverbindungsgruppe hinzufügen.  Sie können zu diesem Zweck integrierte SharePoint-Cmdlets verwenden.  Get-SPServiceApplicationProxyGroup gibt die Liste der Dienstverbindungsgruppen zurück, die in der Farm definiert sind.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### \<CommonParameters>  
 Dieses Cmdlet unterstützt die folgenden allgemeinen Parameter: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer und OutVariable. Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|Keine.|  
|Ausgaben|Keine.|  
  
## Beispiel 1  
  
```  
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 In diesem Beispiel wird eine neue Dienstanwendung erstellt. Die Dienstanwendungsdatenbank wird auf einem Datenbankserver mit dem Namen AdvWorks-SRV01 erstellt, der als benannte [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Instanz installiert wurde. Dies ist eine gängige Konfiguration für viele [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installationen. Sie müssen für die SQL Server-Instanz über dbcreator-Berechtigungen verfügen, um die Datenbank erstellen zu können. Sie müssen db_owner für die SharePoint-Konfigurationsdatenbank sein. Da dies die erste [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienstanwendung in der Farm ist, muss sie Mitglied der Standardproxygruppe sein.  
  
  