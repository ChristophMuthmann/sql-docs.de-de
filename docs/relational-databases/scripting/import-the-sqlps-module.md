---
title: Importieren des SQLPS-Moduls | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 39b5b945994c9531deb3d545dbb438657b1914fe
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="import-the-sqlps-module"></a>Importieren des SQLPS-Moduls
  Es wird empfohlen, zur Verwaltung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] über PowerShell das **sqlps**-Modul in eine Windows PowerShell-Umgebung zu importieren. Das Modul lädt und registriert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Snap-Ins und -Verwaltbarkeitsassemblys.  Ab Windows PowerShell 3.0 werden Module automatisch importiert, wenn ein Cmdlet oder eine Funktion im Modul in einem Befehl verwendet wird. Dieses Feature funktioniert für jedes Modul in einem Verzeichnis, das im Wert der PSModulePath-Umgebungsvariablen enthalten ist.  Weitere Informationen finden Sie unter [Importieren eines PowerShell-Moduls](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx).
  
1.  **Before You Begin:**  [Security](#Security)  
  
2.  **To load the module:**  [Load the sqlps Module](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 Nach dem Importieren des **sqlps** -Moduls in Windows PowerShell stehen Ihnen folgende Möglichkeiten zur Verfügung:  
  
-   Interaktives Ausführen von Windows PowerShell-Befehlen  
  
-   Ausführen von Windows PowerShell-Skriptdateien  
  
-   Ausführen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Cmdlets  
  
-   Verwenden Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anbieterpfade, um durch die Hierarchie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte zu navigieren.  
  
-   Verwenden Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verwaltbarkeit-Objektmodelle (z. B. Microsoft.SqlServer.Management.Smo), um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Objekte zu verwalten.  
  
> [!NOTE]  
>  Die in den Namen von zwei SQL Server-Cmdlets (**Encode-Sqlname** und **Decode-Sqlname**) verwendeten Verben entsprechen nicht den genehmigten Verben für Windows PowerShell. Dies hat keine Auswirkungen auf den Vorgang, aber Windows PowerShell gibt eine Warnung aus, wenn das **sqlps** -Modul in eine Sitzung importiert wird.  
  
###  <a name="Security"></a> Sicherheit  
 Standardmäßig wird Windows PowerShell mit auf **Restricted**festgelegter Skriptausführungsrichtlinie ausgeführt. Dadurch wird die Ausführung von Windows PowerShell-Skripts verhindert. Zum Laden des **sqlps** -Moduls können Sie das **Set-ExecutionPolicy** -Cmdlet verwenden, um die Ausführung signierter Skripts oder anderer Skripts zu ermöglichen. Führen Sie nur Skripts aus vertrauenswürdigen Quellen aus, und sichern Sie alle Eingabe- und Ausgabedateien, indem Sie die geeigneten NTFS-Berechtigungen verwenden. Weitere Informationen zum Aktivieren von Windows PowerShell-Skripts finden Sie unter [Ausführen der Windows PowerShell-Skripts](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx).  
  
##  <a name="LoadSqlps"></a> Laden des sqlps-Moduls  
 **So laden Sie das sqlps-Modul in Windows PowerShell**  
  
1.  Verwenden Sie das Cmdlet **Set-ExecutionPolicy** , um die entsprechende Skriptausführungsrichtlinie festzulegen.  
  
2.  Verwenden Sie das Cmdlet **Import-Module** zum Importieren des sqlps-Moduls. Geben Sie den **DisableNameChecking** -Parameter an, wenn Sie die Warnung zu **Encode-Sqlname** und **Decode-Sqlname**unterdrücken möchten.  
  
### <a name="example"></a>Beispiel  
 In diesem Beispiel wird das **sqlps** -Modul mit deaktivierter Namensüberprüfung geladen.  
  
```powershell 
# Import the SQL Server Module.    
Import-Module Sqlps -DisableNameChecking;

# To check whether the module is installed.
Get-Module -ListAvailable -Name Sqlps;
```  
  
> [!NOTE]  
>  Wenn das **sqlps** -Modul nicht in Ihrem Pfad vorhanden ist, ändern Sie den Speicherort des Moduls, oder verwenden Sie den vollständigen Pfad im Skript (mit doppelten Anführungszeichen, wenn Ordner im Pfad Leerzeichen enthalten). Das **sqlps** -Modul befindet sich im Ordner „Tools\Powershell“ Ihrer SQL Server-Instanz.  
  
 ![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../../analysis-services/instances/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“") [&#91;Top&#93;]()  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [SQL Server PowerShell-Anbieter](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Verwenden der Datenbankmodul-Cmdlets](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
 [Installieren eines PowerShell-Moduls](https://msdn.microsoft.com/library/dd878350(v=vs.85).aspx)  
 [Import-Module](https://technet.microsoft.com/library/hh849725.aspx)
  
  

