---
title: "Designer für tabellarische Modelle | Microsoft Docs"
ms.date: 10/19/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ASVS.BIDTOOLSET.TOPLEVSEMMODUIENTRY.F1
ms.assetid: 45735c57-2a95-4e45-8994-7242df6c9c5f
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 388c20c5fffdd584b2923341db13c7bf634f289b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tabular-model-designer-ssas"></a>Tabellen-Modell-Designer (SSAS)
Der Designer für tabellarische Modelle ist Bestandteil von [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]und in Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]integriert. Der Designer bietet zusätzliche Projekttypvorlagen speziell für die Entwicklung von Projektmappen für professionelle tabellarische Modelle.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] wird als kostenloser Webdownload installiert. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md).    
  
##  <a name="bkmk_benefits"></a> Vorteile  
 Wenn Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installieren, werden den verfügbaren Projekttypen neue Projektvorlagen zum Erstellen tabellarischer Modelle hinzugefügt. Nachdem ein neues Projekt für tabellarische Modelle auf der Grundlage einer der Vorlagen erstellt wurde, können Sie mit der Erstellung von Modellen beginnen. Dazu verwenden Sie die Designer-Tools und Assistenten für tabellarische Modelle.  
  
 Zusätzlich zu neuen Vorlagen und Tools zum Erstellen professioneller Projektmappen für mehrdimensionale und tabellarische Modelle stellt die [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] -Umgebung Debugging- und Projektlebenszyklusfunktionen bereit, mit denen Sie immer die leistungsstärksten BI-Lösungen für Ihre Organisation erstellen können. Weitere Informationen zu [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]finden Sie unter [Erste Schritte mit Visual Studio](http://go.microsoft.com/fwlink/?LinkId=206389).  
  
##  <a name="bkmk_proj_temp"></a>Projektvorlagen  
 Wenn Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installieren, werden den Business Intelligence-Projekttypen die folgenden Projektvorlagen für tabellarische Modelle hinzugefügt:  
  
 **Analysis Services-Projekt für tabellarische Modelle**  
 Mit dieser Vorlage kann ein neues, leeres tabellarisches Modellprojekt erstellt werden. Kompatibilitätsgrade werden beim Erstellen des Projekts angegeben.
  
 **Von Server importieren (tabellarisch)**  
 Mit dieser Vorlage kann ein neues tabellarisches Modellprojekt erstellt werden, indem die Metadaten aus einem vorhandenen tabellarischen Modell in Analysis Services extrahiert werden.  
  
 Ältere Modelle haben ältere Kompatibilitätsgrade. Sie können durch Ändern der kompatibilitätsgradeigenschaft nach dem Importieren der Modelldefinition aktualisieren.  
  
 **Importieren aus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**  
 Mit dieser Vorlage wird ein neues tabellarisches Modellprojekt erstellt, indem die Metadaten und Daten aus einer [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] -Datei extrahiert werden.  
  
##  <a name="bkmk_wind_men"></a> Fenster und Menüs  
 Die [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] -Erstellungsumgebung für tabellarische Modelle schließt Folgendes ein:  
  
### <a name="designer-window"></a>Designerfenster  
 Das Designerfenster dient zur Erstellung tabellarischer Modelle, indem das Modell in einer visuellen Darstellung abgebildet wird. Wenn Sie die Datei Model.bim öffnen, wird das Modell im Designerfenster geöffnet. Zum Erstellen eines Modells im Designerfenster stehen zwei unterschiedliche Ansichtsmodi zur Verfügung:  
  
 **Datensicht**  
 In der Datensicht werden Tabellen in einem tabellarischen Rasterformat angezeigt. Außerdem können Sie Measures mit dem Measureraster definieren, das für jede Tabelle ausschließlich in der Datensicht angezeigt werden kann.  
  
 **Diagrammansicht**  
 In der Diagrammsicht werden Tabellen mit den bestehenden Beziehungen in einem grafischen Format angezeigt. Spalten, Measures, Hierarchien und KPIs können gefiltert werden, und Sie können auswählen, ob das Modell mithilfe einer definierten Perspektive angezeigt wird.  
  
 Die meisten Modellerstellungsaufgaben können in einer beliebigen Ansicht ausgeführt werden.  
  
### <a name="view-code-window"></a>Codefenster anzeigen  
 Sie können den Code hinter einer „Model.bim“-Datei anzeigen, indem Sie mit der rechten Maustaste auf die Datei klicken und im Projektmappen-Explorer **Code anzeigen** auswählen. Für tabellarische Modelle mit Kompatibilitätsgrad 1200 oder höher wird die Modelldefinition im JSON-Format angegeben.  
  
 Beachten Sie, dass Sie eine Vollversion von Visual Studio benötigen, die den JSON-Editor bereitstellt. Sie können die [kostenlose Visual Studio Community Edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) herunterladen und installieren, wenn Sie die zusätzlichen Funktionen der kommerziellen Editionen nicht benötigen.  
  
### <a name="solution-explorer"></a>Projektmappen-Explorer  
 Im Projektmappen-Explorer-Fenster wird die aktive Projektmappe als logischer Container für Projekte für tabellarische Modelle dargestellt und umfasst die dazugehörigen Elemente. Das Modellprojekt (.smproj) enthält gewöhnlich nur ein (leeres) References-Objekt und die Datei Model.bim. In dieser Ansicht können Sie Projektelemente zum Ändern öffnen und andere Verwaltungsaufgaben ausführen.  
  
 Projektmappen für tabellarische Modelle enthalten normalerweise nur ein Projekt. Dagegen kann eine Projektmappe weitere Projekte enthalten, z. B. ein Projekt für Integration Services oder Reporting Services. Sie können eine beliebige Anzahl von Dateien hinzufügen, sofern sie nicht den gleichen Typ aufweisen wie Projektdateien für tabellarische Modelle und ihre Buildvorgang-Eigenschaft nicht auf Kein bzw. ihre In Ausgabeverzeichnis kopieren-Eigenschaft nicht auf Nicht kopieren festgelegt ist.  
  
 Klicken Sie zum Anzeigen des Projektmappen-Explorers auf das Menü **Ansicht** und anschließend auf **Projektmappen-Explorer**.  

### <a name="tabular-model-explorer"></a>Tabellenmodell-Explorer
  Erste in der August 2016-Version (14.0.60812.0) von [SQL Server Data Tools](https://msdn.microsoft.com/mt186501), tabellarische Modell-Explorer können Sie die Metadatenobjekte in tabellarischen Modellen zu navigieren.

 Klicken Sie zum Anzeigen des Tabellenmodell-Explorers auf **Ansicht** > **Weitere Fenster**, und klicken Sie dann auf **Tabellenmodell-Explorer**.
   
  ![Tabellenmodell-Explorer](../../analysis-services/tabular-models/media/tabular-model-explorer.png) 
  
 Tabellarische Modell-Explorer organisiert Metadatenobjekte in einer Baumstruktur, die das Schema eines tabellarischen Modells sehr ähnlich. Datenquellen, Perspektiven, Beziehungen, Rollen, Tabellen und Übersetzungen entsprechen Schemaobjekten der obersten Ebene. Es gibt einige Ausnahmen, insbesondere die KPIs und Measures, die technisch gesehen keine Objekte der obersten Ebene, sondern untergeordnete Objekte verschiedener Tabellen im Modell sind. Wenn Container der obersten Ebene für alle KPIs und Measures konsolidiert wurden, gestaltet sich die Arbeit mit diesen Objekten jedoch einfacher, insbesondere, wenn Ihr Modell eine sehr große Anzahl von Tabellen umfasst. Measures werden auch unter ihren entsprechenden übergeordneten Tabellen aufgelistet, somit erhalten Sie eine deutliche Übersicht über die tatsächlichen Beziehungen zwischen über- und untergeordneten Elementen. Wenn Sie ein Measure im Container auf oberster Ebene auswählen, wird dasselbe Measure auch in der untergeordneten Auflistung unter seiner Tabelle ausgewählt (und umgekehrt).  
 
 Objektknoten im Tabellenmodell-Explorer sind mit den entsprechenden Menüoptionen verknüpft, die in Visual Studio bisher in den Menüs für Modell, Tabelle und Spalte verborgen waren. Sie können mit der rechten Maustaste auf ein Objekt klicken, um Optionen für den Objekttyp anzuzeigen. Es besitzen noch nicht alle Objektknotentypen ein Kontextmenü, aber in künftigen Versionen werden zusätzliche Optionen und Verbesserungen hinzugefügt. 

 Der Tabellenmodell-Explorer bietet auch eine praktische Suchfunktion. Geben Sie einfach einen Teil des Namens in das Suchfeld ein, woraufhin der Tabellenmodell-Explorer die Strukturansicht auf die Übereinstimmungen eingrenzt. 
  
### <a name="properties-window"></a>Fenster "Eigenschaften"  
 Im Eigenschaftenfenster werden Eigenschaften des ausgewählten Objekts aufgelistet. Die folgenden Objekte verfügen über Eigenschaften, die im Eigenschaftenfenster angezeigt und bearbeitet werden können:  
  
-   Model.bim  
  
-   Tabelle  
  
-   Column  
  
-   Measure  
  
 Die Projekteigenschaften im Eigenschaftenfenster enthalten nur den Projektnamen und den Projektordner. Projekte verfügen außerdem über zusätzliche Einstellungen für Bereitstellungsoptionen und den Bereitstellungsserver, die Sie über ein Dialogfeld für modale Eigenschaften festlegen können. Klicken Sie in **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**, um diese Eigenschaften anzuzeigen.  
  
 In die Felder des Eigenschaftenfensters sind Steuerelemente eingebettet, die geöffnet werden, wenn Sie darauf klicken. Der Typ des Bearbeitungssteuerelements hängt von der bestimmten Eigenschaft ab. Die Steuerelemente umfassen Bearbeitungsfelder, Dropdownlisten und Links zu benutzerdefinierten Dialogfeldern. Die in grau angezeigten Eigenschaften sind schreibgeschützt.  
  
 Klicken Sie zum Anzeigen des Fensters **Eigenschaften** auf das Menü **Ansicht** und anschließend auf **Eigenschaftenfenster**.  
  
### <a name="error-list"></a>Fehlerliste  
 Das Fenster mit der Fehlerliste enthält Meldungen zum Modellstatus:  
  
-   Benachrichtigungen zu bewährten Sicherheitsmethoden.  
  
-   Anforderungen für die Datenverarbeitung.  
  
-   Informationen zu Semantikfehlern für berechnete Spalten, Measures und Zeilenfilter für Rollen. Bei berechneten Spalten können Sie auf die Fehlermeldung doppelklicken, um zur Fehlerquelle zu navigieren.  
  
-   DirectQuery-Überprüfungsfehler.  
  
 Die **Fehlerliste** wird standardmäßig erst angezeigt, nachdem ein Fehler zurückgegeben wurde. Sie können das Fenster **Fehlerliste** jedoch jederzeit anzeigen. Klicken Sie zum Anzeigen des Fensters **Fehlerliste** auf das Menü **Ansicht** und anschließend auf **Fehlerliste**.  
  
### <a name="output"></a>Ausgabe  
 Erstellungs- und Bereitstellungsinformationen werden (zusätzlich zum modalen Statusdialogfeld) im Fenster **Ausgabe** angezeigt. Klicken Sie zum Anzeigen des Ausgabefensters auf das Menü **Ansicht** und anschließend auf **Ausgabe** .  
  
### <a name="menu-items"></a>Menüelemente  
 Wenn Sie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]installieren, werden der Visual Studio-Menüleiste zusätzliche Menüelemente speziell für die Erstellung tabellarischer Modelle hinzugefügt. Das Menü **Modell** kann verwendet werden, um den Datenimport-Assistenten zu starten, vorhandene Verbindungen anzuzeigen, Arbeitsbereichsdaten zu verarbeiten und den Modellarbeitsbereich in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel zu durchsuchen. Das Menü **Tabelle** kann verwendet werden, um Beziehungen zwischen Tabellen zu erstellen und zu verwalten, Measures zu erstellen und zu verwalten sowie Datentabelleneinstellungen, Berechnungsoptionen und andere Tabelleneigenschaften anzugeben. Im Menü **Spalte** können Sie Spalten in einer Tabelle hinzufügen und löschen, Spalten aus- und einblenden und verschiedene Spalteneigenschaften angeben, z.B. Datentypen und Filter. Sie können Projektmappen für tabellarische Modelle über das Menü **Erstellen** anlegen und bereitstellen. Die Funktionen zum Kopieren bzw. Einfügen sind im Menü **Bearbeiten** enthalten.  
  
 Zusätzlich zu diesen Menüelementen werden die Analysis Services-Optionen um weitere Einstellungen ergänzt, die im Menü Extras verfügbar sind.  
  
### <a name="toolbar"></a>Symbolleiste  
 Die Analysis Services-Symbolleiste ermöglicht den schnellen und einfachen Zugriff auf die am häufigsten verwendeten Befehle für die Modellerstellung.  
  
##  <a name="bkmk_vsint"></a>Visual Studio-integration  
 **Datenquellen-Steuerelements**  
 Analysis Services-Projekte werden mit dem ausgewählten Plug-In für die Quellcodeverwaltung integriert. Wenn Sie Visual Studio für die Verwendung der Quellcodeverwaltung konfiguriert haben, können Sie die Funktionen zum Ein-/Auschecken im Projektmappen-Explorer verwenden. Weitere Informationen zum Konfigurieren von Team Foundation Server finden Sie unter [Konfigurieren von Visual Studio für die Verwendung der Team Foundation-Versionskontrolle](http://msdn.microsoft.com/library/ms253064.aspx). Viele Drittanbieter-Plug-Ins für die Quellcodeverwaltung werden ebenfalls unterstützt.  
  
 **Schriftarten**  
 Tabellarische Modelle verwenden die Schriftart der [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] -Umgebung, um die Schriftarten in der Anzeige zu steuern. Es kann erforderlich sein, diese Schriftart zu ändern, wenn die [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] -Standardschriftart nicht über alle Unicode-Zeichen verfügt, die Sie für Ihre Sprache benötigen. Klicken Sie zum Ändern von Schriftarten auf das Menü **Extras** &gt; **Optionen**und anschließend auf **Schriftarten und Farben**.  
  
 **Tastenkombinationen**  
 Die Analysis Services-Tastenkombinationen können über das Dialogfeld Tools->Optionen->Tastatur konfiguriert bzw. neu zugeordnet werden. Einige globale [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] -Verknüpfungen, wie z.B. „Erstellen“, „Speichern“, „Debuggen“, „neues Projekt“ usw., werden im Kontext des Designers für tabellarische Modelle unterstützt. Andere spezifische Tastenkombinationen des Designers für tabellarische Modelle sind im Analysis Services-Kontext verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenmodellprojekte &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)   
 [Eigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/properties-ssas-tabular.md)  
  
  
