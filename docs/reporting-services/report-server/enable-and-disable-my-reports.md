---
title: "Aktivieren und Deaktivieren von „Meine Berichte“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
caps.latest.revision: "37"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 352e2118319664c4458c4e46ea5623bcf8290a45
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="enable-and-disable-my-reports"></a>Aktivieren und Deaktivieren von "Meine Berichte"
  Die Funktion Meine Berichte ordnet persönlichen Speicherbereich in der Berichtsserver-Datenbank zu, damit Benutzer ihre eigenen Berichte in einem privaten Ordner speichern können. Als Berichtsserveradministrator können Sie diese Funktion aktivieren bzw. deaktivieren oder dessen Funktionsweise ändern, indem Sie die Sicherheitseinstellungen bearbeiten, die steuern, welche Funktionen die Benutzer mit diesem Arbeitsbereich ausführen können.  
  
 Standardmäßig ist die Funktion Meine Berichte deaktiviert. Diese Funktion kann für alle Benutzer aktiviert oder deaktiviert werden. Es ist jedoch nicht möglich, dieses Funktion nur für bestimmte Benutzer zu aktivieren. Die meisten Benutzer und Organisationen finden diese Funktion hilfreich. Entscheiden Sie anhand der weiter unten in diesem Thema beschriebenen Vor- und Nachteile, ob es für Ihre Organisation geeignet ist.  
  
## <a name="how-to-enable-and-disable-my-reports"></a>Aktivieren und Deaktivieren von Meine Berichte  
 Um Meine Berichte mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]zu aktivieren, stellen Sie eine Verbindung zur Berichtsserverinstanz her, und öffnen Sie die Seite **Servereigenschaften** . Aktivieren Sie dann auf der Registerkarte **Allgemein** Registerkarte die Option **Für jeden Benutzer den Ordner "Meine Berichte" aktivieren** .  
  
 Von der für Meine Berichte verwendeten Rollendefinition hängt es ab, welche Aktionen im Arbeitsbereich Meine Berichte unterstützt werden. Wenn z. B. Verknüpfte Berichte erstellen nicht in der Rolle Meine Berichte enthalten ist, können die Benutzer keine verknüpften Berichte in den Ordnern Meine Berichte erstellen. Weitere Informationen finden Sie unter [Sichern von Meine Berichte](../../reporting-services/security/secure-my-reports.md).  
  
 Zum Deaktivieren von Meine Berichte deaktivieren Sie **Für jeden Benutzer den Ordner 'Meine Berichte' aktivieren**. Dadurch ist der Ordner Meine Berichte für Benutzer überhaupt nicht mehr sichtbar. Die Ordner, die Speicherbereich bereitstellen (d. h. die Unterordner in Benutzerordner), müssen nach der Deaktivierung dieses Funktionen manuell gelöscht werden.  
  
### <a name="when-my-reports-is-activated"></a>Wenn Meine Berichte aktiviert ist  
 Wenn diese Funktion aktiviert ist, wird der Ordner Meine Berichte unterhalb des Stammordners Home angezeigt. Neben dem Ordner Meine Berichte ist für Berichtsserveradministratoren außerdem der Ordner Benutzerordner sichtbar, der einen Unterordner für jeden Benutzer enthält.  
  
 Bei aktivierter Funktion können Benutzerordner und dessen Unterordner nicht gelöscht werden. Außerdem wird der Name "Meine Berichte" zu einem reservierten Namen für Unterordner des Stammknotens (Home).  
  
 Wenn Sie Meine Berichte wieder aktivieren, erstellt der Berichtsserver einen neuen Ordner Benutzerordner, falls dieser Ordner noch nicht vorhanden sein sollte. Falls Benutzerordner bereits vorhanden ist, fügt der Berichtsserver neue Unterordner hinzu, wenn sich Benutzer bei ihren Ordnern Meine Berichte anmelden.  
  
### <a name="when-my-reports-is-deactivated"></a>Wenn Meine Berichte deaktiviert ist  
 Wenn diese Funktion deaktiviert ist, wird die Reservierung des Namens "Meine Berichte" aufgehoben. Die Benutzer können dann einen persönlichen Unterordner Meine Berichte im Ordner Home erstellen. Darüber hinaus ist eine Umleitung von Meine Berichte zu benutzerspezifischen Unterordnern von Meine Berichte nicht mehr ausgeführt. Schließlich sind alle Berichtslinks, die einen benutzerspezifischen Ordner Meine Berichte in der URL-Adresse enthalten, nicht mehr funktionsfähig.  
  
## <a name="choosing-to-use-my-reports"></a>Wählen der Verwendung von Meine Berichte  
 Ob Sie Meine Berichte verwenden, hängt davon ab, ob Sie Serverressourcen zur Unterstützung von Benutzerarbeitsbereichen verwenden möchten. Meine Berichte ist eine leistungsfähige Funktion, mit dem Benutzer Informationsressourcen kontrollieren können, die ihnen das Arbeiten erleichtern. Darüber hinaus handelt es sich dabei für Benutzer um eine Möglichkeit der Verwendung von Berichten, die nicht für den allgemeinen Gebrauch gedacht sind. Einer der überzeugendsten Gründe für die Verwendung von Meine Berichte ist die Tatsache, dass diese Funktion eine sichere, verwaltbare Unterstützung für diejenigen Benutzer ermöglicht, die Berichte erstellen und bearbeiten müssen. Ohne diese Funktion müssten Sie Ordner und Sicherheitsrichtlinien für verschiedene Benutzer auf Ad-hoc-Basis erstellen. Bei der Änderung von Benutzern und Benutzeranforderungen führt diese Vorgehensweise zu einer ständig zunehmenden Zahl von Ordnern und Richtlinien, deren Verwaltung im Laufe der Zeit immer schwieriger wird.  
  
 Beachten Sie, dass beim Aktivieren von Meine Berichte der Berichtsserver einen Ordner Meine Berichte für jeden Benutzer mit einem Domänenkonto erstellt, der auf den Link Meine Berichte klickt, selbst wenn der Benutzer keinen solchen Ordner wünscht oder benötigt. Es gibt keine systematische Methode, um zu ermitteln, welche Ordner verwendet werden. Sie müssen manuell prüfen, ob die Ordner einen Inhalt aufweisen.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern von Meine Berichte](../../reporting-services/security/secure-my-reports.md)   
 [Berichtsserver Content Management (einheitlicher SSRS-Modus)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
