---
title: "Generieren von Sicherungsdateien für die Paketausführung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: troubleshooting
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: be1121099a2ca2bed5e145e47c8720f57e6fc5d9
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="generating-dump-files-for-package-execution"></a>Generieren von Dumpdateien für die Paketausführung
  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]können Sie Debugdumpdateien erstellen, die Informationen über die Ausführung eines Pakets enthalten. Die Informationen in diesen Dateien können Ihnen bei der Behebung von Problemen bei der Paketausführung helfen.  
  
> **HINWEIS!** Debugdumpdateien können vertrauliche Informationen enthalten. Zum Schutz vertraulicher Informationen können Sie eine Zugriffssteuerungsliste verwenden, um den Zugriff auf die Dateien einzuschränken oder die Dateien in einen Ordner mit eingeschränktem Zugriff zu kopieren. Bevor Sie Ihre Debugdateien beispielsweise an [!INCLUDE[msCoName](../../includes/msconame-md.md)] Support Services senden, empfehlen wir, sensible oder vertrauliche Informationen zu entfernen.  
  
 Wenn Sie auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server ein Projekt bereitstellen, können Sie Dumpdateien erstellen, die Informationen über die Ausführung der im Projekt enthaltenen Pakete bereitstellen. Wenn der Prozess "ISServerExec.exe" beendet wird, werden die Dumpdateien erstellt. Sie können angeben, dass eine Dumpdatei erstellt wird, wenn Fehler während der Paketausführung auftreten, indem Sie im Dialogfeld **Paket ausführen** die Option für die **Speicherung von Dumps bei Fehlern** auswählen. Außerdem können Sie Folgendes als gespeicherte Prozeduren verwenden.  
  
-   [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
     Rufen Sie diese gespeicherte Prozedur auf, um zu konfigurieren, dass eine Dumpdatei erstellt wird, wenn ein Fehler oder ein Ereignis auftritt, und wenn spezifische Ereignisse während einer Paketausführung auftreten.  
  
-   [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
  
     Rufen Sie diese gespeicherte Prozedur auf, um ein ausgeführtes Paket zu veranlassen, eine Dumpdatei anzuhalten und zu erstellen.  
  
 Wenn Sie das Paketbereitstellungsmodell verwenden, erstellen Sie die Debugdumpdateien, indem Sie entweder mit dem Hilfsprogramm **dtexec** oder dem Hilfsprogramm **dtutil** in der Befehlszeile eine Debugdumpoption angeben. Weitere Informationen finden Sie unter [dtexec Utility](../../integration-services/packages/dtexec-utility.md) und [dtutil Utility](../../integration-services/dtutil-utility.md). Weitere Informationen zu Paketbereitstellungsmodellen finden Sie unter [Bereitstellung von Integration Services-Projekten (SSIS) und -Paketen](https://msdn.microsoft.com/library/hh213290.aspx) und [Legacy-Paketbereitstellung &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).   
  
## <a name="debug-dump-file-format"></a>Format der Debugdumpdateien  
 Wenn Sie eine Debugdumpoption angeben, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die folgenden Debugdumpdateien:  
  
-   Eine .mdmp-Debugdumpdatei. Hierbei handelt es sich um eine Binärdatei.  
  
-   Eine .tmp-Debugdumpdatei. Hierbei handelt es sich um eine textformatierte Datei.  
  
 In der Standardeinstellung speichert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] diese Dateien im Ordner *\<Laufwerk>:*\Programme\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
 In der folgenden Tabelle werden nur bestimmte Abschnitte der TMP-Datei beschrieben. Die TMP-Datei schließt weitere Daten ein, die nicht in der Tabelle aufgeführt werden.  
  
|Art der Informationen|Description|Beispiel|  
|-------------------------|-----------------|-------------|  
|Umgebung|Betriebssystemversion, Speicherauslastungsdaten, Prozess-ID und Name des Prozessimages. Die Umgebungsinformationen befinden sich am Anfang der TMP-Datei.|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Programme\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory: 58% in use. Physical: 845M/2044M  Paging: 2404M/4095M (avail/total)|  
|Pfad und Version der Dynamic Link Library (DLL)|Pfad und Versionsnummer jeder DLL, die das System während der Verarbeitung eines Pakets lädt.|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module: C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module: C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|Letzte Meldungen|Letzte Meldungen, die vom System ausgegeben wurden. Schließt die Zeit, Typ, Beschreibung und Thread-ID jeder Meldung ein.|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( @ 0282F1A8 )<br /><br /> [E:3]         Time Stamp: 2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID: 2368           (ThreadID)<br /><br /> [E:3]         Event Name: OnError                        (EventName)<br /><br /> [E:3]         Source Name:                (SourceName)<br /><br /> [E:3]         Source ID:                        (SourceID)<br /><br /> [E:3]         Execution ID:                 (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         Description: The component is missing, not registered, not upgradeable, or missing required interfaces. Die Kontaktinformationen für diese Komponente lauten "".|  
  
## <a name="related-information"></a>Verwandte Informationen  
 [Paket ausführen (Dialogfeld)](../../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
  
