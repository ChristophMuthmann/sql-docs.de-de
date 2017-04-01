---
title: "Ereignisprotokollierung durch den Integration Services-Dienst | Microsoft Docs"
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
  - "Dienst [Integration Services], Ereignisse"
  - "Ereignisse [Integration Services], Dienst"
  - "Integration Services-Dienst, Ereignisse"
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Ereignisprotokollierung durch den Integration Services-Dienst
  Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst protokolliert verschiedene Meldungen in das Windows-Anwendungsereignisprotokoll. Der Dienst Paket protokolliert diese Meldungen, wenn er startet, wenn er anhält und wenn bestimmte Probleme auftreten.  
  
 Dieses Thema enthält Informationen über die allgemeinen Ereignismeldungen, die von einem Dienst im Anwendungsereignisprotokoll protokolliert werden. Der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst protokolliert alle in diesem Thema beschriebenen Meldungen mit der Ereignisquelle SQLISService.  
  
 Allgemeine Informationen zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Dienst finden Sie unter [Integration Services-Dienst &#40;SSIS-Dienst&#41;](../../integration-services/service/integration-services-service-ssis-service.md).  
  
## Meldungen zum Dienststatus  
 Wenn Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zur Installation auswählen, wird der Dienst [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installiert und gestartet, und der Starttyp wird auf Automatisch gesetzt.  
  
|Ereignis-ID|Symbolischer Name|Text|Hinweise|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|Starten des [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Diensts.|Der Dienst wird gerade gestartet.|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Der  -Dienst wurde gestartet.|Der Dienst wurde gestartet.|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Diensts.%nFehler: %1|Der Dienst konnte nicht gestartet werden. Dass der Dienst nicht starten konnte, könnte die Folge einer beschädigten Installation oder eines unpassenden Dienstkontos sein.|  
|258|DTS_MSG_SERVER_STOPPING|Der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst wird angehalten.% n%nAlle ausgeführten Pakete beim Beenden anhalten: %1|Der Dienst wird angehalten, und wenn der Dienst so konfiguriert ist, hält er alle ausgeführten Pakete an. In der Konfigurationsdatei können Sie den Wert True oder False festlegen. Dieser Wert bestimmt, ob der Dienst die Ausführung von Paketen beendet, wenn der Dienst selbst beendet wird. Die Meldung für dieses Ereignis enthält den Wert dieser Einstellung.|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst wurde beendet.%nServerversion %1|Der Dienst wurde beendet.|  
  
## Meldungen über die Konfigurationsdatei  
 Einstellungen für den [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst werden in einer XML-Datei gespeichert, die Sie ändern können. Weitere Informationen finden Sie unter [Konfigurieren des Integration Services-Diensts &#40;SSIS-Dienst&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
|Ereignis-ID|Symbolischer Name|Text|Hinweise|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst: %nRegistrierungseinstellung mit Angabe der Konfigurationsdatei ist nicht vorhanden. %nEs wird versucht, die Standardkonfigurationsdatei zu laden.|Der Registrierungseintrag, der den Pfad der Konfigurationsdatei enthält, ist nicht vorhanden oder leer.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst ist nicht vorhanden.%nWird mit Standardeinstellungen geladen.|Die Konfigurationsdatei ist am angegebenen Speicherort nicht vorhanden.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst.%nFehler beim Lesen der Konfigurationsdatei: %1%n%nServer wird mit Standardeinstellungen geladen.|Die Konfigurationsdatei konnte nicht gelesen werden oder ist nicht gültig. Dieser Fehler könnte die Folge eines XML-Syntaxfehlers in der Datei sein.|  
  
## Andere Meldungen  
  
|Ereignis-ID|Symbolischer Name|Text|Hinweise|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Dienst: Ausführung des Pakets wird beendet.% nPaketinstanz-ID:%1%nPaket-ID:%2%nPaketname:%3%nPaketbeschreibung:%4%nPaket|Der Dienst versucht, ein ausgeführtes Paket zu beenden. Sie können ausgeführte Pakete in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]überwachen und anhalten. Weitere Informationen zum Verwalten von Paketen in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] finden Sie unter [Paketverwaltung &#40;SSIS-Dienst&#41;](../../integration-services/service/package-management-ssis-service.md).|  
  
## Verwandte Aufgaben  
 Informationen zum Anzeigen von Protokolleinträgen finden Sie unter [Anzeigen der Protokolleinträge im Fenster „Protokollereignisse“](../../integration-services/performance/view-log-entries-in-the-log-events-window.md).  
  
## Siehe auch  
 [Durch ein Integration Services-Paket protokollierte Ereignisse](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
  
  