---
title: "Arbeitsbereichsdatenbank (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 0d10c2fab9cb3a613446015e8bd3dbe3dbdce868
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="workspace-database-ssas-tabular"></a>Arbeitsbereichsdatenbank (SSAS – tabellarisch)
  Die Arbeitsbereichsdatenbank für Tabellenmodelle, die während der Modellerstellung verwendet wird, wird erstellt, wenn Sie ein Projekt für Tabellenmodelle in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]anlegen.
  
## <a name="specifying-a-workspace-instance"></a>Angeben einer Arbeitsbereichinstanz  
  Beim Erstellen eines neuen Tabellenmodellprojekts mit SSDT können Sie eine Analysis Services-Instanz angeben, die beim Erstellen des Projekts verwendet werden soll. Mit dem [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]-Release vom September 2016 (14.0.60918.0) wurden für die Erstellung eines neuen Tabellenmodellprojekts zwei Modi zum Angeben einer Arbeitsbereichsinstanz eingeführt. 

**Ein integrierter Arbeitsbereich:** Verwendet die SSDT-eigene Analysis Services-Instanz

**Ein Arbeitsbereichsserver:** Eine Arbeitsbereichsdatenbank wird auf einer expliziten Analysis Services-Instanz erstellt, die sich häufig auf dem gleichen Computer wie SSDT oder auf einem anderen Computer im selben Netzwerk befindet.


  
### <a name="integrated-workspace"></a>Ein integrierter Arbeitsbereich:
Bei einem integrierten Arbeitsbereich wird eine Arbeitsdatenbank speicherintern mithilfe der SSDT-eigenen, impliziten Analysis Services-Instanz erstellt. Der Modus „Integrierter Arbeitsbereich“ reduziert die Komplexität der Erstellung von tabellarischen Projekten in SSDT erheblich, da keine separate, explizite Installation von SQL Server Analysis Services erforderlich ist.

Mit dem Modus „Integrierter Arbeitsbereich“ startet SSDT für Analysis Services-Projekte für tabellarische Modelle im Hintergrund dynamisch eine eigene interne SSAS-Instanz und lädt die Datenbank. Sie können Tabellen, Spalten und Daten im Modell-Designer hinzufügen und anzeigen. Wenn Sie weitere Tabellen, Spalten, Beziehungen usw. hinzufügen, ändern Sie die Arbeitsbereichsdatenbank. Der Modus „Integrierter Arbeitsbereich“ verändert die Funktionsweise von SSDT für Analysis Services-Projekte für tabellarische Modelle mit einem Arbeitsbereichsserver und einer Arbeitsbereichsdatenbank nicht. Was sich ändert, ist der Ort, an dem SSDT für Analysis Services-Projekte für tabellarische Modelle die Arbeitsbereichsdatenbank hostet.

Sie können den Modus „Integrierter Arbeitsbereich“ zum Erstellen eines neuen Tabellenmodellprojekts in SSDT auswählen.

![Der SSAS-Modus „Integrierter Arbeitsbereich“](../../analysis-services/tabular-models/media/ssas-integrated-workspace-mode.png)

Sie können mithilfe der Eigenschaften „Arbeitsbereichsdatenbank“ und „Arbeitsbereichsserver“ für „model.bim“ den Namen der temporären Datenbank und den TCP-Port der internen SSAS-Instanz ermitteln, auf der SSDT für Analysis Services-Projekte für tabellarische Modelle die Datenbank hostet. Sie können die Arbeitsbereichsdatenbank so lange mit SSMS verbinden, wie die Datenbank in SSDT für Analysis Services-Projekte für tabellarische Modelle geladen ist. Die Einstellung „Arbeitsbereich beibehalten“ gibt an, dass SSDT für Analysis Services-Projekte für tabellarische Modelle die Arbeitsbereichsdatenbank auf dem Datenträger, aber nicht im Arbeitsspeicher beibehält, nachdem ein Modellprojekt geschlossen wurde. Dies reduziert die Arbeitsspeicherauslastung gegenüber einer permanenten Beihaltung des Modells im Arbeitsspeicher. Wenn Sie diese Einstellungen steuern möchten, legen Sie die Eigenschaft „Modus ,Integrierter Arbeitsbereich‘“ auf FALSE fest, und stellen Sie einen expliziten Arbeitsbereichsserver bereit. Ein expliziter Arbeitsbereichsserver ist auch sinnvoll, wenn die Daten, die Sie in ein Modell importieren, die Speicherkapazität Ihrer SSDT-Arbeitsstation überschreiten.

> [!NOTE]  
>  Bei Verwendung der integrierten Arbeitsbereich Modus ist die lokale Instanz von Analysis Services 64-Bit-während SSDT in der 32-Bit-Umgebung von Visual Studio ausgeführt wird. Wenn Sie eine Verbindung zu speziellen Datenquellen herstellen, sollten Sie unbedingt sowohl die 32-Bit- als auch die 64-Bit-Version der entsprechenden Datenanbieter auf Ihrer Arbeitsstation installieren. Der 64-Bit-Anbieter ist erforderlich für die 64-Bit-Analysis Services-Instanz und die 32-Bit-Version ist erforderlich, damit der Tabellenimport-Assistent in SSDT.

###  <a name="bkmk_overview"></a> Ein Arbeitsbereichsserver:  
 Eine Arbeitsbereichsdatenbank wird auf der von der Eigenschaft Arbeitsbereichsserver angegebenen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz erstellt, wenn ein neues Business Intelligence-Projekt anhand einer der Projektvorlagen für tabellarische Modelle in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]erstellt wird. Jedes tabellarische Modellprojekt verfügt über eine eigene Arbeitsbereichsdatenbank. Sie können [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden, um die Arbeitsbereichsdatenbank auf dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server anzuzeigen. Der Name der Arbeitsbereichsdatenbank umfasst den Projektnamen, gefolgt von einem Unterstrich, dem Benutzernamen, einem weiteren Unterstrich und einer GUID.  
  
 Die Arbeitsbereichsdatenbank befindet sich im Arbeitsspeicher, während das tabellarische Modellprojekt in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]geöffnet ist. Wenn Sie das Projekt schließen, wird die Arbeitsbereichsdatenbank entweder im Arbeitsspeicher beibehalten, auf dem Datenträger gespeichert und aus dem Arbeitsspeicher entfernt (Standardeinstellung) oder aus dem Arbeitsspeicher entfernt und nicht auf dem Datenträger gespeichert. Dies hängt von der Einstellung der Eigenschaft Arbeitsbereich beibehalten ab. Weitere Informationen zur Eigenschaft Arbeitsbereich beibehalten finden Sie weiter unten im Abschnitt [Eigenschaften von Arbeitsbereichsdatenbanken](#bkmk_ws_prop) .  
  
 Nachdem Sie dem Modellprojekt mit dem Tabellenimport-Assistenten oder mit „Kopieren/Einfügen“ Daten hinzugefügt haben, zeigen Sie die Arbeitsbereichsdatenbank an, wenn Sie Tabellen, Spalten und Daten im Modell-Designer anzeigen. Wenn Sie weitere Tabellen, Spalten, Beziehungen usw. hinzufügen, ändern Sie die Arbeitsbereichsdatenbank.  
  
 Wenn Sie ein tabellarisches Modellprojekt bereitstellen, wird die bereitgestellte Modelldatenbank, die letztlich eine Kopie der Arbeitsbereichsdatenbank ist, auf der in der Bereitstellungsserver-Eigenschaft angegebenen Analysis Server-Instanz erstellt. Weitere Informationen zur Bereitstellungsserver-Eigenschaft finden Sie unter [Projekteigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md).  
  
 Die Arbeitsbereichsdatenbank des Modells befindet sich in der Regel auf "localhost" oder einer lokalen benannten Instanz eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Servers. Sie können die Arbeitsbereichsdatenbank mithilfe einer Remoteinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] hosten, diese Konfiguration wird jedoch aufgrund der Latenzzeit während Datenabfragen und anderer Einschränkungen nicht empfohlen. Im Idealfall werden die Arbeitsbereichsdatenbanken von der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz auf demselben Computer gehostet wie [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Wenn Modellprojekte auf demselben Computer wie die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz erstellt werden, von der die Arbeitsbereichsdatenbank gehostet wird, kann sich dies leistungssteigernd auswirken.  
  
 Remote-Arbeitsbereichsdatenbanken unterliegen folgenden Einschränkungen:  
  
-   Potenzielle Latenzzeit während der Abfragen.  
  
-   Die Eigenschaft **Datensicherung**kann nicht auf Auf Datenträger sichern festgelegt werden.  
  
-   Sie können keine Daten aus einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe importieren, wenn Sie mit der Projektvorlage für das Importieren von Daten aus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ein neues Tabellenmodellprojekt erstellen.  
  
  > [!IMPORTANT]  
>  Der Kompatibilitätsgrad für das Modell und der Arbeitsbereichsserver müssen zueinander passen.
  
> [!NOTE]  
>  Wenn eine der Tabellen im Modell eine große Anzahl von Zeilen aufweist, erwägen Sie, während der Modellerstellung nur eine Teilmenge der Daten zu importieren. Sie können die Verarbeitungszeit und den Verbrauch von Arbeitsbereichsdatenbank-Serverressourcen reduzieren, indem Sie eine Teilmenge der Daten importieren.  
  
> [!NOTE]  
>  Das Vorschaufenster auf der Seite Tabellen und Sichten auswählen im Tabellenimport-Assistenten im Dialogfeld Tabelleneigenschaften bearbeiten und im Dialogfeld Partitions-Manager enthält die Tabellen, Spalten und Zeilen in der Datenquelle und kann nicht die gleichen Tabellen, Spalten und Zeilen enthalten wie die Arbeitsbereichsdatenbank.  
  
  
##  <a name="bkmk_ws_prop"></a> Eigenschaften von Arbeitsbereichsdatenbanken  
 Die Eigenschaften von Arbeitsbereichsdatenbanken sind in den Modelleigenschaften enthalten. Um Modelleigenschaften in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im **Projektmappen-Explorer**anzuzeigen, klicken Sie auf die Datei **Model.bim** . Modelleigenschaften können mit dem **Eigenschaftenfenster** konfiguriert werden. Die Eigenschaften von Arbeitsbereichsdatenbanken umfassen:  
  
> [!NOTE]  
>  Auf die Eigenschaften **Modus „Integrierter Arbeitsbereich“**, **Arbeitsbereichsserver**, **Arbeitsbereich beibehalten** und **Datensicherung** werden beim Erstellen eines neuen Modellprojekts die Standardeinstellungen angewendet. Die Standardeinstellungen für neue Modellprojekte können auf der Seite **Datenmodellierung** in den Einstellungen für **Analysis-Server** im Dialogfeld „Extras/Optionen“ geändert werden. Diese und andere Eigenschaften können auch für jedes Modellprojekt im **Eigenschaftenfenster** festgelegt werden. Änderungen an den Standardeinstellungen wirken sich nicht auf bereits erstellte Modellprojekte aus. Weitere Informationen finden Sie unter [Konfigurieren von Standarddatenmodellierung und Bereitstellungseigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Modus „Integrierter Arbeitsbereich“**|TRUE, FALSE|Wenn bei der Projekterstellung der Modus „Integrierter Arbeitsbereich“ für die Arbeitsbereichsdatenbank ausgewählt ist, ist diese Eigenschaft TRUE. Wenn bei der Projekterstellung der Modus **Arbeitsbereichsserver** ausgewählt ist, ist diese Eigenschaft FALSE. | 
|**Arbeitsbereichsdatenbank**|Name|Der Name der Arbeitsbereichsdatenbank. Diese Eigenschaft kann nicht bearbeitet werden, wenn der **Modus „Integrierter Arbeitsbereich“** auf **TRUE**festgelegt ist.|  
|**Arbeitsbereich beibehalten**|Aus dem Arbeitsspeicher entladen|Gibt an, wie eine Arbeitsbereichsdatenbank beibehalten wird, nachdem ein Modellprojekt geschlossen wurde. Eine Arbeitsbereichsdatenbank enthält Modellmetadaten, die in ein Modell importiert wurden. In einigen Fällen kann die Arbeitsbereichsdatenbank sehr groß sein und viel Arbeitsspeicher benötigen. Wenn Sie ein Modellprojekt in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]schließen, wird die Arbeitsbereichsdatenbank standardmäßig aus dem Arbeitsspeicher entladen. Wenn Sie diese Einstellung ändern, sind die folgenden Überlegungen wichtig: verfügbare Speicherressourcen und wie häufig das Modellprojekt bearbeitet werden soll. Für diese Eigenschafteneinstellung gibt es die folgenden Optionen:<br /><br /> **Im Arbeitsspeicher beibehalten** : Gibt an, dass die Arbeitsbereichsdatenbank im Arbeitsspeicher beibehalten wird, nachdem ein Modellprojekt geschlossen wurde. Diese Option erfordert mehr Arbeitsspeicher. Wenn Sie jedoch ein Modellprojekt in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]öffnen, werden weniger Ressourcen belegt, und die Arbeitsbereichsdatenbank wird schneller geladen.<br /><br /> **Aus dem Arbeitsspeicher entladen** : Gibt an, dass die Arbeitsbereichsdatenbank auf dem Datenträger, aber nicht im Arbeitsspeicher beibehalten wird, nachdem ein Modellprojekt geschlossen wurde. Diese Option belegt weniger Arbeitsspeicher. Wenn Sie jedoch ein Modellprojekt in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]öffnen, muss die Arbeitsbereichsdatenbank erneut angefügt werden. Zusätzliche Ressourcen werden belegt, und das Laden des Modellprojekts dauert länger, als wenn die Arbeitsbereichsdatenbank im Arbeitsspeicher beibehalten wird. Verwenden Sie diese Option, wenn die Arbeitsspeicherressourcen beschränkt sind, oder wenn Sie mit einer Remote-Arbeitsbereichsdatenbank arbeiten.<br /><br /> **Arbeitsbereich löschen** : Gibt an, dass die Arbeitsbereichsdatenbank aus dem Arbeitsspeicher gelöscht und nicht auf dem Datenträger beibehalten wird, nachdem das Modellprojekt geschlossen wurde. Diese Option erfordert weniger Arbeitsspeicher und Speicherplatz. Wenn Sie jedoch ein Modellprojekt in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]öffnen, werden zusätzliche Ressourcen belegt, und das Laden des Modellprojekts dauert länger, als wenn die Arbeitsbereichsdatenbank im Arbeitsspeicher oder auf dem Datenträger beibehalten wird. Verwenden Sie diese Option, wenn Sie nur gelegentlich an Modellprojekten arbeiten.<br /><br /> Die Standardeinstellung für diese Eigenschaft kann auf der Seite **Datenmodellierung** in den Einstellungen für **Analysis-Server** im Dialogfeld „Extras/Optionen“ geändert werden. Diese Eigenschaft kann nicht bearbeitet werden, wenn der **Modus „Integrierter Arbeitsbereich“** auf **TRUE**festgelegt ist.|  
|**Workspace Server**|localhost|Diese Eigenschaft gibt den Standardserver an, der zum Hosten der Arbeitsbereichsdatenbank verwendet wird, während das Modellprojekt in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]erstellt wird. Alle verfügbaren [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanzen, die auf dem lokalen Computer ausgeführt werden, sind im Listenfeld enthalten.<br /><br /> Um einen anderen (im tabellarischen Modus ausgeführten) [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server anzugeben, geben Sie den Servernamen ein. Der angemeldete Benutzer muss Administrator auf dem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server sein.<br /><br /> Es wird empfohlen, einen lokalen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server als Arbeitsbereichsserver anzugeben. Für Arbeitsbereichsdatenbanken auf einem Remoteserver wird das Importieren aus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nicht unterstützt. Außerdem können Daten nicht lokal gesichert werden, und bei Abfragen kommt es auf der Benutzeroberfläche möglicherweise zu Latenzen.<br /><br /> Die Standardeinstellung für diese Eigenschaft kann in den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Einstellungen im Dialogfeld „Extras\Optionen“ auf der Seite „Datenmodellierung“ geändert werden. Diese Eigenschaft kann nicht bearbeitet werden, wenn der **Modus „Integrierter Arbeitsbereich“** auf **TRUE**festgelegt ist.|  
  
##  <a name="bkmk_use_ssms"></a> Verwenden von SSMS zur Verwaltung von Arbeitsbereichsdatenbanken  
 Sie können SQL Server Management Studio (SSMS) zum Herstellen einer Verbindung zu einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server verwenden, der eine Arbeitsbereichsdatenbank hostet. In der Regel ist keine Verwaltung der Arbeitsbereichsdatenbank erforderlich. Eine Ausnahme liegt jedoch vor, wenn eine Arbeitsbereichsdatenbank getrennt oder gelöscht werden soll. Diese Schritte müssen in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]vorgenommen werden. Verwenden Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nicht, um die Arbeitsbereichsdatenbank zu verwalten, während das Projekt im Modell-Designer geöffnet ist. Dies kann zu Datenverlusten führen.
   
## <a name="see-also"></a>Siehe auch  
[Modelleigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/model-properties-ssas-tabular.md) 
  
  
