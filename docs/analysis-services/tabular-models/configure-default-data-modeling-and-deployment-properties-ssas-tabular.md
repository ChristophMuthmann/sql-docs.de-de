---
title: "Konfigurieren von Standarddatenmodellierung und Bereitstellungseigenschaften (SSAS – tabellarisch) | Microsoft Docs"
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
f1_keywords:
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql13.asvs.bidtoolset.deployment.f1
- sql13.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 704a719e3f2d509b5a949f7e44dd86cdcea7b183
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>Konfigurieren von Standarddatenmodellierung und Bereitstellungseigenschaften (SSAS – tabellarisch)
  In diesem Thema wird die Konfiguration der Einstellungen für die Eigenschaften Standardkompatibilitätsgrad, Bereitstellung und Arbeitsbereichsdatenbank beschrieben, die für jedes neue Projekt für tabellarische Modelle, das Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellen, vorab definiert werden können. Auch nachdem ein neues Projekt erstellt wurde, können diese Eigenschaften abhängig von Ihren speziellen Anforderungen geändert werden.  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>So konfigurieren Sie die Einstellung der Eigenschaft "Standardkompatibilitätsgrad" für neue Modellprojekte  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Extras** , und klicken Sie anschließend auf **Optionen**.  
  
2.  Erweitern Sie im Dialogfeld **Optionen** **Analysis Services-Tabellen-Designer**, und klicken Sie anschließend auf **Kompatibilitätsgrad**.  
  
3.  Konfigurieren Sie die folgenden Eigenschafteneinstellungen:  
  
    |Eigenschaft|Standardeinstellung|Description|  
    |--------------|---------------------|-----------------|  
    |**Standardkompatibilitätsgrad für neue Projekte**|SQL Server 2016 (1200)|Mit dieser Einstellung wird der beim Erstellen eines neuen Projekts für tabellarische Modelle zu verwendende Standardkompatibilitätsgrad angegeben. Sie können SQL Server 2012 (1100) auswählen, wenn die Bereitstellung in einer Analysis Services-Instanz ohne SP1 erfolgt, oder SQL Server 2012 SP1 oder höher, wenn in der Bereitstellungsinstanz SP1 angewendet wird. Weitere Informationen finden Sie unter [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
    |**Kompatibilitätsgradoptionen**|Alles überprüft|Gibt Kompatibilitätsgradoptionen für neue Projekte für tabellarische Modelle und für das Bereitstellen in eine andere Analysis Services-Instanz an.|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>So konfigurieren Sie die Einstellung der Eigenschaft „Standardbereitstellungsserver“ für neue Modellprojekte  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Extras** , und klicken Sie anschließend auf **Optionen**.  
  
2.  Erweitern Sie im Dialogfeld **Optionen** **Analysis Services-Tabellen-Designer**, und klicken Sie anschließend auf **Bereitstellung**.  
  
3.  Konfigurieren Sie die folgenden Eigenschafteneinstellungen:  
  
    |Eigenschaft|Standardeinstellung|Description|  
    |--------------|---------------------|-----------------|  
    |**Standard-Deployment Server**|localhost|Diese Einstellung gibt den Standardserver an, der beim Bereitstellen eines Modells verwendet werden soll. Sie können auf den Pfeil nach unten klicken, um nach verfügbaren lokalen Analysis Services-Netzwerkservern zu suchen, oder den Namen eines Remoteservers eingeben.|  
  
    > [!NOTE]  
    >  Änderungen an der Einstellung der Eigenschaft Standardbereitstellungsserver wirken sich nicht auf vorhandene Projekte aus, die vor der Änderung erstellt wurden.  
  
###  <a name="bkmk_conf_default"></a> So konfigurieren Sie die Einstellungen der Eigenschaft "Standardarbeitsbereichsdatenbank" für neue Modellprojekte  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf **Extras** , und klicken Sie anschließend auf **Optionen**.  
  
2.  Erweitern Sie im Dialogfeld **Optionen** **Analysis Services-Tabellen-Designer**, und klicken Sie anschließend auf **Arbeitsbereichsdatenbank**.  
  
3.  Konfigurieren Sie die folgenden Eigenschafteneinstellungen:  
  
    |Eigenschaft|Standardeinstellung|Description|  
    |--------------|---------------------|-----------------|  
    |**Standard-Arbeitsbereichsserver**|**localhost**|Diese Eigenschaft gibt den Standardserver an, der zum Hosten der Arbeitsbereichsdatenbank verwendet wird, während das Modell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellt wird. Alle verfügbaren Analysis Services-Instanzen, die auf dem lokalen Computer ausgeführt werden, sind im Listenfeld enthalten.<br /><br /> <br /><br /> Hinweis: Es wird empfohlen, dass Sie immer einen lokalen Analysis Services-Server als Arbeitsbereichsserver angeben. Für Arbeitsbereichsdatenbanken auf einem Remoteserver wird das Importieren von Daten aus [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nicht unterstützt. Außerdem können Daten nicht lokal gesichert werden, und bei Abfragen kommt es auf der Benutzeroberfläche möglicherweise zu Latenzen.|  
    |**Beibehalten der Arbeitsbereichsdatenbank nach dem Schließen des Modells**|**Arbeitsbereichsdatenbanken auf dem Datenträger beibehalten, aber aus dem Arbeitsspeicher entladen**|Gibt an, wie eine Arbeitsbereichsdatenbank beibehalten wird, nachdem ein Modell geschlossen wurde. Eine Arbeitsbereichsdatenbank enthält Modellmetadaten, die in ein Modell importierten Daten und Identitätswechselinformationen (verschlüsselt). In einigen Fällen kann die Arbeitsbereichsdatenbank sehr groß sein und viel Arbeitsspeicher benötigen. Arbeitsbereichsdatenbanken werden standardmäßig aus dem Arbeitsspeicher entfernt. Wenn Sie diese Einstellung ändern, sind die folgenden Überlegungen wichtig: verfügbare Speicherressourcen und wie häufig das Modell bearbeitet werden soll. Für diese Eigenschafteneinstellung gibt es die folgenden Optionen:<br /><br /> **Arbeitsbereiche im Arbeitsspeicher beibehalten** – Gibt an, dass Arbeitsbereiche im Arbeitsspeicher beibehalten werden, nachdem ein Modell geschlossen wurde. Diese Option erfordert mehr Arbeitsspeicher. Wenn Sie jedoch ein Modell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]öffnen, werden weniger Ressourcen belegt, und der Arbeitsbereich wird schneller geladen.<br /><br /> **Arbeitsbereichsdatenbanken auf dem Datenträger beibehalten, aber aus dem Arbeitsspeicher entladen** – Gibt an, dass die Arbeitsbereichsdatenbank auf dem Datenträger beibehalten werden, nach dem Schließen eines Modells aber nicht mehr im Arbeitsspeicher verfügbar sein soll. Diese Option erfordert weniger Arbeitsspeicher. Wenn Sie jedoch ein Modell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]öffnen, werden zusätzliche Ressourcen belegt, und das Laden des Modells dauert länger, als bei einer Arbeitsbereichsdatenbank, die im Arbeitsspeicher beibehalten wird. Verwenden Sie diese Option, wenn die Arbeitsspeicherressourcen beschränkt sind, oder wenn Sie mit einer Remote-Arbeitsbereichsdatenbank arbeiten.<br /><br /> **Arbeitsbereich löschen** – Gibt an, dass die Arbeitsbereichsdatenbank aus dem Arbeitsspeicher gelöscht und nicht auf dem Datenträger beibehalten wird, nachdem das Modell geschlossen wurde. Diese Option erfordert weniger Arbeitsspeicher und Speicherplatz. Wenn Sie jedoch ein Modell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]öffnen, werden zusätzliche Ressourcen belegt, und das Laden des Modells dauert länger, als bei einer Arbeitsbereichsdatenbank, die im Arbeitsspeicher oder auf dem Datenträger beibehalten wird. Verwenden Sie diese Option, wenn Sie nur gelegentlich an Modellen arbeiten.|  
    |**Datensicherung**|**Datensicherung auf Datenträger beibehalten**|Gibt an, ob eine Sicherung der Modelldaten in einer Sicherungsdatei beibehalten wird. Für diese Eigenschafteneinstellung gibt es die folgenden Optionen:<br /><br /> **Datensicherung auf Datenträger beibehalten** – Gibt an, dass eine Sicherung der Modelldaten auf dem Datenträger beibehalten wird. Wenn das Modell gespeichert wird, werden die Daten auch in der Sicherungsdatei (ABF) gespeichert. Wenn diese Option ausgewählt wird, dauert es möglicherweise länger, Modelle zu speichern und zu laden.<br /><br /> **Keine Datensicherung auf dem Datenträger beibehalten** – Gibt an, dass keine Sicherung der Modelldaten auf dem Datenträger beibehalten wird. Diese Option minimiert die Speicher- und Ladezeiten für Modelle.|  
  
> [!NOTE]  
>  Änderungen an Standardmodelleigenschaften wirken sich nicht auf die Eigenschaften vorhandener Modelle aus, die vor der Änderung erstellt wurden.  
  
## <a name="see-also"></a>Siehe auch  
 [Projekteigenschaften &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)   
 [Modelleigenschaften &#40; SSAS – tabellarisch &#41;](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
