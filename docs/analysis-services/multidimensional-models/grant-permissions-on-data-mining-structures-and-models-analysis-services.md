---
title: "Erteilen von Berechtigungen für Datamining-Strukturen und-Modellen (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 12b69f08e0c56b614c2e181ca3cb62a24496e2b9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>Erteilen von Berechtigungen für Data Mining-Strukturen und -Modellen (Analysis Services)
  Standardmäßig besitzt nur ein Analysis Services-Serveradministrator Berechtigungen zum Anzeigen von Data Mining-Strukturen oder Miningmodellen in der Datenbank. Befolgen Sie die Anweisungen unten, um Berechtigungen für Benutzer, die keine Administratoren sind, zu vergeben.  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>Festlegen von Berechtigungen für den Zugriff auf eine Miningstruktur  
  
1.  Verbinden Sie sich in SSMS mit Analysis Services. Falls Sie Hilfe bei den Schritten brauchen, gehen Sie unter [Herstellen einer Verbindung von Clientanwendungen &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md).  
  
2.  Öffnen Sie den Ordner **Datenbanken** in Objekt-Explorer, und wählen Sie eine Datenbank aus.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Rollen** , und wählen Sie **Neue Rolle**aus.  
  
4.  Geben Sie auf der Seite "Allgemein" einen Namen und optional eine Beschreibung ein. Diese Seite enthält auch mehrere Datenbankberechtigungen wie beispielsweise "Vollzugriff", "Datenbank verarbeiten" und "Definition lesen". Für den Data Mining-Zugriff ist keine dieser Berechtigungen erforderlich. Weitere Informationen zu Datenbankberechtigungen finden Sie unter [Erteilen von Datenbankberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md).  
  
5.  Wählen Sie im Bereich **Miningstruktur** entweder **Lesen** oder **Lesen/Schreiben** für jede Data Mining-Struktur aus.  
  
6.  Geben Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen ein, die mit dieser Rolle eine Verbindung zu Analysis Services herstellen.  
  
7.  Klicken Sie auf **OK** , um die Erstellung der Rolle zu abzuschließen.  
  
## <a name="set-permissions-to-access-a-mining-model"></a>Festlegen von Berechtigungen für den Zugriff auf ein Miningmodell  
 Für ein Data Mining-Modell kann eine Rolle entweder über **Lesen** - oder **Lesen/Schreiben** -Berechtigungen verfügen sowie über die Berechtigungen **Drillthrough** und **Definition lesen** , die das Anzeigen und Durchsuchen der zugrunde liegenden Daten ermöglichen.  
  
 **Hinweis** Wenn Sie Drillthrough sowohl für die Miningstruktur als auch für das Miningmodell aktivieren, kann jeder Benutzer, der Mitglied einer Rolle mit Drillthroughberechtigungen für das Miningmodell und die Miningstruktur ist, auch Spalten in der Miningstruktur einsehen, selbst wenn diese Spalten nicht Teil des Miningmodells sind. Deswegen sollten Sie zum Schutz sensibler Informationen die Datenquellensicht so einrichten, dass persönliche Informationen verborgen sind, und Drillthroughzugriff auf die Miningstruktur nur zulassen, wenn es wirklich erforderlich ist.  
  
 Um einer Datenbankrolle Lese-/Schreibberechtigungen zu erteilen, muss der Benutzer Mitglied der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Serverrolle oder ein Mitglied einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankrolle sein, die über die Berechtigung Vollzugriff (Administrator) verfügt.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, erweitern Sie im Objekt-Explorer das **Rollen** -Element für die entsprechende Datenbank, und klicken Sie dann auf eine Datenbankrolle (oder erstellen Sie eine neue Datenbankrolle).  
  
2.  Suchen Sie im Bereich **Miningstuktur** das Miningmodell in der Liste **Miningmodelle** , und wählen Sie anschließend für dieses Miningmodell die Option **Lesen**, **Lesen/Schreiben**, **Drillthrough**oder **Durchsuchen** aus.  
  
3.  Geben Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen ein, die mit dieser Rolle eine Verbindung zu Analysis Services herstellen.  
  
4.  Klicken Sie auf **OK** , um die Erstellung der Rolle zu abzuschließen.  
  
 Wenn Sie eine Datenquelle in einer Drillthroughabfrage verwenden möchten, die die OPENQUERY-Klausel der Data Mining-Erweiterungen (DMX) verwendet, muss die Datenbankrolle auch über Lese-/Schreibberechtigungen für das entsprechende Datenquellenobjekt verfügen. Weitere Informationen finden Sie unter [Erteilen von Berechtigungen für ein Datenquellenobjekt &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) und [OPENQUERY &#40;DMX&#41;](../../dmx/source-data-query-openquery.md).  
  
> [!NOTE]  
>  Standardmäßig ist die Einreichung von DMX-Abfragen über OPENROWSET deaktiviert.  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Erteilen von benutzerdefiniertem Zugriff auf die dimension von Daten &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Erteilen von benutzerdefiniertem Zugriff auf Zellendaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  

