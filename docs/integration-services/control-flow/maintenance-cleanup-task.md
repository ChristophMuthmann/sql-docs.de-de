---
title: "Wartungscleanup (Task) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.maintenancecleanuptask.f1"
helpviewer_keywords: 
  - "Löschen von Dateien"
  - "Entfernen von Dateien"
  - "Wartungscleanup (Task)"
ms.assetid: 73ad3cd6-9a6d-44cf-905f-c56aa658bf42
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Wartungscleanup (Task)
  Mit dem Task Wartungscleanup werden Dateien entfernt, die mit Wartungsplänen verbunden sind, einschließlich Datenbanksicherungsdateien und Berichte, die von Wartungsplänen erstellt wurden. Weitere Informationen finden Sie unter [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md) und [Sichern und Wiederherstellen von SQL Server-Datenbanken](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 Ein Paket kann mithilfe des Tasks Wartungscleanup die Sicherungsdateien oder Wartungsplanberichte auf dem angegebenen Server entfernen. Der Task Wartungscleanup schließt eine Option zum Entfernen einer bestimmten Datei bzw. einer Gruppe von Dateien eines Ordners ein. Optional können Sie die Erweiterung der zu löschenden Dateien angeben.  
  
 Wenn Sie den Task Wartungscleanup zum Entfernen von Sicherungsdateien konfigurieren, lautet die Standard-Dateinamenerweiterung BAK. Für Berichtsdateien lautet die Standard-Dateinamenerweiterung TXT. Sie können die Erweiterungen nach Ihren Bedürfnissen aktualisieren. Als einzige Beschränkung gilt, dass Erweiterungen eine Länge von maximal 256 Zeichen aufweisen dürfen.  
  
 In der Regel werden alte Dateien, die nicht mehr benötigt werden, entfernt. Der Task Wartungscleanup kann so konfiguriert werden, dass sämtliche Dateien, die ein bestimmtes Alter erreicht haben, gelöscht werden. Der Task kann beispielsweise zum Löschen von Dateien konfiguriert werden, die älter als vier Wochen sind. Sie können das Alter der zu löschenden Dateien angeben, indem Sie Tage, Wochen, Monate oder Jahre verwenden. Wenn Sie das Mindestalter der zu löschenden Dateien nicht angeben, werden alle Dateien des angegebenen Typs gelöscht.  
  
 Im Gegensatz zu früheren Versionen des Tasks Wartungscleanup löscht die Version des Tasks in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht automatisch Dateien in den Unterverzeichnissen des angegebenen Verzeichnisses. Diese Einschränkung verringert die Oberfläche eines Angriffs, der die Funktionalität des Tasks Wartungscleanup ausnutzen könnte, um Dateien in böswilliger Absicht zu löschen. Wenn Sie die Unterordner auf oberster Ebene löschen möchten, müssen Sie dies ausdrücklich durch Aktivieren der Option **Unterordner auf oberster Ebene einschließen** im Dialogfeld **Task "Wartungscleanup"** auswählen.  
  
## Konfiguration des Task "Wartungscleanup"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Wartungscleanup“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/maintenance-cleanup-task-maintenance-plan.md)  
  
## Verwandte Aufgaben  
 Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer finden Sie unter [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
## Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  