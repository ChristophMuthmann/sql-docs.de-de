---
title: Autorisieren des Zugriffs auf Objekte und Vorgänge (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a8dc16e1f2885141f20395cbe5e150996919e06
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>Autorisieren des Zugriffs auf Objekte und Vorgänge (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Der Zugriff für Nichtadministratorbenutzer auf Cubes, Dimensionen und Miningmodelle innerhalb einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank wird durch die Mitgliedschaft in mindesten einer Datenbankrolle gewährt. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Administratoren erstellen diese Datenbankrollen, gewähren Lese- oder Lese-/Schreibberechtigungen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Objekte und weisen dann jeder Rolle [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzer und Gruppen zu.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bestimmt die gültigen Berechtigungen für einen bestimmten Windows-Benutzer oder eine bestimmte Windows-Benutzergruppe, indem die Berechtigungen kombiniert werden, die jeder Datenbankrolle zugeordnet sind, zu der der Benutzer oder die Gruppe gehört. Das führt dazu, dass wenn eine bestimmte Datenbankrolle einem Benutzer oder einer Gruppe die Berechtigung zum Anzeigen einer Dimension, eines Measures oder eines Attributs erteilt, eine andere Datenbankrolle diese Benutzer- oder Gruppenberechtigung jedoch nicht erteilt, der Benutzer oder die Gruppe über die Berechtigung zum Anzeigen des Objekts verfügt.  
  
> [!IMPORTANT]  
>  Mitglieder der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Serveradministratorrolle und Mitglieder einer Datenbankrolle, die über die Berechtigung „Vollzugriff (Administrator)“ verfügen, können auf alle Daten und Metadaten in der Datenbank zugreifen und benötigen keine weiteren Berechtigungen zum Anzeigen spezieller Objekte. Darüber hinaus kann den Mitgliedern der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Serverrolle in keiner Datenbank der Zugriff auf irgendein Objekt verweigert werden, und Mitgliedern einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbankrolle, die über die Berechtigung „Vollzugriff (Administrator)“ verfügen, kann in dieser Datenbank nicht der Zugriff auf irgendein Objekt verweigert werden. Spezielle Administratorvorgänge wie die Verarbeitung können über separate Rollen mit weniger Berechtigungen autorisiert werden. Einzelheiten finden Sie unter [Erteilen von Verarbeitungsberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md).  
  
## <a name="list-roles-defined-for-your-database"></a>Auflisten der für Ihre Datenbank definierten Rollen  
 Administratoren können eine einfache DMV-Abfrage in SQL Server Management Studio ausführen, um eine Liste aller auf dem Server definierter Rollen abzurufen.  
  
1.  Klicken Sie in SSMS mit der rechten Maustaste auf eine Datenbank, und wählen Sie **Neue Abfrage** | **MDX**aus.  
  
2.  Geben Sie die folgende Abfrage ein, und drücken Sie F5, um sie auszuführen:  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     Die Ergebnisse enthalten den Datenbanknamen, eine Beschreibung, den Rollennamen und das Datum der letzten Änderung. Mit diesen Informationen als Ausgangspunkt können Sie mit individuellen Datenbanken fortfahren, um die Mitgliedschaft und Berechtigungen einer bestimmten Rolle zu prüfen.  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>Umfassende Übersicht über die Analysis Services-Autorisierung  
 In diesem Abschnitt ist der grundlegende Workflow für das Konfigurieren von Berechtigungen dargestellt.  
  
 **Schritt 1: Server-Verwaltung**  
  
 Entscheiden Sie als ersten Schritt, wer Administratorrechte auf der Serverebene haben wird. Während der Installation muss der lokale Administrator, der SQL Server installiert, mindestens ein Windows-Konto als Analysis Services-Serveradministrator angeben. Serveradministratoren verfügen über alle möglichen Berechtigungen auf einem Server, darunter die Berechtigung, jedes Objekt auf dem Server anzeigen, ändern und löschen oder damit verbundene Daten anzeigen zu können. Wenn die Installation abgeschlossen ist, kann ein Serveradministrator Konten hinzufügen oder löschen, um die Mitgliedschaft dieser Rolle zu ändern. Weitere Informationen zu dieser Berechtigungsebene finden Sie unter [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) .  
  
 **Schritt 2: Datenbankverwaltung**  
  
 Nach dem Erstellen einer tabellarischen oder mehrdimensionalen Lösung wird diese dann als Datenbank an den Server bereitgestellt. Ein Serveradministrator kann Datenverwaltungsaufgaben delegieren, indem er eine Rolle definiert, die über die Berechtigung "Vollzugriff" für die entsprechende Datenbank verfügt. Mitglieder dieser Rolle können Objekte in der Datenbank verarbeiten oder abfragen sowie zusätzliche Rollen für den Zugriff auf Cubes, Dimensionen und andere Objekte in der Datenbank selbst erstellen. Weitere Informationen finden Sie unter [Erteilen von Datenbankberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md).  
  
 **Schritt 3: Aktivieren des Cube- oder Modellzugriffs für Abfrage- und Verarbeitungsworkloads**  
  
 Standardmäßig haben nur Server- und Datenbankadministratoren Zugriff auf Cubes oder tabellarische Modelle. Damit diese Datenstrukturen auch anderen Personen in Ihrer Organisation zur Verfügung stehen, sind zusätzliche Rollenzuweisungen erforderlich, die Windows-Benutzer- und -Gruppenkonten zu Cubes oder Modellen zuordnen, zusammen mit Berechtigungen, die **Lese**-Berechtigungen angeben. Einzelheiten finden Sie unter [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Verarbeitungsaufgaben können von andere Verwaltungsfunktionen isoliert werden, sodass Server- und Datenbankadministratoren diese Aufgabe an andere Personen delegieren oder eine unbeaufsichtigte Verarbeitung konfigurieren können, indem Sie Dienstkonten angeben, die eine Planungssoftware ausführen. Einzelheiten finden Sie unter [Erteilen von Verarbeitungsberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md).  
  
> [!NOTE]  
>  Benutzer benötigen keine Berechtigungen für die Verweistabellen in der zugrunde liegenden relationalen Datenbank, aus der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] seine Daten lädt, und benötigen keine Berechtigungen auf Dateiebene für den Computer, auf dem die Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ausgeführt wird.  
  
 **Schritt 4 (optional): Zulassen oder Verweigern des Zugriffs auf innere Cubeobjekte**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bietet Sicherheitseinstellungen für das Festlegen von Berechtigungen für einzelne Objekte, einschließlich Dimensionselemente und Zellen in einem Datenmodell. Einzelheiten finden Sie unter [Erteilen von benutzerdefiniertem Zugriff auf Dimensionsdaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) und [Erteilen von benutzerdefiniertem Zugriff auf Zellendaten &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
 Sie können Berechtigungen auch auf der Basis der Benutzeridentität variieren. Dies wird oft als dynamische Sicherheit bezeichnet und wird über die Funktion [UserName &#40;MDX&#41;](../../mdx/username-mdx.md) implementiert.  
  
## <a name="best-practices"></a>Bewährte Methoden  
 Für eine bessere Verwaltung von Berechtigungen schlagen wir einen Ansatz wie den folgenden vor:  
  
1.  Erstellen Sie Rollen nach Funktion (zum Beispiel dbadmin, cubedeveloper, processadmin), damit derjenige, der die Rollen verwaltet, auf einen Blick sehen kann, was die Rolle zulässt. Wie bereits erwähnt, können Sie Rollen in der Modelldefinition definieren und diese Rollen damit über nachfolgende Lösungsbereitstellungen beibehalten.  
  
2.  Erstellen Sie eine entsprechende Windows-Sicherheitsgruppe in Active Directory, und verwalten Sie die Sicherheitsgruppe dann in Active Directory, um sicherzustellen, dass sie die richtigen individuellen Konten enthält. Damit wird die Verantwortung für die Mitgliedschaft in Sicherheitsgruppen an Sicherheitsspezialisten übergeben, die bereits mit den Tools und Prozessen für die Kontoverwaltung in Ihrer Organisation vertraut sind.  
  
3.  Generieren Sie Skripts in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], damit Sie Rollenzuweisungen schnell replizieren können, wenn das Modell erneut aus seinen Quelldateien an einen Server bereitgestellt wird. Informationen dazu, wie Sie schnell ein Skript generieren, finden Sie unter [Erteilen von Cube- oder Modellberechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
4.  Übernehmen Sie eine Benennungskonvention, die den Umfang und die Mitgliedschaft der Rolle widerspiegelt. Da Rollennamen nur in Entwurfs- und Verwaltungstools sichtbar sind, sollten Sie eine Benennungskonvention verwenden, die für Ihre Cubesicherheitsspezialisten Sinn macht. Zum Beispiel weist **processadmin-windowsgroup1** auf Lesezugriff und Verarbeitungsrechte für Personen in Ihrer Organisation hin, deren individuelle Windows-Benutzerkonten Mitglied der Sicherheitsgruppe **windowsgroup1** sind.  
  
     Das Hinzufügen von Kontoinformationen kann Ihnen helfen, den Überblick darüber zu behalten, welche Konten in verschiedenen Rollen verwendet werden. Da Rollen additiv sind, machen die kombinierten, **windowsgroup1** zugewiesenen Rollen den effektiven Berechtigungssatz für Personen aus, die zu dieser Sicherheitsgruppe gehören.  
  
5.  Cubeentwickler benötigen die Berechtigung "Vollzugriff" für Modelle und Datenbanken in Entwicklung, aber nur Leseberechtigungen, sobald eine Datenbank an einen Produktionsserver bereitgestellt wurde. Denken Sie daran, Rollendefinitionen und -zuweisungen für alle Szenarien zu entwickeln, einschließlich Entwicklungs-, Test- und Produktionsbereitstellungen.  
  
 Ein solcher Ansatz minimiert die Belastung für Rollendefinitionen und Rollenmitgliedschaften im Modell und bietet einen transparenten Einblick in die Rollenzuweisungen, mit dem sich Cubeberechtigungen einfacher implementieren und verwalten lassen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Rollen und Berechtigungen &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Von Analysis Services Unterstützte Authentifizierungsmethoden](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  
