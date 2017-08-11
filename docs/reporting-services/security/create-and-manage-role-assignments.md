---
title: Erstellen und Verwalten von Rollenzuweisungen | Microsoft Docs
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
- removing role assignments
- roles [Reporting Services], assignments
- security [Reporting Services], role assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 086d0987-b43c-4834-8372-e08fb4b432f8
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8c07e836a48774cbf9c0c5441fde9d5df854fdcb
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="create-and-manage-role-assignments"></a>Erstellen und Verwalten von Rollenzuweisungen
  Eine *Rollenzuweisung* ist eine Sicherheitsrichtlinie, die bestimmt, ob ein Benutzer oder eine Gruppe auf einen bestimmten Berichtsserver zugreifen und einen Vorgang ausführen kann. Eine Rollenzuweisung besteht aus einem einzelnen Benutzer- oder Gruppenkontonamen und mindestens einer Rollendefinition.  
  
 Rollenzuweisungen gelten auf *Elementebene* oder *Systemebene*.  
  
-   Rollenzuweisungen auf Elementebene werden immer im Kontext eines bestimmten Elements oder Zweigs in der Ordnerhierarchie des Berichtsservers erstellt. Sie navigieren zu einem bestimmten Ordner oder Element, um eine Rollenzuweisung dafür zu erstellen.  
  
-   Mit Rollenzuweisungen auf Systemebene wird es ausgewählten Benutzern ermöglicht, Aufgaben auszuführen, die die Berichtsserversite insgesamt betreffen. Zu diesen Aufgaben zählt das Erstellen freigegebener Zeitpläne, das Verwalten von Aufträgen, das Verarbeiten von Berichten im Berichts-Generator und das Festlegen von Eigenschaften. Die Sicherheit auf Systemebene betrifft nicht den Zugriff auf Elemente in der Ordnerhierarchie des Berichtsservers.  
  
## <a name="creating-an-item-level-role-assignment"></a>So erstellen Sie eine Rollenzuweisung auf Elementebene  
 Öffnen Sie im Berichts-Manager die Eigenschaftsseiten Sicherheit des Elements, das Sie schützen möchten.  
  
 Sie müssen für jedes Benutzer- oder Gruppenkonto, das auf den Berichtsserver zugreifen können muss, eine eigene Rollenzuweisung erstellen. Befindet sich das Konto nicht in der Domäne, in der der Berichtsserver enthalten ist, geben Sie den Domänennamen an. Nachdem Sie ein Konto angegeben haben, können Sie eine oder mehrere Rollendefinitionen auswählen. Die Rollendefinitionen sind kumulativ. Der kombinierte Satz aller Aufgaben aus allen Definitionen wird in der Zuweisung für einen bestimmten Benutzer oder eine bestimmte Gruppe unterstützt.  
  
 Um den Zugriff auf breiter Basis zu ermöglichen, sollten Sie ein Element auswählen, das weit oben in der Ordnerhierarchie angeordnet ist (z. B. den Stammknoten Stamm). Anschließend können Sie Rollenzuweisungen erstellen, um bestimmte Bereiche der Ordnerhierarchie zu sperren.  
  
 Sie müssen Mitglied der lokalen Gruppe Administratoren auf dem Berichtsserver-Computer sein, um eine Rollenzuweisung erstellen zu können. Sie können diese Aufgabe delegieren, indem Sie andere Benutzer der Rolle **Inhalts-Manager** zuweisen.  
  
 Weitere Informationen finden Sie unter [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md).  
  
## <a name="creating-a-system-level-role-assignment"></a>Erstellen einer Rollenzuweisung auf Systemebene  
 Öffnen Sie im Berichts-Manager die Seite Siteeinstellungen, um Rollenzuweisungen auf Systemebene zu definieren und zu verwalten.  
  
 Rollenzuweisungen auf System- und Elementebene ergänzen sich. Sie sollten allen Benutzern oder Gruppen, die über eine Rollenzuweisung auf Elementebene verfügen, auch eine Rolle auf Systemebene zuweisen.  
  
 Rollenzuweisungen auf Systemebene umfassen eine Vielzahl von Berechtigungen, jedoch keine Berechtigungen, die Teil einer Rollenzuweisung auf Elementebene sind. Im Gegensatz zu den Systemberechtigungen auf einem Computer umfassen die Systemrollen in Berichtsservern keine übergreifenden Berechtigungen, die den gesamten Satz an möglichen Vorgängen beinhalten. Bei Rollenzuweisungen auf Systemebene handelt es sich einfach um eine Menge von Tasks, die die Berichtsserversite betreffen. Berechtigungen, die über die Systemrollenzuweisungen übertragen werden, bestimmen, ob Benutzer Anwendungseigenschaften (beispielsweise als Bild oder Titel der Homepage) anzeigen, freigegebene Zeitpläne anzeigen oder verwalten oder den Berichts-Generator ausführen können.  
  
 Weitere Informationen finden Sie unter [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md) und [Vordefinierte Rollen](../../reporting-services/security/role-definitions-predefined-roles.md).  
  
## <a name="modifying-a-role-assignment"></a>Ändern einer Rollenzuweisung  
 Eine Rollenzuweisung kann jederzeit geändert werden. Die Änderungen werden wirksam, wenn Sie die Rollenzuweisung speichern. Benutzersitzungen sind von Rollenzuweisungsänderungen nicht betroffen. Wenn ein Benutzer einen Bericht geöffnet hat, und Sie ändern eine Rollenzuweisung, um den Zugriff darauf zu sperren, kann der Benutzer den Bericht weiterhin in der aktuellen Sitzung verwenden.  
  
 Wenn Sie ein Benutzerkonto einer Gruppe hinzufügen, die bereits Teil einer Rollenzuweisung ist, gibt es eine Verzögerung, bevor das Benutzerkonto über die Gruppenkontorichtlinien auf Elemente zugreifen kann. Diese Verzögerung wird durch das Zwischenspeichern von Authentifizierungstokens durch Internetinformationsdienste (Internet Information Services, IIS) verursacht. Sie können entweder warten, bis die Tokens aktualisiert werden (die Wartezeit beträgt normalerweise fünfzehn Minuten), oder Sie können IIS zurücksetzen, um den Cache sofort zu aktualisieren.  
  
 Es kann immer nur eine Rollenzuweisung geändert werden. Sie können nicht global suchen und ersetzen, um die Namen oder Einstellungen von Rollendefinitionen zu ändern oder um alle Rollenzuweisungen mit einem bestimmten Benutzer oder einer bestimmten Gruppe zu suchen.  
  
## <a name="deleting-a-role-assignment"></a>Löschen einer Rollenzuweisung  
 Zum Löschen von Rollenzuweisungen aktivieren Sie das Kontrollkästchen neben den Rollenzuweisungen, die Sie löschen möchten, und klicken Sie dann auf **Löschen**. Zum Löschen von Rollenzuweisungen können Sie auch auf die Schaltfläche **Zur übergeordneten Sicherheit zurückkehren**klicken. Dadurch werden die vorhandenen Rollenzuweisungen für das Element gelöscht und stattdessen die Rollenzuweisungen eines übergeordneten Elements verwendet.  
  
## <a name="see-also"></a>Siehe auch  
 [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [Ändern Sie oder löschen Sie einer Rollenzuweisung &#40; Berichts-Manager &#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)   
 [Rollenzuweisungen](../../reporting-services/security/role-assignments.md)   
 [Rollendefinitionen](../../reporting-services/security/role-definitions.md)   
 [Vordefinierte Rollen](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
