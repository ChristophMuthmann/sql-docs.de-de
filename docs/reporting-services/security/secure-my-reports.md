---
title: Sichern von Meine Berichte | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 162f43fc4f81c228d90839c75d1959d71eff9322
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="secure-my-reports"></a>Sichern von Meine Berichte
  Die Funktion Meine Berichte stellt einen vom Benutzer verwalteten Arbeitsbereich zum Verwenden von Berichten bereit. Damit der Ordner Meine Berichte seinen Zweck erfüllt, sind im Vergleich zu anderen Ordnern, die zur allgemeinen Verwendung dienen, für den Ordner Meine Berichte weniger stark einschränkende Berechtigungen erforderlich. Benutzer, die nur über die Berechtigung zum Anzeigen und Ausführen von Berichten in anderen Ordnern verfügen, benötigen möglicherweise erweiterte Berechtigungen, um den Ordner "Meine Berichte" und die in ihrem Besitz befindlichen Inhalt zu verwalten. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält zu diesem Zweck eine spezielle Rollenzuweisung und Rollendefinition.  
  
> [!NOTE]  
>  Meine Berichte ist nur im Berichts-Manager verfügbar. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="role-assignment-for-my-reports"></a>Rollenzuweisung für Meine Berichte  
 Die Rollenzuweisung für Meine Berichte enthält vordefinierte Elemente und wird automatisch für jeden Benutzer erstellt, der einen Ordner Meine Berichte aktiviert. Die automatische Zuweisung der Sicherheit durch den Berichtsserver ist besonders hilfreich für Organisationen, die Meine Berichte auf breiter Basis verwenden, weil es nicht notwendig ist, dass Administratoren den Zugriff für jeden Benutzer von Meine Berichte aktivieren.  
  
 Eine Rollenzuweisung für **Meine Berichte** setzt sich wie folgt zusammen:  
  
-   Der benutzerorder Meine Berichte-Ordner, Datei befindet sich im Benutzerordner\\*\<Benutzername >*\My Ordner "Berichte".  
  
-   Das Benutzerkonto, das beim Aktivieren des Ordners Meine Berichte bestimmt wird. Ein Ordner wird aktiviert, wenn ein Benutzer auf einen Ordner Meine Berichte im Berichts-Manager klickt oder wenn ein Bericht im Berichts-Designer im Ordner Meine Berichte veröffentlicht wird. Dieser Ordner wird außerdem aktiviert, wenn ein Benutzer Eigenschaften über den Link Meine Berichte anfordert.  
  
-   Die vordefinierte Rollendefinition für Meine Berichte.  
  
## <a name="role-definition-for-my-reports"></a>Rollendefinition für Meine Berichte  
 In der Rollendefinition für **Meine Berichte** sind Aufgaben enthalten, die die Inhaltsverwaltung eines Ordners Meine Berichte unterstützen. Die Rolle **Meine Berichte** ist als Rolle für einen einzelnen Verwendungszweck gedacht. Sie können diese Rolle zwar für eine beliebige Sicherheitsrichtlinie auf Elementebene auswählen, aber davon wird abgeraten, um zu verhindern, dass Sie die Rolle für andere Ordneranforderungen anpassen. Das Reservieren der **Meine Berichte** -Rolle für die Funktion Meine Berichte trägt dazu bei, dass die Benutzer eine einheitliche Oberfläche vorfinden.  
  
 Standardmäßig ändern nur Berichtsserveradministratoren die **Meine Berichte** -Rolle. Sie können die **Meine Berichte** -Rolle anpassen, indem Sie die darin enthaltenen Aufgaben ändern. Außerdem können Sie diese Rolle durch eine andere Rolle ersetzen.  
  
## <a name="denying-access-to-my-reports"></a>Verweigern des Zugriffs auf Meine Berichte  
 Sie können Benutzern folgendermaßen den Zugriff auf Meine Berichte verweigern:  
  
-   Deaktivieren von Meine Berichte auf der Seite Siteeinstellungen. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren von "Meine Berichte"](../../reporting-services/report-server/enable-and-disable-my-reports.md).  
  
-   Entfernen aller Aufgaben aus der **Meine Berichte** -Rolle.  
  
 Wenn Sie Meine Berichte deaktivieren, wird der Link zum Ordner Meine Berichte aus dem Berichts-Manager entfernt. Die zugrunde liegende Ordnerstruktur, die Meine Berichte unterstützt (d. h. der Ordner Benutzerordner und die zugehörigen Unterordner), sind weiterhin verfügbar und können aufgerufen werden, wenn ein Benutzer den Ordnerpfad kennt. Durch das Entfernen von Aufgaben aus der **Meine Berichte** -Rolle wird die Zugriffsverweigerung sichergestellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md)   
 [Sichere Ordner](../../reporting-services/security/secure-folders.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
