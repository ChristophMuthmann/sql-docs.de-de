---
title: Herunterladen des SQL Server PowerShell-Moduls | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/05/2018
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords: SQL Server PowerShell installieren, SQL Server PowerShell herunterladen
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: de203080dcc9b2c296003606e9a8067fd5dc532d
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2018
---
# <a name="install-sql-server-powershell-module"></a>Installieren des SQL Server PowerShell-Moduls
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Dieser Artikel enthält Anleitungen zur Installation des PowerShell-Moduls **SqlServer**.

> [!NOTE]
> Es gibt zwei SQL Server PowerShell-Module: **SqlServer** und **SQLPS**. Das **SQLPS**-Modul ist zwar in der SQL Server-Installation (für die Abwärtskompatibilität) enthalten, wird jedoch nicht mehr aktualisiert. Das **SqlServer**-Modul ist das aktuellste PowerShell-Modul. Das **SqlServer**-Modul enthält aktualisierte Versionen der Cmdlets in **SQLPS** sowie neue Cmdlets zur Unterstützung der neuesten SQL-Funktionen. Vorherige Versionen des **SqlServer**-Moduls *waren* in SQL Server Management Studio (SSMS) enthalten, allerdings nur in den Versionen 16.x. Das **SqlServer**-Modul muss über den PowerShell-Katalog installiert werden, damit PowerShell mit SSMS 17.0 und höher verwendet werden kann.

Starten Sie eine **PowerShell**-Sitzung, und verwenden Sie folgende Befehle, um das [SqlServer](https://docs.microsoft.com/powershell/scripting/powershell-scripting)-Modul über den PowerShell-Katalog zu installieren. Wenn bei der Installation Probleme auftreten, finden Sie weitere Informationen unter [Install-Module documentation (Dokumentation zu „Install-Module“)](https://docs.microsoft.com/powershell/gallery/psget/module/psget_install-module) und [Install-Module reference (Referenz zu „Install-Module“)](https://docs.microsoft.com/powershell/module/powershellget/Install-Module).

So installieren Sie das **SqlServer**-Modul:

```Install-Module -Name SqlServer```

Wenn vorherige Versionen des **SqlServer**-Moduls auf dem Computer vorhanden sind, können Sie wie später in diesem Artikel beschrieben `Update-Module` verwenden oder den Parameter `-AllowClobber` bereitstellen:  

```Install-Module -Name SqlServer -AllowClobber```

Wenn Sie die PowerShell-Sitzung nicht als Administrator ausführen können, können Sie die Installation für den aktuellen Benutzer durchführen:

```Install-Module -Name SqlServer -Scope CurrentUser```

Wenn aktualisierte Versionen des **SqlServer**-Moduls verfügbar sind, können Sie die Version mithilfe von `Update-Module` aktualisieren:

```Update-Module -Name SqlServer```

So zeigen Sie die Versionen der installierten Module an:

```Get-Module SqlServer -ListAvailable```

Wenn Sie eine spezifische Version des Moduls verwenden möchten, können Sie dieses folgendermaßen mit einer spezifischen Versionsnummer importieren:

```Import-Module SqlServer -Version 21.0.17178```


Die Versionen des **SqlServer**-Moduls im PowerShell-Katalog unterstützen die Versionsverwaltung und erfordern Version 5.0 oder höher von PowerShell. 

* [SqlServer-Modul im PowerShell-Katalog](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer-Cmdlets](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS-Cmdlets](https://docs.microsoft.com/powershell/module/sqlps)
