---
title: "Lektion 1: Erstellen eines neuen Tabellenmodellprojekts | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Lektion 1: Erstellen eines neuen Tabellenmodellprojekts
In dieser Lektion erstellen Sie ein neues leeres Tabellenmodellprojekt in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Sobald das neue Projekt erstellt wird, können Sie mithilfe des Tabellenimport-Assistenten Daten hinzufügen. Zusätzlich zum Erstellen eines neuen Projekts bietet diese Lektion auch eine kurze Einführung in die Umgebung zur Tabellenmodellerstellung in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
Weitere Informationen zu den verschiedenen Typen von Tabellenmodellprojekten finden Sie unter [Tabellenmodellprojekte &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Weitere Informationen zur Umgebung für die Tabellenmodellerstellung finden Sie unter [Tabellen-Modell-Designer &#40;SSAS&#41;](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema stellt die erste Lektion in einem Lernprogramm zur Tabellenmodellerstellung dar. Um diese Lektion abzuschließen, benötigen Sie die auf einer SQL Server-Instanz installierte AdventureWorksDW-Datenbank. Weitere Informationen finden Sie unter [Tabellenmodellierung &#40;Adventure Works-Tutorial&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## Erstellen eines neuen Tabellenmodellprojekts  
  
#### So erstellen Sie ein neues Tabellenmodellprojekt  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]auf das Menü **Datei** , auf **Neu**und dann auf **Projekt**.  
  
2.  Klicken Sie im Dialogfeld **Neues Projekt** unter **Installiert** auf **Business Intelligence**. Klicken Sie anschließend auf **Analysis Services** und anschließend auf **Analysis Services-Projekt für tabellarische Modelle**.  
  
3.  Geben Sie im Feld **Name** die Zeichenfolge **AW Internet Sales Tabular Model** ein, und geben Sie einen Speicherort für die Projektdateien ein.  
  
    Standardmäßig entspricht der **Projektmappenname** dem Projektnamen. Sie können jedoch auch einen anderen Projektmappennamen eingeben.  
  
4.  Klicken Sie auf **OK**.  
  
5.  Geben Sie im Dialogfeld **Designer für tabellarische Modelle** unter **Arbeitsbereichsserver** den Namen einer Analysis Services-Instanz von SQL Server 2016 ein, für die Sie die Berechtigungen eines Server-Administrators haben, und klicken Sie anschließend auf **Verbindung testen**.  
  
    Die von Ihnen angegebene Arbeitsbereich-Serverinstanz hostet eine tabellarische Modelldatenbank mit dem gleichen Namen wie das Projekt während der Erstellung.   
      
6.  Überprüfen Sie im Listenfeld **Kompatibilitätsgrad**, ob **SQL Server 2016 (1200)** ausgewählt ist, und klicken Sie anschließend auf **OK**.   
      
    Wenn „SQL Server 2016 (1200)“ nicht im Listenfeld „Kompatibilitätsgrad“ angezeigt wird, verwenden Sie nicht die neueste Version von SQL Server Data Tools. Sie können die neueste Version unter [Installieren von SQL Server Data Tools](https://msdn.microsoft.com/hh500335(v=vs.103).aspx) herunterladen.   
      
    Die Auswahl eines früheren Kompatibilitätsgrads wird nur empfohlen, falls Sie Ihr abgeschlossenes tabellarisches Modell auf einer anderen Analysis Services-Instanz bereitstellen möchten, die auf SQL Server 2012 oder SQL Server 2014 ausgeführt wird. Weitere Informationen finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## Einblick in die SQL Server Data Tools-Umgebung zur Tabellenmodellerstellung  
Nachdem Sie ein neues Projekt für tabellarische Modelle erstellt haben, soll nun die Umgebung zur Erstellung tabellarischer Modelle in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 oder höher) erkundet werden.  
  
Nach der Erstellung des Projekts wird es in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] geöffnet. Ein leeres Modell wird im Modell-Designer angezeigt, und die Datei **Model.bim** wird im Fenster des **Projektmappen-Explorers** ausgewählt. Wenn Sie Daten hinzufügen, werden Tabellen und Spalten im Designer angezeigt. Wird der Designer (das leere Fenster mit der Registerkarte Model.bim) im **Projektmappen-Explorer** nicht unter **AW Internet Sales Tabular Model** angezeigt, doppelklicken Sie auf die Datei **Model.bim**.  
  
Sie können die grundlegenden Eigenschaften für das Projekt im Fenster **Eigenschaften** anzeigen. Klicken Sie im **Projektmappen-Explorer** auf **AW Internet Sales Tabular Model**. Im Fenster **Eigenschaften** unter **Projektdatei** wird **AW Internet Sales Tabular Model.smproj** angezeigt. Dies ist der Projektdateiname, und unter **Projektordner** wird der Projektdateispeicherort angegeben.  
  
Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt **AW Internet Sales Tabular Model**, und klicken Sie anschließend auf **Eigenschaften**. Das Dialogfeld für die **Eigenschaftenseiten des AW Internet Sales-Tabellenmodells** wird angezeigt. Hierbei handelt es sich um die erweiterten Projekteigenschaften. Sie werden später einige dieser Eigenschaften festlegen, wenn Sie für die Bereitstellung des Modells bereit sind.  
  
Nun sehen wir uns die Modelleigenschaften an. Klicken Sie im **Projektmappen-Explorer** auf **Model.bim**. Im Fenster **Eigenschaften** sehen Sie jetzt die Modelleigenschaften, wobei die wichtigste Eigenschaft die Eigenschaft **DirectQuery-Modus** ist. Diese Eigenschaft gibt an, ob das Modell im InMemory-Modus (Aus) oder im DirectQuery-Modus (Ein) bereitgestellt wird. In diesem Lernprogramm wird das Modell im InMemory-Modus erstellt und bereitgestellt.  
  
Wenn Sie ein neues Modell erstellen, werden bestimmte Modelleigenschaften automatisch gemäß den Datenmodellierungseinstellungen festgelegt, die im Dialogfeld für Tools und Optionen angegeben werden können. Die Eigenschaften für die Datensicherung, Beibehaltung des Arbeitsbereichs und den Arbeitsbereichsserver geben an, wie und wo die Arbeitsbereichsdatenbank (Datenbank zur Modellerstellung) gesichert, speicherintern beibehalten und erstellt wird. Sie können diese Einstellungen ggf. später ändern. Lassen Sie sie jedoch vorerst unverändert.  
  
Bei der Installation von [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] wurden der Visual Studio-Umgebung mehrere neue Menüelemente hinzugefügt. Sehen wir die neuen Menüelemente an, die für die Erstellung von Tabellenmodellen konzipiert sind. Klicken Sie auf das Menü **Modell**. Über dieses Menü können Sie den Tabellenimport-Assistenten starten, vorhandene Verbindungen anzeigen und bearbeiten, Arbeitsbereichsdaten aktualisieren, Ihr Modell in [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel mit der Funktion "In Excel analysieren" durchsuchen, Perspektiven und Rollen erstellen, die Modellsicht auswählen und Berechnungsoptionen festlegen.  
  
Klicken Sie auf das Menü **Tabelle**. Hier können Sie Beziehungen zwischen Tabellen erstellen und verwalten, Datumstabelleneigenschaften festlegen, Partitionen erstellen und Tabelleneigenschaften bearbeiten.  
  
Klicken Sie auf das Menü **Spalte**. Hier können Sie Spalten in einer Tabelle hinzufügen und löschen, Spalten fixieren und die Sortierreihenfolge angeben. Sie können auch die AutoSumme-Funktion verwenden, um ein Standardaggregationsmeasure für eine ausgewählte Spalte zu erstellen. Weitere Schaltflächen in der Symbolleiste bieten einen schnellen Zugriff auf häufig verwendete Funktionen und Befehle.  
  
Erkunden Sie einige der Dialogfelder und Positionen für verschiedene Funktionen, die für die Erstellung von Tabellenmodellen konzipiert sind. Obwohl einige Elemente noch nicht aktiv sind, erhalten Sie dennoch einen Einblick in die Umgebung zur Tabellenmodellerstellung.  
  
## Nächste Schritte  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 2: Hinzufügen von Daten](../analysis-services/lesson-2-add-data.md).  
  
  
  
