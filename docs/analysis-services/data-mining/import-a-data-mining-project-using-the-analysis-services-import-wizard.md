---
title: Importieren Sie eine Data Mining-Projekte mit der Analysis Services-Import-Assistenten | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62bc9fc5-c6ff-4517-b598-d92df76743a2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9ac94cfcd17842f118ea6bda19af830d8d737b94
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>Importieren eines Data Mining-Projekts mithilfe des Analysis Services-Import-Assistenten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
In diesem Thema wird beschrieben, wie ein neues Data Mining-Projekt erstellt wird, indem die Metadaten aus einem vorhandenen Data Mining-Projekt auf einen anderen Server mithilfe der Vorlage **Import from Server (Multidimensional and Data Mining) Project** (Vom Server importieren (mehrdimensionales und Data Mining-Projekt)) in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] importiert werden.  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>Importieren von Datenquellen, Miningstrukturen und Miningmodellen aus einem vorhandenen Data Mining-Projekt  
 Wenn Sie die Vorlage **Import from Server (Multidimensional and Data Mining) Project**verwenden, erstellt [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ein neues Data Mining-Projekt und kopiert die Metadaten anschließend aus dem angegebenen Data Mining-Projekt. Das neue Projekt enthält die gleichen Datenquellen, Datenquellensichten, Miningstrukturen und Miningmodelle wie die ssASnoversion-Datenbank, aus der der Import erfolgt ist. Das Projekt kann jedoch erst verwendet werden, wenn Sie bestimmte Eigenschaften aktualisiert und die Objekte wie beschrieben verarbeitet haben:  
  
-   Die Daten selbst werden nicht vom Quellserver in das neue Data Mining-Projekt kopiert – nur die Definitionen der Datenquellen und Datenquellensichten werden importiert. Nachdem der Importvorgang abgeschlossen ist und die Objekte erstellt wurden, müssen Sie die Objekte mit Daten auffüllen, indem Sie die Miningstrukturen und abhängigen Modelle trainieren. Sie können den Befehl **Alles verarbeiten** im Data Mining-Designer verwenden, um die Modelle und Strukturen zu trainieren.  
  
-   Wenn Sie ein Projekt importieren, das in einer früheren Version von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellt wurde, könnte die Datenquelle Anbieter verwenden, die nicht auf dem Server installiert sind, auf den Sie das Projekt importieren. Wenn beim Verarbeiten der importierten Miningstrukturen Fehler auftreten, klicken Sie mit der rechten Maustaste auf jede Datenquelle, und wählen Sie **Designer öffnen** aus, um die Verbindungszeichenfolge zu bearbeiten und die Anbietereigenschaften zu überprüfen.  
  
     Zu diesem Zeitpunkt müssen Sie ggf. auch überprüfen, ob das Konto, das Sie zum Verarbeiten der Data Mining-Objekte oder Abfragen von Data Mining-Modellen verwenden, über die notwendigen Berechtigungen für die Datenquelle verfügt.  
  
-   Wenn Sie ein Projekt importieren, wird standardmäßig die Arbeitsbereichsdatenbank auf "localhost" oder auf die als **Standardzielserver** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]konfigurierte Standardinstanz festgelegt. Um diese Eigenschaft festzulegen, wählen Sie im Menü **Optionen** **Business Intelligence-Designer**aus und anschließend **Analysis Services**, und wählen Sie dann **Allgemein**aus.  
  
     Beachten Sie, dass in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]eine weitere separate Option vorhanden ist, die Sie festlegen können, um den Standardbereitstellungsserver für tabellarische [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Modellprojekte zu konfigurieren. Die Einstellung **Standard-Deployment Server**bestimmt die Standardarbeitsbereichsdatenbank für tabellarische Modellprojekte. Sie können keine Instanzen verwenden, die tabellarische Modelle für Data Mining-Projekte unterstützen.  
  
     Wenn Sie die Standardbereitstellungsdatenbank nicht ändern können, um eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zu verwenden, die im mehrdimensionalen oder Data Mining-Modus ausgeführt wird, können Sie immer die Bereitstellungsdatenbank mit dem Dialogfeld **Projekteigenschaften** angeben.  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>So erstellen Sie ein neues Data Mining-Projekt durch Importieren eines vorhandenen Data Mining-Projekts  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Datei** , auf **Neu**und dann auf **Projekt**.  
  
2.  Klicken Sie im Dialogfeld **Neues Projekt** unter **Installierte Vorlagen**auf **Business Intelligence**und anschließend auf **Analysis Services**&gt; **Import from Server (Multidimensional/Data Mining)**(Von Server importieren (Multidimensional/Data Mining)).  
  
3.  Geben Sie unter **Name**einen Namen für das Projekt ein. Geben Sie dann einen Speicherort und einen Projektmappennamen an, und klicken Sie auf **OK**.  
  
     Der **Assistent zum Importieren einer Analysis Services-Datenbank** wird gestartet. Klicken Sie auf der Willkommensseite auf "OK", um fortzufahren.  
  
4.  Geben Sie auf der Seite **Quelldatenbank auswählen**für **Server**die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz an, die die Projektmappe enthält, die Sie importieren möchten.  
  
     Wählen Sie die **-Datenbank, die die zu importierenden Data Mining-Objekte enthält, für**Datenbank [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aus.  
  
    > [!WARNING]  
    >  Sie können die Objekte nicht angeben, die Sie importieren möchten. Wenn Sie eine vorhandene [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank auswählen, werden alle mehrdimensionalen und Data Mining-Objekte importiert.  
  
     Klicken Sie auf **Weiter**.  
  
5.  Die Seite **Assistenten abschließen**zeigt den Fortschritt beim Import an. Sie können den Vorgang nicht abbrechen oder die Objekte ändern, die importiert werden. Klicken Sie anschließend auf **Fertig stellen** .  
  
     Das neue Projekt wird automatisch mit [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]geöffnet.  
  
## <a name="see-also"></a>Siehe auch  
 [Projekteigenschaften](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
