---
title: "Erstellen der Richtlinie „Finance Name“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 260f0934e69d1db1ffd8f2af4cb71b0b96f64c84
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-2-1---create-the-finance-name-policy"></a>Lektion 2.1: Erstellen der Richtlinie „Finance Name“
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In diesem Task erstellen Sie eine Datenbank mit dem Namen Finanzen. Anschließend erstellen Sie eine Bedingung, die vorschreibt, dass alle Tabellen mit den Buchstaben **fintbl**anfangen. Dann erstellen Sie eine Richtlinie und eine Richtlinienkategorie, um einen Namensstandard für Tabellen in der Datenbank Finanzen zu erzwingen.  
  
### <a name="to-create-the-finance-database"></a>So erstellen Sie die Datenbank "Finance"  
  
1.  Öffnen Sie ein Abfragefenster in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], und führen Sie die folgende Anweisung aus:  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  Klicken Sie im Objekt-Explorer auf **Datenbanken**, und drücken Sie anschließend F5, um die Liste der Datenbanken zu aktualisieren.  
  
### <a name="to-create-the-finance-tables-condition"></a>So erstellen Sie die Bedingung 'Finanz_Tabellen'  
  
1.  Erweitern Sie im Objekt-Explorer **Verwaltung**, erweitern Sie **Richtlinienverwaltung**, klicken Sie mit der rechten Maustaste auf **Bedingungen**und anschließend auf **Neue Bedingung**.  
  
2.  Geben Sie im Dialogfeld **Neue Bedingung erstellen** im Feld **Name** den Namen **Finanz_Tabellen**ein.  
  
3.  Wählen Sie in der Liste **Facet** die Option **Mehrteiliger Name**aus.  
  
4.  Geben Sie im Dialogfeld **Ausdruck** im Feld **Feld** die Option **@Name**aus, wählen Sie im Feld **Operator** die Option **Like**aus, und geben Sie in das Feld **Wert** den Namen **'fintbl%'** ein, um zu erzwingen, dass alle Namen mit den Buchstaben **fintbl**anfangen.  
  
5.  Geben Sie auf der Seite **Beschreibung** die Beschreibung **Finanz_Tabellen-Namen müssen mit fintbl beginnen**ein, und klicken Sie anschließend auf **OK** , um die Bedingung zu erstellen.  
  
### <a name="to-create-the-finance-name-policy"></a>So erstellen Sie die Richtlinie 'Finanz_Name'  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **Richtlinien**und anschließend auf **Neue Richtlinie**.  
  
2.  Geben Sie im Dialogfeld **Neue Richtlinie erstellen** im Feld **Name** den Namen **Finanz_Name**ein.  
  
3.  Wählen Sie in der Liste **Bedingung überprüfen** die Option **Finanz_Tabellen**aus. Diese befindet sich im Abschnitt **Mehrteiliger Name** .  
  
4.  Im Abschnitt **Für** wird eine Liste der Datenbankobjekte angezeigt, die diese Richtlinie anwenden könnten. Aktivieren Sie das Kontrollkästchen für **Jede Tabelle**.  
  
5.  Erweitern Sie im Abschnitt **Jede Datenbank** den Eintrag **Jede**, und klicken Sie anschließend auf **Neue Bedingung**.  
  
6.  Geben Sie im Dialogfeld **Neue Bedingung erstellen** im Feld **Name** den Namen **Finanz_Datenbank**ein.  
  
7.  Vervollständigen Sie im Feld **Ausdruck** den Ausdruck so, dass er **@Name = 'Finance'** umfasst, und klicken Sie anschließend auf **OK**, um die Bedingungsseite zu schließen.  
  
    > [!NOTE]  
    > Sie müssen möglicherweise mit dem Cursor aus dem Feld **Wert** wechseln, um die Schaltfläche **OK** zu aktivieren.  
  
8.  Wählen Sie in der Liste **Auswertungsmodus** die Option **Bei Änderung: Verhindern**aus. Dadurch wird die Richtlinie erzwungen, indem ein Datenbanktrigger für die Datenbank Finanzen erstellt wird.  
  
9. Wählen Sie in der Liste **Aktiviert** aus. (Das Feld **Aktiviert** gilt nicht für **bedarfsgesteuerte** Richtlinien.)  
  
10. Wählen Sie in der Liste **Serverbeschränkung** die Option **Keine**aus.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>So erstellen Sie die Richtlinienkategorie 'Finanzen'  
  
1.  Erweitern Sie im Objekt-Explorer **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Richtlinienverwaltung**und anschließend auf **Kategorien verwalten**.  
  
2.  Geben Sie im Dialogfeld **Richtlinienkategorien verwalten** unter **Name**die Zeichenfolge **Finanzen** in das leere Feld ein, und deaktivieren Sie **Datenbankabonnements beauftragen**. **Datenbankabonnements beauftragen** zwingt jede Datenbank in der Instanz, die zu dieser Richtlinienkategorie gehörenden Richtlinien zu abonnieren. Für diese Lektion darf nur die Datenbank Finanzen die Richtlinie Finanz_Name abonnieren.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Abonnieren und Überprüfen der Richtlinie 'Finanz_Name'](../../relational-databases/policy-based-management/lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
  
