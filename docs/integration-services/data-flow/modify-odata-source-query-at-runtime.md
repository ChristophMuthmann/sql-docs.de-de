---
title: Geben Sie einen OData-Quellabfrage zur Laufzeit | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 9da1f1be0a790d01f9403d6fc05a5c1498c0ee8b
ms.contentlocale: de-de
ms.lasthandoff: 08/23/2017

---
# <a name="provide-an-odata-source-query-at-runtime"></a>Geben Sie einen OData-Quellabfrage zur Laufzeit
 Sie können die OData-Quellabfrage zur Laufzeit ändern, indem Hinzufügen einer *Ausdruck* auf die **[OData-Quelle]. [ Abfrage]** Eigenschaft des Datenflusstasks.  
  
 Die zurückgegebenen Spalten müssen die gleichen Spalten, die zur Entwurfszeit zurückgegeben wurden, werden; Andernfalls erhalten Sie einen Fehler auf, wenn das Paket ausgeführt wird. Geben Sie bei Verwendung der $select-Abfrageoption die gleichen Spalten (in der gleichen Reihenfolge) an. Eine sicherere Alternative zur Verwendung der $select-Option besteht darin, die nicht benötigten Spalten direkt in der Benutzeroberfläche der Quellkomponente zu deaktivieren.  
  
 Es gibt einige verschiedene Möglichkeiten, den Abfragewert zur Laufzeit dynamisch festzulegen. Hier sind einige der gängigeren Methoden.  
  
## <a name="provide-the-query-as-a-parameter"></a>Geben Sie die Abfrage als parameter  
 Das folgende Verfahren zeigt, wie ein OData-Quellkomponente als Parameter des Pakets verwendete Abfrage verfügbar zu machen.  
  
1.  Klicken Sie mit der rechten Maustaste auf **Datenflusstask** , und wählen Sie die Option **Parametrisieren** aus.  
  
2.  In der **parametrisieren** wählen Sie im Dialogfeld **[\<Name der OData-Quellkomponente >]. [ Abfrage]** für **Eigenschaft**.  
  
3.  Wählen Sie **Neuen Parameter erstellen** oder **Vorhandenen Parameter verwenden**aus.  
  
4.  Bei Auswahl des **neuen Parameter erstellen**:  
  
    1.  Geben Sie den **Name** und eine **Beschreibung** für den Parameter ein.  
  
    2.  Geben Sie den standardmäßigen **Wert** für den Parameter ein.  
  
    3.  Geben Sie den **Bereich** (**Paket** oder **Projekt**) für den Parameter an.  
  
    4.  Geben Sie an, ob der Parameter **erforderlich** ist oder nicht.  
  
5.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
## <a name="provide-the-query-with-an-expression"></a>Geben Sie die Abfrage mit einem Ausdruck
 Diese Methode ist nützlich, wenn die Abfragezeichenfolge zur Laufzeit dynamisch erstellt werden sollen.
  
1.  Wählen Sie die **Data Flow Task** , enthält Ihre **OData-Quelle**.  
  
2.  Heben Sie im Fenster **Eigenschaften** die Eigenschaft **Ausdrücke** hervor.  
  
3.  Klicken Sie auf die (Schaltfläche) um die **Eigenschaftsausdrucks-Editor**.  
  
4.  Wählen Sie die Eigenschaft **[OData-Quelle].[Abfrage]** aus.  
  
5.  Klicken Sie auf die (Schaltfläche) für **Ausdruck**.  
  
6.  Geben Sie den **Ausdruck**ein.  
  
7.  Klicken Sie auf **OK**.  
  
> [!NOTE]  
> Wenn Sie diesen Ansatz verwenden, müssen Sie sicherstellen, dass die festgelegten Werte ordnungsgemäß URL-codiert werden. Bei der Übernahme der Werte aus der Benutzereingabe (z. B. der parameterbasierten Festlegung einzelner Abfrageoptionswerte) müssen Sie sicherstellen, dass die Werte überprüft werden, um potenzielle Angriffe durch die Einschleusung von SQL-Befehlen zu vermeiden.  
  
  
