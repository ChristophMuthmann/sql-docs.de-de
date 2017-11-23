---
title: Testen eines Modells im DirectQuery-Modus | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 11260792-ff8b-4d0e-b845-ca210dd3fced
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d6f55de10089d304fe5dc5d00c388d007a2241a6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="test-a-model-in-directquery-mode"></a>Testen eines Modells im DirectQuery-Modus

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Erfahren Sie hier, welche Optionen Ihnen in jeder Phase der Entwicklung beginnend beim Entwurf zum Testen eines tabellarischen Modells im DirectQuery-Modus zur Verfügung stehen.  
  
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
  
  
