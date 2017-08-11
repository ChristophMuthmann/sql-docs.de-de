---
title: "Bericht und die Momentaufnahme Größe überschreiten | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- large reports
- maximum report size
- size [SQL Server], reports
- report size [Reporting Services]
- reports [Reporting Services], size
- denial of service attacks [Reporting Services]
ms.assetid: 1e3be259-d453-4802-b2f5-6b81ef607edf
caps.latest.revision: 48
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8a101dd362ea9ec71a0d4e75347bea60171cd8d1
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="report-and-snapshot-size-limits"></a>Größenbeschränkungen für Berichte und Momentaufnahmen
  Mithilfe der Informationen in diesem Thema können Administratoren, die eine [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bereitstellung verwalten, mehr zu Größenbeschränkungen für einen Bericht erfahren, der auf einem Berichtsserver veröffentlicht, zur Laufzeit gerendert und in einem Dateisystem gespeichert wird. In diesem Thema erhalten Sie zudem eine praktische Anleitung zum Ermitteln der Größe einer Berichtsserver-Datenbank und eine Beschreibung zur Auswirkung der Größe von Momentaufnahmen auf die Serverleistung.  
  
## <a name="maximum-size-for-published-reports"></a>Maximale Größe für veröffentlichte Berichte  
 Auf dem Berichtsserver basiert die Größe von Berichten und Modellen auf der Größe der Berichtsdefinitionsdateien (RDL) und Berichtsmodelldateien (SMD), die Sie auf einem Berichtsserver veröffentlichen. Die Größe eines von Ihnen veröffentlichten Berichts wird nicht vom Berichtsserver beschränkt. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] erzwingt jedoch eine maximale Größe für Elemente, die an den Server gesendet werden. Standardmäßig liegt dieser Höchstwert bei 4 MB. Wenn Sie auf einem Berichtsserver eine Datei hochladen oder veröffentlichen, die diesen Höchstwert überschreitet, wird ein HTTP-Ausnahmefehler gemeldet. In diesem Fall können Sie den Standardwert ändern, indem Sie den Wert des Elements **maxRequestLength** in der Datei Machine.config erhöhen.  
  
 Obwohl ein Berichtsmodell sehr groß sein kann, wird für Berichtsdefinition die Größe von 4 MB nur selten überschritten. Die Größe von Berichten liegt in der Regel im Bereich von Kilobytes (KB). Wenn Sie jedoch eingebettete Bilder einbeziehen, kann die Codierung dieser Bilder zu umfangreichen Berichtsdefinitionen führen, die den 4 MB-Grenzwert übersteigen.  
  
 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] erzwingt einen Grenzwert für bereitgestellte Dateien, um das Risiko von Denial-of-Service-Angriffen auf den Server zu reduzieren. Durch einen höheren Grenzwert wird dieser Schutz teilweise unterlaufen. Erhöhen Sie den Wert nur, wenn Sie sicher sind, dass die Vorteile etwaige zusätzliche Sicherheitsrisiken aufwiegen.  
  
 Beachten Sie, dass der für das **maxRequestLength** -Element festgelegte Wert über den tatsächlichen Größenbeschränkungen liegen muss, die Sie durchsetzen möchten. Sie müssen den Wert vergrößern, um die unvermeidliche Zunahme der HTTP-Anforderungsgröße zu berücksichtigen, die auftritt, nachdem alle Parameter in einem SOAP-Umschlag gekapselt wurden und die Base64-Codierung auf bestimmte Parameter angewendet wurde. Durch die Base64-Codierung nimmt die Größe der ursprünglichen Daten um ca. 33 % zu. Folglich muss der für das **maxRequestLength** -Element angegebene Wert etwa 33 % über der tatsächlichen verwendbaren Elementgröße liegen. Wenn Sie für **maxRequestLength**beispielsweise den Wert 64 MB angeben, können Sie im Normalfall davon ausgehen, dass die maximale Größe für Berichtsdateien, die an den Berichtsserver gesendet werden, ungefähr 48 MB entspricht.  
  
## <a name="report-size-in-memory"></a>Berichtsgröße im Arbeitsspeicher  
 Wenn Sie einen Bericht ausführen, ist die Berichtsgröße gleich der im Bericht zurückgegebenen Datenmenge zuzüglich der Größe des Ausgabedatenstroms. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nicht begrenzt. Der obere Grenzwert für die Größe wird vom Systemarbeitsspeicher bestimmt (ein Berichtsserver verwendet beim Rendern eines Berichts standardmäßig den gesamten verfügbaren konfigurierten Arbeitsspeicher). Sie können jedoch Konfigurationseinstellungen festlegen, um Grenzwerte für den Arbeitsspeicher und Speicherverwaltungsrichtlinien zu definieren. Weitere Informationen finden Sie unter [Konfigurieren von verfügbarem Speicher für Berichtsserveranwendungen](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).  
  
 Die Größe der einzelnen Berichte kann sich beträchtlich unterscheiden. Dies hängt von der zurückgegebenen Datenmenge und vom Renderingformat ab, das Sie für den Bericht verwenden. Ein parametrisierter Bericht kann abhängig von der Auswirkung der Parameterwerte auf die Abfrageergebnisse größer oder kleiner sein. Das von Ihnen ausgewählte Ausgabeformat des Berichts wirkt sich folgendermaßen auf die Größe des Berichts aus:  
  
-   Der Bericht wird von HTML seitenweise verarbeitet. Da der Bericht in kleineren Einheiten verarbeitet wird, ist zum Verarbeiten bestimmter Segmente weniger Arbeitsspeicher erforderlich.  
  
-   Von PDF, Excel, TIFF und CSV wird der gesamte Bericht im Arbeitsspeicher verarbeitet, bevor der Bericht dem Benutzer angezeigt wird.  
  
 Sie können das Berichtsausführungsprotokoll anzeigen, um die Größe eines gerenderten Berichts zu ermitteln. Weitere Informationen finden Sie unter [Berichtsserverausführungsprotokoll und die ExecutionLog3-Ansicht](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 Wenn Sie die Größe eines gerenderten Berichts auf einem Datenträger berechnen möchten, können Sie den Bericht exportieren und anschließend im Dateisystem speichern (die gespeicherte Datei enthält Informationen zu den Daten und zur Formatierung des Berichts).  
  
 Der einzige feste Grenzwert für die Größe von Berichten besteht beim Rendern in das Excel-Format. Arbeitsblätter dürfen maximal 65536 Zeilen oder 256 Spalten enthalten. Bei anderen Renderingformaten bestehen diese Beschränkungen nicht. Die Größe wird daher nur durch die Anzahl der Ressourcen auf dem Server beschränkt.  
  
> [!NOTE]  
>  Die Verarbeitung und das Rendern von Berichten erfolgt nur im Arbeitsspeicher. Wenn Sie über umfangreiche Berichte oder eine große Anzahl von Benutzern verfügen, sollten Sie eine Kapazitätsplanung vornehmen, um sicherzustellen, dass die Berichtsserverbereitstellung auf einem für die Benutzer zufrieden stellenden Niveau ausgeführt wird. Weitere Informationen zu Tools und Richtlinien stehen in den folgenden Publikationen auf MSDN zur Verfügung: [Skalierbarkeits- und Leistungsplanung bei Reporting Services](http://go.microsoft.com/fwlink/?LinkID=70650) und [Verwenden von Visual Studio 2005 zum Ausführen von Ladetests für einen SQL Server 2005 Reporting Services-Berichtsserver](http://go.microsoft.com/fwlink/?LinkID=77519).  
  
## <a name="measuring-snapshot-storage"></a>Messen des Speichers für Momentaufnahmen  
 Die Größe einer Momentaufnahme ist direkt proportional zur Datenmenge im Bericht. Momentaufnahmen sind in der Regel viel größer als andere Elemente, die auf einem Berichtsserver gespeichert sind. Die Größe von Momentaufnahmen liegt in der Regel zwischen einigen Megabyte und mehreren zehn Megabyte. Wenn Sie über umfangreiche Berichte verfügen, können Sie davon ausgehen, dass die Momentaufnahmen noch größer sind. Je nachdem, wie häufig Sie Momentaufnahmen verwenden und wie Sie den Berichtsverlauf konfigurieren, kann sich der für die Berichtsserver-Datenbank erforderliche Speicherplatz innerhalb eines kurzen Zeitraums schnell erhöhen.  
  
 Standardmäßig sind die Datenbanken **reportserver** und **reportservertempdb** so festgelegt, dass eine automatische Vergrößerung erfolgt. Obwohl sich die Datenbankgröße automatisch erhöhen kann, kann sie sich nicht automatisch verringern. Wenn für die **reportserver** -Datenbank zusätzliche Kapazitäten zur Verfügung stehen, da Sie Momentaufnahmen gelöscht haben, müssen Sie die Größe manuell reduzieren, um Speicherplatz zu gewinnen. Wenn sich die Größe der **reportservertempdb** -Datenbank erhöht, da eine ungewöhnlich große Anzahl von interaktiven Berichten aufgenommen wurde, bleibt diese Einstellung für die Speicherplatzzuordnung entsprechend erhalten, bis Sie sie reduzieren.  
  
 Sie können die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehle ausführen, um die Größe der Berichtsserver-Datenbanken zu ermitteln. Durch regelmäßiges Berechnen der Gesamtgröße von Datenbanken können Sie im Verlauf der Zeit entsprechende Schätzungen zur Zuordnung von Speicherplatz für die Berichtsserver-Datenbank vornehmen. Mit den folgenden Anweisungen wird der derzeit verwendete Speicherplatz ermittelt (bei den Anweisungen wird davon ausgegangen, dass Sie Standarddatenbanknamen verwenden):  
  
```  
USE ReportServer  
EXEC sp_spaceused  
```  
  
## <a name="snapshot-size-and-report-server-performance"></a>Größe von Momentaufnahmen und Berichtsserverleistung  
 Die Größe von Momentaufnahmen wirkt sich auf die Serverleistung aus, wenn der Bericht verarbeitet und gerendert wird. Renderingvorgänge wirken sich am stärksten auf die Serverleistung aus. Daher können bei einer großen Momentaufnahme Verzögerungen auftreten, wenn Benutzer den Bericht anfordern. In Abhängigkeit von der Anzahl der Benutzer können Verzögerungen auftreten, wenn die Momentaufnahmegröße 100 Megabyte übersteigt.  
  
 Gehen Sie folgendermaßen vor, um die Leistungsverzögerungen aufgrund umfangreicher Momentaufnahmen zu minimieren:  
  
-   Stellen Sie den Berichtsserver und den [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] auf separaten Computern bereit.  
  
-   Fügen Sie weiteren Systemarbeitsspeicher hinzu.  
  
-   Lesen Sie das Dokument "Skalierbarkeits- und Leistungsplanung bei Reporting Services" auf der MSDN-Website, um Informationen zu den bewährten Methoden zum Konfigurieren eines Berichtsservers für Unternehmen zu erhalten.  
  
 Die Menge der in einer Berichtsserver-Datenbank gespeicherten Momentaufnahmen stellt an sich keinen Leistungsfaktor dar. Sie können eine große Anzahl von Momentaufnahmen speichern, ohne die Serverleistung zu beeinträchtigen. Sie können Momentaufnahmen über einen unbegrenzten Zeitraum speichern. Beachten Sie jedoch, dass der Berichtsverlauf konfiguriert werden kann. Wenn ein Berichtsserveradministrator den Grenzwert für den Berichtsverlauf senkt, gehen Berichtsverläufe, die Sie aufbewahren möchten, möglicherweise verloren. Wenn Sie den Bericht löschen, wird auch der gesamte Berichtsverlauf gelöscht.  
  
## <a name="see-also"></a>Siehe auch  
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Berichtsserver-Datenbank &#40; SSRS im einheitlichen Modus &#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Process Large Reports (Verarbeiten von großen Berichten)](../../reporting-services/report-server/process-large-reports.md)  
  
  
