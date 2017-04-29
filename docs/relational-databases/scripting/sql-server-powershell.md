---
title: SQL Server-PowerShell | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c7181877fcc1fa7553b5e11508bc1c9425166ccd
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-powershell"></a>SQL Server-PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt Windows PowerShell, ein leistungsstarkes Skriptshell, mit der Administratoren und Entwickler die Serververwaltung und die Anwendungsbereitstellung automatisieren können. Die Windows PowerShell-Sprache unterstützt komplexere Logik als [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts und ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratoren dadurch die Erstellung stabiler Verwaltungsskripts. Windows PowerShell-Skripts können außerdem dazu verwendet werden, andere [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Serverprodukte zu verwalten. So steht Administratoren eine serverübergreifende allgemeine Skriptsprache zur Verfügung.  
  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell-Komponenten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt das Windows PowerShell-Modul **sqlps** bereit, mit dem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten in eine Windows PowerShell 2.0-Umgebung oder ein Windows PowerShell-Skript importiert werden. Mit dem **sqlps** -Modul werden zwei Windows PowerShell-Snap-Ins geladen, mit denen folgende Elemente implementiert werden können:  
  
-   Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieter, der einen einfachen Navigationsmechanismus aktiviert, der Dateisystempfaden ähnelt. Sie können Dateisystempfaden ähnelnde Pfade erstellen, in denen das Laufwerk einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object-Modell zugeordnet ist, und deren Knoten auf Objektmodellklassen basieren. Sie können dann vertraute Befehle wie **cd** und **dir** verwenden, um auf den Pfaden zu navigieren, auf ähnliche Weise, wie Sie in einem Eingabeaufforderungsfenster in Ordnern navigieren. Mit anderen Befehlen, wie **ren** oder **del**, können Sie Aktionen für die Knoten im Pfad ausführen.  
  
-   Ein Satz von Cmdlets, bei denen es sich um Befehle handelt, mit denen in Windows PowerShell-Skripts eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Aktion angegeben wird. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Cmdlets unterstützen Aktionen wie das Ausführen eines **sqlcmd** -Skripts, das [!INCLUDE[tsql](../../includes/tsql-md.md)] - oder XQuery-Anweisungen enthält.  
  
 Informationen zu Windows PowerShell finden Sie unter [Erste Schritte mit Windows PowerShell](https://msdn.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell).  
  
## <a name="sql-server-versions"></a>SQL Server-Versionen  
 Die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] PowerShell-Komponenten können zur Verwaltung von Instanzen von [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] oder höher verwendet werden. Instanzen von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] müssen SP2 oder höher ausführen. Instanzen von [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] müssen SP4 oder höher ausführen. Wenn die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] PowerShell-Komponenten mit früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden, sind sie auf die in diesen Versionen verfügbaren Funktionen beschränkt.  
     
## <a name="sql-server-powershell-tasks"></a>SQL Server PowerShell-Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------| 
|Installieren von Microsoft® Windows PowerShell Extensions für Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  Die PowerShell-Module werden standardmäßig installiert, wenn [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert wird.  Sie können die PowerShell Extensions für SQL Server 2016 manuell installieren, indem Sie die folgenden Komponenten aus dem Microsoft® SQL Server® 2016 Feature Pack installieren:<br/>     Microsoft® System CLR-Typen für Microsoft SQL Server® 2016 (SQLSysClrTypes.msi)<br/>Freigegebene Verwaltungsobjekte für Microsoft® SQL Server® 2016 (SharedManagementObjects.msi)<br/> Microsoft® Windows PowerShell Extensions für Microsoft SQL Server® 2016 (PowerShellTools.msi)|[Microsoft® SQL Server® 2016 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=52676).   | 
|Beschreibt den bevorzugten Mechanismus zum Ausführen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Komponenten, um eine PowerShell-Sitzung zu öffnen und das **sqlps** -Modul zu laden. Das **sqlps** -Modul lädt den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Anbieter und die Cmdlets sowie die vom Anbieter und den Cmdlets verwendeten SMO-Assemblys (SQL Server Management Object).|[Importieren des SQLPS-Moduls](../../relational-databases/scripting/import-the-sqlps-module.md)|  
|Beschreibt, wie nur die SMO-Assemblys ohne den Anbieter oder die Cmdlets geladen werden.|[Laden der SMO-Assemblys in Windows PowerShell](../../relational-databases/scripting/load-the-smo-assemblies-in-windows-powershell.md)|  
|Beschreibt, wie eine Windows-PowerShell-Sitzungen durch Rechtsklick auf einen Knoten im **Objekt-Explorer**ausgeführt wird. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] startet eine Windows PowerShell-Sitzung, lädt das **sqlps** -Modul und legt den Pfad des SQL Server-Anbieters auf das ausgewählte Objekt fest.|[Ausführen von Windows PowerShell über SQL Server Management Studio](../../relational-databases/scripting/run-windows-powershell-from-sql-server-management-studio.md)|  
|Beschreibt, wie Auftragsschritte des SQL Server-Agents erstellt werden, die ein Windows PowerShell-Skript ausführen. Die Aufträge können dann zum Ausführen zu bestimmten Zeitpunkten oder als Reaktion auf Ereignisse geplant werden.|[Ausführen von Windows PowerShell-Schritten in SQL Server-Agent](../../relational-databases/scripting/run-windows-powershell-steps-in-sql-server-agent.md)|  
|Beschreibt, wie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieter zum Navigieren in einer Hierarchie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekten verwendet wird.|[SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)|  
|Beschreibt, wie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Cmdlets verwendet werden, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Aktionen wie Ausführen eines [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts angeben.|[Verwenden der Datenbankmodul-Cmdlets](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)|  
|Beschreibt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Begrenzungsbezeichner angegeben werden, die von Windows PowerShell nicht unterstützte Zeichen enthalten.|[SQL Server-Bezeichnern in PowerShell](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)|  
|Beschreibt, wie SQL Server-Authentifizierungsverbindungen hergestellt werden. Standardmäßig verwenden die SQL Server PowerShell-Komponenten Windows-Authentifizierungsverbindungen mithilfe der Windows-Anmeldeinformationen für den Prozess, der Windows PowerShell ausführt.|[Verwalten der Authentifizierung in PowerShell des Datenbankmoduls](../../relational-databases/scripting/manage-authentication-in-database-engine-powershell.md)|  
|Beschreibt, wie vom SQL Server PowerShell-Anbieter implementierte Variablen verwendet werden, um die Anzahl der bei Verwendung der Windows PowerShell-Befehlszeilenergänzung aufgeführten Objekte zu steuern. Dies ist vor allem beim Arbeiten an Datenbanken mit einer großen Anzahl von Objekten nützlich.|[Verwalten der Befehlszeilenergänzung &#40;SQL Server PowerShell&#41;](../../relational-databases/scripting/manage-tab-completion-sql-server-powershell.md)|  
|Beschreibt, wie mit Get-Help Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten in der Windows PowerShell-Umgebung abgerufen werden.|[Aufrufen der SQL Server PowerShell-Hilfe](../../relational-databases/scripting/get-help-sql-server-powershell.md)|  
  
  

