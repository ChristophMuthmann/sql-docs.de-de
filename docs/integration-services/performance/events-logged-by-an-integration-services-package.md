---
title: Durch ein Integration Services-Paket protokollierte Ereignisse | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- package [Integration Services], events
- events [Integration Services], package
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: df4b2e68a9b024ed2911d4b5c1d5bcea8984ae15
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="events-logged-by-an-integration-services-package"></a>Durch ein Integration Services-Paket protokollierte Ereignisse
  Ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket protokolliert verschiedene Ereignismeldungen in das Windows-Anwendungsereignisprotokoll. Ein Paket protokolliert diese Meldungen, wenn das Paket startet, wenn das Paket anhält und wenn bestimmte Probleme auftreten.  
  
 Dieses Thema enthält Informationen über die allgemeinen Ereignismeldungen, die von einem Paket im Anwendungsereignisprotokoll protokolliert werden. Standardmäßig protokolliert ein Paket einige dieser Meldungen, auch wenn Sie die Protokollfunktion für das Paket nicht aktiviert haben. Andere Meldungen werden hingegen vom Paket nur protokolliert, wenn Sie die Protokollfunktion für das Paket aktiviert haben. Unabhängig davon, ob das Paket diese Meldungen standardmäßig oder aufgrund der aktivierten Protokollfunktion protokolliert, ist die Ereignisquelle für die Meldungen SQLISPackage.  
  
 Allgemeine Informationen zum Ausführen von SSIS-Paketen finden Sie unter [Ausführung von Projekten und Paketen](../packages/run-integration-services-ssis-packages.md).  
  
 Informationen zur Behandlung von Problemen bei der Ausführung von Paketen finden Sie unter [Behandlung von Problemen mit Paketausführungstools](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="messages-about-the-status-of-the-package"></a>Meldungen zum Paketstatus  
 Wenn Sie ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket ausführen, protokolliert das Paket normalerweise verschiedene Meldungen über den Fortschritt und den Status des Pakets. Die entsprechenden Meldungen sind in der folgenden Tabelle aufgeführt.  
  
> [!NOTE]  
>  Das Paket protokolliert die Meldungen in der folgenden Tabelle, auch wenn Sie die Protokollfunktion für das Paket nicht aktiviert haben.  
  
|Ereignis-ID|Symbolischer Name|Text|Hinweise|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|Das Paket "" wurde gestartet.|Die Ausführung des Pakets wurde begonnen.|  
|12289|DTS_MSG_PACKAGESUCCESS|Das Paket "" wurde erfolgreich beendet.|Das Paket wurde erfolgreich ausgeführt und wird zurzeit nicht mehr ausgeführt.|  
|12290|DTS_MSG_PACKAGECANCEL|Das Paket "%1!s!" wurde abgebrochen.|Das Paket wird nicht mehr ausgeführt, da es abgebrochen wurde.|  
|12291|DTS_MSG_PACKAGEFAILURE|Fehler beim Paket "".|Das Paket konnte nicht erfolgreich ausgeführt werden und wurde angehalten.|  
  
 Bei einer Neuinstallation wird [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] standardmäßig so konfiguriert, dass bestimmte Ereignisse im Zusammenhang mit der Ausführung von Paketen im Anwendungsereignisprotokoll nicht protokolliert werden. Mit dieser Einstellung wird verhindert, dass zu viele Ereignisprotokolleinträge erstellt werden, wenn Sie die Datensammler-Funktion der aktuellen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Zu den nicht protokollierten Ereignissen gehören EventID 12288 "Paket wurde gestartet" und EventID 12289 "Paket wurde erfolgreich beendet". Wenn Sie diese Ereignisse im Anwendungsereignisprotokoll protokollieren möchten, öffnen Sie die Registrierung zum Bearbeiten. Suchen Sie anschließend in der Registrierung den Knoten „HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS“, und ändern Sie den DWORD-Wert der Einstellung LogPackageExecutionToEventLog von 0 auf 1. Bei einer Upgradeinstallation wird [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] jedoch zum Protokollieren dieser zwei Ereignisse konfiguriert. Wenn Sie die Protokollierung deaktivieren möchten, ändern Sie den Wert der LogPackageExecutionToEventLog-Einstellung von 1 in 0.  
  
## <a name="messages-associated-with-package-logging"></a>Mit der Paketprotokollierung verknüpfte Meldungen  
 Wenn Sie die Protokollfunktion für das Paket aktiviert haben, ist das Anwendungsereignisprotokoll eines der Ziele, die von den optionalen Protokollierungsfunktionen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen unterstützt werden. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Wenn Sie die Protokollfunktion für das Paket aktiviert haben und der Protokollspeicherort das Anwendungsereignisprotokoll ist, protokolliert das Paket Einträge, für die folgende Informationen gelten:  
  
-   Meldungen über die Phase, in der sich das Paket bei seiner Ausführung befindet.  
  
-   Meldungen über besondere Ereignisse, die auftreten, während das Paket ausgeführt wird.  
  
### <a name="messages-about-the-stages-of-package-execution"></a>Meldungen zu den Phasen der Paketausführung  
  
|Ereignis-ID|Symbolischer Name|Text|Hinweise|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Dieses generische Format wird von verschiedenen Meldungen verwendet, wenn Sie die Paketprotokollierung für das Anwendungsereignisprotokoll konfigurieren.|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Das Paket wurde gestartet.|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Die Überprüfung des Objekts beginnt in Kürze.|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Die Überprüfung des Objekts wurde beendet.|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Diese generische Meldung gibt Aufschluss über den Paketfortschritt.|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Das Objekt hat seine Arbeit beendet.|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Die Ausführung des Pakets ist abgeschlossen.|  
  
### <a name="messages-about-events-that-occur"></a>Meldungen über Ereignisse, die auftreten  
 In der folgenden Tabelle werden nur einige der Meldungen aufgeführt, die aus Ereignissen resultieren. Eine umfangreichere Liste von Fehler-, Warnungs- und Informationsmeldungen, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet werden, finden Sie unter [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md).  
  
|Ereignis-ID|Symbolischer Name|Text|Hinweise|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Der Task ist fehlgeschlagen.|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Diese Meldung meldet einen Fehler, der aufgetreten ist.|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Diese Meldung meldet eine Warnung, die aufgetreten ist.|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|Ereignisname: %1%r Meldung: %9%r Operator: %2%r Quellenname: %3%r Quellen-ID: %4%r Ausführungs-ID: %5%r Startzeit: %6%r Beendigungszeit: %7%r Datencode: %8|Diese Meldung enthält Informationen, die nicht mit einem Fehler oder einer Warnung verbunden sind.|  

## <a name="view-log-entries-in-the-log-events-window"></a>Anzeigen der Protokolleinträge im Fenster „Protokollereignisse“
  In diesem Verfahren wird das Ausführen eines Pakets und das Anzeigen der geschriebenen Protokolleinträge beschrieben. Sie können die Protokolleinträge in Echtzeit anzeigen. Die im Fenster **Protokollereignisse** geschriebenen Protokolleinträge können auch kopiert und für die spätere Analyse gespeichert werden.  
  
 Dabei müssen die Protokolleinträge nicht in ein Protokoll geschrieben werden, um die Einträge in das Fenster **Protokollereignisse** zu schreiben.  
  
### <a name="to-view-log-entries"></a>So zeigen Sie Protokolleinträge an  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie im Menü **SSIS** auf **Protokollereignisse**. Sie können das Fenster **Protokollereignisse** auch anzeigen, indem Sie im Dialogfeld **Optionen** auf der Seite **Tastatur** den Befehl View.LogEvents einer beliebigen Tastenkombination zuordnen.  
  
3.  Klicken Sie im Menü **Debuggen** auf **Debuggen starten**.  
  
     Sobald die Laufzeit feststellt, dass das Protokoll für Ereignisse und benutzerdefinierte Meldungen aktiviert wurde, werden die Protokolleinträge für die Ereignisse und Meldungen in das Fenster **Protokollereignisse** geschrieben.  
  
4.  Klicken Sie im Menü **Debuggen** auf **Debuggen beenden**.  
  
     Die Protokolleinträge sind so lange im Fenster **Protokollereignisse** verfügbar, bis Sie das Paket erneut ausführen, ein anderes Paket ausführen oder [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]schließen.  
  
5.  Zeigen Sie die Protokolleinträge im Fenster **Protokollereignisse** an.  
  
6.  Klicken Sie optional auf die zu kopierenden Protokolleinträge, klicken Sie auf die rechte Maustaste, und klicken dann Sie auf **Kopieren**.  
  
7.  Doppelklicken Sie optional auf einen Protokolleintrag, und zeigen Sie die Details eines einzelnen Protokolleintrags im Dialogfeld **Protokolleintrag** an.  
  
8.  Klicken Sie im Dialogfeld **Protokolleintrag** auf die Nach-Oben- oder Nach-Unten-Taste, um den vorigen oder nächsten Protokolleintrag anzuzeigen, und klicken Sie zum Kopieren des Protokolleintrags auf das Kopiersymbol.  
  
9. Öffnen Sie einen Texteditor, um den Protokolleintrag in eine Textdatei einzufügen und zu speichern.

