---
title: Vordefinierte Rollen | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/22/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Reporting Services], defaults
- default security
- role-based security [Reporting Services], defaults
ms.assetid: 6b46db51-7c30-467d-a251-50f50647fe21
caps.latest.revision: "42"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 492f85664f3a1068d32fca9910717d794fb6dc6e
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="role-definitions---predefined-roles"></a>Rollendefinitionen: vordefinierte Rollen
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird mit vordefinierten Rollen installiert, mit denen Sie den Zugriff auf Berichtsservervorgänge gewähren können. Jede vordefinierte Rolle beschreibt eine Auflistung verwandter Aufgaben. Sie können Gruppen und Benutzerkonten vordefinierten Rollen zuweisen, um den unmittelbaren Zugriff auf Berichtsservervorgänge bereitzustellen.  
  
## <a name="how-to-use-predefined-roles"></a>Verwenden vordefinierter Rollen  
  
1.  Überprüfen Sie die vordefinierten Rollen, um zu ermitteln, ob Sie sie unverändert verwenden können. Wenn Sie die Aufgaben anpassen oder zusätzliche Rollen definieren müssen, sollte dies erfolgen, bevor Sie den einzelnen Rollen Benutzer zuweisen.  
  
2.  Identifizieren Sie, für welche Benutzer und Gruppen der Zugriff auf den Berichtsserver erforderlich ist und auf welcher Ebene. Die meisten Benutzer sollten der **Browser** -Rolle oder der **Berichts-Generator** -Rolle zugewiesen werden. Eine kleinere Anzahl von Benutzern sollte der **Verleger** -Rolle zugewiesen werden. **Inhalts-Manager**sollten nur sehr wenige Benutzer zugewiesen werden.  
  
3.  Verwenden Sie den Berichts-Manager, wenn Sie bereit sind, Benutzer- und Gruppenkonten bestimmten Rollen zuzuweisen. Weitere Informationen finden Sie unter [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)sollten nur sehr wenige Benutzer zugewiesen werden.  
  
##  <a name="bkmk_rolelist"></a> Vordefinierte Rollendefinitionen  
 Vordefinierte Rollen werden durch die von ihnen unterstützten Aufgaben definiert. Sie können diese Rollen ändern oder durch benutzerdefinierte Rollen ersetzen.  
  
 Der*Bereich* definiert die Grenzen, innerhalb derer Rollen verwendet werden. Rollen auf Elementebene bieten verschiedene Ebenen des Zugriffs auf Berichtsserverelemente und -vorgänge, die sich auf diese Elemente auswirken. Rollen auf Elementebene werden für den Stammknoten (Stamm) und alle Elemente in der Ordnerhierarchie des Berichtsservers definiert. Rollen auf Systemebene autorisieren den Zugriff auf Websiteebene. Rollen auf Element- und Systemebene schließen sich gegenseitig aus, werden aber zusammen verwendet, um umfassende Berechtigungen für Berichtsserverinhalt und -vorgänge bereitzustellen.  
  
 In der folgenden Tabelle werden die vordefinierten Rollen, ihr Bereich und ihre Verwendung beschrieben.  
  
|Vordefinierte Rolle|Bereich|Description|  
|---------------------|-----------|-----------------|  
|[Inhalts-Manager-Rolle](#bkmk_content)|Element|Schließt alle Aufgaben auf Elementebene ein. Benutzer, die dieser Rolle zugewiesen sind, haben die Vollberechtigung zum Verwalten von Berichtsserverinhalt. In diesem Rahmen können Sie anderen Benutzern Berechtigungen gewähren und die Ordnerstruktur zum Speichern von Berichten und anderen Elementen definieren.|  
|[Verleger-Rolle](#bkmk_publisher)|Element|Benutzer, die dieser Rolle zugewiesen sind, können einem Berichtsserver Elemente hinzufügen und die Ordner erstellen und verwalten, in denen diese Elemente enthalten sind.|  
|[Browser-Rolle](#bkmk_browser)|Element|Benutzer, die dieser Rolle zugewiesen sind, können Berichte ausführen, Berichte abonnieren und in der Ordnerstruktur navigieren.|  
|[Berichts-Generator-Rolle](#bkmk_reportbuilder)|Element|Benutzer, die dieser Rolle zugewiesen sind, können im Berichts-Generator Berichte erstellen und bearbeiten.|  
|[Meine Berichte-Rolle](#bkmk_myreports)|Element|Benutzer, die dieser Rolle zugewiesen sind, können einen persönlichen Arbeitsbereich zum Speichern und Verwenden von Berichten und anderen Elementen verwalten.|  
|[Systemadministrator-Rolle](#bkmk_systemadministrator)|System|Benutzer, die dieser Rolle zugewiesen sind, können Funktionen aktivieren und Standardwerte festlegen, sie können die siteweite Sicherheit festlegen, Rollendefinitionen in Management Studio erstellen und Aufträge verwalten.|  
|[Systembenutzer-Rolle](#bkmk_systemuser)|System|Benutzer, die dieser Rolle zugewiesen sind, können grundlegende Informationen zum Berichtsserver anzeigen, z. B. die Zeitplaninformationen in einem freigegebenen Zeitplan.|  
  
##  <a name="bkmk_content"></a> Inhalts-Manager-Rolle  
 Die **Inhalts-Manager** -Rolle ist eine vordefinierte Rolle, die hilfreiche Aufgaben für einen Benutzer enthält, der Berichte und Webinhalt verwaltet, aber nicht notwendigerweise Berichte erstellt oder einen Webserver oder eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verwaltet. Ein Inhalts-Manager stellt Berichte bereit, verwaltet Berichtsmodelle und Datenquellenverbindungen und fällt Entscheidungen zur Verwendungsweise von Berichten. Für alle Aufgaben auf Elementebene wird standardmäßig die **Inhalts-Manager** -Rollendefinition ausgewählt.  
  
 Die **Inhalts-Manager** -Rolle wird häufig mit der **Systemadministrator** -Rolle verwendet. Zusammen stellen die beiden Rollendefinitionen einen vollständigen Satz von Aufgaben für Benutzer bereit, die einen vollständigen Zugriff auf alle Elemente auf einem Berichtsserver benötigen. Obwohl die **Inhalts-Manager** -Rolle vollständigen Zugriff auf Berichte, Berichtsmodelle, Ordner und andere Elemente in der Ordnerhierarchie bietet, ermöglicht sie keinen Zugriff auf Elemente oder Vorgänge auf Websiteebene. Aufgaben wie das Erstellen und Verwalten freigegebener Zeitpläne, das Festlegen von Servereigenschaften und das Verwalten von Rollendefinitionen sind Aufgaben auf Systemebene, die in der **Systemadministrator** -Rolle enthalten sind. Aus diesem Grund wird empfohlen, eine zweite Rollenzuweisung auf Websiteebene zu erstellen, mit der Zugriff auf freigegebene Zeitpläne bereitgestellt wird.  
  
### <a name="content-manager-tasks"></a>Aufgaben des Inhalts-Managers  
 In der folgenden Tabelle sind die in der **Inhalts-Manager** -Rolle enthaltenen Aufgaben aufgeführt.  
  
|Task|Description|  
|----------|-----------------|  
|Berichte lesen|Lesen von Berichtsdefinitionen.|  
|Verknüpfte Berichte erstellen|Verknüpfte Berichte erstellen, die auf einem nicht verknüpften Bericht basieren.|  
|Alle Abonnements verwalten|Ein Abonnement für Berichte und verknüpfte Berichte anzeigen, ändern und löschen, unabhängig vom Besitzer des Abonnements. Diese Aufgabe ermöglicht auch das Erstellen von datengesteuerten Abonnements.|  
|Datenquellen verwalten|Freigegebene Datenquellenelemente erstellen und löschen, Datenquelleneigenschaften und Inhalt anzeigen und ändern.|  
|Ordner verwalten|Ordner erstellen, anzeigen und löschen sowie Ordnereigenschaften anzeigen und ändern.|  
|Modelle verwalten|Ermöglicht das Erstellen, Anzeigen und Löschen von Modellen sowie das Anzeigen und Ändern von Modelleigenschaften.|  
|Einzelne Abonnements verwalten|Abonnements für Berichte und verknüpfte Berichte, die dem Benutzer gehören, erstellen, anzeigen, ändern und löschen.|  
|Berichtsverlauf verwalten|Ermöglicht das Erstellen, Anzeigen und Löschen des Berichtsverlaufs, das Anzeigen von Berichtsverlaufeigenschaften sowie das Anzeigen und Ändern von Einstellungen, die Grenzwerte für den Momentaufnahmeverlauf und die Funktionsweise der Zwischenspeicherung bestimmen.|  
|Berichte verwalten|Berichte hinzufügen und löschen, Berichtsparameter ändern, Berichtseigenschaften anzeigen und ändern, Datenquellen, die Inhalt für den Bericht bereitstellen, anzeigen und ändern, Berichtsdefinitionen anzeigen und ändern sowie Sicherheitsrichtlinien auf Berichtsebene festlegen.|  
|Ressourcen verwalten|Ressourcen erstellen, ändern und löschen sowie Ressourceneigenschaften anzeigen und ändern.|  
|Die Sicherheit für einzelne Elemente festlegen|Sicherheitsrichtlinien für Berichte, verknüpfte Berichte, Ordner, Ressourcen und Datenquellen definieren. Weitere Informationen finden Sie unter [Projektelemente](../../reporting-services/security/securable-items.md).|  
|Datenquellen anzeigen|Freigegebene Datenquellenelemente in der Ordnerhierarchie anzeigen.|  
|Berichte anzeigen|Berichte ausführen und Berichtseigenschaften anzeigen.|  
|Modelle anzeigen|Anzeigen von Modellen in der Ordnerhierarchie, Verwenden von Modellen als Datenquellen für Berichte und Ausführen von Abfragen für das Modell, um Daten abzurufen.|  
|Ressourcen anzeigen|Ressourcen und Ressourceneigenschaften anzeigen.|  
|Ordner anzeigen|Ordnerinhalte anzeigen und in der Ordnerhierarchie navigieren.|  
  
### <a name="customizing-the-content-manager-role"></a>Anpassen der Inhalts-Manager-Rolle  
 Diese Rolle ist für vertrauenswürdige Benutzer gedacht, die die allgemeine Verantwortung für das Verwalten und Warten des Berichtsserverinhalts tragen. Sie können zwar Aufgaben aus dieser Definition entfernen, aber dadurch ist möglicherweise nicht mehr eindeutig definiert, was verwaltet werden kann. Beispielsweise würde durch das Entfernen der Aufgabe "Berichte anzeigen" aus dieser Rollendefinition verhindert, dass ein **Inhalts-Manager** Berichtsinhalte anzeigen kann, wodurch Änderungen an Parametern und Einstellungen für Anmeldeinformationen nicht überprüft werden könnten.  
  
 Die **Inhalts-Manager** -Rolle wird für die Standardsicherheit verwendet.  
  
##  <a name="bkmk_publisher"></a> Verleger-Rolle  
 Die **Verleger** -Rolle ist eine integrierte Rollendefinition, die Aufgaben umfasst, mit denen Benutzer einem Berichtsserver Inhalt hinzufügen können. Diese Rolle ist vordefiniert. Sie wird erst verwendet, wenn Sie Rollenzuweisungen erstellen, in denen sie enthalten ist. Diese Rolle ist für Benutzer vorgesehen, die Berichte oder Modelle im Berichts-Designer oder Modell-Designer erstellen und diese Elemente dann auf einem Berichtsserver veröffentlichen.  
  
> [!CAUTION]  
>  Die Berechtigung zum Veröffentlichen von Elementen auf einem Berichtsserver sollte nur vertrauenswürdigen Benutzern gewährt werden. Die Verleger-Rolle gewährt umfassende Berechtigungen, die es Benutzern ermöglichen, sämtliche Dateitypen auf einen Berichtsserver hochzuladen. Wenn ein hochgeladener Bericht oder eine hochgeladene HTML-Datei ein böswilliges Skript enthält, wird dieses von einem Benutzer, der auf den Bericht oder das HTML-Dokument klickt, unter dessen Anmeldedaten ausgeführt.  
  
 Berichtsdefinitionen können Skripts und andere Elemente enthalten, die für HTML-Injection-Angriffe anfällig sind, wenn der Bericht zur Laufzeit in HTML gerendert wird. Wenn ein veröffentlichter Bericht ein böswilliges Skript enthält, bewirkt ein Benutzer, der diesen Bericht ausführt, beim Öffnen des Berichts versehentlich das Ausführen des Skripts. Wenn der Benutzer über erweiterte Berechtigungen verfügt, wird das Skript mit diesen Berechtigungen ausgeführt.  
  
 Wenn Sie das Risiko, dass Benutzer böswillige Skripts versehentlich ausführen, vermindern möchten, begrenzen Sie die Anzahl der Benutzer, die über Berechtigungen zum Veröffentlichen von Inhalt verfügen. Stellen Sie außerdem sicher, dass die Benutzer nur Dokumente und Berichte aus vertrauenswürdigen Quellen veröffentlichen. Wenn Sie nicht sicher sind, ob eine Berichtsdefinition bedenkenlos veröffentlicht werden kann, sollen Sie die RDL-Datei in einem Text-Editor öffnen und nach Skripttags suchen. Ein böswilliges Skript kann in Ausdrücken und URLs (z.B. einer URL in einer Navigationsaktion) verborgen sein.  
  
### <a name="publisher-tasks"></a>Verlegeraufgaben  
 In der folgenden Tabelle sind die in der **Verleger** -Rolle enthaltenen Aufgaben aufgeführt.  
  
|Task|Description|  
|----------|-----------------|  
|Verknüpfte Berichte erstellen|Verknüpfte Berichte erstellen und in einem Berichtsserverordner veröffentlichen.|  
|Datenquellen verwalten|Freigegebene Datenquellenelemente erstellen und löschen, Datenquelleneigenschaften und Inhalt anzeigen und ändern.|  
|Ordner verwalten|Ordner erstellen, anzeigen und löschen; Ordnereigenschaften anzeigen und ändern.|  
|Berichte verwalten|Berichte hinzufügen und löschen, Berichtsparameter ändern, Berichtseigenschaften anzeigen und ändern, Datenquellen, die Inhalte für den Bericht bereitstellen, anzeigen und ändern, Berichtsdefinitionen anzeigen und ändern.|  
|Modelle verwalten|Berichtsmodelle erstellen, anzeigen und löschen; Berichtsmodelleigenschaften anzeigen und ändern.|  
|Ressourcen verwalten|Ressourcen erstellen, ändern und löschen; Ressourceneigenschaften anzeigen und ändern.|  
  
### <a name="customizing-the-publisher-role"></a>Anpassen der Verleger-Rolle  
 Sie können die **Verleger** -Rolle Ihren Anforderungen entsprechend ändern. Beispielsweise können Sie die Aufgabe "Verknüpfte Berichte erstellen" entfernen, wenn die Benutzer nicht in der Lage sein sollen, verknüpfte Berichte zu erstellen und zu veröffentlichen. Oder Sie fügen die Aufgabe "Ordner anzeigen" hinzu, damit die Benutzer in der Ordnerhierarchie navigieren können, um einen Speicherort für das neue Element auszuwählen.  
  
 Benutzer, die im Berichts-Designer Berichte veröffentlichen, benötigen mindestens die Aufgabe "Berichte verwalten", um dem Berichtsserver einen Bericht hinzufügen zu können. Wenn der Benutzer Berichte veröffentlichen muss, die freigegebene Datenquellen oder externe Dateien verwenden, sollten Sie auch die Aufgaben "Datenquellen verwalten" und "Ressourcen verwalten" einschließen. Damit der Benutzer beim Veröffentlichen auch einen Ordner erstellen kann, müssen Sie auch die Aufgabe "Ordner verwalten" einschließen.  
  
##  <a name="bkmk_browser"></a> Browser-Rolle  
 Die **Browser** -Rolle ist eine vordefinierte Rolle, die hilfreiche Aufgaben für einen Benutzer enthält, der Berichte anzeigt, diese jedoch nicht notwendigerweise erstellt oder verwaltet. Diese Rolle ermöglicht grundlegende Funktionen für die konventionelle Verwendung eines Berichtsservers. Ohne diese Aufgaben kann es sich für Benutzer als schwierig erweisen, einen Berichtsserver zu verwenden.  
  
 Die **Browser** -Rolle sollte mit der **Systembenutzer** -Rolle verwendet werden. Zusammen ermöglichen die beiden Rollendefinitionen einen vollständigen Satz von Aufgaben für Benutzer, die mit Elementen auf einem Berichtsserver interagieren. Obwohl die **Browser** -Rolle den Sichtzugriff auf Berichte, Berichtsmodelle, Ordner und andere Elemente in der Ordnerhierarchie bietet, ermöglicht sie keinen Zugriff auf Elemente auf Websiteebene, z.B. freigegebene Zeitpläne, die beim Erstellen von Abonnements hilfreich sind. Aus diesem Grund wird empfohlen, eine zweite Rollenzuweisung auf Websiteebene zu erstellen, mit der Zugriff auf freigegebene Zeitpläne bereitgestellt wird.  
  
### <a name="browser-tasks"></a>Browseraufgaben  
 In der folgenden Tabelle sind die in der **Browser** -Rolle enthaltenen Aufgaben beschrieben.  
  
|Task|Description|  
|----------|-----------------|  
|Berichte anzeigen|Berichte ausführen und Berichtseigenschaften anzeigen.|  
|Ressourcen anzeigen|Ressourcen und Ressourceneigenschaften anzeigen.|  
|Ordner anzeigen|Ordnerinhalte anzeigen und in der Ordnerhierarchie navigieren.|  
|Modelle anzeigen|Anzeigen von Modellen in der Ordnerhierarchie, Verwenden von Modellen als Datenquellen für Berichte und Ausführen von Abfragen für das Modell, um Daten abzurufen.|  
|Einzelne Abonnements verwalten|Abonnements für Berichte und verknüpfte Berichte, die dem Benutzer gehören, erstellen, anzeigen, ändern und löschen sowie Zeitpläne für diese Abonnements erstellen.|  
  
### <a name="customizing-the-browser-role"></a>Anpassen der Browser-Rolle  
 Sie können die **Browser** -Rolle Ihren Anforderungen entsprechend ändern. Beispielsweise können Sie die Aufgabe "Einzelne Abonnements verwalten" entfernen, damit keine Abonnements unterstützt werden. Oder Sie entfernen die Aufgabe "Ressourcen anzeigen", wenn Benutzern keine zusätzliche Dokumentation oder sonstigen auf den Berichtsserver hochgeladenen Elemente angezeigt werden sollen.  
  
 Diese Rolle sollte mindestens die Aufgaben "Berichte anzeigen" und "Ordner anzeigen" unterstützen, um die Anzeige und die Ordnernavigation zu ermöglichen. Sie sollten die Aufgabe "Ordner anzeigen" nur entfernen, wenn Sie die Ordnernavigation deaktivieren möchten. Entsprechend sollten Sie die Aufgabe "Berichte anzeigen" nur entfernen, wenn für Benutzer keine Berichte angezeigt werden sollen. Für diese Änderungen ist eine benutzerdefinierte Rollendefinition erforderlich, die selektiv für eine bestimmte Benutzergruppe angewandt wird.  
  
##  <a name="bkmk_reportbuilder"></a> Berichts-Generator-Rolle  
 Die **Berichts-Generator** -Rolle ist eine vordefinierte Rolle, die Aufgaben zum Laden von Berichten im Berichts-Generator sowie zum Anzeigen der Ordnerhierarchie und zum Navigieren in der Hierarchie einschließt. Zum Erstellen und Ändern von Berichten im Berichts-Generator müssen Sie zudem über eine Systemrollenzuweisung verfügen, die die Aufgabe "Berichtsdefinitionen ausführen" einschließt, die für die lokale Verarbeitung von Berichten im Berichts-Generator erforderlich ist.  
  
### <a name="report-builder-tasks"></a>Berichts-Generator-Aufgaben  
 In der folgenden Tabelle sind die Aufgaben beschrieben, die die **Berichts-Generator** -Rolle einschließt.  
  
|Task|Description|  
|----------|-----------------|  
|Berichte lesen|Lesen von Berichtsdefinitionen.|  
|Berichte anzeigen|Berichte ausführen und Berichtseigenschaften anzeigen.|  
|Ressourcen anzeigen|Ressourcen und Ressourceneigenschaften anzeigen.|  
|Ordner anzeigen|Ordnerinhalte anzeigen und in der Ordnerhierarchie navigieren.|  
|Modelle anzeigen|Anzeigen von Modellen in der Ordnerhierarchie, Verwenden von Modellen als Datenquellen für Berichte und Ausführen von Abfragen für das Modell, um Daten abzurufen.|  
|Einzelne Abonnements verwalten|Abonnements für Berichte und verknüpfte Berichte, die dem Benutzer gehören, erstellen, anzeigen, ändern und löschen sowie Zeitpläne für diese Abonnements erstellen.|  
  
### <a name="customizing-the-report-builder-role"></a>Anpassen der Berichts-Generator-Rolle  
 Sie können die **Berichts-Generator** -Rolle Ihren Anforderungen entsprechend ändern. Die Empfehlungen entsprechen im Wesentlichen den Empfehlungen für die **Browser** -Rolle: Entfernen Sie die Aufgabe "Einzelne Abonnements verwalten", wenn Abonnements nicht unterstützt werden sollen, entfernen Sie die Aufgabe "Ressourcen anzeigen", wenn Ressourcen für die Benutzer nicht sichtbar sein sollen, und behalten Sie die Aufgaben "Berichte anzeigen" und "Ordner anzeigen" bei, um das Anzeigen von und Navigieren in Ordnern zu unterstützen.  
  
 Die wichtigste Aufgabe in dieser Rollendefinition ist die Aufgabe "Berichte lesen", die es einem Benutzer ermöglicht, eine Berichtsdefinition vom Berichtsserver in eine lokale Berichts-Generator-Instanz zu laden. Wenn diese Aufgabe nicht unterstützt werden soll, können Sie diese Rollendefinition löschen und stattdessen die **Browser** -Rolle verwenden, da diese den allgemeinen Zugriff auf einen Berichtsserver unterstützt.  
  
##  <a name="bkmk_myreports"></a> Meine Berichte-Rolle  
 Die **Meine Berichte** -Rolle ist eine vordefinierte Rolle, die eine Reihe von Aufgaben einschließt, die für Benutzer der Funktion "Meine Berichte" hilfreich sind. Zu dieser Rollendefinition gehören Aufgaben, die Benutzern Administratorrechte für die den eigenen Ordner Meine Berichte gewähren.  
  
 Sie können zwar eine andere Rolle für die Funktion Meine Berichte auswählen, aber es wird empfohlen, eine Rolle ausschließlich für die Sicherheit von Meine Berichte zu verwenden. Weitere Informationen finden Sie unter [Sichern von Meine Berichte](../../reporting-services/security/secure-my-reports.md).  
  
### <a name="my-reports-tasks"></a>Aufgaben in Meine Berichte  
 In der folgenden Tabelle sind die in der **Meine Berichte** -Rolle enthaltenen Aufgaben aufgeführt.  
  
|Task|Description|  
|----------|-----------------|  
|Verknüpfte Berichte erstellen|Verknüpfte Berichte erstellen, die auf Berichten basieren, die im Ordner Meine Berichte des Benutzers gespeichert sind.|  
|Ordner verwalten|Ordner erstellen, anzeigen und löschen sowie Ordnereigenschaften anzeigen und ändern.|  
|Datenquellen verwalten|Freigegebene Datenquellenelemente erstellen und löschen, Datenquelleneigenschaften und Inhalt anzeigen und ändern.|  
|Einzelne Abonnements verwalten|Abonnements für Berichte und verknüpfte Berichte erstellen, anzeigen, ändern und löschen.|  
|Berichte verwalten|Berichte hinzufügen und löschen, Berichtsparameter ändern, Berichtseigenschaften anzeigen und ändern, Datenquellen, die Inhalt für den Bericht bereitstellen, anzeigen und ändern, Berichtsdefinitionen anzeigen und ändern sowie Sicherheitsrichtlinien auf Berichtsebene festlegen.|  
|Ressourcen verwalten|Ressourcen erstellen, ändern und löschen sowie Ressourceneigenschaften anzeigen und ändern.|  
|Berichte anzeigen|Berichte ausführen, die im Ordner Meine Berichte des Benutzers gespeichert sind, und Berichtseigenschaften anzeigen.|  
|Datenquellen anzeigen|Freigegebene Datenquellenelemente in der Ordnerhierarchie anzeigen.|  
|Ressourcen anzeigen|Ressourcen und Ressourceneigenschaften anzeigen.|  
|Ordner anzeigen|Ordnerinhalte anzeigen.|  
  
### <a name="customizing-the-my-reports-role"></a>Anpassen der Meine Berichte-Rolle  
 Sie können diese Rolle an Ihre speziellen Anforderungen anpassen. Es wird jedoch empfohlen, die Aufgaben Berichte verwalten und Ordner verwalten beizubehalten, um eine grundlegende Inhaltsverwaltung zu ermöglichen. Darüber hinaus sollte diese Rolle alle anzeigebasierten Aufgaben unterstützen, damit Benutzer Ordnerinhalte anzeigen und die verwalteten Berichte ausführen können.  
  
 Die Aufgabe "Sicherheit für einzelne Elemente festlegen" ist zwar standardmäßig nicht Bestandteil der Rollendefinition, Sie können diese Aufgabe jedoch zur **Meine Berichte** -Rolle hinzufügen, damit die Benutzer Sicherheitseinstellungen für Unterordner und Berichte anpassen können.  
  
##  <a name="bkmk_systemadministrator"></a> Systemadministrator-Rolle  
 Die **Systemadministrator** -Rolle ist eine vordefinierte Rolle mit Aufgaben, die für einen Berichtsserveradministrator hilfreich sind, der die allgemeine Verantwortung für einen Berichtsserver trägt, jedoch nicht notwendigerweise für den Inhalt auf dem Berichtsserver.  
  
 Wenn Sie eine Rollenzuweisung erstellen möchten, die diese Regel umfasst, verwenden Sie die Seite Siteeinstellungen im Berichts-Manager, oder verwenden Sie die Befehle, die durch Klicken mit der rechten Maustaste für den Berichtsserverknoten in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]angezeigt werden.  
  
 Die **Systemadministrator** -Rolle vermittelt nicht denselben vollen Umfang an Berechtigungen, die ein lokaler Administrator möglicherweise für einen Computer besitzt. Die **Systemadministrator** -Rolle umfasst vielmehr Vorgänge, die auf Websiteebene und nicht auf Elementebene ausgeführt werden. Erstellen Sie für Benutzer, für die der Zugriff auf siteweite Vorgänge und auf Elemente erforderlich ist, die auf dem Berichtsserver gespeichert sind, eine zweite Rollenzuweisung für den Ordner Home, die die **Inhalts-Manager** -Rolle umfasst. Zusammen stellen die beiden Rollendefinitionen einen vollständigen Satz von Aufgaben für Benutzer bereit, die einen vollständigen Zugriff auf alle Elemente auf einem Berichtsserver benötigen.  
  
### <a name="system-administrator-tasks"></a>Systemadministratoraufgaben  
 In der folgenden Tabelle sind die in der **Systemadministrator** -Rolle enthaltenen Aufgaben aufgeführt.  
  
|Task|Description|  
|----------|-----------------|  
|Berichtsdefinitionen ausführen|Ausführung der Berichtsdefinition, ohne die Veröffentlichung auf einem Berichtsserver zu starten.|  
|Aufträge verwalten|Aufträge, die ausgeführt werden, anzeigen und abbrechen. Weitere Informationen finden Sie unter [Verwalten eines ausgeführten Prozesses](../../reporting-services/subscriptions/manage-a-running-process.md).|  
|Berichtsservereigenschaften verwalten|Eigenschaften für den Berichtsserver und für vom Berichtsserver verwaltete Elemente anzeigen und ändern.<br /><br /> Mit dieser Aufgabe können Sie den Berichts-Manager umbenennen, Meine Berichte aktivieren und Standardwerte für den Berichtsverlauf festlegen.|  
|Rollen verwalten|Rollendefinitionen erstellen, anzeigen, ändern und löschen.<br /><br /> Mitglieder der **Systemadministrator** -Rolle können mithilfe der Seite Siteeinstellungen Rollen verwalten.|  
|Freigegebene Zeitpläne verwalten|Freigegebene Zeitpläne, mit denen Berichte ausgeführt oder aktualisiert werden, erstellen, anzeigen, ändern und löschen.|  
|Berichtsserversicherheit verwalten|Systemweite Rollenzuweisungen anzeigen und ändern.|  
  
 Die **Systemadministrator** -Rolle wird für die Standardsicherheit verwendet.  
  
##  <a name="bkmk_systemuser"></a> Systembenutzer-Rolle  
 Die **Systembenutzer** -Rolle ist eine vordefinierte Rolle mit Aufgaben, mit denen Benutzer grundlegende Informationen zum Berichtsserver anzeigen können. Sie unterstützt außerdem das Laden eines Berichts im Berichts-Generator. Beim Berichts-Generator handelt es sich um eine Clientanwendung, die einen Bericht unabhängig von einem Berichtsserver verarbeiten kann. Die Aufgabe "Berichtsdefinitionen ausführen" ist zum Verwenden mit dem Berichts-Generator gedacht. Wenn Sie den Berichts-Generator nicht verwenden, können Sie diese Aufgabe aus der **Systembenutzer** -Rolle entfernen. In der folgenden Tabelle sind die in der **Systembenutzer** -Rollendefinition enthaltenen Aufgaben aufgeführt.  
  
### <a name="system-user-tasks"></a>Systembenutzeraufgaben  
  
|Task|Description|  
|----------|-----------------|  
|Berichtsdefinitionen ausführen|Führen Sie einen Bericht aus, ohne ihn auf einem Berichtsserver zu veröffentlichen.|  
|Berichtsservereigenschaften anzeigen|Eigenschaften für den Berichtsserver anzeigen, wie z. B. den Anwendungsnamen, Standardwerte für den Berichtsverlauf sowie ob Meine Berichte aktiviert ist.<br /><br /> Wenn Sie diese Aufgabe aus der **Systembenutzer** -Rolle entfernen, ist die Seite Siteeinstellungen nicht verfügbar. Außerdem wird der Titel der Anwendung nicht oben auf jeder Seite angezeigt. Standardmäßig lautet der Titel für den Berichtsmanager "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]".|  
|Freigegebene Zeitpläne anzeigen|Freigegebene Zeitpläne anzeigen, mit denen Berichte ausgeführt oder aktualisiert werden.<br /><br /> Wenn Sie diese Aufgabe aus der **Systembenutzer** -Rolle entfernen, können Benutzer keine freigegebenen Zeitpläne für Abonnements und sonstige geplante Vorgänge auswählen.|  
  
 Mithilfe der **Systembenutzer** -Rolle kann die Standardsicherheit ergänzt werden. Sie können die Rolle in neuen Rollenzuweisungen verwenden, die den Berichtsserverzugriff auf Berichtsbenutzer erweitern. Weitere Informationen finden Sie unter [Granting Permissions on a Native Mode Report Server](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen, Löschen oder Ändern einer Rolle &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)   
 [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [Ändern oder Löschen einer Rollenzuweisung (Berichts-Manager)](../../reporting-services/security/role-assignments-modify-or-delete.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Tasks and Permissions (Aufgaben und Berechtigungen)](../../reporting-services/security/tasks-and-permissions.md)  
  
  
