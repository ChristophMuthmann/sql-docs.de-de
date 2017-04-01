---
title: "Quelldatenbankdateien | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1"
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Quelldatenbankdateien
  Verwenden Sie das Dialogfeld **Quelldatenbankdateien** , um die Namen und Speicherorte der Datenbankdateien auf dem Quellserver anzuzeigen, oder um für den Task "Datenbanken übertragen" eine Dateifreigabe auf dem Netzwerk anzugeben. Weitere Informationen zu diesem Task finden Sie unter [Datenbanken übertragen (Task)](../../integration-services/control-flow/transfer-database-task.md).  
  
 Um dieses Dialogfeld mit den Datenbankdateinamen und -speicherorten des Quellservers aufzufüllen, geben Sie zuerst auf der Seite **Datenbanken** des Dialogfelds **Editor für den Task 'Datenbanken übertragen'** die Parameter **SourceConnection** und **SourceDatabaseName** an.  
  
## enthalten  
 **Quelldatei**  
 Die Namen der zu übertragenden Datenbankdateien auf dem Quellserver. **Quelldatei** ist schreibgeschützt.  
  
 **Quellordner**  
 Der Ordner auf dem Quellserver, in dem sich die zu übertragenden Datenbankdateien befinden. **Quellordner** ist schreibgeschützt.  
  
 **Netzwerkdateifreigabe**  
 Der auf dem Netzwerk freigegebene Ordner auf dem Quellserver, aus dem die Datenbankdateien übertragen werden sollen. Verwenden Sie **Netzwerkdateifreigabe** , wenn Sie eine Datenbank im Offlinemodus übertragen, indem Sie auf der Seite **Datenbanken** des Dialogfelds **Editor für den Task 'Datenbanken übertragen'** als **Methode** **DatabaseOffline** angeben.  
  
 Geben Sie den Speicherort der Netzwerkdateifreigabe ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(…)**, um zu dieser Netzwerkdateifreigabe zu navigieren.  
  
 Beim Übertragen einer Datenbank im Offlinemodus werden die Datenbankdateien zunächst in den als **Netzwerkdateifreigabe** angegebenen Speicherort auf dem Quellserver kopiert, bevor sie auf den Zielserver übertragen werden.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „Datenbanken übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [Editor für den Task „Datenbanken übertragen“ &#40;Seite „Datenbanken“&#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  