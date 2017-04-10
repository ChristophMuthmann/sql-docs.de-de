---
title: "MSMQ-Verbindungs-Manager | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verbindungen [Integration Services], Nachrichtenwarteschlangen"
  - "Verbindungs-Manager [Integration Services], MSMQ"
  - "MSMQ-Verbindungs-Manager"
  - "Nachrichtenwarteschlangenverbindungen [Integration Services]"
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 35
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 35
---
# MSMQ-Verbindungs-Manager
  Mit einem MSMQ-Verbindungs-Manager kann ein Paket eine Verbindung mit einer Nachrichtenwarteschlange herstellen, die Message Queuing (MSMQ) verwendet. Der Task Nachrichtenwarteschlange von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet einen MSMQ-Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen MSMQ-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine MSMQ-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections**-Sammlung im Paket den Verbindungs-Manager hinzufügt. Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **MSMQ**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um einen MSMQ-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie eine Verbindungszeichenfolge an.  
  
-   Stellen Sie den Pfad der Nachrichtenwarteschlange bereit, mit der eine Verbindung hergestellt werden soll.  
  
 Das Format des Pfads richtet sich nach dem Typ der Warteschlange, wie in der folgenden Tabelle dargestellt.  
  
|Warteschlangentyp|Beispielpfad|  
|----------------|-----------------|  
|Öffentlich|\<Computername>\\<Warteschlangenname\>|  
|Privat|\<Computername>\Private$\\<Warteschlangenname\>|  
  
 Sie können einen Punkt (.) verwenden, um den lokalen Computer darzustellen.  
  
## Konfiguration des MSMQ-Verbindungs-Managers  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer festlegen können, finden Sie unter [MSMQ-Verbindungs-Manager-Editor](../../integration-services/connection-manager/msmq-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Siehe auch  
 [Nachrichtenwarteschlange (Task)](../../integration-services/control-flow/message-queue-task.md)   
 [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  