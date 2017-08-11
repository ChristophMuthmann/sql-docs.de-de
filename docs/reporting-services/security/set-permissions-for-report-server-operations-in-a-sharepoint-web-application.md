---
title: "Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- SharePoint integration [Report Builder]
- security [Reporting Services], SharePoint integrated mode
- Report Builder 1.0, SharePoint integration
- model item security [Reporting Services]
ms.assetid: 9ea71f1a-ee9e-4337-95ff-d7cef79946e7
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d6d0c434fbac82990ad43e0b631cc7e418e47db8
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="set-permissions-for-report-server-operations-in-a-sharepoint-web-application"></a>Festlegen von Berechtigungen für Berichtsservervorgänge in einer SharePoint-Webanwendung
  Bei einem im integrierten SharePoint-Modus ausgeführten Berichtsserver wird durch die für die SharePoint-Website definierten Sicherheitseinstellungen bestimmt, wie Sie Berichte, Berichtsmodelle und freigegebene Datenquellen anzeigen und verwalten. Wenn Sie die standardmäßigen SharePoint-Gruppen, Berechtigungsebenen und Berechtigungszuweisungen verwenden, können Sie mit Berichten und anderen Dokumenten arbeiten und die aktuellen Sicherheitseinstellungen verwenden.  
  
 Wenn von den standardmäßigen Sicherheitseinstellungen nicht die gewünschte Zugriffsebene bereitgestellt wird, können Sie den Informationen der folgenden Abschnitte entnehmen, welche Berechtigungen für bestimmte Vorgänge erforderlich sind:  
  
-   [Berechtigungen zum Anzeigen und Verwalten von Berichten](#permissionReports)  
  
-   [Berechtigungen zum Erstellen von Berichten und zum Verwenden des Berichts-Generators](#permissionReportBuilder)  
  
-   [Berechtigungen zum Erstellen und Verwalten freigegebener Zeitpläne](#permissionSharedSchedules)  
  
-   [Berechtigungen zum Erstellen und Verwalten von Abonnements](#permissionSubscriptions)  
  
-   [Berechtigungen zum Erstellen und Verwalten von freigegebenen Datenquellen und Berichtsmodellen](#permissionDataSources)  
  
 Einige Hauptberechtigungen sind erforderlich, um die meisten Vorgänge auf einer SharePoint-Website abzuschließen. Diese Berechtigungen werden nicht in den Task- und Berechtigungstabellen unten aufgeführt, aber sie sind nötig für das Erstellen benutzerdefinierter Berechtigungsebenen:  
  
-   Benutzerinformationen durchsuchen  
  
-   Remoteschnittstellen verwenden  
  
-   Öffnen  
  
-   Anwendungsseiten anzeigen  
  
 Wenn Sie vordefinierte Berechtigungsebenen verwenden, ist keine Aktion erforderlich, da die oben genannten Berechtigungen bereits in Full Control, Design, Contribute, Read und Limited Access enthalten sind. Wenn Sie jedoch benutzerdefinierte Berechtigungsebenen verwenden oder die einem bestimmten Benutzer oder einer Gruppe zugewiesenen Berechtigungen bearbeiten, müssen Sie die Berechtigung manuell hinzufügen.  
  
 Die Berechtigung "Benutzerinformationen durchsuchen" ermöglicht dem Berichtsserver die Rückgabe von Informationen zum Ersteller des Elements und zum Benutzer, der das Element zuletzt geändert hat. Ohne diese Berechtigung gibt der Berichtsserver die folgenden Fehler zurück. Bei Suchvorgängen lautet der Fehler: "SharePoint-Fehler beim Berichtsserver. ---> System.UnauthorizedAccessException: Der Zugriff wird verweigert.“ Bei Veröffentlichungsvorgängen lautet der Fehler lautet: "die Berechtigungen für Benutzer"\<Domäne >\\< Benutzer\>"zum Ausführen des Vorgangs unzureichend sind."  
  
##  <a name="permissionReports"></a> Berechtigungen zum Anzeigen und Verwalten von Berichten  
 Berechtigungen für Berichtsdefinitionen werden über Listenberechtigungen für die Bibliothek definiert, die den Bericht enthält. Sie können Berechtigungen jedoch für einzelne Berichte festlegen, wenn Sie den Zugriff einschränken möchten. Die folgende Tabelle enthält eine Liste von Aufgaben und der Berechtigungen, die diese jeweils unterstützen.  
  
|Task|Berechtigung|  
|----------|----------------|  
|Anzeigen eines Berichts.|**Elemente lesen** für die Bibliothek, die die Dateien enthält, oder für den einzelnen Bericht.|  
|Anzeigen eines Berichts mit Durchklicken, für den ein Berichtsmodell als Datenquelle verwendet wird.|**Elemente lesen** für die Bibliothek, die den Bericht und das Berichtsmodell enthält, oder für den einzelnen Bericht und das einzelne Modell. Wenn Sie keine Berechtigungen zum Anzeigen des Modells besitzen, können Sie den Bericht zwar öffnen, jedoch kein Ad-hoc-Durchsuchen der Daten ausführen.<br /><br /> Wenn für das Berichtsmodell die Modellelementsicherheit verwendet wird, muss der Benutzer auch über die Berechtigung **Berechtigungen auflisten** für das Berichtsmodell verfügen.|  
|Anzeigen von Momentaufnahmen im Berichtsverlauf.|**Elemente bearbeiten** für die Bibliothek mit den Dateien oder für den einzelnen Bericht. Für einen bestimmten Bericht können Sie den gesamten Berichtsverlauf oder nichts davon anzeigen. Es ist nicht möglich, Berechtigungen für einzelne Momentaufnahmen im Berichtsverlauf festzulegen.|  
|Hochladen eines Berichts in die Bibliothek oder Veröffentlichen eines Berichts in der Bibliothek.|**Elemente hinzufügen** für die Bibliothek, die den Bericht enthalten wird.|  
|Festlegen von Eigenschaften für einen Bericht, einschließlich Datenquellen-Verbindungsinformationen, Verarbeitungsoptionen und Parametereigenschaften.|**Elemente bearbeiten** für die Bibliothek, die den Bericht enthält, oder für den einzelnen Bericht. Sie müssen auch Berechtigungen zum Anzeigen einer freigegebenen Datenquelle (RSDS) besitzen, um sie für die Verwendung mit dem Bericht auswählen zu können.|  
|Planen der Berichtsverarbeitung.|Zum Auswählen eines freigegebenen Zeitplans benötigen Sie die Berechtigung **Öffnen** für die Website, die die Bibliothek enthält, welche den Bericht enthält. Zum Planen der Datenverarbeitung oder des Cacheablaufzeitpunktes benötigen Sie die Berechtigung **Elemente bearbeiten** für die Bibliothek, die den Bericht enthält, oder für den einzelnen Bericht.|  
|Löschen eines Berichts.|**Elemente löschen** für die Bibliothek, die den Bericht enthält, oder für den einzelnen Bericht.|  
|Ersetzen der Berichtsdefinition (ohne Auswirkungen auf Eigenschaften, Berechtigungen, Verlauf oder Abonnements) durch eine neuere Version.|**Elemente bearbeiten** für die Bibliothek, die den Bericht enthält, oder für den einzelnen Bericht.|  
|Erstellen von Momentaufnahmen im Berichtsverlauf.|**Elemente hinzufügen** für die Bibliothek, die den Bericht enthält, für den Sie einen Berichtsverlauf erstellen.|  
|Erstellen von Momentaufnahmen im Berichtsverlauf.|**Elemente hinzufügen** für die Bibliothek, die den Bericht enthält, für den Sie einen Berichtsverlauf erstellen.|  
|Löschen von Momentaufnahmen im Berichtsverlauf und Löschen bestimmter Versionen von Berichtsdefinitionen, die über einen Zeitraum ausgecheckt und geändert wurden.|**Versionen löschen** für die Bibliothek, die den Bericht enthält, für den Sie den Berichtsverlauf löschen.|  
|Anzeigen von Momentaufnahmen im Berichtsverlauf und Anzeigen bestimmter Versionen von Berichtsdefinitionen, die über einen Zeitraum ausgecheckt und geändert wurden.|**Versionen anzeigen** für die Bibliothek, die den Bericht enthält.|  
  
##  <a name="permissionReportBuilder"></a> Berechtigungen zum Erstellen von Berichten und zum Verwenden des Berichts-Generators  
 Der Berichts-Generator ist ein Berichterstellungstool, das Sie zum Erstellen von Ad-hoc-Berichten verwenden können. Der Berichts-Generator verwendet Berichtsmodelle als Datenquelle, um das Ad-hoc-Durchsuchen von Daten zu unterstützen. Sie können ein Modell im Berichts-Generator laden, um einen Bericht zu erstellen, das Modell ausführen, durch die Daten im Modell klicken und den Bericht optional in einer Bibliothek speichern. Benutzer mit ausreichenden Berechtigungen können den Bericht anschließend öffnen und außerdem das Ad-hoc-Durchsuchen von Daten ausführen.  
  
> [!NOTE]  
>  Der Zugriff auf den Berichts-Generator kann durch andere Faktoren als durch Berechtigungen bestimmt sein. Ein Websiteadministrator kann die Ad-hoc-Berichterstellung deaktivieren, indem er Servereigenschaften festlegt, oder die Verfügbarkeit des Berichts-Generators beschränken, indem er nicht den Inhaltstyp Berichts-Generator-Bericht hinzufügt, sodass Benutzer keine neuen Berichte über das Menü **Neu** in einer Bibliothek erstellen können. Außerdem kann ein Berichtsserveradministrator veranlassen, dass der Berichts-Generator nicht verfügbar ist, indem er Eigenschaften auf dem Berichtsserver festlegt. Wenn eine dieser Bedingungen für den Server zutrifft, können Sie den Berichts-Generator nicht verwenden, selbst wenn Sie die erforderlichen Berechtigungen besitzen.  
  
 Die folgende Tabelle enthält eine Liste von Aufgaben zum Erstellen von Berichten und Verwenden des Berichts-Generators sowie Berechtigungen, die diese jeweils unterstützen:  
  
|Task|Berechtigung|  
|----------|----------------|  
|Starten des Berichts-Generators.|Es sind keine Berechtigungen vorhanden, die explizit zum Steuern des Zugriffs für die Verwendung des Berichts-Generators verwendet werden. Der Berichts-Generator ist verfügbar, wenn die Berichtsserverintegration konfiguriert ist und Sie die Berechtigung zum Hinzufügen von Elementen in einer Bibliothek besitzen. Zum Starten des Berichts-Generators über das Menü **Neu** in der Bibliothek müssen Sie den Berichts-Generator-Inhaltstyp registrieren. Weitere Informationen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Hochladen eines Modells oder einer freigegebenen Datenquelle.|**Elemente hinzufügen** für die Bibliothek, die die Dateien enthalten wird.|  
|Anzeigen eines Modells oder einer abhängigen freigegebenen Datenquelle.|**Elemente lesen** für die Bibliothek, die die Dateien enthält.<br /><br /> Wenn das Modell Sicherheitseinstellungen für Modellelemente enthält, muss der Benutzer auch über die Berechtigung **Berechtigungen auflisten** für das Modell verfügen.|  
|Generieren eines Modells aus einer freigegebenen Datenquelle.|**Elemente hinzufügen** für die Bibliothek, die die freigegebene Datenquellendatei (RSDS) enthält, aus der Sie das Modell generieren.|  
|Festlegen von Berechtigungen innerhalb eines Modells für bestimmte Modellelemente.|**Berechtigungen verwalten** für die Website, die die Bibliothek und die Berichtsmodelldatei (SMDL) enthält.|  
|Laden eines Modells im Berichts-Generator.|**Elemente bearbeiten** für die Berichtsmodelldatei (SMDL).|  
|Erstellen einer Berichtsdefinition im Berichts-Generator und Speichern eines Berichts in einer Bibliothek.|**Elemente hinzufügen** zum Speichern der Datei in einer Bibliothek.|  
|Bearbeiten eines Berichts im Berichts-Generator.|**Elemente bearbeiten** für die Berichtsdefinitionsdatei.|  
  
 Die Berechtigungen zum Erstellen und Verwenden von Abonnements oder Berichtsverläufen und zum Festlegen von Berichts- oder Datenverarbeitungsoptionen für einen Bericht des Berichts-Generators sind identisch mit den Berechtigungen zum Ausführen der gleichen Aktionen für standardmäßige Berichtsdefinitionsdateien.  
  
##  <a name="permissionSharedSchedules"></a> Berechtigungen zum Erstellen und Verwalten freigegebener Zeitpläne  
 Freigegebene Zeitpläne sind keine Dokumente, die in einer Bibliothek gespeichert werden. Deshalb sind für das Erstellen und Verwalten dieser Zeitpläne Websiteberechtigungen erforderlich. Sie können den Zugriff nicht auf bestimmte freigegebene Zeitpläne einschränken. Jeder freigegebene Zeitplan, den Sie erstellen, ist für jeden Benutzer verfügbar, der die Berechtigung zum Öffnen für die gesamte Website besitzt.  
  
 Die folgende Tabelle enthält eine Liste von Aufgaben und Berechtigungen zum Erstellen, Verwalten und Verwenden freigegebener Zeitpläne:  
  
|Task|Berechtigung|  
|----------|----------------|  
|Erstellen, Bearbeiten oder Löschen eines freigegebenen Zeitplans.|**Website verwalten** für die Website.|  
|Auswählen eines freigegebenen Zeitplans für die Abonnementverarbeitung oder das Abrufen von Daten.|**Öffnen** für die Website, die die Bibliothek enthält.|  
  
##  <a name="permissionSubscriptions"></a> Berechtigungen zum Erstellen und Verwalten von Abonnements  
 Mit SharePoint wird eine Abhängigkeit zwischen Abonnement und Anzeigeberechtigungen erzwungen. Sie können einen Bericht nicht abonnieren, für den Sie keine Berechtigung zum Anzeigen besitzen. Wenn Sie Berechtigungen zum Abonnieren eines Berichts erteilen, werden automatisch auch Anzeigeberechtigungen erteilt.  
  
 Die folgende Tabelle enthält eine Liste von Aufgaben und Berechtigungen zum Erstellen, Verwalten und Verwenden von Abonnements:  
  
|Task|Berechtigung|  
|----------|----------------|  
|Erstellen, Bearbeiten oder Löschen eines im Besitz eines Benutzers befindlichen Abonnements für einen bestimmten Bericht.|**Elemente bearbeiten** für den Bericht oder für die Bibliothek, die den Bericht enthält. Elemente lesen ist eine abhängige Berechtigung und wird automatisch in die Berechtigungsebene eingeschlossen. Benutzer, die ein Abonnement erstellen können, können auch benutzerdefinierte Zeitpläne zum Ausführen dieses Abonnements erstellen.|  
|Auswählen eines freigegebenen Zeitplans für die Verwendung mit dem Abonnement.|**Öffnen** für die Website, die die Bibliothek enthält.|  
|Erstellen, Bearbeiten oder Löschen aller Abonnements auf einer Website.|**Benachrichtigungen verwalten** für die Website.|  
  
##  <a name="permissionDataSources"></a> Berechtigungen zum Erstellen und Verwalten von freigegebenen Datenquellen und Berichtsmodellen  
 Eine freigegebene Datenquellendatei (RSDS) enthält Datenquellen-Verbindungsinformationen, die von mehreren Berichten und Modellen verwendet werden können. Für Standardberichte ist die Verwendung einer RSDS-Datei zum Angeben von Datenquellen-Verbindungsinformationen optional. Für modellgesteuerte Berichte ist die Verwendung einer RSDS-Datei erforderlich. Ein Berichtsmodell verwendet immer eine RSDS-Datei zum Herstellen von Verbindungen mit externen Datenquellen.  
  
 Sie können Eigenschaften für freigegebene Datenquellen festlegen, die bestimmen, ob einzelne Benutzer freigegebene Datenquellen anzeigen oder verwalten können. Berechtigungen zum Anzeigen oder Verwalten einer freigegebenen Datenquelle unterscheiden sich von Berechtigungen zum Anzeigen von Berichten. Sie können einen Bericht anzeigen, der eine RSDS-Datei verwendet, ohne die Berechtigung zum Anzeigen der RSDS-Datei selbst zu haben.  
  
|Aufgaben|Berechtigung|  
|-----------|----------------|  
|Erstellen einer freigegebenen Datenquelle.|**Elemente hinzufügen** für die Bibliothek, die die freigegebene Datenquelle enthält. Sie können neue freigegebene Datenquellen über das Menü Neu in einer Bibliothek erstellen. Dazu müssen Sie den Inhaltstyp Berichtsdatenquelle mit der Bibliothek registrieren. Weitere Informationen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).|  
|Bearbeiten einer freigegebenen Datenquelle.|**Elemente bearbeiten** für die Bibliothek, die die freigegebene Datenquelle enthält, oder für die freigegebene Datenquelle selbst.|  
|Löschen einer freigegebenen Datenquelle.|**Elemente löschen** für die Bibliothek, die die freigegebene Datenquelle enthält, oder für die freigegebene Datenquelle selbst.|  
|Verwenden einer freigegebenen Datenquelle (RSDS) mit einem Bericht.|**Elemente bearbeiten** für den Bericht oder für die Bibliothek, die den Bericht enthält. Das Auswählen einer freigegebenen Datenquelle gehört zum Festlegen von Datenquelleneigenschaften für einen Bericht.|  
|Generieren eines Berichtsmodells aus einer freigegebenen Datenquelle.|**Elemente hinzufügen** für die Bibliothek, die das Berichtsmodell enthalten wird.|  
|Löschen eines Berichtsmodells.|**Elemente löschen** für die Bibliothek, die das Berichtsmodell enthält, oder für das Berichtsmodell selbst.|  
|Festlegen von Berechtigungen innerhalb eines Modells für bestimmte Modellelemente.|**Berechtigungen verwalten** für die Website, die die Bibliothek und die Berichtsmodelldatei (SMDL) enthält.|  
  
> [!NOTE]  
>  Es sind keine Berechtigungen zum Bearbeiten von Berichtsmodellen vorhanden. Sie können Berichtsmodelle zwar generieren oder löschen, jedoch nicht von einer SharePoint-Website aus bearbeiten. Für das Bearbeiten von Berichtsmodellen ist der Modell-Designer erforderlich, ein Clienterstellungstool, auf das Berechtigungen, die Sie in SharePoint festlegen, keine Auswirkungen haben.  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Vergleich zwischen Sie Rollen und Aufgaben in Reporting Services to SharePoint Groups and Permissions](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Verwenden der integrierten Sicherheit in Windows SharePoint Services für Berichtsserverelemente](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
  
  
