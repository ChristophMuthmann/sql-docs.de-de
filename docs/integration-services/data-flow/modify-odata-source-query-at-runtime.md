---
title: Bereitstellen einer OData-Quellabfrage zur Laufzeit | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 190cbebff69d08424e62ec82b70ea9759d13a96c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="provide-an-odata-source-query-at-runtime"></a>Bereitstellen einer OData-Quellabfrage zur Laufzeit
 Sie können die OData-Quellabfrage zur Laufzeit ändern, indem Sie der Eigenschaft **[OData-Quelle].[Abfrage]** des Datenflusstasks einen *Ausdruck* hinzufügen.  
  
 Die zurückgegebenen Spalten müssen die gleichen Spalten sein, die zur Entwurfszeit zurückgegeben wurden; andernfalls erhalten Sie eine Fehlermeldung, wenn das Paket ausgeführt wird. Geben Sie bei Verwendung der $select-Abfrageoption die gleichen Spalten (in der gleichen Reihenfolge) an. Eine sicherere Alternative zur Verwendung der $select-Option besteht darin, die nicht benötigten Spalten direkt in der Benutzeroberfläche der Quellkomponente zu deaktivieren.  
  
 Es gibt einige verschiedene Möglichkeiten, den Abfragewert zur Laufzeit dynamisch festzulegen. Hier werden einige der gängigeren Methoden beschrieben.  
  
## <a name="provide-the-query-as-a-parameter"></a>Bereitstellen der Abfrage als Parameter  
 Anhand der folgenden Schritte können Sie eine Abfrage, die von der OData-Quellkomponente als Parameter verwendet wird, für das Paket verfügbar machen.  
  
1.  Klicken Sie mit der rechten Maustaste auf **Datenflusstask** , und wählen Sie die Option **Parametrisieren** aus.  
  
2.  Wählen Sie im Dialogfeld **Parametrisieren** für **Eigenschaft** **[\<Name der OData-Quellkomponente>].[ Abfrage]** aus.  
  
3.  Wählen Sie **Neuen Parameter erstellen** oder **Vorhandenen Parameter verwenden**aus.  
  
4.  Wenn Sie **Neuen Parameter erstellen** auswählen:  
  
    1.  Geben Sie den **Name** und eine **Beschreibung** für den Parameter ein.  
  
    2.  Geben Sie den standardmäßigen **Wert** für den Parameter ein.  
  
    3.  Geben Sie den **Bereich** (**Paket** oder **Projekt**) für den Parameter an.  
  
    4.  Geben Sie an, ob der Parameter **erforderlich** ist oder nicht.  
  
5.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
## <a name="provide-the-query-with-an-expression"></a>Bereitstellen der Abfrage mit einem Ausdruck
 Diese Methode ist hilfreich, wenn Sie eine Abfragezeichenfolge zur Laufzeit dynamisch erstellen möchten.
  
1.  Wählen Sie den **Datenflusstask** aus, der die **OData-Quelle** enthält.  
  
2.  Heben Sie im Fenster **Eigenschaften** die Eigenschaft **Ausdrücke** hervor.  
  
3.  Klicken Sie auf die Schaltfläche mit den Auslassungspunkten (...), um den **Eigenschaftsausdrucks-Editor** aufzurufen.  
  
4.  Wählen Sie die Eigenschaft **[OData-Quelle].[Abfrage]** aus.  
  
5.  Klicken Sie auf die auf die Schaltfläche mit den Auslassungspunkten (...) für **Ausdruck**.  
  
6.  Geben Sie den **Ausdruck**ein.  
  
7.  Klicken Sie auf **OK**.  
  
> [!NOTE]  
> Stellen Sie bei Verwendung dieser Methode sicher, dass die festgelegten Werte ordnungsgemäß URL-codiert sind. Bei der Übernahme der Werte aus der Benutzereingabe (z. B. der parameterbasierten Festlegung einzelner Abfrageoptionswerte) müssen Sie sicherstellen, dass die Werte überprüft werden, um potenzielle Angriffe durch die Einschleusung von SQL-Befehlen zu vermeiden.  
  
  
