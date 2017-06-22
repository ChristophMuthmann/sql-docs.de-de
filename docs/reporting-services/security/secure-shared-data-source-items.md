---
title: Sichern freigegebener Datenquellenelemente | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
- security [Reporting Services], data sources
ms.assetid: 7299e498-0a1a-4821-a22a-5199bb773ce0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e056f5577c2c569e333f2341060862c06d803f6b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="secure-shared-data-source-items"></a>Sichern freigegebener Datenquellenelemente
  Sie können ein freigegebenes Datenquellenelement sichern, um den Zugriff darauf zu aktivieren bzw. zu deaktivieren.  
  
 Ein Benutzer mit dem Mindestzugriffsrecht für eine freigegebene Datenquelle (z.B. der Zugriff über die **Browser** -Rolle) kann die Liste der Berichte anzeigen, die das Element verwenden, vorausgesetzt der Benutzer hat auch die Berechtigung zum Anzeigen der Berichte selbst.  
  
 Ein Benutzer mit zusätzlichen Zugriffsrechten (z.B. über die **Inhalts-Manager** -Rolle) kann Eigenschaften für die freigegebene Datenquelle anzeigen und festlegen.  
  
 Zum Festlegen der Sicherheit erstellen Sie eine Rollenzuweisung, die angibt, welches Benutzer- oder Gruppenkonto Zugriff auf die freigegebene Datenquelle hat. Benutzer mit Zugriff auf ein freigegebenes Datenquellenelement können dessen Namen, Beschreibung, Verbindungszeichenfolge oder Anmeldeinformationen ändern.  
  
## <a name="tasks-and-access-to-items"></a>Aufgaben und Zugriffsrechte für Elemente  
 Beim Erstellen von Rollenzuweisungen sollten Sie eine Rolle verwenden, die die folgenden Aufgaben einschließt, um den Benutzern und Gruppen die geeigneten Berechtigungen zuzuweisen.  
  
|Verwendete Aufgabe|Berechtigt zu folgender Aktion|  
|----------------------|---------------------------------|  
|Datenquellen anzeigen|Anzeigen des freigegebenen Datenquellenelements in der Ordnerhierarchie. Ohne diese Aufgabe ist das Element für die Benutzer nicht sichtbar, und sie wissen möglicherweise nicht, dass die Datenquelle verfügbar ist.|  
|Datenquellen verwalten|Anzeigen von Eigenschaften, die den Namen, eine Beschreibung und Verbindungsinformationen angeben. Mit dieser Aufgabe wird auch ein freigegebenes Datenquellenelement in der Ordnerhierarchie angezeigt. Wenn Sie diese Aufgabe auswählen, können Sie die Aufgabe "Datenquellen anzeigen" auslassen.|  
|Die Sicherheit für einzelne Elemente festlegen|Erstellen und Ändern von Rollenzuweisungen, die den Zugriff auf die freigegebene Datenquelle steuern. Diese Aufgabe muss zusammen mit Datenquellen anzeigen oder Datenquellen verwalten verwendet werden. Andernfalls zeigt sie keine Wirkung, weil der Benutzer das Element nicht auswählen kann.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Berichtsdatenquellen](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Sichere Ordner](../../reporting-services/security/secure-folders.md)   
 [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
