---
title: "Erstellen der Richtlinie „Standardmäßig aus“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad1ef04caea4fc15cc53fced05ab5861d54ad7eb
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-1---create-the-off-by-default-policy"></a>Lektion 1-1 – Erstellen der Richtlinie „Standardmäßig aus“
In dieser Aufgabe erstellen Sie eine Bedingung mit dem Namen Mail aus, die auf dem Oberflächenkonfigurationsfacet basiert. Anschließend erstellen Sie eine Richtlinie mit dem Namen Standardmäßig aus.  
  
### <a name="to-create-the-mail-off-condition"></a>So erstellen Sie die Bedingung 'Mail aus'  
  
1.  Erweitern Sie im Objekt-Explorer **Verwaltung**, erweitern Sie **Richtlinienverwaltung**, erweitern Sie **Facets**, klicken Sie mit der rechten Maustaste auf **Oberflächenkonfiguration**und anschließend auf **Neue Bedingung**.  
  
2.  Geben Sie im Dialogfeld **Neue Bedingung erstellen** im Feld **Name** den Namen **Mail aus**ein.  
  
3.  Bestätigen Sie im Feld **Facet** , dass das Facet **Oberflächenkonfiguration** ausgewählt ist.  
  
4.  Geben Sie im Dialogfeld **Ausdruck** im Feld **Feld** den Ausdruck **@DatabaseMailEnabled**aus, wählen Sie im Feld **Operator** die Option **=**aus, und wählen Sie im Feld **Wert** die Option **False**.  
  
5.  Geben Sie auf der Seite **Beschreibung** eine Beschreibung der Bedingung ein, und klicken Sie dann auf **OK** , um die Bedingung zu erstellen.  
  
### <a name="to-create-the-off-by-default-policy"></a>So erstellen Sie die Richtlinie 'Standardmäßig aus'  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **Oberflächenkonfiguration**und anschließend auf **Neue Richtlinie**.  
  
2.  Geben Sie im Dialogfeld **Neue Richtlinie erstellen** im Feld **Name** den Namen **Standardmäßig aus**ein.  
  
3.  Lassen Sie das Kontrollkästchen **Aktiviert** deaktiviert. Das Kontrollkästchen **Aktiviert** gilt für automatisierte Richtlinien, und diese Richtlinie wird bei Bedarf ausgeführt.  
  
4.  Führen Sie im Kontrollkästchen **Bedingung überprüfen** einen Bildlauf nach unten zum Bereich **Oberflächenkonfiguration** durch, und wählen Sie dann **Mail aus** als die zu überprüfende Bedingung aus.  
  
5.  Das Feld **Für Ziele** ist leer, da dies eine serverbezogene Richtlinie ist.  
  
6.  Wählen Sie im Feld **Auswertungsmodus** den Modus **Bedarfsgesteuert** aus.  
  
7.  Wählen Sie im Feld **Serverbeschränkung** die Option **Keine**aus.  
  
8.  Geben Sie auf der Seite **Beschreibung** eine Beschreibung der Richtlinie ein.  
  
9. Sie können im Bereich **Zusätzlicher Hilfelink** einen Link zu einer Webseite für Ihre Richtlinien bereitstellen. Geben Sie im Feld **Anzuzeigender Text** den Text ein, der für den Link angezeigt wird.  
  
10. Geben Sie in das Feld **Adresse** einen Link zu einer Hilfeseite ein, z. B. die Startseite der IT-Abteilung Ihres Unternehmens.  
  
11. Um diese Webseite zur Bestätigung der Adresse zu öffnen, klicken Sie auf **Link testen**.  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Konfigurieren eines Servers für das Ausführen der Richtlinie 'Standardmäßig aus'](../../relational-databases/policy-based-management/lesson-1-2-configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
  

