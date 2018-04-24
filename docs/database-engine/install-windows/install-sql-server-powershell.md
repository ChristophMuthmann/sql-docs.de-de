---
title: Installieren von SQL Server PowerShell | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 573d8c10ae60680d3085c61d8f0c30b6b600701d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-powershell"></a>Installieren von SQL Server PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup konfiguriert PowerShell-Komponenten automatisch.  

Die Software, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Unterstützung für Windows PowerShell bietet, installieren Sie mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen auswählen, die PowerShell-Unterstützung erfordern, installiert Setup die folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Komponenten:  
  
- Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Snap-Ins. Die Snap-Ins sind DLL-Dateien, die zwei Arten der Windows PowerShell-Unterstützung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementieren:  
  
  - Ein Satz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Cmdlets. Cmdlets sind Befehle, die eine bestimmte Aktion implementieren. Beispielsweise führt **Invoke-Sqlcmd** ein [!INCLUDE[tsql](../../includes/tsql-md.md)] - oder XQuery-Skript aus, das auch vom **sqlcmd** -Hilfsprogramm ausgeführt werden kann. **Invoke-PolicyEvaluation** meldet, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte den richtlinienbasierten Verwaltungsrichtlinien entsprechen.  
  
  - Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieter. Mit dem Anbieter können Sie in der Hierarchie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte mithilfe eines Pfads navigieren, der einem Dateisystempfad ähnelt. Jedes Objekt ist einer Klasse der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object-Modelle zugeordnet. Sie können die Methoden und die Eigenschaften der Klasse zur Arbeit mit den Objekten verwenden. Wenn Sie z. B. cd zu einem Datenbankobjekt in einem Pfad ausführen, können Sie die Methoden und Eigenschaften der Microsoft.SqlServer.Management.SMO.Database-Klasse verwenden, um die Datenbank zu verwalten.  
 
- Das **sqlps** -Modul, das in Windows PowerShell-Sitzungen importiert wird, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Snap-Ins zu laden.  
 
- [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] unterstützt das Starten von Windows PowerShell-Sitzungen aus der Struktur des Objekt-Explorers. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent unterstützt Windows PowerShell-Auftragsschritte.  
  
In Windows Server 2012 und höher sowie Windows 8 und höher ist PowerShell bereits installiert und konfiguriert. Informationen zum Installieren von Windows PowerShell finden Sie auf der Seite [Installieren von Windows PowerShell](http://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell).  

Weitere Informationen finden Sie in den folgenden Themen:   

- [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
