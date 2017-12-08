---
title: Erteilen von Berechtigungen zum Verarbeiten (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], process
- process permissions [Analysis Services]
ms.assetid: c1531c23-6b46-46a8-9ba3-b6d3f2016443
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 33582b08bd8579d7c2c3318594dcbf877c186757
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="grant-process-permissions-analysis-services"></a>Erteilen von Berechtigungen zum Verarbeiten (Analysis Services)
  Als Administrator können Sie eine dedizierte Rolle für Verarbeitungsvorgänge in Analysis Services erstellen. Mit dieser können Sie diesen Task an andere Benutzer oder Anwendungen für unbeaufsichtigte Geplante Verarbeitung delegieren. Die Berechtigungen zum Verarbeiten können auf der Datenbank-, Cube-, Dimensions- und Miningstrukturebene erteilt werden. Wenn Sie nicht mit einem/einer umfangreichen Cube/tabellarischen Datenbank arbeiten, wird empfohlen, Verarbeitungsberechtigungen auf Datenbankebene zu gewähren, einschließlich aller Objekte und derer, zwischen denen Abhängigkeiten bestehen.  
  
 Berechtigungen werden über Rollen gewährt, die Objekte mit Berechtigungen und Windows-Benutzerkonten oder Windows-Gruppenkonten verknüpfen. Beachten Sie, dass Berechtigungen additiv sind. Wenn eine Rolle die Berechtigung erteilt, einen Cube zu verarbeiten, während eine zweite Rolle die Berechtigung gewährt, eine Dimension zu verarbeiten, werden die Berechtigungen aus beiden Rollen kombiniert. Der Benutzer erhält so die Berechtigung, sowohl den Cube als auch die angegebene Dimension innerhalb der Datenbank zu verarbeiten.  
  
> [!IMPORTANT]  
>  Ein Benutzer, dessen Rolle nur Verarbeitungsberechtigungen besitzt, ist nicht in der Lage, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] für die Verbindung zu [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] und die Verarbeitung von Objekten zu verwenden. Diese Tools erfordern die **Read Definition** -Berechtigung für den Zugriff auf Objektmetadaten. Ohne die Möglichkeit, eines der beiden Tools zu verwenden, müssen Sie ein XMLA-Skript nutzen, um einen Verarbeitungsvorgang auszuführen.  
>   
>  Es wird empfohlen, zu Testzwecken auch **Read Definition** -Berechtigungen zu erteilen. Ein Benutzer, der über die Berechtigungen **Definition lesen** und **Datenbank verarbeiten** verfügt, kann Objekte interaktiv in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]verarbeiten. Weitere Einzelheiten finden Sie unter [Erteilen von Berechtigungen zum Lesen von Definitionen für Objektmetadaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) .  
  
## <a name="set-processing-permissions-at-the-database-level"></a>Festlegen von Verarbeitungsberechtigungen auf Datenbankebene  
 In diesem Abschnitt erfahren Sie, wie Sie die Verarbeitung aller Cubes, Dimensionen, Miningstrukturen und Miningmodelle in der Datenbank durch Nicht-Administratoren ermöglichen.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zur Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, öffnen Sie den Ordner "Datenbanken", und wählen Sie eine Datenbank aus.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Rollen** | **Neue Rolle**. Geben Sie einen Namen und eine Beschreibung an.  
  
3.  Aktivieren Sie im Bereich **Allgemein** das Kontrollkästchen **Datenbank verarbeiten** . Aktivieren Sie zusätzlich **Definition lesen** , um interaktive Verarbeitung über eines der SQL Server-Tools wie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zu ermöglichen.  
  
4.  Fügen Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen hinzu, welche die Berechtigung besitzen, beliebige Objekte in der Datenbank zu verarbeiten.  
  
5.  Klicken Sie auf **OK** , um die Rollendefinition abzuschließen.  
  
## <a name="set-processing-permissions-on-individual-objects"></a>Festlegen von Verarbeitungsberechtigungen für individuelle Objekte  
 Sie können Verarbeitungsberechtigungen für individuelle Cubes, Dimensionen, Data Miningstrukturen oder -modelle festlegen.  
  
 Die Verarbeitung kann fehlschlagen, wenn Sie unbeabsichtigt Objekte ausschließen, die zusammen verarbeitet werden müssen. (Wenn Sie beispielsweise die Verarbeitung eines Cube aktivieren, jedoch nicht die Verarbeitung zugehöriger Dimensionen). Da Objektabhängigkeiten leicht übersehen werden können, ist gründliches Testen bei der Festlegung von Verarbeitungsberechtigungen für individuelle Objekte sehr wichtig.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zur Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, öffnen Sie den Ordner "Datenbanken", und wählen Sie eine Datenbank aus.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Rollen** | **Neue Rolle**. Geben Sie einen Namen und eine Beschreibung an.  
  
3.  Deaktivieren Sie im Bereich **Allgemein** das Kontrollkästchen **Datenbank verarbeiten** . Datenbankberechtigungen überschreiben die Möglichkeit, Berechtigungen für Objekte mit geringerer Ebene festzulegen. Rollenoptionen sind dann ausgegraut oder können nicht ausgewählt werden.  
  
     Technisch gesehen sind keine Datenbankberechtigungen für dedizierte Verarbeitungsrollen erforderlich. Ohne **Definition lesen** auf Datenbankebene können Sie die Datenbank jedoch nicht in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen. Dadurch wird das Testen schwieriger.  
  
4.  Wählen Sie individuelle Objekte für die Verarbeitung aus:  
  
    -   Aktivieren Sie im Bereich **Cubes** für jeden Cube das Kontrollkästchen **Verarbeiten** .  
  
    -   Aktivieren Sie im Bereich **Dimensionen** für jede Dimension das Kontrollkästchen **Alle Datenbankdimensionen**und dann **Verarbeiten** . Wählen Sie alternativ alle Zeilen aus, und verwenden Sie dann Umschalt + Klicken, um die Auswahl der Kontrollkästchen umzuschalten.  
  
5.  Fügen Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen hinzu, welche die Berechtigung besitzen, diese Objekte zu verarbeiten.  
  
6.  Klicken Sie auf **OK** , um die Rollendefinition abzuschließen.  
  
## <a name="test-processing"></a>Testen der Verarbeitung  
  
1.  Halten Sie die Umschalttaste gedrückt, und klicken Sie mit der rechten Maustaste auf [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Wählen Sie **Als anderer Benutzer ausführen** aus, und stellen Sie eine Verbindung mit der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] her. Verwenden Sie hierfür ein Windows-Konto, das der Rolle zugewiesen ist, die Sie testen.  
  
2.  Öffnen Sie den Ordner "Datenbanken", und wählen Sie eine Datenbank aus. Es werden nur Datenbanken angezeigt, die für die Rollen sichtbar sind, für die das Konto eine Mitgliedschaft besitzt.  
  
3.  Klicken Sie mit der rechten Maustaste auf einen Cube oder eine Dimension, und wählen Sie **Verarbeiten**. Wählen Sie eine Verarbeitungsoption aus. Testen Sie alle Optionen für sämtliche Objektkombinationen. Falls Fehler aufgrund von fehlenden Objekten auftreten, fügen Sie diese Objekte zur Rolle hinzu.  
  
## <a name="set-processing-permissions-on-a-data-mining-structure"></a>Festlegen von Verarbeitungsberechtigungen für eine Data Miningstruktur  
 Sie können eine Rolle mit der Berechtigung zur Verarbeitung von Data Miningstrukturen erstellen. einschließlich der Verarbeitung aller Miningmodelle.  
  
 Die Berechtigungen **Drillthrough ausführen** und **Definition lesen**, die für das Durchsuchen von Miningmodellen und -strukturen verwendet werden, sind atomisch und können zur selben Rolle hinzugefügt oder in eine andere Rolle ausgelagert werden.  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zur Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, öffnen Sie den Ordner "Datenbanken", und wählen Sie eine Datenbank aus.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Rollen** | **Neue Rolle**. Geben Sie einen Namen und eine Beschreibung an. Stellen Sie sicher, dass im Bereich **General** die Kontrollkästchen für Datenbankberechtigungen deaktiviert sind. Datenbankberechtigungen überschreiben die Möglichkeit, Berechtigungen für Objekte mit geringerer Ebene festzulegen. Rollenoptionen sind dann grau hinterlegt oder können nicht ausgewählt werden.  
  
3.  Aktivieren Sie im Bereich **Miningstruktur** für jede Miningstruktur das Kontrollkästchen **Verarbeiten** .  
  
4.  Fügen Sie im **Mitgliedschaft** sbereich die Windows-Konten von Benutzern und Gruppen hinzu, welche die Berechtigung besitzen, beliebige Objekte in der Datenbank zu verarbeiten.  
  
5.  Klicken Sie auf **OK** , um die Rollendefinition abzuschließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verarbeiten von Datenbank, Tabelle oder Partition &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Verarbeiten eines mehrdimensionalen Modells &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Erteilen von Datenbankberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [Erteilen von Berechtigungen zum Lesen von Definitionen für Objektmetadaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
  
