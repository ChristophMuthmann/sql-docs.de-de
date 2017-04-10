---
title: "Abonnieren und &#220;berpr&#252;fen der Richtlinie &#39;Finanz_Name&#39; | Microsoft Docs"
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
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Abonnieren und &#220;berpr&#252;fen der Richtlinie &#39;Finanz_Name&#39;
In dieser Aufgabe konfigurieren Sie die Datenbank Finanzen, um die Richtlinienkategorie Finanzen zu abonnieren. Anschließend testen Sie die Richtlinie Finanz_Name.  
  
### So abonnieren Sie die Richtlinienkategorie 'Finanzen'  
  
1.  Erweitern Sie im Objekt-Explorer **Datenbanken**, klicken Sie mit der rechten Maustaste auf **Finanzen**, zeigen Sie auf **Richtlinien**, und klicken Sie anschließend auf **Kategorien**.  
  
2.  Aktivieren Sie das Kontrollkästchen **Abonniert** für die Kategorie **Finanzen**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### So testen Sie die Durchsetzung der Richtlinie 'Finanz_Name'  
  
1.  Öffnen Sie ein Abfragefenster in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Führen Sie die folgenden Anweisungen aus, mit denen versucht wird, eine Tabelle zu erstellen, die gegen die Richtlinie **Finanz_Name** verstößt. Die Tabelle verstößt gegen die Richtlinie, da der Tabellenname nicht mit den Buchstaben **fintbl** beginnt.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
    Beachten Sie, dass die Richtlinie das Erstellen der Tabelle verhindert und eine Informationsmeldung zurückgibt, die den Richtliniennamen liefert.  
  
2.  Um einen gültigen Namen anzugeben, ändern Sie den Code wie folgt, und führen Sie dann erneut die Anweisung aus.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
    Nun wird die Tabelle erstellt.  
  
### So übernehmen Sie die Richtlinie für den ganzen Server  
  
1.  Momentan hat nur die Datenbank Finanzen die Richtlinienkategorie Finanzen abonniert. In vielen Fällen ist es einfacher, die Richtlinienkategorie für den ganzen Server zu übernehmen. Erweitern Sie im Objekt-Explorer **Verwaltung**, klicken Sie mit der rechten Maustaste auf **Richtlinienverwaltung** und anschließend auf **Kategorien verwalten**.  
  
2.  Suchen Sie im Dialogfeld **Richtlinienkategorien verwalten** nach der Kategorie „Finanzen“, und aktivieren Sie das Kontrollkästchen **Datenbankabonnements beauftragen** für die Kategorie „Finanzen“.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Nun gilt die Kategorie „Finanzen“ für alle Datenbanken, aber durch die von Ihnen erstellte Bedingung ist die Richtlinie „Finanz_Name“ nur auf die Datenbank „Finanzen“ beschränkt. Dieses Beispiel zeigt, wie Sie komplexe Kombinationen von Bedingungen verwenden können, um Richtlinien so zuzuweisen, dass sie für viele Server richtig übernommen werden.  
  
## Zusammenfassung  
Dieses Lernprogramm hat gezeigt, wie Sie Bedingungen, Richtlinien und Richtliniengruppen der richtlinienbasierten Verwaltung erstellen und die Kompatibilität der Ziele der richtlinienbasierten Verwaltung überprüfen können.  
  
## Weiter  
Dieses Lernprogramm ist beendet. Um zum Anfang des Tutorials zurückzukehren, klicken Sie auf [Tutorial: Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Eine Liste der Tutorials finden Sie unter [Tutorials für SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## Siehe auch  
[Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
  
