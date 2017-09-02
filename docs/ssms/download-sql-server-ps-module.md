---
title: Herunterladen des SQL Server PowerShell-Moduls | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- SQL Server PowerShell installieren, SQL Server PowerShell herunterladen
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-powershell-module"></a>Herunterladen des SQL Server PowerShell-Moduls
Als Teil der Version 17.0 von SQL Server Management Studio ist das SQL Server PowerShell-Modul nun im PowerShell-Katalog enthalten.  Das Modul ist nicht mehr im SSMS-Installationspaket enthalten. Um PowerShell mit Version 17.0 und neuer von SSMS zu verwenden, muss das SQL Server-Modul in einem zusätzlichen Schritt auf dem Computer installiert werden.

Die vollständige Dokumentation über die Installation der neuesten Version von Microsoft Management Framework und die allgemeine Installation von PowerShell-Modulen finden Sie auf der Seite [Power Shell Gallery (PowerShell-Katalog)](https://www.powershellgallery.com/).

Der PowerShell-Befehl zum Installieren des SQL Server-Moduls lautet:

> Install-module -Name SqlServer -Scope CurrentUser

Wenn sich noch ältere Versionen der SQL Server PowerShell-Module auf dem Computer befinden, kann die Angabe des Parameters „-AllowClobber“ nötig werden.  

Die Versionen des SQL Server PowerShell-Moduls, die im PowerShell-Katalog enthalten sind, unterstützen die Versionsverwaltung und benötigen die PowerShell-Version 5.0 oder neuer.

