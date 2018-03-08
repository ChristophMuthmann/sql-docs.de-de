---
title: "Ziel-Editor für SAP BW (Seite „Zuordnungen“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3019f68825fd8fd52ea85b9b1b5c0fad37b4fb2b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="sap-bw-destination-editor-mappings-page"></a>Ziel-Editor für SAP BW (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** im **Ziel-Editor für SAP BW** können Sie eine Zuordnung zwischen Eingabe- und Zielspalten vornehmen.  
  
 Weitere Informationen zum SAP BW-Ziel von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW finden Sie unter [SAP BW-Ziel](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
 **So öffnen Sie die Seite "Zuordnungen"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem das SAP BW-Ziel enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf das SAP BW-Ziel.  
  
3.  Klicken Sie im **Ziel-Editor für SAP BW**auf **Zuordnungen** , um die Seite **Zuordnungen** des Editors zu öffnen.  
  
## <a name="options"></a>Tastatur  
  
> [!NOTE]  
>  Wenn Sie nicht alle Werte kennen, die zur Konfiguration des Ziels erforderlich sind, müssen Sie ggf. Ihren SAP-Administrator um Unterstützung bitten.  
  
 Die Seite **Zuordnungen** im **Ziel-Editor für SAP BW** besteht aus zwei Abschnitten:  
  
-   Der obere Abschnitt enthält die verfügbaren Eingabe- und Zielspalten. Dort können Sie Zuordnungen zwischen den beiden Spaltentypen erstellen.  
  
-   Der untere Abschnitt ist eine Tabelle, der Sie entnehmen können, welche Eingabespalten welchen Ausgabespalten zugeordnet wurden.  
  
### <a name="upper-section-options"></a>Optionen im oberen Abschnitt  
 Der obere Abschnitt enthält die folgenden Optionen:  
  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an.  
  
 Um einer Zielspalte eine Eingabespalte zuzuordnen, ziehen Sie eine Spalte aus der Liste **Verfügbare Eingabespalten** auf eine Spalte in der Liste **Verfügbare Zielspalten** .  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an.  
  
 Um einer Zielspalte eine Eingabespalte zuzuordnen, ziehen Sie eine Spalte aus der Liste **Verfügbare Eingabespalten** auf eine Spalte in der Liste **Verfügbare Zielspalten** .  
  
 Der obere Abschnitt enthält auch ein Kontextmenü, das Sie öffnen, indem Sie mit der rechten Maustaste auf den Hintergrund klicken. Das Kontextmenü enthält die folgenden Optionen:  
  
-   **Alle Zuordnungen auswählen**  
  
-   **Ausgewählte Zuordnungen löschen**  
  
-   **Elemente nach übereinstimmenden Namen zuordnen**  
  
### <a name="lower-section-columns"></a>Spalten im unteren Abschnitt  
 Der untere Abschnitt enthält eine Tabelle der Zuordnungen und weist die folgenden Spalten auf:  
  
 **Eingabespalte**  
 Zeigt die ausgewählten Eingabespalten an.  
  
 Um derselben Zielspalte eine andere Eingabespalte zuzuordnen, wählen Sie eine andere Eingabespalte aus der Liste aus. Wählen Sie zum Entfernen einer Zuordnung **\<ignore>** aus, um die Eingabespalte von der Ausgabe auszuschließen.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, und zwar unabhängig davon, ob die Spalte zugeordnet ist oder nicht.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ziel-Editor für SAP BW &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Ziel-Editor für SAP BW &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Ziel-Editor für SAP BW &#40;Seite „Erweitert“&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
