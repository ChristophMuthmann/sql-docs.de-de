---
title: Testen eines Modells im DirectQuery-Modus | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 11260792-ff8b-4d0e-b845-ca210dd3fced
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ad389541ba4bb964df0c3a0ca7cb08277d1bd1d9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="test-a-model-in-directquery-mode"></a>Testen eines Modells im DirectQuery-Modus
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Überprüfen Sie die Optionen für ein tabellarisches Modell im DirectQuery-Modus in den einzelnen Phasen der Entwicklung beginnend beim Entwurf zu testen.  
  
## <a name="test-in-excel"></a>Testen in Excel 
  
 Beim Entwerfen des Modells in SSDT können Sie die Funktion **In Excel analysieren** verwenden, um Ihre Modellierungsentscheidungen für ein Beispieldataset im Arbeitsspeicher oder für die relationale Datenbank zu testen.  Wenn Sie „In Excel analysieren“ auswählen, wird ein Dialogfeld geöffnet, in dem Sie Optionen angeben können.
 
 ![„In Excel analysieren“-DirectQuery-Optionen](../../analysis-services/tabular-models/media/analyze-in-excel-directquery-options.png)
 
 Wenn der DirectQuery-Modus Ihres Modells aktiviert ist, können Sie den DirectQuery-Verbindungsmodus bestimmen. Dazu haben Sie zwei Möglichkeiten:
 - **Beispieldatensicht** – Mit dieser Option werden alle Abfragen aus Excel zu Beispielpartitionen übermittelt, die über ein Beispieldataset verfügen, das sich im Speicher befindet. Diese Option ist hilfreich, wenn Sie sicherstellen möchten, dass alle DAX-Formeln in Measures, berechnete Spalten oder die Sicherheit auf Zeilenebene ordnungsgemäß ausgeführt wird.
 
 - **Vollständige Datenansicht** – mit dieser Option werden Anfragen von Excel zu Analysis Services übermittelt und dann an die relationale Datenbank gesendet. Diese Option stellt einen voll funktionsfähigen DirectQuery-Modus dar.
 
 ### <a name="other-clients"></a>Andere Clients
 Wenn Sie „In Excel analysieren“ verwenden, wird eine .odc-Datei erstellt. Sie können die Verbindungszeichenfolgeninformation aus dieser Datei verwenden, um eine Verbindung von anderen Clientanwendungen zu Ihrem Modell herzustellen. Es wird ein zusätzlicher Parameter, DataView=Sample, hinzugefügt, um anzugeben, dass der Client eine Verbindung mit Beispieldatenpartitionen herstellen soll.  
  
## <a name="monitor-query-execution-on-backend-systems-using-xevents-or-sql-profiler"></a>Überwachung der Ausführung von Abfragen auf Back-End-Systemen mit xEvents oder SQL Profiler. 
 Starten Sie die Ablaufverfolgung der Sitzung mit der relationalen SQL Server-Datenbank, um die vom tabellarischen Modell ausgehenden Verbindungen zu überwachen:  
  
-   [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
-   [Verwenden von SQL Server Profiler zum Überwachen von Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
 Wenn Sie mit Oracle oder Teradata arbeiten, verwenden Sie die Trace-Überwachungstools dieser Systeme.  
  
  
