---
title: Export und Importieren von DQS-Wissensdatenbanken mit DQSInstaller.exe | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8234c63b-a018-4e55-8184-9a6bdf03274d
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8060994f8f7da132b848150f1c005140b9eba2c6
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="export-and-import-dqs-knowledge-bases-using-dqsinstallerexe"></a>Export und Importieren von DQS-Wissensdatenbanken mit DQSInstaller.exe
  Bei einer vorhandenen DQS-Installation können Sie alle Wissensdatenbanken auf dem [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] gleichzeitig in eine DQS-Sicherungsdatei (DQSB) exportieren und dann später die DQSB-Datei verwenden, um alle Wissensdatenbanken gleichzeitig auf einen anderen [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] zu importieren, indem Sie die Datei DQSInstaller.exe an der Eingabeaufforderung ausführen. Weitere Informationen zum Ausführen von DQSInstaller.exe von der Eingabeaufforderung finden Sie unter [Run DQSInstaller.exe from Command Prompt](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#CommandPrompt) in [Run DQSInstaller.exe to Complete Data Quality Server Installation](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
 Diese Funktion ermöglicht es Ihnen, sofort eine Sicherung *aller* Wissensdatenbanken in [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] durchzuführen, ohne jede Wissensdatenbank einzeln mithilfe des [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]in eine DQS-Datei exportieren zu müssen. Auf ähnliche Weise können Sie *alle* Wissensdatenbanken gleichzeitig aus der Sicherungsdatei in einen anderen [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] importieren, ohne jede Wissensdatenbank einzeln aus einer DQS-Datei mithilfe des [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]importieren zu müssen. Dies ist besonders nützlich beim Sichern und Wiederherstellen der Wissensdatenbanken, wenn Sie [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] auf einem Computer deinstallieren und dann auf einem anderen Computer neu installieren. Sie können ganz einfach alle Wissensdatenbanken in einer vorhandenen Installation von [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in eine DQS-Sicherungsdatei (.dqsb) exportieren und dann alle Wissensdatenbanken aus der Sicherungsdatei importieren, nachdem Sie [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] auf einem anderen Computer installiert haben.  
  
##  <a name="export"></a> Exportieren von Wissensdatenbanken in eine DQSB-Datei  
 Sie können jederzeit alle Wissensdatenbanken aus dem vorhandenen [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] oder beim Deinstallieren von [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]exportieren.  
  
-   Um alle Wissensdatenbanken aus einem [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] in eine DQS-Sicherungsdatei (.dqsb) zu exportieren, führen Sie DQSInstaller.exe mit dem `exportkbs` -Parameter von der Eingabeaufforderung, zusammen mit dem vollständigen Pfad und dem Dateinamen, wohin Sie die Wissensdatenbanken exportieren möchten, aus. Beispiel: Um alle Wissensdatenbanken in die Datei DQSBackup.dqsb auf Laufwerk C: zu exportieren:  
  
    ```  
    dqsinstaller.exe –exportkbs c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Wenn der angegebene Dateiname bereits am festgelegten Speicherort vorhanden ist, werden Sie vom Installationsprogramm gefragt, ob die Datei überschrieben werden soll.  
  
-   Um alle Wissensdatenbanken bei der Deinstallation von [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]in eine DQS-Sicherungsdatei zu exportieren, führen Sie DQSInstaller.exe mit dem `uninstall` -Parameter von der Eingabeaufforderung, zusammen mit dem vollständigen Pfad und dem Dateinamen, wohin Sie die Wissensdatenbanken exportieren möchten, aus. Beispiel: Um alle Wissensdatenbanken in die Datei DQSBackup.dqsb auf Laufwerk C: zu exportieren und dann [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]zu deinstallieren:  
  
    ```  
    dqsinstaller.exe –uninstall c:\DQSBackup.dqsb  
    ```  
  
    > [!NOTE]  
    >  Wenn Sie beim Deinstallieren von [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] von der Eingabeaufforderung unter Verwendung des `uninstall` -Parameters nicht den vollständigen Pfad und den Dateinamen der DQS-Sicherungsdatei angeben, wird eine Meldung mit den Hinweis angezeigt, dass alle Wissensdatenbanken gelöscht werden, und ermöglicht Ihnen auszuwählen, ob der Deinstallationsvorgang fortgesetzt werden soll.  
  
##  <a name="import"></a> Importieren von Wissensdatenbanken aus einer DQSB-Datei  
 Sie können alle Wissensdatenbanken aus einer DQS-Sicherungsdatei (DQSB-Format) importieren, nachdem Sie die [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] -Installation abgeschlossen haben. Um Wissensdatenbanken zu importieren, benötigen Sie eine gültige DQS-Sicherungsdatei (.dqsb).  
  
 Führen Sie DQSInstaller.exe mit dem `importkbs` -Parameter von der Eingabeaufforderung, zusammen mit dem vollständigen Pfad und dem Dateinamen, von wo Sie die Wissensdatenbanken importieren möchten, aus. Beispiel: Um alle Wissensdatenbanken aus der Datei DQSBackup.dqsb auf Laufwerk C: zu importieren:  
  
```  
dqsinstaller.exe –importkbs c:\DQSBackup.dqsb  
```  
  
 Wenn auf dem [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] Wissensdatenbanken mit dem gleichen Namen wie den zu importierenden vorhanden sind, wird an die Namen der importierten Wissensdatenbanken ein Unterstrich (_) angefügt, gefolgt von einem ganzzahligen Wert, beginnend mit 1. Wenn die Domäne "Firmenname" z. B. doppelt ist, ist der importierte Domänenname "Firmenname_1".  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausführen von DQSInstaller.exe zum Abschließen der Installation von Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)   
 [Installieren von Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Exportieren einer Wissensdatenbank in eine DQS-Datei](../../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)   
 [Importieren einer Wissensdatenbank aus einer DQS-Datei](../../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)  
  
  
