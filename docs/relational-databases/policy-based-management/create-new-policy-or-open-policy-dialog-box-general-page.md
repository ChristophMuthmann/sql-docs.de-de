---
title: "Dialogfeld 'Neue Richtlinie erstellen' oder 'Richtlinie öffnen', Seite 'Allgemein'|Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.policy.f1
- sql13.swb.dmf.policy.filter.f1
- sql13.swb.dmf.newgroup.f1
ms.assetid: c00bebd0-d04b-4c64-840e-8b7a2c603436
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c03db3581e9a01f23eb81c7d4c2a706785abcbb7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-new-policy-or-open-policy-dialog-box-general-page"></a>Dialogfeld 'Neue Richtlinie erstellen' oder 'Richtlinie öffnen', Seite 'Allgemein'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe dieses Dialogfelds können Sie eine neue Richtlinie für die richtlinienbasierte Verwaltung erstellen oder eine vorhandene Richtlinie ändern. Verwenden Sie die Bereiche **Für Ziele** und **Serverbeschränkung** als Filter, um Richtlinien auf eine Teilmenge aller möglichen Ziele zu beschränken. Damit Bedingungen als Zielfilter verwendet werden können, müssen sie auf einem physischen Facet definiert werden und dürfen weder Funktionen noch den LIKE-Operator enthalten. Wenn das System den Objektsatz für eine Richtlinie berechnet, werden die Systemobjekte standardmäßig ausgeschlossen.  Falls der Objektsatz der Richtlinie z. B. auf alle Tabellen verweist, gilt die Richtlinie nicht für Systemtabellen. Wenn Benutzer eine Richtlinie in Verbindung mit Systemobjekten auswerten möchten, können sie dem Objektsatz Systemobjekte explizit hinzufügen. Obwohl alle Richtlinien für den Auswertungsmodus **Zeitplan prüfen** unterstützt werden, werden aus Leistungsgründen jedoch nicht alle Richtlinien mit beliebigen Objektsätzen für den Auswertungsmodus **Änderungen prüfen** unterstützt. Weitere Informationen finden Sie unter [http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="options"></a>Optionen  
 **Name**  
 Geben Sie für eine neue Richtlinie den Namen der neuen Richtlinie ein. Für eine vorhandene Richtlinie wird der Name angezeigt.  
  
 **Aktiviert**  
 Aktivieren Sie das Kontrollkästchen **Aktiviert** , um die Richtlinie zu aktivieren. Deaktivieren Sie das Kontrollkästchen **Aktiviert** , um die Richtlinie zu deaktivieren. Das Feld **Aktiviert** gilt für die Richtlinienautomatisierung. Es erstellt oder entfernt das Automatisierungssystem für die Richtlinie. Die Automatisierung verwendet die folgenden Mechanismen:  
  
 **Bei Änderung - Verhindern**  
 Ein Datenbanktrigger erzwingt die Kompatibilität.  
  
 **Bei Änderung - Nur protokollieren**  
 Ein Notification Services-Ereignis überprüft die Kompatibilität.  
  
 **Nach Zeitplan**  
 Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftrag wird erstellt, um die Kompatibilität nach einem Zeitplan zu prüfen.  
  
 Richtlinien, die unter Verwendung des Auswertungsmodus **Bedarfsgesteuert** ausgeführt werden, verwenden dieses Kontrollkästchen nicht.  
  
 **Bedingung überprüfen**  
 Wählen Sie die richtlinienbasierte Verwaltungsbedingung aus, die diese Richtlinie verwendet. Alle Bedingungen auf dem Server für das zugeordnete Facet der richtlinienbasierten Verwaltung werden aufgelistet. Klicken Sie auf **Neue Bedingung** , um eine neue Bedingung zu erstellen. Klicken Sie auf die Schaltfläche mit den Auslassungspunkten (**…**), um die Bedingung zu ändern.  
  
 **Für Ziele**  
 Wählen Sie die Zieltypen aus, die für dieses Facet verfügbar sind, um einen Filterausdruck abzuschließen.  
  
 **Auswertungsmodus**  
 Wählen Sie den Auswertungsmodus für die Richtlinie aus. Einige Richtlinien können überprüft werden, aber nicht erzwungen werden. Folgende Auswertungsmodi sind verfügbar:  
  
 **Bedarfsgesteuert**  
 Die Richtlinie wird nur ausgeführt, wenn Sie sie über das Dialogfeld **Auswerten** ausführen.  
  
 **Nach Zeitplan**  
 Wertet die Richtlinie in regelmäßigen Abständen aus, zeichnet einen Protokolleintrag für Richtlinien auf, die Nicht-Einhaltungen aufweisen, und erstellt einen Bericht. Aktiviert das Feld **Zeitplan** .  
  
 **Bei Änderung - Nur protokollieren**  
 Wenn versucht wird, Änderungen vorzunehmen, verhindert diese Option war keine nicht kompatiblen Änderungen, protokolliert jedoch Richtlinienverstöße.  
  
 **Bei Änderung - Verhindern**  
 Wenn versucht wird, Änderungen vorzunehmen, verhindert diese Option Änderungen, die gegen die Richtlinie verstoßen würden.  
  
 **Zeitplan**  
 Diese Option wird angezeigt, wenn der Auswertungsmodus **Nach Zeitplan** ausgewählt ist. Geben Sie den Namen des Zeitplans ein, klicken Sie auf **Auswählen** , um einen Zeitplan aus der Liste auszuwählen, oder klicken Sie auf **Neu** , um einen neuen Zeitplan zu erstellen. Um den Zeitplanbereich zu aktivieren, muss **Nach Zeitplan** ausgewählt werden.  
  
 **Serverbeschränkung**  
 Wählen Sie die Typen von Servern aus, die für diese Richtlinie geeignet sind. Optionen sind **Keine** , oder wählen Sie eine Bedingung aus, die die möglichen Server filtert.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
