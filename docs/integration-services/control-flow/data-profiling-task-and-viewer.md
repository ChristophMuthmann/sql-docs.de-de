---
title: Datenprofilerstellungs-Task und -Viewer | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling task [Integration Services], about data profiling
- data profiling
- profiling data
ms.assetid: 756840e3-aa09-45cd-9951-1a17af4b5925
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b092926fc7354192293ccdbd7371998354fb626a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="data-profiling-task-and-viewer"></a>Datenprofilerstellungs-Task und -Viewer
  Der Datenprofilerstellungs-Task bietet Funktionen zur Datenprofilerstellung beim Extrahieren, Transformieren und Laden von Daten. Mit dem Datenprofilerstellungs-Task können Sie die folgenden Vorteile erzielen:  
  
-   Sie können die Quelldaten effizienter analysieren.  
  
-   Sie können die Quelldaten besser verstehen.  
  
-   Sie können Datenqualitätsprobleme verhindern, bevor diese ins Data Warehouse eingeführt werden.  
  
> [!IMPORTANT]  
>  Der Datenprofilerstellungs-Task funktioniert nur mit Daten, die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert werden. Dieser Task funktioniert nicht mit Datenquellen von Drittanbietern oder dateibasierten Datenquellen.  
  
## <a name="data-profiling-overview"></a>Übersicht über die Datenprofilerstellung  
 Datenqualität ist für jedes Unternehmen von Bedeutung. Da Unternehmen zusätzlich zu ihren Transaktionssystemen analytische Systeme und Business Intelligence-Systeme erstellen, hängt die Zuverlässigkeit von Key Performance Indicators (KPIs) und Data Mining-Vorhersageabfragen vollständig von der Gültigkeit der Daten ab, auf denen diese Systeme basieren. Obwohl die Bedeutung von gültigen Daten für Geschäftsentscheidungen ständig zunimmt, wird die Gewährleistung der Gültigkeit dieser Daten immer schwieriger. Daten von unterschiedlichen Systemen und Quellen und zahlreichen Benutzern strömen unaufhörlich in das Unternehmen.  
  
 Es kann schwierig sein, Metriken für die Datenqualität zu definieren, da diese spezifisch für die jeweilige Domäne oder Anwendung sind. Ein gebräuchliches Verfahren zur Definition von Datenqualität ist die Datenprofilerstellung.  
  
 Ein Datenprofil ist eine Auflistung von Gesamtstatistiken zu Daten, die Folgendes einschließen könnten:  
  
-   Die Anzahl der Zeilen in der Customer-Tabelle.  
  
-   Die Anzahl von unterschiedlichen Werten in der Spalte State.  
  
-   Die Anzahl von NULL-Werten oder fehlenden Werten in der Spalte Zip.  
  
-   Die Verteilung der Werte in der Spalte City.  
  
-   Die Stärke der funktionalen Abhängigkeit der Spalte State von der Spalte Zip, d. h., der Staat sollte für einen bestimmten PLZ-Wert immer gleich sein.  
  
 Die Statistiken, die ein Datenprofil bietet, liefern Ihnen die erforderlichen Informationen, um effizient die Qualitätsprobleme zu minimieren, die durch die Verwendung der Quelldaten auftreten könnten.  
  
## <a name="integration-services-and-data-profiling"></a>SQL Server Integration Services und Datenprofilerstellung  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]besteht der Prozess der Datenprofilerstellung aus den folgenden Schritten:  
  
 **Schritt 1: Einrichten des Datenprofilerstellungs-Tasks**  
 Der Datenprofilerstellungs-Task ist ein Task, den Sie verwenden können, um die Profile zu konfigurieren, die Sie berechnen möchten. Sie führen dann das Paket aus, das den Datenprofilerstellungs-Task enthält, um die Profile zu berechnen. Der Task speichert die Profilausgabe im XML-Format in einer Datei oder Paketvariablen.  
  
 **Weitere Informationen finden Sie unter:** [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md)  
  
 **Schritt 2: Überprüfen der Profile, die der Datenprofilerstellungs-Task berechnet**  
 Wenn Sie die vom Datenprofilerstellungs-Task berechneten Datenprofile anzeigen möchten, senden Sie die Ausgabe an eine Datei, und verwenden Sie dann den Datenprofil-Viewer. Dieser Viewer ist ein eigenständiges Hilfsprogramm, das die Profilausgabe im Zusammenfassungs- und Detailformat mit optionaler Drilldownfunktion anzeigt.  
  
 **Weitere Informationen finden Sie unter:** [Datenprofil-Viewer](../../integration-services/control-flow/data-profile-viewer.md)  
  
### <a name="addition-of-conditional-logic-to-the-data-profiling-workflow"></a>Hinzufügen von Bedingungslogik zum Datenprofilerstellungs-Workflow  
 Der Datenprofilerstellungs-Task verfügt über keine integrierten Funktionen, die eine Verwendung von Bedingungslogik ermöglichen, um diesen Task auf der Grundlage der Profilausgabe mit Downstream-Tasks zu verbinden. Mit minimalem Programmieraufwand können Sie diese Logik jedoch problemlos einem Skripttask hinzufügen. Der Skripttask könnte beispielsweise eine XPath-Abfrage für die Ausgabedatei des Datenprofilerstellungs-Tasks ausführen. Durch die Abfrage könnte bestimmt werden, ob der Prozentwert von NULL-Werten in einer bestimmten Spalte einen bestimmten Schwellenwert überschreitet. Wenn der Prozentwert den Schwellenwert überschreitet, könnten Sie das Paket unterbrechen und das Problem in den Quelldaten vor dem Fortsetzen beheben. Weitere Informationen finden Sie unter [Einschließen eines Datenprofilerstellungs-Tasks in den Paketworkflow](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Datenprofiler-Schema](http://go.microsoft.com/fwlink/?LinkId=251524)  
  
  
