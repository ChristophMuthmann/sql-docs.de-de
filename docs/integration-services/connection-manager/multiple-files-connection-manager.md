---
title: "Verbindungs-Manager f&#252;r mehrere Dateien | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Ordner [Integration Services], Verbindungen"
  - "Dateien [Integration Services], Verbindungen"
  - "Verbindungs-Manager für mehrere Dateien"
  - "Verbindungs-Manager [Integration Services], mehrere Dateien"
  - "Verbindungen [Integration Services], Dateien"
  - "Mehrere Dateiverbindungen"
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# Verbindungs-Manager f&#252;r mehrere Dateien
  Mit einem Verbindungs-Manager für mehrere Dateien kann ein Paket auf vorhandene Dateien und Ordner verweisen oder Dateien und Ordner zur Laufzeit erstellen.  
  
> [!NOTE]  
>  Die integrierten Tasks und Datenflusskomponenten in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwenden keinen Verbindungs-Manager für mehrere Dateien. Sie können den Verbindungs-Manager jedoch im Skripttask oder in der Skriptkomponente verwenden. Informationen zum Verwenden von Verbindungs-Managern in der Skripttask finden Sie unter [Connecting to Data Sources in the Script Task](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md). Informationen zum Verwenden von Verbindungs-Managern in der Skriptkomponente finden Sie unter [Connecting to Data Sources in the Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## Verwendungstypen des Verbindungs-Managers für mehrere Dateien  
 Mit der **FileUsageType** -Eigenschaft des Verbindungs-Managers für mehrere Dateien wird angegeben, wie die Verbindung verwendet wird. Der Verbindungs-Manager für mehrere Dateien kann Dateien bzw. Ordner erstellen und vorhandene Dateien bzw. Ordner verwenden.  
  
 In der folgenden Tabelle sind die Werte von **FileUsageType**aufgeführt.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Der Verbindungs-Manager für mehrere Dateien verwendet eine vorhandene Datei.|  
|**1**|Der Verbindungs-Manager für mehrere Dateien erstellt eine Datei.|  
|**2**|Der Verbindungs-Manager für mehrere Dateien verwendet einen vorhandenen Ordner.|  
|**3**|Der Verbindungs-Manager für mehrere Dateien erstellt einen Ordner.|  
  
## Konfiguration des Verbindungs-Managers für mehrere Dateien  
 Wenn Sie einem Paket einen Verbindungs-Manager für mehrere Dateien hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine Verbindung für mehrere Dateien aufgelöst wird, die Eigenschaften der Verbindung für mehrere Dateien festlegt und der **Connections**-Sammlung des Pakets die Verbindung für mehrere Dateien hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **MULTIFILE**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um einen Verbindungs-Manager für mehrere Dateien zu konfigurieren:  
  
-   Geben Sie den Verwendungstyp von Dateien und Ordnern an.  
  
-   Geben Sie Dateien und Ordner an.  
  
-   Falls Sie mehrere Dateien oder Ordner verwenden, geben Sie die Reihenfolge an, in der auf die Dateien und Ordner zugegriffen wird.  
  
 Wenn der Verbindungs-Manager für mehrere Dateien auf mehrere Dateien und Ordner verweist, werden die Pfade der Dateien und Ordner durch einen senkrechten Strich (|) getrennt. Die **ConnectionString** -Eigenschaft des Verbindungs-Managers hat folgendes Format:  
  
 \<*Pfad*>|\<*Pfad*>  
  
 Mehrere Dateien oder Ordner können Sie auch mithilfe von Platzhalterzeichen angeben. Wenn z.B. auf alle Textdateien auf Laufwerk C verwiesen werden soll, kann der Wert der **ConnectionString**-Eigenschaft auf C:\\*.txt festgelegt werden.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer festlegen können, finden Sie unter [Referenz zur Benutzeroberfläche des Dialogfelds Dateiverbindungs-Manager hinzufügen](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  