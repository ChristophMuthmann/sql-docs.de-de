---
title: Erstellen Sie eine DMX-Abfrage in SQL Server Management Studio | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 939d21c596a3f023afaae6931ba1c53efe0ab85b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-dmx-query-in-sql-server-management-studio"></a>Erstellen einer DMX-Abfrage in SQL Server Management Studio
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bietet eine Reihe von Features helfen Ihnen beim Erstellen von Vorhersageabfragen, Inhaltsabfragen und Datendefinitionsabfragen gegen Miningmodelle und Miningstrukturen.  
  
-   Der grafische Generator für Vorhersageabfragen ist sowohl über [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] als auch [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verfügbar, um den Prozess des Schreibens von Vorhersageabfragen und des Zuordnens von Datasets zu Modellen zu vereinfachen.  
  
-   Die Abfragevorlagen ermöglichen im beschleunigten Vorlagen-Explorer die Erstellung vieler verschiedener Arten von DMX-Abfragen, einschließlich verschiedener Typen von Vorhersageabfragen. Die Vorlagen werden für Inhaltsabfragen, für in geschachtelten Datasets verwendete Abfragen, für Abfragen, die Fälle von der Miningstruktur zurückgeben, und sogar für Datendefinitionsabfragen bereitgestellt.  
  
-   Der Metadaten-Explorer in den MDX- und DMX-Abfragebereichen stellt eine Liste von verfügbaren Modellen und Strukturen, die Sie per Drag & Drop in den Abfrage-Generator einbinden können, sowie eine Liste von DMX-Funktionen bereit. Diese Funktion vereinfacht einen korrekten Abruf von Objektnamen ohne Typisierung.  
  
 In diesem Thema wird beschrieben, wie eine DMX-Abfrage erstellt wird, indem der Metadaten-Explorer und der DMX-Abfrage-Editor verwendet werden.  
  
##  <a name="BKMK_Templates"></a> DMX-Abfragevorlagen  
 Zum Erstellen von grundlegenden DMX-Abfragen stehen Vorlagen im Vorlagen-Explorer zur Verfügung. Der **DMX** -Ordner enthält Data Mining-Vorlagen, die in die folgenden Kategorien unterteilt sind:  
  
-   **Modellinhalt**  
  
-   **Modellverwaltung**  
  
-   **Vorhersageabfragen**  
  
-   **Strukturieren von Inhalt**  
  
 Sie können auch benutzerdefinierte Vorlagen für jene Abfragen oder Befehle erstellen, die Sie häufig ausführen.  
  
## <a name="xmla-query-templates"></a>XMLA-Abfragevorlagen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]stellt auch Vorlagen für XMLA-Abfragen bereit.  
  
 Zwischen den Typen der Abfragen, die Sie mit XMLA oder DMX ausführen können, tritt ein gewisses Maß an Überschneidung auf. Sie können z. B. einige Modellinhaltsabfragen erstellen, indem Sie entweder DMX oder die Data Mining-Schemarowsets verwenden. Die Schemarowsets enthalten allerdings gelegentlich Informationen, die in DMX-Inhaltsabfragen nicht verfügbar gemacht werden.  
  
 Außerdem gibt es einige wesentliche Unterschiede bezüglich der Art, wie Vorgänge in DMX oder in XMLA verarbeitet werden. Sie können XMLA z.B. verwenden, um Administratorvorgänge wie etwa die Sicherung einer gesamten [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Datenbank auszuführen. Wenn Sie jedoch ein einzelnes Miningmodell sichern möchten, stellt DMX einen einfachen Befehl bereit ([EXPORT &#40;DMX&#41;](../../dmx/export-dmx.md)), der zu diesem Zweck besser geeignet ist.  
  
##  <a name="BKMK_Building_Queries"></a> Erstellen und Ausführen einer DMX-Abfrage  
  
#### <a name="open-a-new-dmx-query-window"></a>Öffnen eines neuen DMX-Abfragefensters  
  
1.  Klicken Sie auf **Neue Abfrage** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Wählen Sie anschließend **DMX-Abfrage für Analysis Server**.  
  
2.  Wenn das Dialogfeld **Verbindung mit Server herstellen** angezeigt wird, wählen Sie die Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aus, die die zu verwendenden Miningmodelle enthält.  
  
#### <a name="open-template-explorer"></a>Öffnen des Vorlagen-Explorers  
  
1.  Wählen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Ansicht** den **Vorlagen-Explorer**.  
  
2.  Klicken Sie auf **Analysis-Server** , um eine Strukturansicht der Vorlagen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]anzuzeigen.  
  
#### <a name="apply-a-template-to-build-a-query"></a>Übernehmen einer Vorlage zum Erstellen einer Abfrage  
  
-   Klicken Sie mit der rechten Maustaste auf den entsprechenden Abfragetyp. Wählen Sie **Öffnen**aus.  
  
-   Oder ziehen Sie die Vorlage in den Abfrage-Editor.  
  
-   Sie können die Parameter für die Abfrage auch mit der Option **MT+++Werte für Vorlagenparameter angeben**aus dem Menü **Abfrage** eingeben.  
  
 Beispiele hinsichtlich des Erstellens spezieller Typen von Abfragen aus Vorlagen finden Sie unter den folgenden Themen:  
  
 [Erstellen Sie eine Singleton-Abfrage aus einer Vorlage](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
  
 [Eine Inhaltsabfrage für ein Miningmodell erstellen](../../analysis-services/data-mining/create-a-content-query-on-a-mining-model.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Datamining-Erweiterungen & #40; DMX & #41; Referenz](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
