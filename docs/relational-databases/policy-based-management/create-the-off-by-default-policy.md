---
title: "Erstellen der Richtlinie &#39;Standardm&#228;&#223;ig aus&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 98fde3c5-297c-4d95-981e-95700bbf5ccd
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Erstellen der Richtlinie &#39;Standardm&#228;&#223;ig aus&#39;
In dieser Aufgabe erstellen Sie eine Bedingung mit dem Namen Mail aus, die auf dem Oberflächenkonfigurationsfacet basiert. Anschließend erstellen Sie eine Richtlinie mit dem Namen Standardmäßig aus.  
  
### So erstellen Sie die Bedingung 'Mail aus'  
  
1.  Erweitern Sie im Objekt-Explorer **Verwaltung**, erweitern Sie **Richtlinienverwaltung**, erweitern Sie **Facets**, klicken Sie mit der rechten Maustaste auf **Oberflächenkonfiguration** und anschließend auf **Neue Bedingung**.  
  
2.  Geben Sie im Dialogfeld **Neue Bedingung erstellen** im Feld **Name** den Namen **Mail aus**ein.  
  
3.  Bestätigen Sie im Feld **Facet** , dass das Facet **Oberflächenkonfiguration** ausgewählt ist.  
  
4.  Geben Sie im Dialogfeld **Ausdruck** im Feld **Feld** den Ausdruck **@DatabaseMailEnabled**aus, wählen Sie im Feld **Operator** die Option **=**aus, und wählen Sie im Feld **Wert** die Option **False**.  
  
5.  Geben Sie auf der Seite **Beschreibung** eine Beschreibung der Bedingung ein, und klicken Sie dann auf **OK** , um die Bedingung zu erstellen.  
  
### So erstellen Sie die Richtlinie 'Standardmäßig aus'  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **Oberflächenkonfiguration** und anschließend auf **Neue Richtlinie**.  
  
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
  
## Nächste Aufgabe in der Lektion  
[Konfigurieren eines Servers für das Ausführen der Richtlinie 'Standardmäßig aus'](../../relational-databases/policy-based-management/configure-a-server-to-run-the-off-by-default-policy.md)  
  
  
  
