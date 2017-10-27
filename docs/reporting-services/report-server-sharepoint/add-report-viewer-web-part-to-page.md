---
title: "SQL Server Reporting Services Berichts-Viewer-Webpart zu einer SharePoint-Seite hinzufügen | Microsoft Docs"
ms.custom: Display a report, from SQL Server Reporting Services or Power BI Report Server, by adding a Report Viewer web part to a SharePoint page.
ms.date: 09/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: fbc68b6ff9f1edf5cf6ee13f6e93a3d2d1a8f834
ms.contentlocale: de-de
ms.lasthandoff: 10/06/2017

---

# <a name="add-sql-server-reporting-services-report-viewer-web-part-to-a-sharepoint-page"></a>SQL Server Reporting Services Berichts-Viewer-Webpart zu einer SharePoint-Seite hinzufügen

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Einen Bericht, aus SQL Server Reporting Services oder Power BI-Berichtsserver, indem Sie einen Berichts-Viewer-Webpart einer SharePoint-Seite hinzufügen angezeigt.

![Berichts-Viewer-Webpart auf einer SharePoint-Seite](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="prerequisites"></a>Erforderliche Komponenten

* Damit die Berichte erfolgreich geladen eingeschränkte Claims to Windows Token Service (C2WTS) muss für Kerberos konfiguriert werden Delegierung. Weitere Informationen zum Konfigurieren von C2WTS finden Sie unter [Claims to Windows Token Service (C2WTS) und Reporting Services](../install-windows/claims-to-windows-token-service-c2wts-and-reporting-services.md).

* Der Berichts-Viewer-Webpart muss zur SharePoint-Farm bereitgestellt werden. Informationen zum Bereitstellen der Lösung Webpartprojekt in Berichts-Viewer finden Sie unter [das Berichts-Viewer-Webpart auf einer SharePoint-Website bereitstellen](deploy-report-viewer-web-part.md).

* Um ein Webpart zu einer Webseite hinzufügen, müssen Sie die Berechtigung hinzufügen und Anpassen von Seiten auf Websiteebene verfügen. Wenn Sie Standardsicherheitseinstellungen verwenden, wird diese Berechtigung Mitgliedern der Gruppe **Besitzer** erteilt, die über Berechtigungen für den Vollzugriff verfügen.

## <a name="add-web-part"></a>Fügen Sie Webpart hinzu

1. Wählen Sie in der SharePoint-Website, die **Zahnradsymbol** Symbol in der oberen linken Ecke aus, und wählen **fügen Sie eine Seite**.

    ![Fügen Sie eine Seite aus dem Zahnradsymbol auf einer Sharepoint-Website.](media/sharepoint-add-a-page.png)

2. Weisen Sie der Seite einen Namen und eine Select **erstellen**.

3. Wählen Sie im Seitendesigner der **einfügen** Registerkarte im Menüband. Wählen Sie dann **Webpart** innerhalb der **Teile** Abschnitt.

    ![Fügen Sie ein Webpart aus dem Office-Menüband.](media/sharepoint-insert-web-part.png)

4. Klicken Sie unter **Kategorien**Option ** SQL Server Reporting Services (einheitlicher Modus). Klicken Sie unter **Teile**Option **Berichts-Viewer**. Wählen Sie dann **hinzufügen**.

    ![Berichts-Viewer-Webpart hinzufügen.](media/sharepoint-report-viewer-web-part.png)

    Dies kann anfangs mit der Fehlermeldung angezeigt. Der Fehler ist, da die Standard-Berichtsserver-URL, um festgelegt ist *http://localhost* und möglicherweise an diesem Speicherort nicht verfügbar sein.

## <a name="configure-the-report-viewer-web-part"></a>Konfigurieren des Berichts-Viewer-Webparts

Führen Sie folgende Schritte aus, um das Webpart zu einem bestimmten Bericht zeigen zu konfigurieren.

1. Wenn Sie die SharePoint-Seite zu bearbeiten, wählen Sie den Pfeil nach unten in der oberen rechten Ecke des Webparts, und wählen Sie **Webpart bearbeiten**.

    ![Bearbeiten der Webseite Web Teil Dropdownmenü aus.](media/sharepoint-edit-web-part.png)

2. Geben Sie die **Berichtsserver-URL** für den Berichtsserver hostet den Bericht. Dies sollte ungefähr *http://myrsserver/reportserver*.

3. Geben Sie den Pfad und den Namen des Berichts, der innerhalb des Webparts angezeigt werden soll. Dies sieht etwa wie *AdventureWorks Sample Reports/Company Sales*. In diesem Beispiel wird der Bericht *Company Sales* befindet sich in einem Ordner namens *AdventureWorks Sample Reports*.

4. Wenn der Bericht Parameter erfordert, nachdem Sie die Berichtsserver-URL und den Namen des Berichts angegeben haben, wählen Sie **Parameter laden** innerhalb der **Parameter** Abschnitt.

5. Wählen Sie **Ok** zum Speichern der Änderungen an der Konfiguration des Teils.

6. Wählen Sie **speichern**, innerhalb des Office-Menübands, um die Änderungen auf die SharePoint-Seite zu speichern.

![Berichts-Viewer-Webpart auf einer SharePoint-Seite](media/sharepoint-report-viewer-web-part-on-page.png)

## <a name="considerations-and-limitations"></a>Überlegungen und Einschränkungen

* Der Berichts-Viewer-Webpart kann nicht für moderne Seiten in SharePoint verwendet werden.
* Power BI-Berichten können nicht mit dem Berichts-Viewer-Webpart verwendet werden.
* Wenn das Berichts-Viewer-Webpart hinzufügen zu der Seite nicht angezeigt wird, stellen Sie sicher, dass [des Berichts-Viewer-Webparts bereitgestellt](deploy-report-viewer-web-part.md).

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)

