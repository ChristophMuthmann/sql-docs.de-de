---
title: "Editor f&#252;r den Task &#39;Prozess ausf&#252;hren&#39; (Seite Verarbeiten) | Microsoft Docs"
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
  - "sql13.dts.designer.executeprocesstask.process.f1"
helpviewer_keywords: 
  - "Editor für den Task Prozess ausführen"
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# Editor f&#252;r den Task &#39;Prozess ausf&#252;hren&#39; (Seite Verarbeiten)
  Auf der Seite **Verarbeiten** des Dialogfelds **Editor für den Task 'Prozess ausführen'** können Sie die Optionen konfigurieren, die den Prozess ausführen. Zu den Optionen gehören der Name der ausführbaren Datei, der Speicherort dieser Datei, die Argumente der Eingabeaufforderung und die Variablen für die Ein- und Ausgabe.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Execute Process Task](../../integration-services/control-flow/execute-process-task.md).  
  
## enthalten  
 **RequireFullFileName**  
 Geben Sie an, ob der Task fehlschlagen soll, wenn die ausführbare Datei am angegebenen Speicherort nicht gefunden wird.  
  
 **Ausführbare Datei**  
 Geben Sie den Namen der ausführbaren Datei ein.  
  
 **Argumente**  
 Geben Sie Argumente für die Eingabeaufforderung an.  
  
 **WorkingDirectory**  
 Geben Sie den Pfad zu dem Ordner ein, in dem die ausführbare Datei enthalten ist, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(...)**, und suchen Sie den Ordner.  
  
 **StandardInputVariable**  
 Wählen Sie eine Variable für die Bereitstellung der Eingabe zum Prozess aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen:  
  
 **Verwandte Themen:** [Variable hinzufügen](../Topic/Add%20Variable.md)  
  
 **StandardOutputVariable**  
 Wählen Sie eine Variable für die Erfassung der Prozessausgabe aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
 **StandardErrorVariable**  
 Wählen Sie eine Variable für die Erfassung der Fehlerausgabe des Prozesses aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 Geben Sie an, ob beim Task ein Fehler auftritt, wenn der Prozessexitcode von dem unter **SuccessValue** angegebenen Wert abweicht.  
  
 **SuccessValue**  
 Geben Sie den Wert an, der von der ausführbaren Datei zurückgegeben wird, um einen Erfolg zu melden. Standardmäßig ist dieser Wert auf **0**festgelegt.  
  
 **TimeOut**  
 Geben Sie die Anzahl von Sekunden an, die der Prozess ausgeführt werden kann. Durch den Wert **0** wird angezeigt, dass kein Timeoutwert verwendet wird und der Prozess so lange ausgeführt wird, bis er entweder abgeschlossen ist oder ein Fehler auftritt.  
  
 **TerminateProcessAfterTimeOut**  
 Geben Sie an, ob das Ende des Prozesses nach Ablauf des durch die Option **TimeOut** angegebenen Timeoutzeitraumes erzwungen wird. Diese Option ist nur verfügbar, wenn der Wert unter **TimeOut** nicht **0**ist.  
  
 **WindowStyle**  
 Geben Sie die Fensteranordnung an, in der der Prozess ausgeführt wird.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  