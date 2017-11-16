---
title: Data Mining-Abfragetools | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- predictions [Analysis Services]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: a8952427-fd8c-4300-8f62-25f57ac1be0c
caps.latest.revision: 51
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 15b23f5cbe20fd7833a02cb6cff276680c30c9fb
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-query-tools"></a>Data Mining-Abfragetools
  Alle Data Mining-Abfragen verwenden die DMX-Sprache (Data Mining-Erweiterungen). DMX kann zum Erstellen von Modellen für alle Arten von Machine Learning-Tasks verwendet werden, einschließlich Klassifizierung, Risikoanalyse, Generierung von Empfehlungen und linearer Regression. Sie können auch DMX-Abfragen für Informationen zu Mustern und für Statistiken, die beim Verarbeiten des Modells generiert wurden, erstellen.  
  
 Sie können Ihre eigenen DMX-Abfragen schreiben, oder Sie können grundlegende DMX-Abfragen mithilfe eines Tools wie z.B. dem **Generator für Vorhersageabfragen** verwenden und anschließend anpassen. Sowohl [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] als auch [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] stellen Tools bereit, mit deren Hilfe Sie DMX-Vorhersageabfragen erstellen können. In diesem Thema wird das Erstellen und Ausführen von Data Mining-Abfragen unter Verwendung dieser Tools beschrieben.  
  
-   [Generator für Vorhersageabfragen](#bkmk_Builder)  
  
-   [Abfrage-Editor](#bkmk_QueryEditor)  
  
-   [DMX-Vorlagen](#bkmk_Templates)  
  
-   [Integration Services](#bkmk_SSIS)  
  
-   [Anwendungsprogrammierschnittstelle](#bkmk_API)  
  
##  <a name="bkmk_Builder"></a> Generator für Vorhersageabfragen  
 Der Generator für Vorhersageabfragen befindet sich auf der Registerkarte **Miningmodellvorhersage** des Data Mining-Designers, der sowohl in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]als auch in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verfügbar ist.  
  
 Wenn Sie den Abfrage-Generator verwenden, wählen Sie ein Miningmodell aus und fügen neue Falldaten sowie Vorhersagefunktionen hinzu. Sie können dann zum Text-Editor wechseln, um die Abfrage manuell ändern, oder im Bereich **Ergebnisse** die Ergebnisse der Abfrage anzeigen.  
  
##  <a name="bkmk_QueryEditor"></a> Abfrage-Editor  
 Im Abfrage-Editor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Sie auch DMX-Abfragen erstellen und ausführen. Sie können eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]herstellen und anschließend eine Datenbank, Miningstrukturspalten und ein Miningmodell auswählen. Der **Metadaten-Explorer** enthält eine durchsuchbare Liste mit Vorhersagefunktionen.  
  
##  <a name="bkmk_Templates"></a> DMX-Vorlagen  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] stellt interaktive DMX-Abfragevorlagen bereit, die Sie verwenden können, um DMX-Abfragen zu erstellen. Wenn die Vorlagenliste nicht angezeigt wird, klicken auf der Symbolleiste auf **Ansicht** , und wählen Sie **Vorlagen-Explorer**aus. Klicken Sie auf das Cubesymbol, um alle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Vorlagen, einschließlich der Vorlagen für DMX, MDX und XMLA, anzuzeigen.  
  
 Um mithilfe einer Vorlage eine Abfrage zu erstellen, können Sie die Vorlage in ein geöffnetes Abfragefenster ziehen oder auf die Vorlage doppelklicken, um eine neue Verbindung und einen neuen Abfragebereich zu öffnen.  
  
 Ein Beispiel zum Erstellen einer Vorhersageabfrage aus einer Vorlage finden Sie unter [Erstellen einer Singleton-Vorhersageabfrage aus einer Vorlage](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md).  
  
> [!WARNING]  
>  Das Data Mining Add-In für Microsoft Office Excel enthält ebenfalls eine Reihe von Vorlagen und einen interaktiven Abfrage-Generator, der Sie beim Verfassen komplexer DMX-Anweisungen unterstützt. Um die Vorlagen zu verwenden, klicken Sie im Data Mining-Client auf **Abfrage**und anschließend auf **Erweitert** .  
  
##  <a name="bkmk_SSIS"></a> Data Mining-Komponenten von Integration Services  
 Sie können Vorhersageabfragen auch in ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket aufnehmen. Die folgenden Tasks und Transformationen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützen die Erstellung und die Ausführung von DMX-Vorhersageabfragen und DMX-Anweisungen.  
  
|Komponente|Description|  
|---------------|-----------------|  
|Data Mining-Abfragetask|Führt DMX-Abfragen und andere DMX-Anweisungen als Teil einer Ablaufsteuerung aus.<br /><br /> Der Task-Editor stellt den Generator für Vorhersageabfragen und ein Textfeld für die manuelle Bearbeitung der DMX-Abfrage zur Verfügung. Der Task-Editor kann die Abfrage jedoch nicht gegen Objekte in einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Lösung prüfen. Daher empfiehlt es sich, eine Abfrage in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] zu erstellen und dann den Text der Anweisung oder Abfrage in den Task-Editor einzufügen.|  
|Transformation für Data Mining-Abfragen|Führt unter Verwendung von Daten, die von einer Datenflussquelle bereitgestellt wurden, eine Vorhersageabfrage innerhalb eines Datenflusses aus.<br /><br /> Der Task-Editor stellt den Generator für Vorhersageabfragen und ein Textfeld für die manuelle Bearbeitung der DMX-Abfrage zur Verfügung.<br /><br /> Die Transformation kann nur zum Erstellen von Abfragen verwendet werden, die Daten im Datenfluss verwenden, d. h. Abfragen, die die PREDICTION JOIN-Syntax verwenden. Diese Komponente kann nicht zum Ausführen von Inhaltsabfragen oder anderen Arten von DMX-Anweisungen verwendet werden.|  
  
##  <a name="bkmk_API"></a> Anwendungsprogrammierschnittstelle  
 Sie können benutzerdefinierte Anwendungen, durch die Abfragen für Data Mining-Modelle ausgeführt werden, unter Verwendung verschiedener Programmiersprachen in Verbindung mit Serverprotokollen wie OLE DB oder dem ADOMD-Client von Analysis Services erstellen. Weitere Informationen finden Sie unter [Data Mining-Programmierung](../../analysis-services/data-mining-programming.md).  
  
 XMLA bildet jedoch das zugrunde liegende Nachrichtenformat für alle Interaktionen mit einem Analysis Services-Server. Abfragen innerhalb einer XMLA-Nachricht werden unterschiedlich dargestellt, je nachdem, ob Sie eine Vorhersageabfrage auf Grundlage von DMX, eine Inhaltsabfrage oder eine Abfrage senden, von der Modellmetadaten mithilfe der Data Mining-Schemarowsets abgerufen werden.  
  
-   Der Text von **Vorhersageabfragen** (und allen anderen DMX-Anweisungen) wird unter Verwendung der [Execute-Methode&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md) gesendet, wobei die DMX-Abfrage als Text in das [Statement-Element &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) des [Command-Elements &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md) eingefügt wird.  
  
-   Um den **Modellinhalt** und **Modellmetadaten** wie die Anzahl der Cluster, die in Entscheidungsstrukturen verwendeten Attribute, das letzte Verarbeitungsdatum des Modells und die beim Erstellen des Modells verwendeten Algorithmusparameter abzurufen, können Sie die [Discover-Methode &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md) verwenden und im Header des [RequestType-Elements &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) eines der Data Mining-Schemarowsets angeben. Um den Abfragebereich einzugrenzen, geben Sie innerhalb des [RestrictionList-Elements &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/restrictionlist-element-xmla.md) Kriterien zur Einschränkung ein.  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Grundlegendes zur SELECT-Anweisung (DMX)](../../dmx/understanding-the-dmx-select-statement.md)   
 [Struktur und die Verwendung von DMX-Vorhersageabfragen](../../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Erstellen einer Vorhersageabfrage mithilfe des Generators für Vorhersageabfragen](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)   
 [Erstellen einer DMX-Abfrage in SQL Server Management Studio](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)  
  
  

