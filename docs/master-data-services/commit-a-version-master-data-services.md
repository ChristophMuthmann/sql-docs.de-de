---
title: "Durchf&#252;hren eines Commits f&#252;r eine Version (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Durchführen eines Commits für Versionen [Master Data Services]"
  - "Versionen [Master Data Services], Commit ausführen"
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Durchf&#252;hren eines Commits f&#252;r eine Version (Master Data Services)
  Führen Sie in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]einen Commit für eine Version eines Modells durch, um Änderungen an den Elementen des Modells und den Attributen zu verhindern. Versionen mit ausgeführtem Commit können nicht entsperrt werden.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich **Versionsverwaltung** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Der Status der Version muss **Gesperrt**sein. Weitere Informationen finden Sie unter [Sperren einer Version &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md).  
  
-   Alle Elemente müssen erfolgreich überprüft worden sein.  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Versionsverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### So führen Sie einen Commit für eine Version durch  
  
1.  Klicken Sie in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]auf **Versionsverwaltung**.  
  
2.  Klicken Sie auf der Seite **Versionen verwalten** auf der Menüleiste auf **Version überprüfen**.  
  
3.  Wählen Sie auf der Seite **Version überprüfen** das Modell und die Version aus, für das bzw. die Sie einen Commit durchführen möchten.  
  
4.  Klicken Sie auf **Commit**.  
  
5.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
## Nächste Schritte  
  
-   [Erstellen eines Versionsflags &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [Zuweisen eines Flags zu einer Version &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [Kopieren einer Version &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
## Siehe auch  
 [Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  