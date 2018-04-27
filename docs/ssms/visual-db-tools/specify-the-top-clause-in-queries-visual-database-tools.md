---
title: Angeben der TOP-Klausel in Abfragen (Visual Database Tools)|Microsoft-Dokumente
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 239c2c484058977217f12577b55a4af4ce8135de
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>Angeben der TOP-Klausel in Abfragen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Die TOP-Klausel gibt nur die ersten *n* oder *n Prozent* Zeilen aus einer Abfrage zurück. Mithilfe einer TOP-Klausel können Sie ressourcenschonend nur einen Teil der Ergebnisse anstatt alle Abfrageergebnisse prüfen, um zu ermitteln, ob die Abfrage ordnungsgemäß arbeitet.  
  
### <a name="to-specify-the-top-clause-in-queries"></a>So geben Sie die TOP-Klausel in Abfragen an  
  
1.  Öffnen Sie im Projektmappen-Explorer eine Abfrage, oder erstellen Sie eine neue Abfrage.  
  
2.  Klicken Sie im Menü **Ansicht** auf **Eigenschaftenfenster**.  
  
3.  Wechseln Sie in **Eigenschaftenfenster**zur Eigenschaft **Oberste Angabe** , und erweitern Sie diese.  
  
4.  Klicken Sie auf die untergeordnete Eigenschaft **(Oben)** , und legen Sie diese auf **Ja**fest.  
  
5.  Geben Sie in der untergeordneten Eigenschaft **Ausdruck** einen Ausdruck ein, der ein numerisches Ergebnis hat (zum Beispiel „10“ oder „2*5“).  
  
6.  Klicken Sie auf die untergeordnete Eigenschaft **Prozent** , und geben Sie an, ob die Eigenschaft **Ausdruck** als Prozentanteil aller zurückgegebenen Zeilen (Ja) oder als absolute Anzahl von zurückgegebenen Zeilen (Nein) behandelt werden soll.  
  
7.  Wenn bei der Abfrage die ORDER BY-Klausel verwendet wird, klicken Sie auf die untergeordnete Eigenschaft **WITH TIES** . Bei Auswahl von **Ja** werden alle Zeilen in einer Gruppe angezeigt, wenn nur ein Teil der Gruppe enthalten ist. Bei Auswahl von **Nein** werden die Zeilen abgeschnitten.  
  
Bei der Ausführung dieser Schritte werden Sie feststellen, dass die im SQL-Bereich angezeigte TOP-Klausel entsprechend den aktuellen Einstellungen der Eigenschaften geändert wird.  
  
> [!NOTE]  
> Sie können außerdem die Werte der untergeordneten Eigenschaften von **Oberste Angabe** ändern, indem Sie die TOP-Klausel im SQL-Bereich bearbeiten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Abfrageeigenschaften &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-properties-visual-database-tools.md)  
  
