---
title: "PowerShell-Reference f&#252;r Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# PowerShell-Reference f&#252;r Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] schließt einen PowerShell-Anbieter (SQLAS) und Cmdlets (SQLASCMDLETS) ein, damit Sie mithilfe von Windows PowerShell durch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Objekte navigieren und diese verwalten und abfragen können. Weitere Informationen zum Laden und Verwenden des Anbieters und der Cmdlets finden Sie unter [PowerShell-Skripts in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md). Ein Beispiel zur Verwendung von AMO-Typen in PowerShell zum Erstellen einer tabellarischen Datenbank finden Sie unter [Beispiel für AMO PowerShell](../../analysis-services/powershell/amo-powershell-example.md).  
  
##  <a name="bkmk_cmdlets"></a> Analysis Services-Cmdlets  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt Cmdlets bereit, die den Methoden im **Microsoft.AnalysisServices**-Namespace entsprechen. In der folgenden Tabelle wird jedes Cmdlet beschrieben und ein Link zur entsprechenden AMO-Methode angegeben.  
  
 Wenn Sie PowerShell verwenden möchten, um einen Task auszuführen, der nicht in der folgenden Liste enthalten ist (z.B. das Erstellen oder Synchronisieren einer Datenbank), können Sie ein TMSL- oder ein XMLA-Skript für diese Aktion schreiben und dann mithilfe des **Invoke-ASCmd**-Cmdlets ausführen.  
  
|Cmdlet|Description|Entsprechende AMO-Methoden|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember-Cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)|Hinzufügen eines Mitglieds zu einer Datenbankrolle.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase-Cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Sichern einer Analysis Services-Datenbank.|<xref:Microsoft.AnalysisServices.Database.Backup%2A>|  
|[Invoke-ASCmd-Cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|Ausführen einer Abfrage oder eines Skripts im XMLA- oder TSML-Format (JSON).|<xref:Microsoft.AnalysisServices.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|Verarbeiten einer Datenbank.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube-Cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Verarbeiten eines Cubes.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension-Cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Verarbeiten einer Dimension.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition-Cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Verarbeiten einer Partition.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable-cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Verarbeiten einer Tabelle in einem Tabellenmodell, Kompatibilitätsmodell 1200 oder neuer.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition-Cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)|Zusammenführen einer Partition.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder-Cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Erstellen eines Ordners zum Ablegen einer Datenbanksicherung|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocations-Cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Angeben eines oder mehrerer Remoteserver für die Wiederherstellung der Datenbank|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember-Cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Entfernen eines Mitglieds aus einer Datenbankrolle|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase-Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Wiederherstellen einer Datenbank auf einer Serverinstanz|<xref:Microsoft.AnalysisServices.Server.Restore%2A>|  
  
## Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services Scripting Language &#40;ASSL for XMLA&#41; (Analysis Services Scripting Language (ASSL für XMLA))](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [PowerShell-Skripts in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  