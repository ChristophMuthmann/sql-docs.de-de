---
title: "Installieren von SQL Server PowerShell | Microsoft Docs"
ms.custom: ""
ms.date: "02/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 9
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 9
---
# Installieren von SQL Server PowerShell
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup konfiguriert PowerShell-Komponenten automatisch.  
  
## Installieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Unterstützung  
 Die Software, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Unterstützung für Windows PowerShell bietet, installieren Sie mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup. Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen auswählen, die PowerShell-Unterstützung erfordern, installiert Setup die folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Komponenten:  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Snap-Ins. Die Snap-Ins sind DLL-Dateien, die zwei Arten der Windows PowerShell-Unterstützung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementieren:  
  
    -   Ein Satz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Cmdlets. Cmdlets sind Befehle, die eine bestimmte Aktion implementieren. Beispielsweise führt **Invoke-Sqlcmd** ein [!INCLUDE[tsql](../../includes/tsql-md.md)]- oder XQuery-Skript aus, das auch vom **sqlcmd**-Hilfsprogramm ausgeführt werden kann. **Invoke-PolicyEvaluation** meldet, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekte den richtlinienbasierten Verwaltungsrichtlinien entsprechen.  
  
    -   Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anbieter. Mit dem Anbieter können Sie in der Hierarchie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekte mithilfe eines Pfads navigieren, der einem Dateisystempfad ähnelt. Jedes Objekt ist einer Klasse der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object-Modelle zugeordnet. Sie können die Methoden und die Eigenschaften der Klasse zur Arbeit mit den Objekten verwenden. Wenn Sie z. B. cd zu einem Datenbankobjekt in einem Pfad ausführen, können Sie die Methoden und Eigenschaften der Microsoft.SqlServer.Management.SMO.Database-Klasse verwenden, um die Datenbank zu verwalten.  
  
-   Das **sqlps**-Modul, das in Windows PowerShell-Sitzungen importiert wird, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Snap-Ins zu laden.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] unterstützt das Starten von Windows PowerShell-Sitzungen aus der Struktur des Objekt-Explorers. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent unterstützt Windows PowerShell-Auftragsschritte.  
  
 In Windows Server 2012 und höher sowie Windows 8 und höher ist PowerShell bereits installiert und konfiguriert. Informationen zum Installieren von Windows PowerShell finden Sie auf der Seite [Installieren von Windows PowerShell](http://msdn.microsoft.com/library/hh847837.aspx).  
  
## Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  