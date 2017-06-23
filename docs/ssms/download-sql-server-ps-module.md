---
title: Herunterladen von SQL Server PowerShell-Modul | Microsoft Docs
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
- Installieren von Sql Server-Powershell, Herunterladen von Sql Server powershell
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: de-de
ms.lasthandoff: 06/23/2017

---
# <a name="download-sql-server-powershell-module"></a>Herunterladen von SQL Server PowerShell-Modul
Als Teil der 17,0-Version von SQL Server Management Studio wird die SQL Server PowerShell-Modul nun über die PowerShell-Katalog geliefert.  Das Modul ist nicht mehr in der SSMS-Installationspaket enthalten. Wenn Sie PowerShell mit SSMS 17,0 und höher, muss der SQL Server-Modul als ein zusätzlicher Schritt auf dem Computer installiert werden.

Vollständige Dokumentation zur Installation der neuesten Version von Windows Management Framework aus, und installieren Sie PowerShell-Module im Allgemeinen befinden sich auf die [PowerShell-Katalog](https://www.powershellgallery.com/) Standort.

Der PowerShell-Befehl zum Installieren des SQL Server-Moduls ist:

> Install-Module-Name der SQL Server-Bereich CurrentUser

Befinden Sie frühere Versionen von SQL Server PowerShell-Module auf dem Computer an, es kann erforderlich sein, geben Sie den "-AllowClobber" Parameter.  

Die Versionen der SQL Server PowerShell-Modul die PowerShell-Katalog geliefert unterstützt die versionsverwaltung und PowerShell, Version 5.0 oder höher erforderlich.

