---
title: "Verwalten der Befehlszeilenergänzung (SQL Server PowerShell) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 310aa99b485cedf79237f993a8ffbdcffe9d2a46
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="manage-tab-completion-sql-server-powershell"></a>Verwalten der Befehlszeilenergänzung (SQL Server PowerShell)
  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Snap-Ins führen drei Variablen (**$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems**und **$SqlServerIncludeSystemObjects**) zum Steuern der Windows PowerShell-Befehlszeilenergänzung ein. Die Befehlszeilenergänzung reduziert den Tippaufwand durch Zurückgeben von Tabellen mit Elementen, deren Namen mit der eingegebenen Zeichenfolge beginnen.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Wenn Sie die Windows PowerShell-Befehlszeilenergänzung verwenden und einen Teil eines Pfad- oder Cmdlet-Namens eingegeben haben, können Sie die TAB-TASTE drücken, um eine Liste der Elemente anzuzeigen, deren Namen mit dem bereits eingegebenen Teil übereinstimmen. Sie können dann das gewünschte Element aus der Liste auswählen, ohne den Rest des Namens eingeben zu müssen.  
  
 Wenn Sie in einer Datenbank arbeiten, die zahlreiche Objekte enthält, können die Listen der Befehlszeilenergänzung sehr umfangreich werden. Einige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekttypen, z. B. Sichten, verfügen außerdem über zahlreiche Systemobjekte.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Snap-Ins führen drei Systemvariablen ein, mit denen Sie die von der Befehlszeilenergänzung und **Get-ChildItem**bereitgestellte Informationsmenge steuern können.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 Gibt die maximale Anzahl der Objekte an, die in der Befehlszeilenergänzungsliste enthalten sein sollen. Wenn Sie die TAB-TASTE an einem Pfadknoten betätigen, der mehr als *n* Objekte aufweist, wird die Befehlszeilenergänzungs-Liste bei *n*abgeschnitten. *n* ist eine ganze Zahl. 0 ist die Standardeinstellung und bedeutet, dass die Anzahl der aufgeführten Objekte nicht begrenzt ist.  
  
 **$SqlServerMaximumChildItems =** *n*  
 Gibt die maximale Anzahl der von **Get-ChildItem**angezeigten Objekte an. Wenn Sie **Get-ChildItem** an einem Pfadknoten ausführen, der mehr als *n* Objekte aufweist, wird die Befehlszeilenergänzungs-Liste bei *n*abgeschnitten. *n* ist eine ganze Zahl. 0 ist die Standardeinstellung und bedeutet, dass die Anzahl der aufgeführten Objekte nicht begrenzt ist.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** | **$False** }  
 Wenn **$True**, werden Systemobjekte durch Befehlszeilenergänzung und **Get-ChildItem**angezeigt. Wenn **$False**, werden keine Systemobjekte angezeigt. Die Standardeinstellung ist **$False**.  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>Festlegen der Variablen für die SQL Server-Befehlszeilenergänzung  
 Legen Sie für die vom Standardwert zu ändernden Variablen einen neuen Wert fest.  
  
### <a name="example-powershell"></a>Beispiel (PowerShell)  
 Im folgenden Beispiel werden alle drei Variablen festgelegt und ihre Einstellungen aufgeführt:  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
