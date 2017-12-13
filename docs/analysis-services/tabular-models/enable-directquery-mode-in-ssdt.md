---
title: Aktivieren des DirectQuery-Modus in SSDT | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1866cd3c6194edf7065ebb2929cc77f8cc4acc3a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="enable-directquery-mode-in-ssdt"></a>Aktivieren des DirectQuery-Modus in SSDT
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]In diesem Thema beschreiben wir zum Aktivieren der für ein Projekt für tabellarische Modelle im DirectQuery-Modus [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
Wenn Sie den DirectQuery-Modus für ein tabellarisches Modell aktivieren, entwerfen Sie in SSDT:
-   Funktionen, die mit dem DirectQuery-Modus inkompatibel sind, werden deaktiviert.  
-   Das vorhandene Modell wird überprüft. Warnungen werden angezeigt, wenn Funktionen mit dem DirectQuery-Modus inkompatibel sind.  
-   Wenn die Daten bereits vor der Aktivierung des DirectQuery-Modus importiert wurden, wird der Cache des Arbeitsmodells geleert.  
  
### <a name="enable-directquery"></a>Aktivieren von DirectQuery  
  
Ändern Sie in SSDT im Bereich **Eigenschaften** für die Datei **Model.bim** die Eigenschaft **DirectQuery-Modus**auf **On**.  

![Aktivieren des DirectQuery-Modus in SSDT](../../analysis-services/tabular-models/media/enable-directquery-mode-in-ssdt.png)
  
Wenn Ihr Modell bereits eine Verbindung zu einer Datenquelle sowie mit vorhandene Daten hergestellt hat, werden Sie aufgefordert, Datenbankanmeldeinformationen zur Verbindung mit der relationalen Datenbank einzugeben. Bereits vorhandene Daten innerhalb des Modells werden aus dem In-Memory-Cache entfernt.  
  
Wenn Ihr Modell vor der Aktivierung des DirectQuery-Modus teilweise oder zu 100 % abgeschlossen ist, erhalten Sie möglicherweise Fehler in Bezug auf nicht kompatible Funktionen. Öffnen Sie in Visual Studio die **Fehlerliste** , und beheben Sie alle Probleme, durch die verhindert werden würde, dass das Modell in den DirectQuery-Modus wechselt.  


### <a name="whats-next"></a>Wie geht es weiter? 
Sie können nun Daten mit dem Tabellenimport-Assistenten zum Abrufen von Metadaten für das Modell importieren. Sie erhalten keine Datenzeilen, aber Tabellen, Spalten und Beziehungen als Grundlage für Ihr Modell. 

Sie können für jede Tabelle eine Beispielpartition erstellen und Beispieldaten hinzufügen, damit Sie Modellverhalten bei der Erstellung überprüfen können. Beispieldaten, die Sie hinzufügen, werden in **Analysieren für Excel** oder in anderen Clienttools verwendet, die eine Verbindung mit der Arbeitsbereichsdatenbank herstellen können. Einzelheiten finden Sie unter [Hinzufügen von Beispieldaten zu einem DirectQuery-Modell im Entwurfsmodus](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) .  
  
> [!TIP]  
    >  Selbst im DirectQuery-Modus bei einem leeren Modell können Sie sich immer für jede Tabelle ein kleines eingebautes Rowset anzeigen lassen. Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]auf **Tabelle** > **Tabelleneigenschaften** , um das Dataset mit 50 Zeilen anzuzeigen.  
  
  
## <a name="see-also"></a>Siehe auch  
[Aktivieren des DirectQuery-Modus in SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Hinzufügen von Beispieldaten zu einem DirectQuery-Modell im Entwurfsmodus](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)
  
