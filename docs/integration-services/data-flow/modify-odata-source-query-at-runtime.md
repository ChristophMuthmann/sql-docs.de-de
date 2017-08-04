---
title: "Ändern Sie die OData-Quellabfrage zur Laufzeit | Microsoft Docs"
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
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e061fe6989d9629d655d9e0c08f2cd4c1d932540
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="modify-odata-source-query-at-runtime"></a>Ändern einer OData-Quellabfrage zur Laufzeit
  Sie können die OData-Quellabfrage zur Laufzeit ändern, indem Sie der Eigenschaft **[OData-Quelle].[Abfrage]** des Datenflusstasks einen Ausdruck hinzufügen.  
  
 Beachten Sie, dass die Spalten gegenüber der Entwurfszeit unverändert bleiben müssen, da bei der Paketausführung ansonsten ein Fehler auftritt. Geben Sie bei Verwendung der $select-Abfrageoption die gleichen Spalten (in der gleichen Reihenfolge) an. Eine sicherere Alternative zur Verwendung der $select-Option besteht darin, die nicht benötigten Spalten direkt in der Benutzeroberfläche der Quellkomponente zu deaktivieren.  
  
 Es gibt einige verschiedene Möglichkeiten, den Abfragewert zur Laufzeit dynamisch festzulegen. Im Folgenden sind einige der gängigeren Methoden beschrieben.  
  
## <a name="exposing-the-query-as-a-parameter"></a>Verfügbarmachen der Abfrage als Parameter  
 Anhand der folgenden Schritte können Sie eine Abfrage, die von der OData-Quellkomponente als Parameter verwendet wird, für das Paket verfügbar machen.  
  
1.  Klicken Sie mit der rechten Maustaste auf **Datenflusstask** , und wählen Sie die Option **Parametrisieren** aus.  
  
2.  In der **parametrisieren** wählen Sie im Dialogfeld **[\<Name der OData-Quellkomponente >]. [ Abfrage]** für **Eigenschaft**.  
  
3.  Wählen Sie **Neuen Parameter erstellen** oder **Vorhandenen Parameter verwenden**aus.  
  
4.  Wenn Sie **Neuen Parameter erstellen**auswählen, gehen Sie wie folgt vor:  
  
    1.  Geben Sie den **Name** und eine **Beschreibung** für den Parameter ein.  
  
    2.  Geben Sie den standardmäßigen **Wert** für den Parameter ein.  
  
    3.  Geben Sie den **Bereich** (**Paket** oder **Projekt**) für den Parameter an.  
  
    4.  Geben Sie an, ob der Parameter **erforderlich** ist oder nicht.  
  
5.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
## <a name="using-an-expression"></a>Verwenden eines Ausdrucks  
 Diese Methode ist hilfreich, wenn Sie eine Abfragezeichenfolge zur Laufzeit dynamisch erstellen möchten. In diesem Beispiel wird die MaxRows-Variable auf andere Weise (Skript, Parameter usw.) festgelegt.  
  
1.  Wählen Sie den **Datenflusstask** aus, der die **OData-Quelle**enthält.  
  
2.  Heben Sie im Fenster **Eigenschaften** die Eigenschaft **Ausdrücke** hervor.  
  
3.  Klicken Sie auf die Schaltfläche mit den Auslassungspunkten (...), um den **Eigenschaftsausdrucks-Editor**aufzurufen.  
  
4.  Wählen Sie die Eigenschaft **[OData-Quelle].[Abfrage]** aus.  
  
5.  Klicken Sie auf die **Ausdruck**auf die Schaltfläche mit den Auslassungspunkten (...).  
  
6.  Geben Sie den **Ausdruck**ein.  
  
7.  Klicken Sie auf **OK**.  
  
> [!WARNING]  
>  Beachten Sie bei Verwendung dieser Methode, dass die festgelegten Werte ordnungsgemäß URL-codiert sind. Bei der Übernahme der Werte aus der Benutzereingabe (z. B. der parameterbasierten Festlegung einzelner Abfrageoptionswerte) müssen Sie sicherstellen, dass die Werte überprüft werden, um potenzielle Angriffe durch die Einschleusung von SQL-Befehlen zu vermeiden.  
  
  
