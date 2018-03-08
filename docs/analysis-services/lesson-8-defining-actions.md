---
title: 'Lektion 8: Definieren von Aktionen | Microsoft Docs'
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c34913be54a2eb74401d602f1ecafee25d5921c6
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-8-defining-actions"></a>Lektion 8: Definieren von Aktionen
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

In dieser Lektion erfahren Sie, wie Sie Aktionen in Ihrem [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekt definieren können. Eine Aktion bezeichnet einfach eine in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gespeicherte MDX-Anweisung (Multidimensional Expressions), die in Clientanwendungen integriert und von Benutzern gestartet werden kann.  
  
> [!NOTE]  
> Für alle Lektionen in diesem Lernprogramm sind abgeschlossene Projekte online verfügbar. Sie können jede Lektion aufrufen, indem Sie ein abgeschlossenes Projekt aus der vorherigen Lektion als Ausgangspunkt verwenden. [Klicken Sie hier](http://go.microsoft.com/fwlink/?LinkID=221866) , um die Beispielprojekte für dieses Lernprogramm herunterzuladen.  
  
[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt die in der folgenden Tabelle beschriebenen Typen von Aktionen.  
  
|||  
|-|-|  
|CommandLine|Führt einen Befehl an der Eingabeaufforderung aus.|  
|Dataset|Gibt ein Dataset an eine Clientanwendung zurück.|  
|Drillthrough ausführen|Gibt eine Drillthroughanweisung als Ausdruck zurück, den der Client zur Rückgabe eines Rowsets ausführt.|  
|Html|Führt ein HTML-Skript in einem Internetbrowser aus.|  
|Proprietär|Führt einen Vorgang über eine Schnittstelle aus, die nicht in dieser Tabelle aufgelistet ist.|  
|Bericht|Übermittelt eine parametrisierte, URL-basierte Anforderung an einen Berichtsserver und gibt einen Bericht an eine Clientanwendung zurück.|  
|Rowset|Gibt ein Rowset an eine Clientanwendung zurück.|  
|Anweisung|Gibt einen OLE DB-Befehl zurück.|  
|URL|Zeigt eine dynamische Webseite in einem Internetbrowser an.|  
  
Aktionen ermöglichen es Benutzern, eine Anwendung zu starten oder andere Schritte innerhalb des Kontexts eines bestimmten Elements auszuführen. Weitere Informationen finden Sie unter [Aktionen &#40;Analysis Services – mehrdimensionale Daten&#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md) und [Aktionen in mehrdimensionalen Modellen](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md).  
  
> [!NOTE]  
> Beispielaktionen finden Sie in den Aktionsbeispielen auf der Registerkarte Vorlagen im Bereich Berechnungstools oder in den Beispielen des [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW-Data Warehouse-Beispiels. Weitere Informationen zum Installieren dieser Datenbank finden Sie unter [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](../analysis-services/install-sample-data-and-projects.md).  
  
Diese Lektion enthält den folgenden Task:  
  
[Definieren und Verwenden einer Drillthroughaktion](../analysis-services/lesson-8-1-defining-and-using-a-drillthrough-action.md)  
In diesem Task definieren, verwenden und ändern Sie eine Drillthroughaktion über die Faktendimensionsbeziehung, die Sie zu einem früheren Zeitpunkt in diesem Lernprogramm definiert haben.  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 9: Defining Perspectives and Translations](../analysis-services/lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>Siehe auch  
[Analysis Services-Lernprogrammszenario](../analysis-services/analysis-services-tutorial-scenario.md)  
[Mehrdimensionale Modellierung &#40;Adventure Works-Tutorial&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
[Aktionen &#40; Analysis Services – mehrdimensionale Daten &#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[Aktionen in mehrdimensionalen Modellen](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
  
  
