---
title: "Integration Services-Benutzeroberfläche | Microsoft Docs"
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
- SQL Server Integration Services, SSIS Designer
- tools [Integration Services], SSIS Designer
- SSIS Designer
- SSIS, SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: d2c48cff-46f4-4c70-b1f3-c88f9b8757f3
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6f6f682da8a11f99d1d58d85405dd2ff0d526a47
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-user-interface"></a>SQL Server Integration Services-Benutzeroberfläche
  Neben den Entwurfsoberflächen auf den Registerkarten des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers stellt die Benutzeroberfläche den Zugriff auf die folgenden Fenster und Dialogfelder bereit, um Paketen Funktionen hinzuzufügen und die Eigenschaften von Paketobjekten zu konfigurieren:  
  
-   Die Dialogfelder und Fenster, mit denen Sie Paketen Funktionalität hinzufügen, wie z. B. Protokollierung und Konfigurationen.  
  
-   Die benutzerdefinierten Editoren zum Konfigurieren der Eigenschaften von Paketobjekten. Fast jeder Typ von Container, Task und Datenflusskomponente weist einen benutzerdefinierten Editor auf.  
  
-   Das Dialogfeld **Erweiterter Editor** , ein allgemeiner Editor, der für viele Datenflusskomponenten ausführlichere Konfigurationsoptionen bereitstellt.  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] stellt außerdem Fenster und Dialogfelder zum Konfigurieren der Umgebung und zum Verwenden von Paketen bereit.  
  
## <a name="dialog-boxes-and-windows"></a>Dialogfelder und Fenster  
 Nachdem Sie ein Paket geöffnet oder ein neues Paket im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer erstellt haben, sind die folgenden Dialogfelder und Fenster verfügbar.  
  
 In der folgenden Tabelle sind die Dialogfelder aufgelistet, die im Menü **SSIS** und in den Entwurfsoberflächen des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers verfügbar sind.  
  
|Dialogfeld|Zweck|Zugriff|  
|----------------|-------------|------------|  
|**Erste Schritte**|Zugriffsbeispiele, Lernprogramme und Videos.|Klicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** oder der Registerkarte **Datenfluss** mit der rechten Maustaste, und klicken Sie dann auf **Erste Schritte**.<br /><br /> Um das Fenster **Erste Schritte** automatisch anzuzeigen, wenn Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt erstellen, wählen Sie im unteren Bereich des Fensters die Option **In neuem Projekt immer anzeigen** aus.|  
|**SSIS-Protokolle konfigurieren**|Konfigurieren der Protokollierung für ein Paket und dessen Tasks durch Hinzufügen von Protokollen und Festlegen von Protokollierungsinformationen.|Klicken Sie im Menü **SSIS** auf **Protokollierung**.<br /><br /> -oder-<br /><br /> Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** , und klicken Sie dann auf **Protokollierung**.|  
|**Paketkonfigurationsplaner**|Hinzufügen und Bearbeiten von Paketkonfigurationen. In diesem Dialogfeld führen Sie den Paketkonfigurations-Assistenten aus.|Klicken Sie im Menü **SSIS** auf **Paketkonfigurationen**.<br /><br /> -oder-<br /><br /> Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** , und klicken Sie dann auf **Paketkonfigurationen**.|  
|**Digitale Signatur**|Signieren eines Pakets oder Entfernen der Signatur aus dem Paket.|Klicken Sie im Menü **SSIS** auf **Digitale Signatur**.<br /><br /> -oder-<br /><br /> Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** , und klicken Sie dann auf **Digitale Signatur**.|  
|**Breakpoints festlegen**|Aktivieren von Breakpoints für Tasks und Festlegen von Breakpointeigenschaften.|Klicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** mit der rechten Maustaste auf einen Task oder Container, und klicken Sie dann auf **Breakpoints bearbeiten**. Klicken Sie zum Festlegen eines Breakpoints für das Paket mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** , und klicken Sie dann auf **Breakpoints bearbeiten**.|  
  
 Im Fenster **Erste Schritte** werden Links zu Beispielen, Lernprogrammen und Videos bereitgestellt. Sie können Verknüpfungen zu zusätzlichen Inhalten hinzuzufügen, indem Sie die Datei "SamplesSites.xml" ändern, die in der aktuellen Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Es wird empfohlen, dass Sie nicht ändern, die \<GettingStartedSamples >-Element den Wert, der angibt, die RSS feed-URL. Die Datei befindet sich der  *\<Laufwerk >*: Ordner "\Programme\Microsoft SQL Server\110\DTS\Binn". Auf einem 64-Bit-Computer befindet sich die Datei die  *\<Laufwerk >*: \Programme (x86) \Microsoft SQL Server\110\DTS\Binn Ordner ""  
  
 Wenn die Datei SamplesSites.xml beschädigt wird, ersetzen Sie das XML in der Datei durch das folgende Standard-XML.  
  
 `<?xml version="1.0" ?>`  
  
 `- <SamplesSites>`  
  
 `<GettingStartedSamples>http://go.microsoft.com/fwlink/?LinkID=203147</GettingStartedSamples>`  
  
 `- <ToolboxSamples>`  
  
 `<Site>http://go.microsoft.com/fwlink/?LinkID=203286&query=SSIS%20{0}</Site>`  
  
 `</ToolboxSamples>`  
  
 `</SamplesSites>`  
  
 In der folgenden Tabelle sind die Fenster aufgelistet, die in den Menüs **SSIS** und **Ansicht** und in den Entwurfsoberflächen des [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designers verfügbar sind.  
  
|Fenster|Zweck|Zugriff|  
|------------|-------------|------------|  
|**Variablen**|Hinzufügen und Verwalten benutzerdefinierter Variablen.|Klicken Sie im Menü **SSIS** auf **Variablen**.<br /><br /> -oder-<br /><br /> Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarten **Ablaufsteuerung** und **Datenfluss** , und klicken Sie dann auf **Variablen**.<br /><br /> -oder-<br /><br /> Zeigen Sie im Menü **Ansicht** auf **Weitere Fenster**, und klicken Sie dann auf **Variablen**.|  
|**Protokollereignisse**|Anzeigen von Protokolleinträgen zur Laufzeit.|Klicken Sie im Menü **SSIS** auf **Protokollereignisse**.<br /><br /> -oder-<br /><br /> Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle in der Entwurfsoberfläche der Registerkarten **Ablaufsteuerung** und **Datenfluss** , und klicken Sie dann auf **Protokollereignisse**.<br /><br /> -oder-<br /><br /> Zeigen Sie im Menü **Ansicht** auf **Weitere Fenster**, und klicken Sie dann auf **Protokollereignisse**.|  
  
## <a name="custom-editors"></a>Benutzerdefinierte Editoren  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] stellt ein benutzerdefiniertes Dialogfeld für die meisten Container, Tasks, Quellen, Transformationen und Ziele bereit.  
  
 In der folgenden Tabelle wird das Zugreifen auf benutzerdefinierte Dialogfelder beschrieben.  
  
|Editor-Typ|Zugriff|  
|-----------------|------------|  
|Container. Weitere Informationen finden Sie unter [Integration Services-Container](../integration-services/control-flow/integration-services-containers.md).|Doppelklicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** auf den Container.|  
|Task. Weitere Informationen finden Sie unter [Integration Services Tasks](../integration-services/control-flow/integration-services-tasks.md).|Doppelklicken Sie in der Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** auf den Task.|  
|Quelle.|Doppelklicken Sie in der Entwurfsoberfläche der Registerkarte **Datenfluss** auf die Quelle.|  
|Transformation. Weitere Informationen finden Sie unter [Integration Services Transformations](../integration-services/data-flow/transformations/integration-services-transformations.md).|Doppelklicken Sie in der Entwurfsoberfläche der Registerkarte **Datenfluss** auf die Transformation.|  
|Ziel.|Doppelklicken Sie in der Entwurfsoberfläche der Registerkarte **Datenfluss** auf das Ziel.|  
  
## <a name="advanced-editor"></a>Erweiterter Editor  
 Das Dialogfeld **Erweiterter Editor** ist eine Benutzeroberfläche zum Konfigurieren von Datenflusskomponenten. Die Eigenschaften der Komponente werden mithilfe eines allgemeinen Layouts dargestellt. Das Dialogfeld **Erweiterter Editor** ist für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Transformationen mit mehreren Eingaben nicht verfügbar.  
  
 Zum Öffnen dieses Editors klicken Sie im Fenster **Eigenschaften** auf **Erweiterten Editor anzeigen** , oder klicken Sie mit der rechten Maustaste auf eine Datenflusskomponente, und klicken Sie dann auf **Erweiterten Editor anzeigen**.  
  
 Wenn Sie eine benutzerdefinierte Quelle, Transformation oder ein benutzerdefiniertes Ziel erstellen, aber keine benutzerdefinierte Benutzeroberfläche erstellen möchten, können Sie stattdessen das Dialogfeld **Erweiterter Editor** verwenden.  
  
## <a name="sql-server-data-tools-features"></a>Funktionen der SQL Server-Datentools  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] stellt Fenster, Dialogfelder und Menüoptionen zum Verwenden von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paketen bereit.  
  
 Es folgt eine Zusammenfassung der verfügbaren Fenster und Menüs:  
  
-   Im Fenster **Projektmappen-Explorer** werden Projekte, einschließlich des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekts, in dem Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete entwickeln, und Projektdateien aufgelistet.  
  
     Um die in einem Projekt enthaltenen Pakete nach Namen zu sortieren, klicken Sie mit der rechten Maustaste auf den Knoten **SSIS-Pakete** , und klicken Sie dann auf **Nach Namen sortieren**.  
  
-   Im Fenster **Toolbox** werden die Ablaufsteuerungs- und Datenflusselemente zum Erstellen von Ablaufsteuerungen und Datenflüssen aufgelistet.  
  
-   Im Fenster **Eigenschaften** werden Objekteigenschaften aufgelistet.  
  
-   Im Menü **Format** werden Optionen zum Ändern der Größe und zum Ausrichten von Steuerelementen in einem Paket bereitgestellt.  
  
-   Im Menü **Bearbeiten** werden Funktionen zum Kopieren und Einfügen bereitgestellt, um Objekte in den Entwurfsoberflächen zu kopieren.  
  
-   Im Menü **Ansicht** werden Optionen zum Ändern der grafischen Darstellung von Objekten im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer bereitgestellt.  
  
 Weitere Informationen zu zusätzlichen Fenstern und Menüs finden Sie in der Visual Studio-Dokumentation.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Weitere Informationen zum Erstellen von Paketen in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]finden Sie unter [Erstellen von Paketen in SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SSIS-Designer](../integration-services/ssis-designer.md)  
  
  

