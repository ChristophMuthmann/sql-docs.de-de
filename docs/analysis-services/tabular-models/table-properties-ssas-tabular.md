---
title: "Tabelleneigenschaften (SSAS – tabellarisch) | Microsoft Docs"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.tableprop.f1
ms.assetid: 16d3347b-7e43-4a6b-9956-fdd6ede092e6
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a72cbc5fe8e27ee559f748fd93c50a7db8f75a94
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="table-properties-ssas-tabular"></a>Tabelleneigenschaften (SSAS – tabellarisch)
  In diesem Thema werden Tabelleneigenschaften für tabellarische Modelle beschrieben. Die hier beschriebenen Eigenschaften unterscheiden sich von den Eigenschaften im Dialogfeld Tabelleneigenschaften bearbeiten, mit denen definiert wird, welche Spalten aus der Quelle importiert werden.  
  
 Abschnitte in diesem Thema:  
  
-   [Tabelleneigenschaften](#bkmk_properties)  
  
-   [Konfigurieren der Einstellungen für Tabelleneigenschaften](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a> Tabelleneigenschaften  
 **Standard**  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Verbindungsname**|\<Verbindungsname >|Der Name der Verbindung mit der Datenquelle der Tabelle.<br /><br /> Klicken Sie auf die Schaltfläche, um die Verbindung zu bearbeiten.|  
|**Hidden**|False|Gibt an, ob die Tabelle in den Feldlisten von Berichtserstellungsclients ausgeblendet wird.|  
|**Partitionen**||Partitionen für die Tabelle können nicht im **Eigenschaftenfenster** angezeigt werden. Klicken Sie zum Anzeigen, Erstellen oder Bearbeiten von Partitionen auf die Schaltfläche, um den Partitions-Manager zu öffnen.|  
|**Quelldaten**||Quelldaten für die Tabelle können nicht im **Eigenschaftenfenster** angezeigt werden. Klicken Sie zum Anzeigen oder Bearbeiten der Quelldaten auf die Schaltfläche, um das Dialogfeld Tabelleneigenschaften bearbeiten zu öffnen.|  
|**Tabellenbeschreibung**||Eine Textbeschreibung für die Tabelle.<br /><br /> Wenn ein Endbenutzer in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]den Cursor über dieser Tabelle in der Feldliste platziert, wird die Beschreibung als QuickInfo angezeigt.|  
|**Tabellenname**|\<Anzeigename >|Gibt den Anzeigenamen der Tabelle an. Der Tabellenname kann angegeben werden, wenn eine Tabelle mit dem Tabellenimport-Assistenten importiert wird, oder jederzeit nach dem Import. Der Tabellenname im Modell kann sich von der zugeordneten Tabelle am Quellort unterscheiden. Der Anzeigename der Tabelle wird in der Feldliste einer Clientanwendung zur Berichterstellung sowie in der Modelldatenbank in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]angezeigt.|  
  
 **Berichterstellungseigenschaften**  
  
 Ausführliche Beschreibungen und Informationen zur Konfiguration für Berichterstellungseigenschaften finden Sie unter [Power View-Berichterstellungseigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md).  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Standardfeldsatz**|||  
|Tabellenverhalten|||  
  
##  <a name="bkmk_config_prop"></a> Konfigurieren der Einstellungen für Tabelleneigenschaften  
  
1.  Klicken Sie im Modell-Designer in der Datensicht auf eine Tabelle (Registerkarte) oder in der Diagrammsicht auf einen Tabellenkopf.  
  
2.  Klicken Sie im **Eigenschaftenfenster** auf eine Eigenschaft, und geben Sie einen Wert ein, oder klicken Sie auf die Schaltfläche für weitere Konfigurationsoptionen.  
  
  

