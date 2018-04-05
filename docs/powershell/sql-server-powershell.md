---
title: SQL Server-PowerShell | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: d9dc11888ffd63ad97031e666d4e63893dc2db3e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="sql-server-powershell"></a>SQL Server-PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[Installieren von SQL Server PowerShell](download-sql-server-ps-module.md)**

> [!NOTE]
> Es gibt zwei SQL Server PowerShell-Module: **SqlServer** und **SQLPS**. Das **SQLPS**-Modul ist zwar in der SQL Server-Installation (für die Abwärtskompatibilität) enthalten, wird jedoch nicht mehr aktualisiert. Das **SqlServer**-Modul ist das aktuellste PowerShell-Modul. Das **SqlServer**-Modul enthält aktualisierte Versionen der Cmdlets in **SQLPS** sowie neue Cmdlets zur Unterstützung der neuesten SQL-Funktionen.  
> Vorherige Versionen des **SqlServer**-Moduls *waren* in SQL Server Management Studio (SSMS) enthalten, allerdings nur in den Versionen 16.x. Das **SqlServer**-Modul muss über den PowerShell-Katalog installiert werden, damit PowerShell mit SSMS 17.0 und höher verwendet werden kann.
> Informationen zur Installation des **SqlServer**-Moduls finden Sie unter [Installieren von SQL Server PowerShell](download-sql-server-ps-module.md).

**Warum wurde das Modul von „SQLPS“ in „SqlServer“ geändert?**

Zur Freigabe von SQL PowerShell-Updates mussten die Identitäten des SQL PowerShell-Moduls und des Wrappers *SQLPS.exe* geändert werden. Aufgrund dieser Änderung gibt es jetzt zwei SQL PowerShell-Module: das **SqlServer**-Modul und das **SQLPS**-Modul.  

**Aktualisieren Sie Ihre PowerShell-Skripts, wenn diese das SQLPS-Modul importieren.**

Wenn Sie über PowerShell-Skripts verfügen, die `Import-Module -Name SQLPS` ausführen, und Sie die Vorteile der neuen Anbieterfunktionen und Cmdlets nutzen möchten, müssen Sie diese in `Import-Module -Name SqlServer` ändern. Das neue Modul wird im Ordner `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer` installiert. Aus diesem Grund müssen Sie die Variable „$env:PSModulePath“ nicht aktualisieren. Wenn Sie über Skripts verfügen, die eine Community-Version oder eine Version eines Drittanbieters eines Moduls mit dem Namen **SqlServer** verwenden, verwenden Sie den Präfixparameter, um Konflikte mit den Namen zu vermeiden. Es wurden keine Änderungen an dem von SQL Server-Agent verwendeten Modul vorgenommen. 

  
## <a name="sql-server-powershell-components"></a>SQL Server PowerShell-Komponenten  
Mit dem **SqlServer**-Modul werden zwei Windows PowerShell-Snap-Ins geladen:  
  
-   Ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Anbieter, der einen einfachen Navigationsmechanismus aktiviert, der Dateisystempfaden ähnelt. Sie können Dateisystempfaden ähnelnde Pfade erstellen, in denen das Laufwerk einem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object-Modell zugeordnet ist, und deren Knoten auf Objektmodellklassen basieren. Sie können dann vertraute Befehle wie **cd** und **dir** verwenden, um auf den Pfaden zu navigieren, auf ähnliche Weise, wie Sie in einem Eingabeaufforderungsfenster in Ordnern navigieren. Mit anderen Befehlen, wie **ren** oder **del**, können Sie Aktionen für die Knoten im Pfad ausführen.  
  
-   Mehrere Cmdlets unterstützen Aktionen wie das Ausführen eines **sqlcmd**-Skripts, das [!INCLUDE[tsql](../includes/tsql-md.md)]- oder XQuery-Anweisungen enthält.  
  
  
## <a name="sql-server-versions"></a>SQL Server-Versionen  
SQL PowerShell-Cmdlets können verwendet werden, um Instanzen von Azure SQL-Datenbank und Azure SQL Data Warehouse sowie alle [unterstützten SQL Server-Produkte](https://support.microsoft.com/lifecycle/search/1044) zu verwalten.  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>SQL Server-Bezeichner mit Zeichen, die in PowerShell-Pfaden nicht unterstützt werden.  
 
Das **Encode-Sqlname** -Cmdlet und das **Decode-Sqlname** -Cmdlet helfen Ihnen, SQL Server-Bezeichner mit Zeichen anzugeben, die in PowerShell-Pfaden nicht unterstützt werden. Weitere Informationen finden Sie unter [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md).  
  
Mit dem **Convert-UrnToPath** -Cmdlet können Sie einen eindeutigen Ressourcennamen (Unique Resource Name, URN) für ein [!INCLUDE[ssDE](../includes/ssde-md.md)] -Objekt einen Pfad für den SQL Server PowerShell-Anbieter konvertieren. Weitere Informationen finden Sie unter [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Abfrageausdrücke und eindeutige Ressourcennamen  

Bei Abfrageausdrücken handelt es sich um Zeichenfolgen, die eine ähnliche Syntax wie XPath nutzen, um eine Gruppe von Kriterien angeben, mit der ein oder mehrere Objekte in einer Objektmodellhierarchie aufgezählt werden. Ein eindeutiger Ressourcenname (Unique Resource Name, URN) ist ein spezieller Typ einer Abfrageausdrucks-Zeichenfolge, der ein einzelnes Objekt eindeutig kennzeichnet. Weitere Informationen finden Sie unter [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md).       


## <a name="cmdlet-reference"></a>Cmdlet-Referenz
* [SqlServer-Cmdlets](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS-Cmdlets](https://docs.microsoft.com/powershell/module/sqlps)
