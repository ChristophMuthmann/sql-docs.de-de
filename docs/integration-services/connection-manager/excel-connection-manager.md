---
title: "Excel-Verbindungs-Manager | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Dateien [Integration Services], Verbindungen"
  - "Verbindungen [Integration Services], Excel"
  - "Excel [Integration Services]"
  - "Verbindungs-Manager [Integration Services], Excel"
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# Excel-Verbindungs-Manager
  Mit einem Excel-Verbindungs-Manager kann ein Paket eine Verbindung mit einer vorhandenen [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Arbeitsmappendatei herstellen. Die Excel-Quelle und das Excel-Ziel von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwenden den Excel-Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen Excel-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit als Excel-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der Sammlung **Verbindungen** im Paket den Verbindungs-Manager hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **EXCEL**festgelegt.  
  
## Konfiguration des Excel-Verbindungs-Managers  
 Es gibt folgende Möglichkeiten, um den Excel-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie den Pfad der Excel-Arbeitsmappendatei an.  
  
    > [!NOTE]  
    >  Es ist nicht möglich, eine Verbindung mit einer kennwortgeschützten Excel-Datei herzustellen.  
  
-   Geben Sie die Excel-Version an, die zum Erstellen der Datei verwendet wurde.  
  
-   Zeigen Sie an, ob die erste Zeile der abgerufenen Daten in den ausgewählten Arbeitsmappen oder Bereichen Spaltennamen enthält.  
  
 Wenn der Excel-Verbindungs-Manager von einer Excel-Quelle verwendet wird, sind die Spaltennamen in den extrahierten Daten enthalten. Wird dieser von einem Excel-Ziel verwendet, sind die Spaltennamen in den geschriebenen Daten enthalten.  
  
 Weitere Informationen zum Verhalten von Excel-Quellen und Excel-Zielen finden Sie unter [Excel Source](../../integration-services/data-flow/excel-source.md) und [Excel Destination](../../integration-services/data-flow/excel-destination.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer festlegen können, finden Sie unter [Verbindungs-Manager-Editor für Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
 Informationen zum Durchlaufen einer Gruppe von Excel-Dateien finden Sie unter [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## Verwandte Aufgaben  
  
-   [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Herstellen einer Verbindung mit einer Excel-Arbeitsmappe](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  