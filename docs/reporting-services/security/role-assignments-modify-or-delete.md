---
title: "Ändern oder Löschen einer Rollenzuweisung (Berichts-Manager) | Microsoft Docs"
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
- system roles [Reporting Services]
- modifying role assignments
- deleting role assignments
ms.assetid: 523bdd32-92cb-4b48-a3a9-d58b2385bde7
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1a0db8452d082dddf6f5ffc39c1a9bd5802bf114
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="role-assignments---modify-or-delete"></a>Rollenzuweisungen - ändern oder löschen
  Mit einer Rollenzuweisung werden eine Gruppe oder ein Benutzerkonto einer vordefinierten Rollendefinition zugewiesen, die ausführbare Aufgaben beinhaltet. Hiermit werden die Vorgangstypen festgelegt, die ein Benutzer für einen Ordner, einen Bericht, ein Modell oder einen anderen Inhaltstyp ausführen kann. Verwenden Sie den Berichts-Manager zum Erstellen, Löschen oder Ändern von Rollenzuweisungen. Nach der Erstellung einer Rollenzuweisung für einen bestimmten Benutzer oder eine bestimmte Gruppe können Sie diese später durch Auswahl einer anderen Rolle ändern. Möchten Sie Berechtigungen für einen Berichtsserver widerrufen, können Sie die Rollenzuweisung vom Berichtsserver löschen.  
  
 Je nach Zielsetzung können alternative Vorgehensweisen geeigneter sein. Beispiele hierfür sind die Anpassung oder Erstellung einer neuen Rollendefinition beziehungsweise die Änderung der Mitgliedschaft eines Gruppenkontos in Active Directory.  
  
 Angenommen, Sie verfügen beispielsweise über eine Benutzergruppe, die ihren Inhalt vollständig verwalten muss, jedoch nicht über alle dem Inhalts-Manager zugewiesenen Berechtigungen verfügen soll. In diesem Fall könnten Sie eine neue Rollendefinition mit der Bezeichnung "Inhalts-Manager für Abteilung" erstellen, die alle Aufgaben des Inhalts-Manager enthält, ausgenommen **Sicherheit für einzelne Elemente festlegen**.  
  
 Ähnliches gilt, falls Sie System- oder Netzwerkadministrator sind und Active Directory-Gruppenkonten einfacher verwalten können als Rollenzuweisungen im Berichts-Manager. In diesem Fall können Sie den Aufwand für die Verwaltung von Rollenzuweisungen durch die Erstellung einer einzelnen Rollenzuweisung für ein Gruppenkonto und die anschließende Anpassung der Gruppenmitgliedschaft, wenn Benutzer keinen Zugriff mehr auf Berichte benötigen, verringern.  
  
 Sollten Sie zu dem Schluss kommen, dass die Änderung oder Löschung einer Rollenzuweisung die beste Vorgehensweise ist, denken Sie daran, sowohl die Rollenzuweisungen auf Systemebene als auch die Rollenzuweisungen auf Elementebene zu prüfen. Jeder Rollenzuweisungstyp wird auf anderen Seiten im Berichts-Manager konfiguriert.  
  
### <a name="to-modify-or-delete-a-system-role-assignment"></a>So löschen oder ändern Sie eine Systemrollenzuweisung  
  
1.  Starten Sie den [Berichts-Manager &#40;einheitlicher SSRS-Modus&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Klicken Sie auf **Siteeinstellungen**.  
  
3.  Klicken Sie auf **Sicherheit**. Alle aktuell für den Server oder die Bereitstellung für horizontales Skalieren definierten Rollenzuweisungen auf Systemebene werden anhand des Kontonamens aufgeführt.  
  
4.  Suchen Sie die zu ändernde oder zu löschende Rollenzuweisung.  
  
5.  Zum Hinzufügen oder Entfernen der Rolle für einen bestimmten Benutzer oder eine bestimmte Gruppe klicken Sie auf **Bearbeiten**.  
  
6.  Aktivieren Sie zum Löschen einer Rollenzuweisung das Kontrollkästchen neben dem Gruppen- oder Benutzernamen, und klicken Sie dann auf **Löschen**.  
  
### <a name="to-modify-or-delete-an-item-role-assignment"></a>So löschen oder ändern Sie eine Elementrollenzuweisung  
  
1.  Starten Sie den **Berichts-Manager** , und suchen Sie das Element, für das Sie eine Rollenzuweisung bearbeiten oder löschen möchten.  
  
2.  Zeigen Sie auf das Element, und klicken Sie auf den Dropdownpfeil.  
  
3.  Klicken Sie im Dropdownmenü auf **Sicherheit**.  
  
4.  Suchen Sie die zu ändernde oder zu löschende Rollenzuweisung.  
  
5.  Zum Hinzufügen oder Entfernen der Rolle für einen bestimmten Benutzer oder eine bestimmte Gruppe klicken Sie auf **Bearbeiten**.  
  
6.  Aktivieren Sie zum Löschen einer Rollenzuweisung das Kontrollkästchen neben dem Gruppen- oder Benutzernamen, und klicken Sie dann auf **Löschen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Rollenzuweisungen](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Rollenzuweisungen](../../reporting-services/security/role-assignments.md)   
 [Seite "Einstellungen" Standort &#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/4d67a01c-eae4-49ba-a6e8-8e983c0248f5)   
 [Neue Systemrollenzuweisung: Bearbeiten Sie, Seite "System" Zuweisungen "&#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/62a22ab9-1eb4-4ce5-8dd7-06b5ed2d9a2a)  
  
  
