---
title: Festlegen Sie AD Knoten Admin-Anmeldekennwort, im Modus "Verzeichnisdienste wiederherstellen" (APS)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97a9c715-2763-417d-b45c-bb0180759e47
caps.latest.revision: 20
ms.openlocfilehash: 3e09305152a2892ae4acaf7096921d2a73345b63
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm"></a>Legen Sie das Administratorkennwort für das Anmelden beim AD-Knoten im Verzeichnisdienst-Wiederherstellungsmodus (DSRM)
Directory Verzeichnisdienst-Wiederherstellungsmodus (DSRM) ist eine Startmethode zum Reparieren oder Wiederherstellen von Active Directory-Domänendienste (AD DS). Hiermit wird die Appliance AD Knoten anmelden, nachdem AD DS ein Fehler aufgetreten ist oder wenn die AD DS wiederhergestellt werden muss. Das Kennwort für den Verzeichnisdienst-Wiederherstellungsmodus wurde während des Setups Appliance am Standort Hardware-Hersteller initialisiert und sollte vom Administrator Appliance geändert werden. Analyseplattformsystem verfügt über zwei AD DS (Domänencontroller) ***Appliance_domain *-AD01** und ***Appliance_domain *-AD02**. Ändern Sie das DSRM-Kennwort mithilfe der folgenden Schritte für jeden Knoten Appliance AD.  
  
## <a name="HowToDSRM"></a>Das Administratorkennwort zurücksetzen  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster auf einem Gerät AD ***Appliance_domain*– AD*Xx***virtuellen Computer.  
  
2.  Geben Sie an der Eingabeaufforderung `ntdsutil`.  
  
3.  Bei der **Ntdsutil** dazu aufgefordert werden, geben Sie `set dsrm password`.  
  
4.  Bei der **Administratorkennwort zurücksetzen:** dazu aufgefordert werden, geben Sie `reset password on server null`.  
  
5.  Geben Sie an der Eingabeaufforderung das neue Kennwort ein.  
  
6.  Wiederholen Sie die Schritte 1 bis 5 oben für die Appliance AD virtuellen Computer.  
  
    > [!WARNING]  
    > Analyseplattformsystem unterstützt nicht das Dollarzeichen ($) in der Domänenadministrator oder ein lokaler Administratorkennwörter. Ein Kennwort mit einem Dollarzeichen überprüft wird, und werden verwendbaren jedoch Upgrade- und wartungsplanlizenzen Aktivitäten blockieren kann.  
  
> [!NOTE]  
> Wenn die Active Directory-Domänendienste oder des virtuellen Computers für eine bestimmte AD virtuelle Maschine beschädigt wird, ausgeführt **ReplaceVM** für die betroffenen AD virtuelle Computer ist die empfohlene Maßnahme. Wenden Sie sich an CSS um Unterstützung zu erhalten.  
  
## <a name="see-also"></a>Siehe auch  
[Das Zurücksetzen von Kennwörtern &#40;Analyseplattformsystem&#41;](password-reset.md)  
  
