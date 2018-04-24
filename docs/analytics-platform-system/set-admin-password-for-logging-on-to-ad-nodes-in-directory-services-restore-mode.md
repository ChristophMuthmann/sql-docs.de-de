---
title: Legen Sie Active Directory-Kennwort - Analytics Platform System | Microsoft Docs
description: Festlegen Sie Active Directory-Knoten Admin-Anmeldekennwort, im Modus "Verzeichnisdienste wiederherstellen" in das Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e74689216c1485fc0c11c588acb151269e2b5d2b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>Festlegen Sie Admin-Kennwort, für die Anmeldung bei AD-Knoten im Verzeichnisdienste-Wiederherstellungsmodus (DSRM) - Analyseplattformsystem
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
  
