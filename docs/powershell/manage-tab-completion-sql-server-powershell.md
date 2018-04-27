---
title: Verwalten der Befehlszeilenergänzung (SQL Server PowerShell) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7bae2c55184d9b4d23e325269e53080cda62209
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="manage-tab-completion-sql-server-powershell"></a>Verwalten der Befehlszeilenergänzung (SQL Server PowerShell)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


Die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell-Snap-Ins führen drei Variablen (**$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems**und **$SqlServerIncludeSystemObjects**) zum Steuern der Windows PowerShell-Befehlszeilenergänzung ein. Die Befehlszeilenergänzung reduziert den Tippaufwand durch Zurückgeben von Tabellen mit Elementen, deren Namen mit der eingegebenen Zeichenfolge beginnen.  

> [!NOTE]
> Es gibt zwei SQL Server PowerShell-Module: **SqlServer** und **SQLPS**. Das **SQLPS**-Modul ist zwar in der SQL Server-Installation (für die Abwärtskompatibilität) enthalten, wird jedoch nicht mehr aktualisiert. Das **SqlServer**-Modul ist das aktuellste PowerShell-Modul. Das **SqlServer**-Modul enthält aktualisierte Versionen der Cmdlets in **SQLPS** sowie neue Cmdlets zur Unterstützung der neuesten SQL-Funktionen.  
> Vorherige Versionen des **SqlServer**-Moduls *waren* in SQL Server Management Studio (SSMS) enthalten, allerdings nur in den Versionen 16.x. Das **SqlServer**-Modul muss über den PowerShell-Katalog installiert werden, damit PowerShell mit SSMS 17.0 und höher verwendet werden kann.
> Informationen zur Installation des **SqlServer**-Moduls finden Sie unter [Installieren von SQL Server PowerShell](download-sql-server-ps-module.md).
  
Wenn Sie die Windows PowerShell-Befehlszeilenergänzung verwenden und einen Teil eines Pfad- oder Cmdlet-Namens eingegeben haben, können Sie die TAB-TASTE drücken, um eine Liste der Elemente anzuzeigen, deren Namen mit dem bereits eingegebenen Teil übereinstimmen. Sie können dann das gewünschte Element aus der Liste auswählen, ohne den Rest des Namens eingeben zu müssen.  
  
Wenn Sie in einer Datenbank arbeiten, die mehrere Objekte enthält, können die Listen der Befehlszeilenergänzung umfangreich werden. Einige [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Objekttypen, z. B. Sichten, verfügen außerdem über zahlreiche Systemobjekte.  
  
Die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Snap-Ins führen drei Systemvariablen ein, mit denen Sie die von der Befehlszeilenergänzung und **Get-ChildItem**bereitgestellte Informationsmenge steuern können.  
  
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
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server-PowerShell](sql-server-powershell.md)  
  
  
