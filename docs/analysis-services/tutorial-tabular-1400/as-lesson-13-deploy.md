---
title: 'Analysis Services Tutorial Lektion 13: Bereitstellen | Microsoft Docs'
description: Beschreibt, wie in Analysis Services Tutorial-Projekt bereitstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 874d185c5210da9fd8af7e18d79f1e6eed96f7e9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="deploy"></a>Bereitstellen

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion Konfigurieren Sie Bereitstellungseigenschaften; ein Server zum Bereitstellen und einen Namen für das Modell angeben. Anschließend wird das Modell auf dem Server bereitstellen. Nachdem das Modell bereitgestellt wird, können Benutzer das Herstellen einer Verbindung mit einer berichterstellungsclientanwendung. Weitere Informationen finden Sie unter [Bereitstellung in Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) und [tabellenmodelllösungsbereitstellung](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **5 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 12: Analysieren in Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Wenn Azure Analysis Services bereitstellen, benötigen Sie [Administratorberechtigungen](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) auf dem Server.  

> [!IMPORTANT]  
> Wenn Sie die AdventureWorksDW-Beispieldatenbank auf einer lokalen SQL Server installiert, und Sie Ihr Modell mit einem Azure Analysis Services-Server Bereitstellen einer [On-Premises Data Gateway](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) ist erforderlich.
  
## <a name="deploy-the-model"></a>Bereitstellen des Modells  
  
#### <a name="to-configure-deployment-properties"></a>So konfigurieren Sie Bereitstellungseigenschaften  

  
1.  In **Projektmappen-Explorer**, mit der rechten Maustaste die **AW Internet Sales** Projekt, und klicken Sie dann auf **Eigenschaften**.  
  
2.  In der **Eigenschaftenseiten des AW Internet Sales** Dialogfeld unter **Bereitstellungsserver**in der **Server** -Eigenschaft, geben Sie den vollständigen Servernamen. Wenn eine Verbindung mit Azure Analysis Services herstellen, muss die Servernamen enthält die vollständige URL.

    ![als lesson13-bereitstellen-Eigenschaft](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  In der **Datenbank** Eigenschaft **Adventure Works-Internetverkäufe**.  
  
4.  In der **Modellname** Eigenschaft **Adventure Works Internet Sales Model**.  
  
5.  Überprüfen Sie die Auswahl, und klicken Sie anschließend auf **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Die Adventure Works-Internetverkäufe bereitstellen
  
1.  In **Projektmappen-Explorer**, mit der rechten Maustaste die **AW Internet Sales** Projekt > **erstellen**.  

2.  Mit der rechten Maustaste die **AW Internet Sales** Projekt > **bereitstellen**.

    Beim Bereitstellen auf Azure Analysis Services können Sie aufgefordert, Ihr Konto einzugeben. Geben Sie Ihr Unternehmenskonto und-Kennwort, z. B. nancy@adventureworks.com. Dieses Konto muss in "Administratoren" auf dem Server sein.
  
    Das Dialogfeld "Bereitstellen" wird angezeigt und zeigt den Bereitstellungsstatus der Metadaten und jeder im Modell enthaltenen Tabelle an.  
    
    ![als-lesson13-bereitstellen-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. Wenn die Bereitstellung erfolgreich abgeschlossen wurde, fahren Sie fort, und klicken Sie auf **Schließen**.  
  

In dieser Lektion wird beschrieben, die am häufigsten verwendete und einfachste Methode zum Bereitstellen eines tabellarischen Modells von SSDT. Erweiterte Bereitstellungsoptionen, z. B. den Bereitstellungs-Assistenten oder mit XMLA und AMO automatisieren bieten eine größere Flexibilität, Konsistenz- und geplante Bereitstellungen. Weitere Informationen finden Sie unter [tabellenmodelllösungsbereitstellung](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).

## <a name="conclusion"></a>Fazit  
Gratulation! Sie sind nicht mehr benötigen, erstellen und Bereitstellen von Ihrem ersten tabellarischen Analysis Services-Modell. Mit diesem Lernprogramm wurden Sie durch die häufigsten Aufgaben zur Erstellung eines Tabellenmodells geführt. Nach der Bereitstellung des Adventure Works-Internetverkaufsmodells können Sie nun mit SQL Server Management Studio das Modell verwalten und Prozessskripts sowie einen Sicherungsplan erstellen. Benutzer können jetzt auch mit dem Modell mithilfe einer Clientanwendung zur berichtserstellung wie Microsoft Excel oder Power BI eine Verbindung herstellen.  

![Ssms als lesson13](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>Wie geht es weiter?
[Herstellen einer Verbindung mit Power BI Desktop](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[Ergänzende Lektion - dynamische Sicherheit](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[Ergänzende Lektion - Detailzeilen](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[Ergänzende Lektion - unregelmäßige Hierarchien](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
