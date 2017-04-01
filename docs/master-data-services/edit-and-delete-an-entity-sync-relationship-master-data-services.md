---
title: "Bearbeiten und L&#246;schen einer Entit&#228;ten-Synchronisierungspartnerschaft (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a5e37f3-352e-45a6-b4a0-6f98f83b4bd8
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# Bearbeiten und L&#246;schen einer Entit&#228;ten-Synchronisierungspartnerschaft (Master Data Services)
  Entitäten-Synchronisierung ist eine unidirektionale und wiederholbare Synchronisierung zwischen Entitätsversionen. Sie bietet eine Möglichkeit, Entitätsdaten zwischen verschiedenen Modellen freizugeben. Sie können eine Synchronisierungspartnerschaft, die Sie erstellt haben, bearbeiten und löschen.  
  
## Erforderliche Komponenten  
 Voraussetzungen zum Bearbeiten einer Entitäten-Synchronisierungspartnerschaft.  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Systemverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator des Zielmodells sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Sie müssen für die Quellentität und deren Entitätsattribute und -elemente mindestens über Lesezugriff verfügen.  
  
 Voraussetzungen zum Löschen einer Entitäten-Synchronisierungspartnerschaft.  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Systemverwaltung" zuzugreifen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
-   Sie müssen ein Modelladministrator des Zielmodells sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 Berücksichtigen Sie Folgendes, wenn Sie eine Entitäten-Synchronisierungspartnerschaft bearbeiten.  
  
-   Die Quell- und Zielentität müssen sich in unterschiedlichen Modellen befinden  
  
-   Für einen Versionsstatus der Zielentität muss kein Commit ausgeführt werden.  
  
-   Sobald eine Synchronisierungspartnerschaft eingerichtet wurde, wird das Ziel sofort mit der Quelle synchronisiert.  
  
-   Eine Zielentitätsversion kann keine Quellentitätsversion einer anderen Synchronisierungspartnerschaft sein.  
  
 Berücksichtigen Sie Folgendes, wenn Sie eine Entitäten-Synchronisierungspartnerschaft ausführen.  
  
-   Nur Blattelemente werden kopiert.  
  
-   Domänenbasierte Attribute werden nicht kopiert.  
  
-   Vorläufig gelöschte Elemente werden nicht kopiert.  
  
-   Durch die Synchronisierung werden keine Zielentitätstransaktionen/-verläufe generiert.  
  
 **So bearbeiten Sie eine Entitäten-Synchronisierungspartnerschaft**  
  
1.  Klicken Sie im Master Data Manager auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten**, und klicken Sie auf **Entitätensynchronisierung**.  
  
3.  Wählen Sie auf der Seite **Entity Sync Maintenance** (Entitätssynchronisierungsverwaltung) eine Synchronisierungspartnerschaft im Raster aus.  
  
4.  Klicken Sie auf **Bearbeiten**. Auf der rechten Seite wird ein Bereich angezeigt.  
  
5.  Ändern Sie die **Häufigkeit**. Wählen Sie **Synchronisierung bei Bedarf** oder **Automatische Synchronisierung** aus, und legen Sie die Häufigkeit fest.  
  
6.  Klicken Sie auf **Speichern**.  
  
 **So löschen Sie eine Entitäten-Synchronisierungspartnerschaft**  
  
1.  Klicken Sie im Master Data Manager auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Seite **Modellansicht** auf der Menüleiste auf **Verwalten**, und klicken Sie auf **Entitätensynchronisierung**.  
  
3.  Wählen Sie auf der Seite **Entity Sync Maintenance** (Entitätssynchronisierungsverwaltung) eine Synchronisierungspartnerschaft im Raster aus.  
  
4.  Klicken Sie auf **Löschen**.  
  
5.  Klicken Sie im Bestätigungsdialogfeld auf **OK**.  
  
## Siehe auch  
 [Erstellen und Verwenden einer Beziehung für die Entitätensynchronisierung &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Entitäten-Synchronisierungspartnerschaft &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md)  
  
  