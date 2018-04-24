---
title: Erstellen ein Domänenadministratorkontos - Analytics Platform System | Microsoft Docs
description: Einige Vorgänge erfordern Analytics Platform System über Domänenadministratorberechtigungen. Dies wird erläutert, wie zusätzliche Appliance Domänenadministratoren erstellen.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 73eff52cb6e583383f13334e78012721a20a3e25
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="create-an-aps-domain-administrator"></a>Erstellen Sie ein Domänenadministrator APS
Einige Vorgänge erfordern Analytics Platform System über Domänenadministratorberechtigungen. Dies wird erläutert, wie zusätzliche Appliance Domänenadministratoren erstellen.  
  
## <a name="create-a-domain-administrator"></a>Erstellen Sie ein Domänenadministrator  
So konfigurieren Sie alle APS-Knoten, der Benutzer mit über ausreichende Berechtigungen verfügen die **APS-Konfigurations-Manager** (`dwconfig.exe`) muss ein Mitglied der **"Domänen-Admins"** Gruppe. Zum Starten und Beenden der APS-Dienste, muss der Benutzer ein Mitglied der **PdwControlNodeAccess** Gruppe.  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>Zum Hinzufügen eines Benutzers zur Gruppe "Domänen-Admins"  
  
1.  Melden Sie sich den aktiven Knoten des AD **(*Appliance_domain*-AD01** oder ***Appliance_domain*-AD02**) mit einer vorhandenen Appliance-Domänenadministratorkonto.  
  
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
[Starten Sie den Konfigurations-Manager &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md)  
  
