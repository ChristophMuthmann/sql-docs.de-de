---
title: 'Lektion 1: Erstellen ein neuen Tabellenmodellprojekts | Microsoft Docs'
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 6c65307cd9368c976d28b60c567ed0b9bcd29b97
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lektion 1: Erstellen eines neuen Tabellenmodellprojekts
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie ein neues leeres Tabellenmodellprojekt in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Sobald das neue Projekt erstellt wird, können Sie mithilfe des Tabellenimport-Assistenten Daten hinzufügen. In dieser Lektion werden Ihnen auch eine kurze Einführung in das tabellarische Modell in SSDT erstellungsumgebung.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **10 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema stellt die erste Lektion in einem Lernprogramm zur Tabellenmodellerstellung dar. Um diese Lektion abzuschließen, müssen Sie die AdventureWorksDW-Beispieldatenbank auf einer SQL Server-Instanz installiert haben. Weitere Informationen finden Sie unter [tabellarische Modellierung &#40; Adventure Works-Lernprogramm &#41; ](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Erstellen eines neuen Tabellenmodellprojekts  
  
#### <a name="to-create-a-new-tabular-model-project"></a>So erstellen Sie ein neues Tabellenmodellprojekt  
  
1.  In SSDT auf dem **Datei** Menü klicken Sie auf **neu** > **Projekt**.  
  
2.  In der **neues Projekt** Dialogfeld erweitern Sie **installiert** > **Business Intelligence** > **Analysis Services**, und klicken Sie dann auf **tabellarischen Analysis Services-Projekts**.  
  
3.  In **Namen**, Typ **AW Internet Sales**, und geben Sie einen Speicherort für die Projektdateien.  
  
    Standardmäßig entspricht der **Projektmappenname** dem Projektnamen. Sie können jedoch auch einen anderen Projektmappennamen eingeben.  
  
4.  Klicken Sie auf **OK**.  
  
5.  In der **Designer für tabellarische Modelle** wählen Sie im Dialogfeld **integrierten Arbeitsbereich**.  
  
    Der Arbeitsbereich wird eine Datenbank für tabellarische Modelle mit dem gleichen Namen wie das Projekt während der Modellerstellung gehostet werden. Arbeitsbereich "integrierte" bedeutet, dass es sich bei SSDT eine integrierte Instanz verwenden, wird dadurch entfällt die Notwendigkeit eine separaten Analysis Services-Serverinstanz für die Modellerstellung zu installieren. Weitere Informationen finden Sie unter [Arbeitsbereichsdatenbank](../analysis-services/tabular-models/workspace-database-ssas-tabular.md).
      
6.  Überprüfen Sie im Listenfeld **Kompatibilitätsgrad**, ob **SQL Server 2016 (1200)** ausgewählt ist, und klicken Sie anschließend auf **OK**.   
 
    ![als-tabellarische-Lektion 1 zu-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    Wenn Sie SQL Server 2016 RTM (1200) im Compatibility Level Listenfeld nicht angezeigt wird, verwenden Sie nicht die neueste Version von SQL Server Data Tools. Sie können die neueste Version unter [Installieren von SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)herunterladen.  

    Wenn Sie die neueste Version von SSDT verwenden, können Sie auch auswählen, auf SQL Server-2017 (1400). Allerdings für Lektion 13: bereitstellen, benötigen Sie einen 2017 von SQL Server oder Azure-Server bereitstellen.
      
    Auswählen einer früheren Kompatibilitätsgrad wird nur empfohlen, wenn Sie das abgeschlossene tabellarische Modell in einer anderen Analysis Services-Instanz einer früheren Version von SQL Server bereitstellen möchten. Arbeitsbereich "integrierte" wird bei niedrigeren Kompatibilitätsgraden nicht unterstützt. Weitere Informationen finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Grundlegendes zu SSDT tabellenmodellerstellung Umgebung  
Nun, dass Sie ein neues tabellarisches Modellprojekt erstellt haben, werfen wir einen Moment Zeit, die Umgebung in SSDT Erstellung tabellarischen Modelle zu untersuchen.  
  
Nachdem das Projekt erstellt wurde, wird er in SSDT geöffnet. Auf der rechten Seite in **tabellarische Modell-Explorer**, sehen Sie eine Strukturansicht der Objekte in Ihrem Modell. Da Sie Daten noch nicht geschehen importiert haben, werden der Ordner leer sein. Sie können einen Ordner Objekt zum Ausführen von Aktionen, ähnlich wie auf der Menüleiste auf rechtsklicken. Während Sie in diesem Lernprogramm durchlaufen, verwenden Sie das tabellarische Modell-Explorer, um verschiedene Objekte in Ihrem Modellprojekt zu navigieren.

![als-tabellarische-Lektion 1 zu-Zeit](../analysis-services/media/as-tabular-lesson1-tme.png)

Klicken Sie auf die **Projektmappen-Explorer** Registerkarte. Hier sehen Sie Ihre **Model.bim** Datei. Wenn Sie das Designer-Fenster auf der linken Seite (das leere Fenster mit der Registerkarte Model.bim) im sehen **Projektmappen-Explorer**unter **AW Internet Sales Projekt**, doppelklicken Sie auf die **Model.bim** Datei. Die Model.bim-Datei enthält alle Metadaten für das Modellprojekt erstellen. 

![als-tabellarische-Lektion 1 zu-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
Sehen wir uns die Modelleigenschaften an. Klicken Sie auf **Model.bim**. In der **Eigenschaften** Fenster sehen Sie die [Modelleigenschaften](../analysis-services/tabular-models/model-properties-ssas-tabular.md), am wichtigsten, wobei die **DirectQuery-Modus** Eigenschaft. Diese Eigenschaft gibt an, ob das Modell im InMemory-Modus (Aus) oder im DirectQuery-Modus (Ein) bereitgestellt wird. In diesem Lernprogramm wird das Modell im InMemory-Modus erstellt und bereitgestellt.

![als tabellarische-Lektion 1 zu-Eigenschaften.](../analysis-services/media/as-tabular-lesson1-properties.png)
  
Wenn Sie ein neues Modell erstellen, bestimmte Modelleigenschaften werden automatisch festgelegt gemäß den datenmodellierungseinstellungen, die in angegeben werden, können die **Tools** > **Optionen** (Dialogfeld). Die Eigenschaften für die Datensicherung, Beibehaltung des Arbeitsbereichs und den Arbeitsbereichsserver geben an, wie und wo die Arbeitsbereichsdatenbank (Datenbank zur Modellerstellung) gesichert, speicherintern beibehalten und erstellt wird. Sie können diese Einstellungen ggf. später ändern. Lassen Sie sie jedoch vorerst unverändert.  

In **Projektmappen-Explorer**, mit der rechten Maustaste **AW Internet Sales** (Projekt), und klicken Sie dann auf **Eigenschaften**. Die **Eigenschaftenseiten des AW Internet Sales** Dialogfeld wird angezeigt. Hierbei handelt es sich um den erweiterten [Projekteigenschaften](../analysis-services/tabular-models/project-properties-ssas-tabular.md). Sie werden später einige dieser Eigenschaften festlegen, wenn Sie für die Bereitstellung des Modells bereit sind.  
  
Wenn Sie SSDT installiert haben, wurden der Visual Studio-Umgebung mehrere neue Menüelemente hinzugefügt. Betrachten wir nun die speziell zur Erstellung von tabellarischer Models. Klicken Sie auf das Menü **Modell** . Dort können können Sie den Tabellenimport-Assistenten zu starten, anzeigen und Bearbeiten vorhandener Verbindungen, Arbeitsbereichsdaten aktualisieren, Durchsuchen des Modells in Excel mit der Funktion in Excel analysieren, Perspektiven und Rollen erstellen, die modellsicht auswählen und Berechnungsoptionen festlegen.  
  
Klicken Sie auf das Menü **Tabelle** . Hier können Sie Beziehungen zwischen Tabellen erstellen und verwalten, Datumstabelleneigenschaften festlegen, Partitionen erstellen und Tabelleneigenschaften bearbeiten.  
  
Klicken Sie auf das Menü **Spalte** . Hier können Sie Spalten in einer Tabelle hinzufügen und löschen, Spalten fixieren und die Sortierreihenfolge angeben. Sie können auch die AutoSumme-Funktion verwenden, um ein Standardaggregationsmeasure für eine ausgewählte Spalte zu erstellen. Weitere Schaltflächen in der Symbolleiste bieten einen schnellen Zugriff auf häufig verwendete Funktionen und Befehle.  
  
Erkunden Sie einige der Dialogfelder und Positionen für verschiedene Funktionen, die für die Erstellung von Tabellenmodellen konzipiert sind. Obwohl einige Elemente noch nicht aktiv sind, erhalten Sie dennoch einen Einblick in die Umgebung zur Tabellenmodellerstellung.  


## <a name="additional-resources"></a>Weitere Ressourcen
Weitere Informationen zu den verschiedenen Typen von Tabellenmodellprojekten finden Sie unter [Tabellenmodellprojekte &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Weitere Informationen zur Umgebung für die Tabellenmodellerstellung finden Sie unter [Tabellen-Modell-Designer &#40;SSAS&#41;](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  

## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 2: Hinzufügen von Daten](../analysis-services/lesson-2-add-data.md).

  
  
  
