---
title: "Erteilen von Berechtigungen für eine Dimension (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.roledesignerdialog.dimensions.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- read/write permissions
- user access rights [Analysis Services], dimensions
- permissions [Analysis Services], dimensions
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ccf0f7d014bfd85f3368633058984089005101ec
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>Gewähren von Berechtigungen in einer Dimension (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Dimensionssicherheit wird verwendet, zum Festlegen von Berechtigungen für ein Dimensionsobjekt, nicht für dessen Daten. Meist ist das Gewähren oder Verweigern des Zugriffs auf Verarbeitungsvorgänge das Hauptziel bei der Festlegung von Berechtigungen in einer Dimension.  
  
 Unter Umständen möchten Sie jedoch vielleicht nicht die Verarbeitungsvorgänge steuern, sondern den Datenzugriff für eine Dimension oder die darin enthaltenen Attribute und Hierarchien. Ein Unternehmen mit regionalen Vertriebsabteilungen möchte beispielsweise Verkaufsdaten für Mitarbeiter außerhalb der Abteilung sperren. Sie können Berechtigungen für Dimensionsattribute und Dimensionsmitglieder festlegen, um Zugriff auf Teile der Dimensionsdaten für unterschiedliche Komponenten zu gewähren oder zu verweigern. Beachten Sie, dass Sie nicht den Zugriff auf ein bestimmtes Dimensionsobjekt selbst, sondern nur auf dessen Daten verweigern können. Wenn Sie vor allem den Zugriff für Mitglieder in einer Dimension gewähren oder verweigern möchten, einschließlich der Zugriffsrechte für individuelle Attributhierarchien, finden Sie Informationen hierzu unter [Erteilen von benutzerdefiniertem Zugriff auf Dimensionsdaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) .  
  
 Die restlichen Abschnitte dieses Themas behandeln Berechtigungen, die Sie direkt für das Dimensionsobjekt festlegen können, einschließlich:  
  
-   Leseberechtigungen oder Lese-/Schreibberechtigungen (Sie können nur Leseberechtigungen oder Lese-/Schreibberechtigungen wählen. "Keine" ist nicht möglich.) Da Sie ja den Zugriff auf Dimensionsdaten beschränken möchten, lesen Sie unter [Erteilen von benutzerdefiniertem Zugriff auf Dimensionsdaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) nach.  
  
-   Verarbeitungsberechtigungen (Verwenden Sie diese, wenn Szenarios eine Verarbeitungsstrategie benötigen, die individuelle Berechtigungen für einzelne Objekte erforderlich macht.)  
  
-   Berechtigungen für das Lesen von Definitionen (Dies wird meist verwendet, um interaktive Verarbeitung bei einem Tool zu unterstützen oder Transparenz in einem Modell zu gewährleisten. Die Leseberechtigung für Definitionen ermöglicht das Anzeigen der Struktur einer Dimension, ohne Zugriff auf deren Daten oder die Möglichkeit zur Änderung der Definition zu gewähren.)  
  
 Wenn Sie Rollen für eine Dimension definieren, variieren die verfügbaren Berechtigungen abhängig davon, ob es sich beim Objekt um eine eigenständige Datenbankdimension – innerhalb der Datenbank, jedoch außerhalb eines Cubes – oder eine Cubedimension handelt.  
  
> [!NOTE]  
>  Standardmäßig werden Berechtigungen in einer Datenbank von einer Cubedimension geerbt. Wenn Sie zum Beispiel **Lese-/Schreibzugriff** in einer Customer-Datenbankdimension aktivieren, erbt die Customer-Cubedimension den **Lese-/Schreibzugriff** im Kontext der aktuellen Rolle. Sie können geerbte Berechtigungen löschen, wenn Sie eine Berechtigungseinstellung überschreiben möchten.  
  
## <a name="set-permissions-on-a-database-dimension"></a>Erteilen von Berechtigungen für eine Datenbankdimension  
 Datenbankdimensionen sind eigenständige Objekte innerhalb einer Datenbank, mit denen Dimensionen innerhalb desselben Modells erneut verwendet werden können. Denken Sie hierbei an eine DATE-Datenbankdimension, die in einem Modell vielfach verwendet wird, wie die Cubedimensionen Order Date, Ship Date und Due Date. Da Cubes und Datenbankdimensionen in einer Datenbank Peer-Objekte sind, können Sie Verarbeitungsberechtigungen unabhängig für jedes Objekt festlegen.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, erweitern Sie im Objekt-Explorer das **Rollen** -Element für die entsprechende Datenbank, und klicken Sie dann auf eine Datenbankrolle (oder erstellen Sie eine neue Datenbankrolle).  
  
2.  Im Bereich **Dimensionen** sollte für die Dimension **Alle Datenbankdimensionen**festgelegt sein.  
  
     Die Standardeinstellung für Berechtigungen ist **Lesen**.  
  
     Obwohl **Lese-/Schreibzugriff** verfügbar ist, wird empfohlen, diese Berechtigung nicht zu verwenden. **Lesen/Schreiben** wird für das Rückschreiben von Dimensionen verwendet, die veraltet sind. Weitere Informationen finden Sie unter [Veraltete Analysis Services-Funktionen in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md).  
  
     Optional können Sie die Berechtigungen **Definition lesen** und **Verarbeiten** für individuelle Objekte festlegen, solange diese Berechtigungen noch nicht auf Datenbankebene festgelegt wurden. Einzelheiten finden Sie unter [Erteilen von Berechtigungen zum Verarbeiten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) und [Erteilen von Berechtigungen zum Lesen von Definitionen für Objektmetadaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md).  
  
## <a name="set-permissions-on-a-cube-dimension"></a>Erteilen von Berechtigungen für eine Cubedimension  
 Cubedimensionen sind Datenbankdimensionen, die zu einem Cube hinzugefügt wurden. Als solche hängen sie strukturell von den zugehörigen Measuregruppen ab. Obwohl diese Objekte atomar verarbeitet werden können, ist es im Hinblick auf die Autorisierung sinnvoller, den Cube und die Cubedimensionen als einzelne Entität zu behandeln.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, erweitern Sie im Objekt-Explorer das **Rollen** -Element für die entsprechende Datenbank, und klicken Sie dann auf eine Datenbankrolle (oder erstellen Sie eine neue Datenbankrolle).  
  
2.  In der **Dimensionen** Bereich, ändern die Dimension festgelegt \<Cubename > **cube Dimensionen**.  
  
     Standardmäßig werden Berechtigungen von einer entsprechenden Datenbankdimension geerbt. Deaktivieren Sie das Kontrollkästchen **Erben** , um Berechtigungen von **Lesen** zu **Lesen/Schreiben**zu ändern. Lesen Sie zuerst den Hinweis im vorhergehenden Abschnitt, bevor Sie **Lesen/Schreiben**verwenden.  
  
> [!IMPORTANT]  
>  Wenn Sie mithilfe von AMO (Analysis Management Objects) Datenbankrollenberechtigungen konfigurieren, trennt jeder Verweis auf eine Cubedimension im DimensionPermission-Attribut eines Cubes die Berechtigungsvererbung aus dem DimensionPermission-Attribut der Datenbank. Weitere Informationen zu AMO finden Sie unter [Entwickeln mit Analysis Management Objects &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Rollen und Berechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Erteilen von Berechtigungen für Datamining-Strukturen und Modelle &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Erteilen von benutzerdefiniertem Zugriff auf die dimension von Daten &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Erteilen von benutzerdefiniertem Zugriff auf Zellendaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
