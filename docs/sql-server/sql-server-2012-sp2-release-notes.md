---
title: SQL Server 2012 SP2 Release Notes | Microsoft-Dokumentation
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: "6"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31f86cebfc5dc23aac8d56a1a9c75d140b744063
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-2012-sp2-release-notes"></a>SQL Server 2012 SP2 Release Notes
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)] In diesen Versionsanmerkungen werden Probleme beschrieben, die Sie vor der Installation und Problembehandlung von SQL Server 2012 Service Pack 2 kennen müssen. Versionsanmerkungen sind nur online verfügbar, nicht auf dem Installationsmedium. Sie werden regelmäßig mit dem Auftreten neuer Probleme aktualisiert. Weitere Informationen finden Sie unter [Bugs that are fixed in SQL Server 2012 Service Pack 2](http://support.microsoft.com/KB/2958429) .  
  
## <a name="choose-the-correct-file-to-download-and-install"></a>Auswählen der richtigen Download- und Installationsdatei  
Identifizieren Sie anhand der unten stehenden Tabelle und entsprechend der derzeit installierten Version den Speicherort und den Namen der herunterzuladenden Datei. Downloadseiten enthalten Systemanforderungen und grundlegende Installationsanweisungen.  
  
||||  
|-|-|-|  
|**Derzeit installierte Version...**|**Gewünschter Vorgang...**|**Download und Installation von...**|  
|32-Bit-Installationen:|||  
|32-Bit-Version einer beliebigen Edition von SQL Server 2012|Upgrade auf die 32-Bit-Version von SQL Server 2012 SP2|**SQLServer2012SP2-KB2958429-**<arch>**-**<lang id>**.exe** von der [Downloadseite für SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Eine 32-Bit-Version von SQL Server 2012 RTM Express|Upgrade auf die 32-Bit-Version von SQL Server 2012 Express SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32-Bit-Version nur der Client- und Verwaltbarkeitstools für SQL Server 2012 (einschließlich SQL Server 2012 Management Studio)|Upgrade der Client- und Verwaltbarkeitstools auf die 32-Bit-Version von SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Eine 32-Bit-Version von SQL Server 2012 Management Studio Express|Upgrade auf die 32-Bit-Version von SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32-Bit-Version einer beliebigen Edition von SQL Server 2012 und 32-Bit-Version der Client- und Verwaltbarkeitstools (einschließlich SQL Server 2012 RTM Management Studio)|Upgrade aller Produkte auf die 32-Bit-Version von SQL Server 2012 SP2|**SQLEXPRADV_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|32-Bit-Version eines oder mehrerer Tools des [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) oder des [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Upgrade der Tools auf die 32-Bit-Version des Microsoft SQL Server 2012 SP2 Feature Pack|Eines oder mehrere Tools von der [Downloadseite für Microsoft SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)|  
|64-Bit-Installationen:|||  
|64-Bit-Version einer beliebigen Edition von SQL Server 2012|Upgrade auf die 64-Bit-Version von SQL Server 2012 SP2|SQLServer2012SP2-KB2958429-<arch>-<langid>.exe von der [Downloadseite für SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|64-Bit-Version von SQL Server 2012 RTM Express|Upgrade auf die 64-Bit-Version von SQL Server 2012 SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64-Bit-Version ausschließlich der Client- und Verwaltbarkeitstools für SQL Server 2012 (einschließlich SQL Server 2012 Management Studio)|Upgrade der Client- und Verwaltbarkeitstools auf die 64-Bit-Version von SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64-Bit-Version von SQL Server 2012 Management Studio Express|Upgrade auf die 64-Bit-Version von SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** von der [Downloadseite für SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|64-Bit-Version eines oder mehrerer Tools des [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) oder des [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Upgrade der Tools auf die 64-Bit-Version des Microsoft SQL Server 2012 SP2 Feature Pack|Eines oder mehrere Tools von der [Downloadseite für Microsoft SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)|  
  
