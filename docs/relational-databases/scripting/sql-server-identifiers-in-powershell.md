---
title: "SQL Server-Bezeichnern in PowerShell | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Cmdlets [SQL Server], Encode-Sqlname"
  - "PowerShell [SQL Server], Bezeichner"
  - "Encode-Sqlname-Cmdlet"
  - "PowerShell [SQL Server], Encode-Sqlname"
  - "Decode-Sqlname-Cmdlet"
  - "PowerShell [SQL Server], Decode-Sqlname"
  - "Bezeichner [SQL Server], PowerShell"
  - "Cmdlets [SQL Server], Decode-Sqlname"
ms.assetid: 651099b0-33b4-453a-a864-b067f21eb8b9
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# SQL Server-Bezeichnern in PowerShell
  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieter für Windows PowerShell verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bezeichner in Windows PowerShell-Pfaden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bezeichner können Zeichen enthalten, die Windows PowerShell in Pfaden nicht unterstützt. Sie müssen diese Zeichen mit Escapezeichen versehen oder besondere Codierungen für sie verwenden, wenn Sie die Bezeichner in Windows PowerShell-Pfaden verwenden.  
  
## SQL Server-Bezeichner in Windows PowerShell-Pfaden  
 Windows PowerShell-Anbieter machen Datenhierarchien mithilfe einer Pfadstruktur verfügbar, die der für das Windows-Dateisystem verwendeten Pfadstruktur ähnelt. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anbieter implementiert Pfade zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objekten. Für [!INCLUDE[ssDE](../../includes/ssde-md.md)] sind das Laufwerk auf SQLSERVER und der erste Ordner auf \SQL festgelegt, und auf die Datenbankobjekte wird als Container und Elemente verwiesen. Dies ist der Pfad zur Vendor-Tabelle im Purchasing-Schema der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank in einer Standardinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
```  
SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bezeichner sind die Namen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekten, z. B. Tabellen- oder Spaltennamen. Es gibt zwei Arten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Bezeichnern:  
  
-   Reguläre Bezeichner sind auf einen Satz von Zeichen beschränkt, die auch in Windows PowerShell-Pfaden unterstützt werden. Diese Namen können in Windows PowerShell-Pfaden verwendet werden, ohne geändert zu werden.  
  
-   Begrenzungsbezeichner können Zeichen verwenden, die in Windows PowerShell-Pfadnamen nicht unterstützt werden. Begrenzungsbezeichner werden Bezeichner in Klammern genannt, wenn sie in Klammern eingeschlossen sind ([IdentifierName]), und Bezeichner in Anführungszeichen, wenn sie in doppelte Anführungszeichen eingeschlossen sind ("IdentifierName"). Wenn ein Begrenzungsbezeichner Zeichen verwendet, die in Windows PowerShell-Pfaden nicht unterstützt werden, müssen diese Zeichen entweder codiert oder mit Escapezeichen versehen werden, bevor der Bezeichner als Container- oder Elementname verwendet werden kann. Codierung funktioniert bei allen Zeichen. Einige Zeichen, z. B. das Doppelpunktzeichen (:), können nicht mit Escapezeichen versehen werden.  
  
## SQL Server-Bezeichner in Cmdlets  
 Einige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Cmdlets verfügen über einen Parameter, der einen Bezeichner als Eingabe akzeptiert. Die Parameterwerte werden i. d. R. als von Anführungszeichen umschlossene Zeichenfolgenkonstanten oder in Zeichenfolgenvariablen angegeben. Wenn Bezeichner als Zeichenfolgenkonstanten oder in Variablen angegeben werden, gibt es keinen Konflikt mit dem von Windows PowerShell unterstützten Zeichensatz.  
  
## Tasks der SQL Server-Bezeichner  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie ein Instanzname angegeben wird, einschließlich der Name des Computers, auf dem die Instanz ausgeführt wird.|[Angeben von Instanzen im SQL Server PowerShell-Anbieter](../../relational-databases/scripting/specify-instances-in-the-sql-server-powershell-provider.md)|  
|Beschreibt, wie die hexadezimale Codierung für Zeichen in Begrenzungsbezeichnern angegeben wird, die in Windows PowerShell-Pfaden nicht unterstützt werden. Beschreibt außerdem, wie die Hexadezimalzeichen decodiert werden.|[Codierung und Decodierung von SQL Server-Bezeichnern](../../relational-databases/scripting/encode-and-decode-sql-server-identifiers.md)|  
|Beschreibt, wie das Windows PowerShell-Escapezeichen für in PowerShell-Pfaden nicht unterstützte Zeichen verwendet wird.|[Escape-Bezeichner für SQL Server](../../relational-databases/scripting/escape-sql-server-identifiers.md)|  
  
## Siehe auch  
 [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md)  
  
  