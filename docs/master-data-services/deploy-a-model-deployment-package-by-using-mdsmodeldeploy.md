---
title: Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
caps.latest.revision: 16
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3447c507f51d8fba26551959db22dbca132eebeb
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Sie verwenden in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]das Tool MDSModelDeploy, um ein Paket mit dem folgenden Inhalt bereitzustellen:  
  
-   Nur Modellobjekte.  
  
-   Modellobjekte und Daten.  
  
 Wenn Sie ein Paket bereitstellen möchten, das nur Modellobjekte enthält, können Sie stattdessen den Modellbereitstellungs-Assistenten in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung verwenden. Weitere Informationen finden Sie unter [Bereitstellen eines Modellbereitstellungspakets mithilfe des Assistenten](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md).  
  
> [!IMPORTANT]  
>  Pakete können nur in der Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bereitgestellt werden, in der sie erstellt wurden. Dies bedeutet, dass in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] erstellte Pakete nicht in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] oder höher bereitgestellt werden können.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Zielumgebung zuzugreifen.  
  
-   Ein Modellbereitstellungspaket muss vorhanden sein. Weitere Informationen finden Sie unter  [Erstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
-   Sie müssen Administrator in der Umgebung sein, in der Sie das Modell bereitstellen. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
-   Wenn Sie ein Modell mit Daten aktualisieren, kann die von Ihnen bereitgestellte Version nicht den Status **Gesperrt** oder **Commit wurde ausgeführt** aufweisen.  
  
### <a name="to-deploy-a-model-deployment-package"></a>So stellen Sie ein Modellbereitstellungspaket bereit  
  
1.  Legen Sie fest, ob Sie ein neues Modell erstellen, ein Modell klonen oder ein zuvor geklontes Modell aktualisieren. Weitere Informationen finden Sie unter [Optionen für Modellbereitstellung &#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md).  
  
2.  Öffnen Sie eine Administrator-Eingabeaufforderung, und navigieren Sie zu "MDSModelDeploy.exe".  
  
    -   Wenn MDS am Standardspeicherort installiert wurde, ist das Tool unter „ *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services\Configuration“ verfügbar.  
  
    -   Wenn MDS nicht am Standardspeicherort installiert wurde, suchen Sie auf dem lokalen Computer nach der Datei "MDSModelDeploy.exe".  
  
3.  Optional. Dient zum Anzeigen der Optionen und der Hilfe.  
  
    -   Geben Sie `MDSModelDeploy` ein, und drücken Sie EINGABETASTE, um alle verfügbaren Optionen anzuzeigen.  
  
    -   Geben Sie Folgendes ein, um Hilfe für eine Option anzuzeigen, wobei *OptionName* der Name der Option ist: `MDSModelDeploy help OptionName`.  
  
4.  Optional. Wenn Sie über mehrere Webanwendungen verfügen, bestimmen Sie den Namen des Diensts, für den Sie die Bereitstellung durchführen, indem Sie diesen Befehl eingeben und die EINGABETASTE drücken:  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Eine Liste von Werten wird zurückgegeben, z. B. `MDS1, Default Web Site, MDS`. Der erste Wert in dieser Liste (in diesem Fall `MDS1`) wird benötigt, um das Modell bereitzustellen.  
  
5.  Geben Sie an der Eingabeaufforderung Folgendes ein, und drücken Sie die EINGABETASTE. Der Befehl unterscheidet sich je nachdem, ob Sie ein Modell erstellen, ein Modell klonen oder ein Modell aktualisieren.  
  
    -   So erstellen Sie ein neues Modell:  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   So erstellen Sie einen Klon eines Modells  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   So aktualisieren Sie ein vorhandenes Modell samt Daten  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  Wenn Sie das MDSModelDeploy-Tool verwenden, um ein vorhandenes Modell inklusive Daten zu aktualisieren, und das Paket keine Entität, kein Attribut oder kein Element enthält, die bzw. das im Zielmodell enthalten ist, wird diese Entität bzw. dieses Attribut oder Element von MDSModelDeploy nicht aus dem Modell gelöscht.  
  
     Dabei gilt: *PackageName* ist der Name der Paketdatei (PKG-Datei), *ModelName* ist der Name des neuen Modells, *VersionName* ist der Name der Version, und *ServiceName* ist der Name des Diensts, der im vorherigen Schritt zurückgegeben wurde. Stellen Sie sicher, dass die Modell- und Versionsnamen nach Groß-/Kleinschreibung genau mit den Namen übereinstimmen.  
  
6.  Nach der erfolgreichen Bereitstellung des Pakets wird eine Meldung angezeigt, die besagt, dass der MDSModelDeploy-Vorgang erfolgreich abgeschlossen wurde.  
  
 **Hinweise:**  
  
-   Wenn eine Abonnementsicht im Paket denselben Namen wie eine Abonnementsicht in einem vorhandenen Modell ausweist, wird eine Warnung wie diese angezeigt: **Warnung: Die Abonnementsicht des Bereitstellers wurde umbenannt.** . Für die Anzeige wird zudem *modelname.subscriptionviewname*verwendet. Wenn dieser Name bereits verwendet wird, wird die Abonnementsicht nicht erstellt.  
  
-   Der Bereitstellungsprozess umfasst vier Schritte:  
  
    1.  Die Modellobjekte werden erstellt.  
  
    2.  Geschäftsregeln werden erstellt.  
  
    3.  Abonnementsichten werden erstellt.  
  
    4.  Masterdaten werden aufgefüllt.  
  
-   Beim Erstellen eines neuen oder geklonten Modells wird das Modell gelöscht, falls der Prozess während eines beliebigen Schritts fehlschlägt.  
  
     Falls bei der Aktualisierung eines Modells der Prozess während der ersten drei Schritte fehlschlägt, wird sie nicht fortgesetzt. Für bereits vorgenommene Änderungen wird jedoch kein Rollback durchgeführt. Wenn der Prozess in Schritt 4 fehlschlägt, werden Elemente, die aktualisiert werden können, aktualisiert.  
  
## <a name="next-steps"></a>Next Steps  
 Dateiattribute sowie Benutzer- und Gruppenberechtigungen sind nicht in den Modellbereitstellungspaketen enthalten. Nachdem Sie ein Modell bereitgestellt haben, müssen diese manuell aktualisiert werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Bereitstellen von Modellen &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
