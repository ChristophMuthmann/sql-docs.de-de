---
title: "Importieren aus Analysis Services (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: b9a21b23-3a06-4ef8-bc06-9c79cdc54870
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 81cee939240fd9379f2c521443272ae478de6243
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="import-from-analysis-services-ssas-tabular"></a>Importieren aus Analysis Services (SSAS – tabellarisch)
  In diesem Thema wird beschrieben, wie Sie ein neues Projekt für tabellarische Modelle erstellen, indem Sie die Metadaten mithilfe der Projektvorlage Von Server importieren in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aus einem vorhandenen tabellarischen Modell importieren.  
  
## <a name="create-a-new-model-by-importing-metadata-from-an-existing-model-in-analysis-services"></a>Erstellen eines neuen Modells durch Importieren von Metadaten aus einem vorhandenen Modell in Analysis Services  
 Erstellen Sie mithilfe der Projektvorlage Von Server importieren ein neues tabellarisches Modellprojekt, indem Sie die Metadaten aus einem vorhandenen tabellarischen Modell auf einem Analysis Services-Server kopieren. Das neue Projekt wird mit den gleichen Datenquellenverbindungen, Tabellen, Beziehungen, Measures, KPIs, Rollen, Hierarchien, Perspektiven und Partitionen wie das Modell erstellt, aus dem es importiert wurde. Die Daten werden jedoch nicht aus dem vorhandenen Modell in den Arbeitsbereich des neuen Modells kopiert. Sobald der Importvorgang abgeschlossen und das neue Modellprojekt erstellt wurde, müssen Sie Alles verarbeiten (Alles aktualisieren) ausführen, um die Daten aus den Datenquellen in die Arbeitsbereichsdatenbank des neuen Modellprojekts zu laden.  
  
#### <a name="to-create-a-new-model-by-importing-metadata-from-an-existing-model"></a>So erstellen Sie ein neues Modell durch Importieren von Metadaten aus einem vorhandenen Modell  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf das Menü **Datei** , auf **Neu**und dann auf **Projekt**.  
  
2.  Klicken Sie im Dialogfeld **Neues Projekt** unter **Installierte Vorlagen**auf **Business Intelligence**und dann auf **Von Server importieren**.  
  
3.  Geben Sie unter **Name**einen Namen für das Projekt ein. Geben Sie dann einen Speicherort und einen Projektmappennamen an, und klicken Sie auf **OK**.  
  
4.  Geben Sie im Dialogfeld **Aus Analysis Services importieren** im Feld **Servername**den Namen des Analysis Services-Servers ein, auf dem sich die zu importierenden Modellmetadaten befinden.  
  
5.  Wählen Sie im Feld **Datenbankname**die Datenbank für das tabellarische Modell aus, die die Modellmetadaten enthält, die Sie importieren möchten, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Projekteigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  

