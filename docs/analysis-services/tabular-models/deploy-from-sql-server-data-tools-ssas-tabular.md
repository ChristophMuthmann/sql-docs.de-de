---
title: "Bereitstellen in SQL Server-Datentools (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.deploystatus.f1"
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# Bereitstellen in SQL Server-Datentools (SSAS – tabellarisch)
  Verwenden Sie die Aufgaben in diesem Thema, um mit dem Befehl "Bereitstellen" in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]eine Projektmappe für tabellarische Modelle bereitzustellen.  
  
 Abschnitte in diesem Thema:  
  
-   [Konfigurieren der Eigenschaften "Bereitstellungsoptionen" und "Bereitstellungsserver"](#bkmk_deploy)  
  
-   [Bereitstellen einer Projektmappe für tabellarische Modelle](#bkmk_deploy_proc)  
  
-   [Bereitstellungsstatus](#bkmk_deploy_status)  
  
##  <a name="bkmk_deploy"></a> Konfigurieren der Eigenschaften "Bereitstellungsoptionen" und "Bereitstellungsserver"  
 Bevor Sie die Projektmappe für tabellarische Modelle bereitstellen, müssen Sie die Eigenschaft Bereitstellungsoptionen und die Eigenschaft Bereitstellungsserver angeben. Weitere Informationen zu Bereitstellungseigenschaften und -einstellungen finden Sie unter [Bereitstellung von Tabellenmodelllösungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
#### So konfigurieren Sie die Eigenschaften "Bereitstellungsoptionen" und "Bereitstellungsserver"  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] im **Projektmappen-Explorer** mit der rechten Maustaste auf den Projektnamen, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Geben Sie im Dialogfeld **\<Projektname>-Eigenschaften** unter **Bereitstellungsoptionen** die Eigenschafteneinstellungen an, falls diese von den Standardeinstellungen abweichen.  
  
    > [!NOTE]  
    >  Für Modelle, die sich im zwischengespeicherten Modus befinden, ist der **Abfragemodus** immer auf **InMemory** festgelegt.  
  
    > [!NOTE]  
    >  Für Modelle im DirectQuery-Modus können keine **Identitätswechseleinstellungen** angegeben werden.  
  
3.  Legen Sie unter **Bereitstellungsserver** die Einstellungen der Eigenschaften **Server** (Name), **Edition**, **Datenbank** (Name) und **Cubename** fest, falls diese von den Standardeinstellungen abweichen, und klicken Sie anschließend auf **OK**.  
  
> [!NOTE]  
>  Sie können auch die Einstellung der Eigenschaft Standardbereitstellungsserver angeben, damit alle neu erstellten Projekte automatisch auf dem angegebenen Server bereitgestellt werden. Weitere Informationen finden Sie unter [Konfigurieren von Standarddatenmodellierung und Bereitstellungseigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
##  <a name="bkmk_deploy_proc"></a> Bereitstellen einer Projektmappe für tabellarische Modelle  
  
#### So stellen Sie eine Projektmappe für tabellarische Modelle bereit  
  
-   Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] auf das Menü **Erstellen** und anschließend auf **Projektname\> bereitstellen**.  
  
     Im Dialogfeld **Bereitstellen** wird der Status der Metadatenbereitstellung und der Verarbeitung jeder im Modell enthaltenen Tabelle angezeigt (es sei denn, die Eigenschaft „Verarbeitungsoption“ wurde auf „Nicht verarbeiten“ festgelegt). Stellen Sie nach Abschluss des Bereitstellungsprozesses mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Verbindung mit der Analysis Services-Instanz her, und überprüfen Sie, ob das neue Modelldatenbankobjekt erstellt wurde, oder verwenden Sie die Clientberichterstellungsanwendung, um eine Verbindung mit dem bereitgestellten Modell herzustellen.  
  
##  <a name="bkmk_deploy_status"></a> Bereitstellungsstatus  
 Im Dialogfeld **Bereitstellen** können Sie den Status eines Bereitstellungsvorgangs überwachen. Außerdem kann ein Bereitstellungsvorgang beendet werden.  
  
 **Status**  
 Gibt an, ob der Bereitstellungsvorgang erfolgreich war.  
  
 **Details**  
 Listet die bereitgestellten Metadatenelemente sowie den Status für jedes Metadatenelement auf und stellt eine Meldung über etwaige Probleme bereit.  
  
 **Bereitstellung beenden**  
 Klicken Sie auf diese Option, um den Bereitstellungsvorgang anzuhalten. Diese Option ist nützlich, wenn der Bereitstellungsvorgang zu lange dauert oder wenn es zu viele Fehler gibt.  
  
## Siehe auch  
 [Bereitstellung von Tabellenmodelllösungen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)   
 [Konfigurieren von Standarddatenmodellierung und Bereitstellungseigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
  
  