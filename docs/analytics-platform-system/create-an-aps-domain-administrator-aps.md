---
title: "Erstellen Sie eine APS-Domänenadministrator (APS)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed52bf78-2b0a-4252-98a7-8c2805e22d3d
caps.latest.revision: "7"
ms.openlocfilehash: 5ec32cd93b7fece9e12076fa82eea147bf13b81b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-an-aps-domain-administrator"></a>Erstellen Sie ein Domänenadministrator APS
Einige Vorgänge erfordern Analytics Platform System über Domänenadministratorberechtigungen. Dies wird erläutert, wie zusätzliche Appliance Domänenadministratoren erstellen.  
  
## <a name="create-a-domain-administrator"></a>Erstellen Sie ein Domänenadministrator  
So konfigurieren Sie alle APS-Knoten, der Benutzer mit über ausreichende Berechtigungen verfügen die **APS-Konfigurations-Manager** (`dwconfig.exe`) muss ein Mitglied der **"Domänen-Admins"** Gruppe. Zum Starten und Beenden der APS-Dienste, muss der Benutzer ein Mitglied der **PdwControlNodeAccess** Gruppe.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Zum Hinzufügen eines Benutzers zur Gruppe "Domänen-Admins"  
  
1.  Melden Sie sich den aktiven Knoten des AD  **(*Appliance_domain*-AD01 ** oder  ***Appliance_domain*-AD02**) mit einer vorhandenen Domäne in der Anwendung Administratorkonto an.  
  
2.  Klicken Sie im Startmenü auf **Ausführen**. In der **öffnen** geben **dsa.msc**. Klicken Sie auf **OK**.  
  
3.  In der **Active Directory-Benutzer und-Computer** Programmieren der rechten Maustaste auf **Benutzer**, zeigen Sie auf **neu**, und klicken Sie dann auf **Benutzer**.  
  
4.  In der **neues Objekt – Benutzer** (Dialogfeld), die Beschreibung des neuen Benutzers abzuschließen, und klicken Sie dann auf **Weiter**.  
  
    Führen Sie das Kennwort (Dialogfeld), und klicken Sie dann auf **Weiter**.  
  
    > [!WARNING]  
    > Das Dollarzeichen ($) in der Domänenadministrator oder ein lokaler Administratorkennwörter werden von SQL Server PDW nicht unterstützt. Ein Kennwort mit einem Dollarzeichen wird ungültig und verwendet werden können blockiert jedoch Upgrade- und wartungsplanlizenzen Aktivitäten  
  
    Bestätigen Sie die neue benutzerbeschreibung aus, und klicken Sie dann auf **Fertig stellen**.  
  
5.  Doppelklicken Sie in der Liste der Benutzer auf den neuen Benutzer aus, um das Dialogfeld Eigenschaften für Benutzer zu öffnen.  
  
6.  Auf der **Mitglied von** auf **hinzufügen**.  
  
    Typ **Domänen-Admins; PdwControlNodeAccess** , und klicken Sie dann auf **Namen überprüfen**. Klicken Sie auf **OK**.  
  
    Dadurch wird den neuen Benutzer auf die **"Domänen-Admins"** Gruppe und die **PdwControlNodeAccess** Gruppe. Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
[Starten Sie den Konfigurations-Manager &#40; Analyseplattformsystem &#41;](launch-the-configuration-manager.md)  
  
