---
title: Projekteigenschaften | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.depservconfig.f1
- sql13.asvs.bidtoolset.semmodelprojprop.f1
ms.assetid: 333c1fc0-361c-415a-bd68-4e057f67bcb7
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8eb7f31bb441a724835da814ffe005efa34c6883
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="project-properties"></a>Projekteigenschaften 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Dieser Artikel beschreibt die Eigenschaften für modellprojekte. Jedes Projekt für tabellarische Modelle verfügt über Eigenschaften für Bereitstellungsoptionen und den Bereitstellungsserver, die angeben, wie das Projekt und das Modell bereitgestellt werden. Beispielsweise den Server, auf dem das Modell bereitgestellt wird, und den Namen der bereitgestellten Modelldatenbank. Diese Einstellungen unterscheiden sich von Modelleigenschaften, die sich auf die Arbeitsbereichsdatenbank des Modells auswirken. Die hier beschriebenen Projekteigenschaften befinden sich in einem modalen Eigenschaftendialogfeld, das sich von dem Eigenschaftenfenster unterscheidet, in dem andere Typen von Eigenschaften angezeigt werden. Klicken Sie zum Anzeigen der modalen Projekteigenschaften in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]in **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
 Abschnitte in diesem Thema:  
  
-   [Projekteigenschaften](#bkmk_proj_properties)  
  
-   [Konfigurieren der Einstellungen der Eigenschaften „Bereitstellungsoptionen“ und „Bereitstellungsserver“](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a> Projekteigenschaften  
 **Bereitstellungsoptionen**  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Verarbeitungsoption**|**Standardwert**|Analysis Services bestimmt standardmäßig den Verarbeitungstyp, der beim Bereitstellen der an Objekten vorgenommenen Änderungen erforderlich ist. Diese Einstellung ermöglicht im Allgemeinen die schnellste Bereitstellungszeit. Sie haben aber auch die Möglichkeit, für die jeweilige Bereitstellung die vollständige Verarbeitung oder keine Verarbeitung zu wählen.|  
|**Transaktionsbereitstellung**|**False**|Gibt an, ob es sich um eine Transaktionsbereitstellung des Modells handelt. Standardmäßig ist die Bereitstellung aller oder geänderter Objekte keine Transaktionsbereitstellung bei der Verarbeitung dieser bereitgestellten Objekte. Die Bereitstellung kann erfolgreich ausgeführt werden und persistent sein, auch wenn bei der Verarbeitung ein Fehler auftritt. Sie können diese Einstellung ändern, um die Bereitstellung und Verarbeitung in einer einzelnen Transaktion zu integrieren.|  
|**Abfragemodus**|**Speicherintern**|Gibt die Quelle an, aus der Abfrageergebnisse zurückgegeben werden. Weitere Informationen finden Sie unter [DirectQuery-Modus](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).|  
  
 **Bereitstellungsserver**  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Server**|**localhost**|Gibt eine Analysis Services-Instanz an. Standardmäßig werden Modelle in der Standardinstanz von Analysis Services auf dem lokalen Computer bereitgestellt. Sie können diese Einstellung ändern und eine benannte Instanz auf dem lokalen Computer bzw. eine beliebige Instanz auf einem Remotecomputer angeben, auf dem Sie über die Berechtigung zum Erstellen von Analysis Services-Objekten verfügen. Normalerweise sind dies Administratorberechtigungen.<br /><br /> Die Standardeinstellung für diese Eigenschaft kann im Dialogfeld Extras\Optionen auf der Seite Bereitstellung in den Analysis-Server-Einstellungen mithilfe der Eigenschaft Standardbereitstellungsserver geändert werden. Weitere Informationen finden Sie unter [modellierungs- und Bereitstellungseigenschaften Standardeigenschaften konfigurieren](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).|  
|**Edition**|**Entwickler**|Gibt die Edition des Analysis Services-Servers an, auf dem das Modell bereitgestellt wird. In der Serveredition sind verschiedene Funktionen definiert, die in das Projekt eingebunden werden können.|  
|**Datenbank**|**Model**|Gibt den Namen der Analysis Services-Datenbank an, in der die Modellobjekte nach der Bereitstellung instanziiert werden. Dieser Name wird in einer Datenverbindung oder einer RSDS-Datenverbindungsdatei angegeben. Es wird empfohlen, einen Namen anzugeben, der den Typ der Analyse widerspiegelt, die mit dem Modell durchgeführt wird, z. B. AdventureWorksSalesModel.<br /><br /> Um doppelte Namen für bereitgestellte Modelle zu vermeiden, sollten Sie die Namenseinstellung der **Datenbank** -Eigenschaft ändern, um sie dem Modellzweck anzupassen. Wenn Benutzer eine Verbindung mit dem Modell als Datenquelle herstellen, wird dieser Name angezeigt.|  
|**Cubename**|**Model**|Gibt den Namen des Datenbankcubes an, wie in der Datenverbindung für einen Berichtserstellungsclient angezeigt.|  
|**Version**|**13.0**|Die Version der Analysis Services-Instanz, auf der das Projekt bereitgestellt wird.|  
  
 **DirectQuery-Optionen**  
  
|Eigenschaft|Standardeinstellung|Description|  
|--------------|---------------------|-----------------|  
|**Identitätswechseleinstellungen**|**Standardwert**|Gibt die Anmeldeinformationen an, über die ein Modell, das im DirectQuery-Modus ausgeführt wird, mit Datenquellen verbunden wird. Diese Anmeldeinformationen unterscheiden sich von den Identitätswechselinformationen, die im speicherinternen Standardmodus verwendet werden. Weitere Informationen finden Sie unter [Identitätswechsel](../../analysis-services/tabular-models/impersonation-ssas-tabular.md).|  
  
##  <a name="bkmk_conf_proj_settings"></a> Konfigurieren der Einstellungen der Eigenschaften „Bereitstellungsoptionen“ und „Bereitstellungsserver“  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]in **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und klicken Sie anschließend auf **Eigenschaften**.  
  
2.  Klicken Sie im Fenster **Eigenschaften** auf eine Eigenschaft, und geben Sie dann einen Wert ein, oder klicken Sie auf den Pfeil nach unten, um eine Einstellungsoption auszuwählen.  
  
## <a name="see-also"></a>Siehe auch  
 [Modellierungs- und Bereitstellungseigenschaften Standardeigenschaften konfigurieren](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Modelleigenschaften](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [Bereitstellung von Tabellenmodelllösungen](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
