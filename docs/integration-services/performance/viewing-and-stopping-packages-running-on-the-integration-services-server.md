---
title: "Anzeigen und Beenden von auf dem Integration Services-Server ausgef&#252;hrten Paketen | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pakete [Integration Services], verwalten"
  - "Verwalten ausgeführter Pakete [Integration Services]"
  - "Pakete [Integration Services], ausführen"
  - "Ausgeführtes Paket [Integration Services], verwalten"
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Anzeigen und Beenden von auf dem Integration Services-Server ausgef&#252;hrten Paketen
  In der **SSISDB** -Datenbank wird der Ausführungsverlauf in internen Tabellen gespeichert, die für Benutzer nicht sichtbar sind. Es werden jedoch Informationen verfügbar gemacht, die für öffentliche Sichten benötigt werden, die Sie abfragen können. Außerdem werden gespeicherte Prozeduren bereitgestellt, die Sie aufrufen können, um allgemeine Aufgaben im Zusammenhang mit Paketen auszuführen.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Objekte auf dem Server werden i. d. R. in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verwaltet. Sie können jedoch auch die Datenbanksichten abfragen und gespeicherte Prozeduren direkt aufrufen oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und die verwaltete API führen zur Ausführung vieler Aufgaben eine Abfrage der Sichten durch und rufen gespeicherte Prozeduren auf. Sie können beispielsweise die Liste der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete anzeigen, die derzeit auf dem Server ausgeführt werden, und bei Bedarf einzelne Pakete anhalten.  
  
## Anzeigen der Liste ausgeführter Pakete  
 Sie können die Liste der momentan auf dem Server ausgeführten Pakete im Dialogfeld **Aktive Vorgänge** anzeigen. Weitere Informationen finden Sie unter [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md).  
  
 Informationen zu weiteren Methoden, mit denen Sie die Liste der ausgeführten Pakete anzeigen können, finden Sie in den folgenden Themen.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff  
 Fragen Sie die Sicht [catalog.executions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) nach Paketen ab, die einen Status von 2 aufweisen, um die Liste der Pakete anzuzeigen, die auf dem Server ausgeführt werden.  
  
 Programmgesteuerter Zugriff auf die verwaltete API  
 Weitere Informationen finden Sie im Namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> und dessen Klassen.  
  
## Beenden eines ausgeführten Pakets  
 Sie können die Beendigung eines ausgeführten Pakets im Dialogfeld **Aktive Vorgänge** anfordern. Weitere Informationen finden Sie unter [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md).  
  
 Informationen zu weiteren Methoden, mit denen Sie Pakete beenden können, die derzeit ausgeführt werden, finden Sie in den folgenden Themen.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff  
 Rufen Sie die gespeicherte Prozedur [catalog.stop_operation &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md) auf, um ein Paket zu beenden, das auf dem Server ausgeführt wird.  
  
 Programmgesteuerter Zugriff auf die verwaltete API  
 Weitere Informationen finden Sie im Namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> und dessen Klassen.  
  
## Anzeigen des Verlaufs ausgeführter Pakete  
 Verwenden Sie den Bericht [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]Alle Ausführungen **, um den Verlauf der Pakete anzuzeigen, die in** ausgeführt wurden. Weitere Informationen zum Bericht **Alle Ausführungen** und zu anderen Standardberichten finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
 Informationen zu weiteren Methoden, mit denen Sie den Verlauf der ausgeführten Pakete anzeigen können, finden Sie in den folgenden Themen.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff  
 Um Informationen zu Paketen anzuzeigen, die ausgeführt wurden, fragen Sie die Sicht [catalog.executions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) ab.  
  
 Programmgesteuerter Zugriff auf die verwaltete API  
 Weitere Informationen finden Sie im Namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> und dessen Klassen.  
  
## Siehe auch  
 [Ausführung von Projekten und Paketen](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Behandlung von Problemen in Berichten für die Paketausführung](https://msdn.microsoft.com/library/gg471512.aspx)  
  
  