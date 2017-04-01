---
title: "Ausf&#252;hren des Bereitstellungs-Assistenten f&#252;r Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Bereitstellungs-Assistent für Analysis Services, ausführen"
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
caps.latest.revision: 41
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 38
---
# Ausf&#252;hren des Bereitstellungs-Assistenten f&#252;r Analysis Services
  Wenn Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zum Bereitstellen eines [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts verwenden, gibt es folgende Möglichkeiten, um diesen Assistenten auszuführen:  
  
-   **Interaktiv** Bei interaktiver Ausführung generiert der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf der Basis der durch die Benutzereingabe interaktiv geänderten Eingabedateien ein XML-Bereitstellungsskript. Der Assistent wendet alle Änderungen durch den Benutzer ausschließlich auf das Bereitstellungsskript an. Der Assistent nimmt dabei keine Änderungen an den Eingabedateien vor. Weitere Informationen zu den Eingabedateien finden Sie unter [Grundlegendes zu den zum Erstellen des Bereitstellungsskripts verwendeten Eingabedateien](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md).  
  
-   **An der Eingabeaufforderung** Wenn der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung ausgeführt wird, generiert er auf der Basis der Schalter, die Sie beim Ausführen des Assistenten verwenden, ein \(XMLA\)-Bereitstellungsskript (XML for Analysis). Der Assistent kann dann einen der folgenden Schritte ausführen: den Benutzer zur Eingabe auffordern und die Eingabedateien entsprechend der Benutzereingabe ändern, eine unbeaufsichtigte Bereitstellung mithilfe der unveränderten Eingabedateien durchführen oder ein Bereitstellungsskript erstellen, das vom Benutzer zu einem späteren Zeitpunkt verwendet werden kann.  
  
## Interaktives Ausführen des Bereitstellungs-Assistenten für Analysis Services  
 Wenn Sie den Bereitstellungs-Assistenten für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interaktiv ausführen, liest er die Werte aus den Eingabedateien und präsentiert Ihnen diese Informationen. Sie können diese Eingabewerte – z. B. das Bereitstellungsziel, Konfigurationseinstellungen, Bereitstellungsoptionen und Kennwörter für Verbindungszeichenfolgen – je nach Bedarf ändern oder unverändert übernehmen. Wenn Sie Änderungen an den Eingabewerten vornehmen, verwendet der Assistent diese Änderungen beim Generieren des XMLA-Bereitstellungsskripts. Der Assistent nimmt dabei jedoch keine Änderungen an den Werten in der Eingabedatei vor.  
  
> [!NOTE]  
>  Wenn Sie möchten, dass der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Änderungen an den Eingabewerten vornimmt, müssen Sie den Assistenten an der Eingabeaufforderung ausführen und dabei festlegen, dass der Assistent im Antwortmodus ausgeführt wird.  
  
 Nachdem Sie die Eingabewerte überprüft und ggf. geändert haben, generiert der Assistent das XMLA-Bereitstellungsskript. Sie können dieses Bereitstellungsskript entweder sofort auf dem Zielserver ausführen oder zur späteren Verwendung speichern.  
  
#### So führen Sie den Bereitstellungs-Assistenten für Analysis Services interaktiv aus  
  
-   Zeigen Sie im Menü **Start**auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server**, zeigen Sie auf **Analysis Services**, und klicken Sie dann auf **Bereitstellungs-Assistent**.  
  
     – oder –  
  
-   Doppelklicken Sie im Ordner **Projekte** des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]\-Projekts auf die Datei „*\<Projektname\>*.asdatabase“.  
  
    > [!NOTE]  
    >  Wenn Sie die Datei „*\<Projektname\>*.asdatabase“ nicht sofort finden können, verwenden Sie die Suche, und geben Sie dabei „\*.asdatabase“ an.  
  
## Ausführen des Bereitstellungs-Assistenten für Analysis Services an der Eingabeaufforderung  
 Der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] kann auch an der Eingabeaufforderung ausgeführt werden. Wenn Sie den Assistenten an der Eingabeaufforderung ausführen, geben Sie den vollständigen Pfad zur ASDATABASE-Datei an, und führen Sie den Assistenten in einem der folgenden Modi aus:  
  
 **Antwortdateimodus**  
 Im Antwortdateimodus können Sie die Eingabedateien interaktiv ändern, die ursprünglich beim Erstellen des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Projekts in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] generiert wurden. Der Assistent speichert diese geänderten Eingabedateien, bevor er das XMLA-Bereitstellungsskript generiert. Die geänderten Eingabedateien werden dann zum Ausgangspunkt beim nächsten Ausführen des Assistenten.  
  
 Verwenden Sie zum Ausführen des Assistenten im Antwortdateimodus den Schalter **\/a**.  
  
 **Unbeaufsichtigter Modus**  
 Im unbeaufsichtigten Modus führt der Assistent auf der Basis der in den Eingabedateien enthaltenen Informationen eine Bereitstellung im Hintergrund aus, ohne dass dabei in irgendeiner Weise eingegriffen werden muss.  
  
 Verwenden Sie zum Ausführen des Assistenten im unbeaufsichtigten Modus den Schalter **\/s**. Wenn Sie den Assistenten im unbeaufsichtigten Modus ausführen, werden Meldungen an die Konsole ausgegeben oder an eine Protokolldatei (sofern vorhanden).  
  
 **Ausgabemodus**  
 Im Ausgabemodus generiert der Assistent auf der Basis der Eingabedateien ein XMLA-Bereitstellungsskript, das zu einem späteren Zeitpunkt ausgeführt werden kann.  
  
 Verwenden Sie zum Ausführen des Assistenten im Ausgabemodus den Schalter **\/o**, und geben Sie einen Namen für die Ausgabedatei an.  
  
 Weitere Informationen zu diesen Befehlszeilenoptionen finden Sie unter [Bereitstellen von Modelllösungen mit dem Bereitstellungshilfsprogramm](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md).  
  
 Im folgenden Verfahren wird beschrieben, wie der Bereitstellungs-Assistent für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] an der Eingabeaufforderung ausgeführt wird.  
  
#### So führen Sie den Bereitstellungs-Assistenten für Analysis Services an der Eingabeaufforderung aus  
  
1.  Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum Ordner „C:\\Programme\(x86\)\\Microsoft SQL Server\\120\\Tools\\Binn\\ManagementStudio“.  
  
2.  Geben Sie **Microsoft.AnalysisServices.Deployment.exe** ein und darauf folgend die Schalter für den Modus, in dem der Assistent ausgeführt werden soll.  
  
## Siehe auch  
 [Grundlegendes zum Analysis Services-Bereitstellungsskript](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [Bereitstellen von Modelllösungen mithilfe des Bereitstellungs-Assistenten](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  