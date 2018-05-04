---
title: Bereitstellen von SQL Server Datatools | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 94d9b0cd934dfe3738c24e1ca2c1e6230a4f3873
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-from-sql-server-data-tools"></a>Bereitstellen in SQL Server Data Tools
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Verwenden Sie die Aufgaben in diesem Thema, um eine Projektmappe für tabellarische Modelle bereitstellen, indem Sie mit dem Bereitstellungsbefehl in SSDT.  
  
##  <a name="bkmk_deploy"></a> Konfigurieren der Eigenschaften "Bereitstellungsoptionen" und "Bereitstellungsserver"  
 Bevor Sie die Projektmappe für tabellarische Modelle bereitstellen, müssen Sie die Eigenschaft Bereitstellungsoptionen und die Eigenschaft Bereitstellungsserver angeben. Weitere Informationen zu Bereitstellungseigenschaften und Einstellungen finden Sie unter [tabellenmodelllösungsbereitstellung](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
#### <a name="to-configure-options-and-properties"></a>So konfigurieren Sie Optionen und Eigenschaften  
  
1.  In SSDT im **Projektmappen-Explorer**mit der rechten Maustaste auf den Projektnamen, und klicken Sie dann auf **Eigenschaften**.  
  
2.  In der  **\<Projektname > Eigenschaften** Dialogfeld im **Bereitstellungsoptionen**, eigenschafteneinstellungen angeben, wenn diese von den Standardeinstellungen abweichen.  
  
    > [!NOTE]  
    >  Für Modelle, die sich im zwischengespeicherten Modus befinden, ist der **Abfragemodus** immer auf **InMemory**festgelegt.  
  
    > [!NOTE]  
    >  Für Modelle im DirectQuery-Modus können keine **Identitätswechseleinstellungen** angegeben werden.  
  
3.  Legen Sie unter **Bereitstellungsserver**die Einstellungen der Eigenschaften **Server** (Name), **Edition**, **Datenbank** (Name) und **Cubename** fest, falls diese von den Standardeinstellungen abweichen, und klicken Sie anschließend auf **OK**.  
  
> [!NOTE]  
>  Sie können auch die Einstellung der Eigenschaft Standardbereitstellungsserver angeben, damit alle neu erstellten Projekte automatisch auf dem angegebenen Server bereitgestellt werden. Weitere Informationen finden Sie unter [modellierungs- und Bereitstellungseigenschaften Standardeigenschaften konfigurieren](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
##  <a name="bkmk_deploy_proc"></a> Bereitstellen eines tabellarischen Modells  
  
#### <a name="to-deploy-a-tabular-model"></a>Zum Bereitstellen eines tabellarischen Modells
  
-   In SSDT auf dem **erstellen** Menü klicken Sie auf **bereitstellen \<Projektname >**.  
  
     Im Dialogfeld **Bereitstellen** wird der Status der Metadatenbereitstellung und der Verarbeitung jeder im Modell enthaltenen Tabelle angezeigt (es sei denn, die Eigenschaft „Verarbeitungsoption“ wurde auf „Nicht verarbeiten“ festgelegt). Nachdem der Bereitstellungsvorgang abgeschlossen ist, verwenden Sie SSMS eine Verbindung mit Analysis Services-Instanz, und stellen Sie sicher, dass das neue modelldatenbankobjekt erstellt wurde, oder verwenden Sie die clientberichterstellungsanwendung, für die Verbindung mit dem bereitgestellten Modell.  
  
##  <a name="bkmk_deploy_status"></a> Bereitstellungsstatus  
 Im Dialogfeld **Bereitstellen** können Sie den Status eines Bereitstellungsvorgangs überwachen. Außerdem kann ein Bereitstellungsvorgang beendet werden.  
  
 **Status**  
 Gibt an, ob der Bereitstellungsvorgang erfolgreich war.  
  
 **Details**  
 Listet die bereitgestellten Metadatenelemente sowie den Status für jedes Metadatenelement auf und stellt eine Meldung über etwaige Probleme bereit.  
  
 **Bereitstellung beenden**  
 Klicken Sie auf diese Option, um den Bereitstellungsvorgang anzuhalten. Diese Option ist nützlich, wenn der Bereitstellungsvorgang zu lange dauert oder wenn es zu viele Fehler gibt.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenmodelllösungsbereitstellung](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)   
 [Konfigurieren von Standarddatenmodellierung und Bereitstellungseigenschaften](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
  
  
