---
title: Analysis Services PowerShell-Referenz | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3876581c0be890870db4d760b41715c36018e25f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-powershell-reference"></a>PowerShell-Reference für Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell-Cmdlets sind in enthalten die [SqlServer-Modul](https://www.powershellgallery.com/packages/SqlServer/21.0.17099). 
  
>[!NOTE] 
> Vorgänge der Azure Analysis Services-Datenbank verwenden Sie das gleiche SqlServer-Modul als SQL Server Analysis Services. Allerdings werden nicht alle Cmdlets für Azure Analysis Services unterstützt. Weitere Informationen finden Sie unter [Verwalten von Azure Analysis Services mit PowerShell](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell).
  
##  <a name="bkmk_cmdlets"></a> Analysis Services-Cmdlets  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt Cmdlets bereit, die den Methoden im **Microsoft.AnalysisServices** -Namespace entsprechen. In der folgenden Tabelle wird jedes Cmdlet beschrieben und ein Link zur entsprechenden AMO-Methode angegeben.  
  
 Wenn Sie PowerShell verwenden möchten, um einen Task auszuführen, der nicht in der folgenden Liste enthalten ist (z.B. das Erstellen oder Synchronisieren einer Datenbank), können Sie ein TMSL- oder ein XMLA-Skript für diese Aktion schreiben und dann mithilfe des **Invoke-ASCmd** -Cmdlets ausführen.  
  
|Cmdlet|Description|Entsprechende AMO-Methoden|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember-Cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)|Hinzufügen eines Mitglieds zu einer Datenbankrolle.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase-Cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Sichern einer Analysis Services-Datenbank.|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Invoke-ASCmd cmdlet (Invoke-ASCmd-Cmdlet)](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|Ausführen einer Abfrage oder eines Skripts im XMLA- oder TSML-Format (JSON).|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase (Invoke-ProcessASDatabase)](../../analysis-services/powershell/invoke-processasdatabase.md)|Verarbeiten einer Datenbank.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet (Invoke-ProcessCube-Cmdlet)](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Verarbeiten eines Cubes.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet (Invoke-ProcessDimension-Cmdlet)](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Verarbeiten einer Dimension.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition-Cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Verarbeiten einer Partition.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet (Invoke-ProcessTable-Cmdlet)](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Verarbeiten Sie eine Tabelle in einem Tabellenmodell, kompatibilitätsmodell 1200 oder höher.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet (Merge-Partition-Cmdlet)](../../analysis-services/powershell/merge-partition-cmdlet.md)|Zusammenführen einer Partition.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet (New-RestoreFolder-Cmdlet)](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Erstellen eines Ordners zum Ablegen einer Datenbanksicherung|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocations-Cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Angeben eines oder mehrerer Remoteserver für die Wiederherstellung der Datenbank|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember-Cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Entfernen eines Mitglieds aus einer Datenbankrolle|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet (Restore-ASDatabase-Cmdlet)](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Wiederherstellen einer Datenbank auf einer Serverinstanz|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
