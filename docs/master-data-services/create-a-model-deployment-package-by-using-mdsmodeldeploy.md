---
title: Erstellen eines Modellbereitstellungspakets mit MDSModelDeploy | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c2687e39-dc20-494f-a707-2aa29f4c329e
caps.latest.revision: 13
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11ddf076e371a44b457ba03dd95a35c666da1b0f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Erstellen eines Modellbereitstellungspakets mit MDSModelDeploy

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Sie verwenden in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]das Tool MDSModelDeploy, um ein Paket zu erstellen. Abhängig von den angegebenen Befehlen kann das Paket folgenden Inhalt haben:  
  
-   Nur Modellobjekte.  
  
-   Modellobjekte und Daten.  
  
 Wenn Sie ein Paket bereitstellen möchten, das nur Modellobjekte enthält, können Sie stattdessen den Modellbereitstellungs-Assistenten in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung verwenden. Weitere Informationen finden Sie unter [Erstellen eines Modellbereitstellungspakets mithilfe des Assistenten](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
1.  Die grundlegenden Berechtigungen zum Ausführen des MDSModelDeploy-Tools lauten wie folgt:  
  
    -   Die gleiche Windows-Berechtigung wie der MDS-Konfigurations-Manager (Windows-Administrator)  
  
    -   DBA-Berechtigung für die MDS-Datenbank  
  
2.  Die grundlegenden Berechtigungen zum Erstellen des Pakets mit dem MDSModelDeploy-Tool lauten wie folgt:  
  
    -   MDS-Modelladministratorberechtigung für das Datenmodell.  
  
    -   Informationen zu Berechtigungen für MDS-Import/Export-Funktionsbereiche  
  
3.  Die grundlegenden Berechtigungen zum Bereitstellen eines Modells mit dem MDSModelDeploy-Tool lauten wie folgt:  
  
    -   Funktionsberechtigung für den MDS-Explorer  
  
    -   Funktionsberechtigung für die MDS-Systemverwaltung  
  
4.  Die grundlegenden Berechtigungen zum Auflisten von Modellen mit dem MDSModelDeploy-Tool lauten wie folgt:  
  
    -   Funktionsberechtigung für den MDS-Explorer  
  
    -   MDS-Modelladministratorberechtigung für das Datenmodell zum Anzeigen des Modells in der Liste.  
  
 Es muss ein Modell vorhanden sein, aus dem Sie ein Paket erstellen können. Weitere Informationen finden Sie unter [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md).  
  
 Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
### <a name="to-create-a-model-deployment-package-by-using-mdsmodeldeploy"></a>So erstellen Sie ein Modellbereitstellungspaket mit MDSModelDeploy  
  
1.  Öffnen Sie eine Administrator-Eingabeaufforderung.  
  
2.  Navigieren Sie zum Speicherort von "MDSModelDeploy.exe".  
  
    -   Wenn MDS am Standardspeicherort installiert wurde, befindet sich die Datei unter „ *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services\Configuration“.  
  
    -   Wenn MDS nicht am Standardspeicherort installiert wurde, suchen Sie auf dem lokalen Computer nach der Datei "MDSModelDeploy.exe".  
  
3.  Optional. Dient zum Anzeigen der Optionen und der Hilfe.  
  
    -   Geben Sie `MDSModelDeploy` ein, und drücken Sie EINGABETASTE, um alle verfügbaren Optionen anzuzeigen.  
  
    -   Geben Sie Folgendes ein, um Hilfe für eine Option anzuzeigen, wobei *OptionName* der Name der Option ist: `MDSModelDeploy help OptionName`.  
  
4.  Optional. Wenn Sie über mehrere Webanwendungen verfügen, bestimmen Sie den Namen des Diensts, für den Sie die Bereitstellung durchführen, indem Sie diesen Befehl eingeben und die EINGABETASTE drücken:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Eine Liste von Werten wird zurückgegeben, z. B. `MDS1, Default Web Site, MDS`. Der erste Wert in dieser Liste (in diesem Fall `MDS1`) wird benötigt, um das Modell bereitzustellen.  
  
5.  Geben Sie Folgendes ein, um ein Paket zu erstellen, das Modellobjekte und Daten enthält. Dabei gilt: *ModelName*, *VersionName*, *ServiceName*und *PackageName* sind die Namen des Modells, der Version, des Diensts bzw. der PKG-Ausgabedatei:  
  
    ```  
    MDSModelDeploy createpackage -model ModelName -version VersionName -service ServiceName -package PackageName -includedata  
    ```  
  
     Wenn Sie keine Daten einschließen möchten, verwenden Sie nicht die Schalter `-version` und `-includedata` .  
  
6.  Drücken Sie die EINGABETASTE. Nach der erfolgreichen Erstellung des Pakets wird eine Meldung angezeigt, die besagt, dass der MDSModelDeploy-Vorgang erfolgreich abgeschlossen wurde.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Optionen für Modellbereitstellung &#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md)   
 [Bereitstellen von Modellen &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
