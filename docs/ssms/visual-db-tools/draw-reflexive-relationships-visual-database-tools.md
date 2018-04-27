---
title: Zeichnen reflexiver Beziehungen (Visual Database Tools) | Microsoft-Dokumentation
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
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c83c60ed963ea2317d958cc041fc97fd048e712e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>Zeichnen reflexiver Beziehungen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Sie erstellen eine reflexive Beziehung, um eine Spalte oder mehrere Spalten in einer Tabelle mit einer anderen Spalte oder mehreren Spalten in derselben Tabelle zu verknüpfen. Angenommen, in der Tabelle `employee` gibt es die Spalte `emp_id` und die Spalte `mgr_id` . Da jeder Manager gleichzeitig ein Mitarbeiter ist, verknüpfen Sie diese beiden Spalten, indem Sie eine Beziehungslinie innerhalb der Tabelle ziehen. Durch diese Beziehung wird sichergestellt, dass jede der Tabelle hinzugefügte Manager-ID mit einer vorhandenen Mitarbeiter-ID übereinstimmt.  
  
Bevor Sie eine Beziehung erstellen, müssen Sie zunächst einen Primärschlüssel oder eine UNIQUE-Einschränkung für die Tabelle definieren. Anschließend verknüpfen Sie die Primärschlüsselspalte mit einer übereinstimmenden Spalte. Wenn die Beziehung erstellt ist, wird die übereinstimmende Spalte der Fremdschlüssel für die Tabelle.  
  
### <a name="to-draw-a-reflexive-relationship"></a>So erstellen Sie eine reflexive Beziehung  
  
1.  Klicken Sie im Datenbankdiagramm auf den Zeilenselektor für die Datenbankspalte, die Sie zu einer anderen Spalte in Beziehung setzen möchten, und ziehen Sie den Mauszeiger aus der Tabelle heraus, bis eine Linie angezeigt wird.  
  
2.  Ziehen Sie die Linie zurück in die ausgewählte Tabelle.  
  
3.  Lassen Sie die Maustaste los. Das Dialogfeld **Tabellen und Spalten** wird angezeigt.  
  
4.  Wählen Sie die Fremdschlüsselspalte und die Primärschlüsseltabelle sowie -spalte aus, zu denen eine Beziehung hergestellt werden soll.  
  
5.  Klicken Sie zweimal auf **OK** , um die Beziehung zu erstellen.  
  
Wenn Sie Abfragen in einer Tabelle ausführen, können Sie mithilfe einer reflexiven Beziehung einen Selbstjoin erstellen. Informationen über das Abfragen von Tabellen mit Joins finden Sie unter [Erstellen von Abfragen mit Joins &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen von Abfragen mit Joins &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
