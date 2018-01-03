---
title: Herunterladen des SQL Server PowerShell-Moduls | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords: SQL Server PowerShell installieren, SQL Server PowerShell herunterladen
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 208bf291819a3e847e784e76611acdec0bf2f2d0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="download-sql-server-powershell-module"></a>Herunterladen des SQL Server PowerShell-Moduls
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Als Teil des Release 17.0 von SQL Server Management Studio ist das SQL Server PowerShell-Modul nun im PowerShell-Katalog enthalten.  Das Modul ist nicht mehr im SSMS-Installationspaket enthalten. Um PowerShell mit Version 17.0 und neuer von SSMS zu verwenden, muss das SQL Server-Modul in einem zusätzlichen Schritt auf dem Computer installiert werden.

Die vollständige Dokumentation über die Installation der neuesten Version von Microsoft Management Framework und die allgemeine Installation von PowerShell-Modulen finden Sie auf der Seite [Power Shell Gallery (PowerShell-Katalog)](https://www.powershellgallery.com/).

Der PowerShell-Befehl zum Installieren des SQL Server-Moduls lautet:

> Install-module -Name SqlServer

Mit diesem Befehl wird das Modul für alle Benutzer des Computers installiert. Sie müssen den PowerShell-Prozess als Administrator ausführen.

> Install-Module -Name SqlServer -Scope CurrentUser

Mit diesem Befehl wird das Modul für den Benutzer installiert, der den aktuellen PowerShell-Prozess ausführt. Sie müssen den PowerShell-Prozess nicht mit Administratorrechten ausführen.

Wenn sich noch ältere Versionen der SQL Server PowerShell-Module auf dem Computer befinden, kann die Angabe des Parameters „-AllowClobber“ nötig werden.  

Verwenden Sie folgenden Befehl, wenn Sie als Administrator angemeldet sind und das Modul für alle Benutzer des Computers installiert werden soll:

> Install-Module -Name SqlServer -AllowClobber

Verwenden Sie folgenden Befehl, wenn Sie sich nicht als Administrator anmelden können bzw. wenn das Modul nur für den aktuellen Benutzer installiert werden soll:

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

Wenn aktualisierte Versionen des SqlServer-Moduls verfügbar sind, können Sie die Version aktualisieren, indem sie den Befehl „Update-Module“ eingeben:

> Update-Module -Name SqlServer

Geben Sie Folgendes ein, damit Ihnen die Versionen des auf dem Computer installierten Moduls angezeigt werden:

> Get-Module SqlServer -ListAvailable

Mit dem folgenden Befehl können Sie einen Import vornehmen, wenn Sie eine bestimmte Version des Moduls in Ihren Skripten verwenden möchten:

> Import-Module SqlServer -Version 21.0.17178

Die Versionen des SQL Server PowerShell-Moduls, die im PowerShell-Katalog enthalten sind, unterstützen die Versionsverwaltung und benötigen die PowerShell-Version 5.0 oder neuer. Sie finden das SqlServer-Modul [PowerShell-Katalog](https://www.powershellgallery.com/packages/Sqlserver/) 
