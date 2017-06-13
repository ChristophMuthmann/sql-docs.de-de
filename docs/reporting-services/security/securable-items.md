---
title: "Sicherungsfähige Elemente | Microsoft Docs"
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
- securable items [Reporting Services]
- roles [Reporting Services], securable items
- security [Reporting Services], securable items listed
- role-based security [Reporting Services], securable items
ms.assetid: 27f58d4c-5c7b-4947-af5b-0f1fa60faf5f
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b1c11b204b5a48e4324f49e05467cc3ac96e7fa4
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="securable-items"></a>Sicherbare Elemente
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet rollenbasierte Sicherheit zur Steuerung des Zugriffs auf die Elemente, die auf einem Berichtsserver gespeichert sind. Wenn Sie Benutzerzugriff auf einen Berichtsserver gewähren, erstellen Sie in der Regel ein Rollenzuweisungspaar:  
  
-   Auf Websiteebene  
  
-   Im Stammordner, dem Stammknoten der Ordnerhierarchie auf dem Berichtsserver  
  
 Die Sicherheit wird innerhalb der Ordnerhierarchie des Berichtsservers vererbt. Wenn Sie Rollenzuweisungen auf Websiteebene und im Stammordner erstellen, wird eine Vererbung der Berechtigungen festgelegt, die sich auf alle Elemente und Vorgänge auf einem Berichtsserver erstreckt.  
  
 Sie können die Berechtigungsvererbung überschreiben, indem Sie Sicherheit für einzelne Elemente definieren. Zu den Elementen, die Sie einzeln sichern können, gehören:  
  
-   Ordner  
  
-   Berichte  
  
-   Berichtsmodelle  
  
-   Ressourcen  
  
-   Freigegebene Datenquellen  
  
-   Freigegebene Datasets  
  
 Andere Konstrukte, wie z. B. Zeitpläne und Abonnements, werden nicht explizit gesichert. Zeitpläne und Abonnements verwenden die Sicherheit eines Berichts.  
  
## <a name="item-descriptions"></a>Elementbeschreibungen  
 In der folgenden Tabelle werden die sicherungsfähigen Elemente aufgelistet und ihre Merkmale beschrieben.  
  
|Element|Merkmale|  
|----------|---------------------|  
|Ordner|Die Ordnersicherheit gilt für den Ordner selbst und die darin enthaltenen Elemente. Der Ordner Stamm ist der Stammknoten der Ordnerhierarchie. Die Sicherheit, die Sie für diesen Ordner festlegen, stellt die anfänglichen Sicherheitseinstellungen für alle untergeordneten Ordner, Berichte, Ressourcen und freigegebenen Datenquellen in der Ordnerhierarchie her. Weitere Informationen finden Sie unter [Sichere Ordner](../../reporting-services/security/secure-folders.md).<br /><br /> Meine Berichte ist ein spezieller Ordner, der über eine implizite Rollenzuweisung basierend auf einer dedizierten Rolle gesichert wird. Weitere Informationen finden Sie unter [Sichern von Meine Berichte](../../reporting-services/security/secure-my-reports.md).|  
|Berichte|Berichte und verknüpfte Berichte können gesichert werden, um die verfügbaren Aktionen, die Benutzer ausführen können, zu steuern, wie z. B. das Ändern der Eigenschaften eines bestimmten Berichts.<br /><br /> Der Berichtsverlauf wird über den Bericht, der den Verlauf enthält, gesichert. Einzelne Momentaufnahmen des Berichtsverlaufs können nicht gesichert werden.<br /><br /> Weitere Informationen zur Berichtssicherheit finden Sie unter [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md).|  
|Berichtsmodelle|Sie können die Rollenzuweisung für den gesamten oder für einen Teil des Berichts angeben. Da Berichtsmodelle äußerst umfangreich sein können, möchten Sie möglicherweise die Modellelemente sichern, die vertraulichen Daten zugeordnet sind.|  
|Ressourcen|Ressourcen können gesichert werden, um den Zugriff auf die Ressource selbst und deren Eigenschaften zu steuern.<br /><br /> Nur eigenständige Ressourcen können als separate Elemente gesichert werden. Ressourcen, die in einen Bericht eingebettet sind, können nicht separat von diesem Bericht gesichert werden.<br /><br /> Weitere Informationen zur Ressourcensicherheit finden Sie unter [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md).|  
|Freigegebene Datenquellen|Freigegebene Datenquellen können gesichert werden, um den Zugriff auf das Element und seine Eigenschaftsseiten einzuschränken. Weitere Informationen finden Sie unter [Sichern freigegebener Datenquellenelemente](../../reporting-services/security/secure-shared-data-source-items.md).|  
|Freigegebene Datasets|Freigegebenen Datasets können gesichert werden, um die von Benutzern ausführbaren Aktionen zu steuern, z. B. Anzeigen oder Ändern der Definition bzw. Ändern der Eigenschaften eines bestimmten freigegebenen Datasets.<br /><br /> Weitere Informationen finden Sie unter [Sichern von freigegebenen Datasetelementen](../../reporting-services/security/secure-shared-dataset-items.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Erteilen von Berechtigungen für einen Berichtsserver im einheitlichen Modus](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Erstellen, Löschen oder Ändern einer Rolle &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)   
 [Gewähren von Benutzerzugriff auf einen Berichtsserver &#40;Berichts-Manager&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md)   
 [Ändern oder Löschen einer Rollenzuweisung &#40;Berichts-Manager&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)  
  
  
