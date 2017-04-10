---
title: "Bereitstellen eines Modellbereitstellungspakets mithilfe des Assistenten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Bereitstellungspakete [Master Data Services], bereitstellen"
  - "Modelle [Master Data Services], Bereitstellen eines Pakets"
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
caps.latest.revision: 16
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 16
---
# Bereitstellen eines Modellbereitstellungspakets mithilfe des Assistenten
  Verwenden Sie den Modellbereitstellungs-Assistenten von [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], um Pakete bereitzustellen, die nur Modellobjekte enthalten. Wenn Sie ein Paket mit Daten bereitstellen müssen, finden Sie weitere Informationen unter [Bereitstellen eines Modellbereitstellungspakets mit MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
> [!IMPORTANT]  
>  Pakete können nur in der Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bereitgestellt werden, in der sie erstellt wurden. Dies bedeutet, dass in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] erstellte Pakete nicht in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] bereitgestellt werden können.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Systemverwaltung** in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Zielumgebung zuzugreifen.  
  
-   Ein Modellbereitstellungspaket muss vorhanden sein. Weitere Informationen finden Sie unter [Erstellen eines Modellbereitstellungspakets mithilfe des Assistenten](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md).  
  
-   Sie müssen Administrator in der Umgebung sein, in der Sie das Modell bereitstellen. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### So stellen Sie ein Modellbereitstellungspaket bereit, das ausschließlich Modellobjekte enthält  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **System** , und klicken Sie auf **Bereitstellung**.  
  
3.  Klicken Sie auf **Bereitstellen** im **Modellbereitstellungs-Assistenten**.  
  
4.  Klicken Sie auf **Durchsuchen**.  
  
5.  Suchen Sie das Bereitstellungspaket (PKG-Datei), und klicken Sie auf **Öffnen**.  
  
6.  Klicken Sie auf **Weiter**.  
  
7.  Nachdem das Paket geladen wurde, klicken Sie auf **Weiter**.  
  
8.  Wenn bereits ein Modell vorhanden ist, können Sie es aktualisieren, indem Sie **Vorhandenes Modell aktualisieren** auswählen. Wählen Sie **Neues Modell erstellen** aus, um ein neues Modell zu erstellen. Nachdem Sie auf **Weiter** geklickt haben, können Sie einen Namen für das neue Modell eingeben.  
  
9. Klicken Sie auf **Fertig stellen**, um den Assistenten zu beenden.  
  
 **Hinweise:**  
  
-   Wenn eine Abonnementsicht im Paket denselben Namen wie eine Abonnementsicht in einem vorhandenen Modell aufweist, wird eine Warnung wie diese angezeigt: **Die Abonnementsicht des Bereitstellers wurde umbenannt**. Darüber hinaus wird die Sicht als *Modellname.Name der Abonnementsicht* erstellt. Wenn dieser Name bereits verwendet wird, wird die Abonnementsicht nicht erstellt.  
  
-   Der Bereitstellungsprozess umfasst vier Schritte:  
  
    1.  Die Modellobjekte werden erstellt.  
  
    2.  Abonnementsichten werden erstellt.  
  
    3.  Geschäftsregeln werden erstellt.  
  
-   Beim Erstellen eines neuen oder geklonten Modells wird das Modell gelöscht, falls der Prozess während eines beliebigen Schritts fehlschlägt.  
  
     Falls bei der Aktualisierung eines Modells der Prozess während eines der ersten drei Schritte fehlschlägt, wird sie nicht über diesen Schritt hinaus fortgesetzt. Für bereits vorgenommene Änderungen wird jedoch kein Rollback durchgeführt.  
  
## Nächste Schritte  
 Dateiattribute sowie Benutzer- und Gruppenberechtigungen sind nicht in den Modellbereitstellungspaketen enthalten. Nachdem Sie ein Modell bereitgestellt haben, müssen diese manuell aktualisiert werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## Siehe auch  
 [Bereitstellen von Modellen &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  