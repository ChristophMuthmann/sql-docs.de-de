---
title: Datamining-Abfrage | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31f807cb94296fecef77ae5964218a6c30a25dfe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="data-mining-query"></a>Data Mining-Abfrage
  Im Entwurfsbereich befindet sich der Data Mining-Generator für Vorhersageabfragen, mit dem Sie Data Mining-Vorhersageabfragen erstellen können. Vorhersageabfragen können entweder auf der Grundlage von Eingabetabellen oder von SINGLETON-Vorhersageabfragen erstellt werden. Wechseln Sie zur Ergebnissicht, um die Abfrage auszuführen und die Ergebnisse anzuzeigen. Die Abfragesicht zeigt die vom Generator für Vorhersageabfragen erstellte DMX-Abfrage (Data Mining Extensions).  
  
## <a name="options"></a>Tastatur  
 Schaltfläche Ansicht wechseln  
 Klicken Sie auf ein Symbol, um zwischen dem Entwurfs- und Abfragebereich zu wechseln. Standardmäßig ist der Entwurfsbereich geöffnet.  
  
 Klicken Sie auf das ![Design-Symbol](../../integration-services/control-flow/media/ssis-designicon.gif "Design-Symbol"), um in den Entwurfsbereich zu wechseln.  
  
 Klicken Sie auf das ![SQL-Symbol](../../integration-services/control-flow/media/ssis-queryicon.gif "SQL-Symbol"), um in den Abfragebereich zu wechseln.  
  
 **Miningmodell**  
 Zeigt das Miningmodell an, auf dem Sie die Vorhersagen aufbauen wollen.  
  
 **Modell auswählen**  
 Öffnet das Dialogfeld **Miningmodell auswählen** .  
  
 **Eingabespalten**  
 Zeigt die zum Generieren der Vorhersagen ausgewählten Eingabespalten an.  
  
 **Quelle**  
 Wählen Sie in der Dropdownliste die Quelle aus, die das Feld enthält, das Sie für die Spalte verwenden wollen. Sie können entweder das in der **Miningmodell** -Tabelle ausgewählte Miningmodell, die in der **Eingabetabelle(n) auswählen** -Tabelle ausgewählten Eingabetabellen, eine Vorhersagefunktion oder einen benutzerdefinierten Ausdruck verwenden.  
  
 Spalten können aus den das Miningmodell enthaltenden Tabellen und den Eingabespalten auf die Zelle gezogen werden.  
  
 **Feld**  
 Wählen Sie eine Spalte aus der Liste der aus der Quelltabelle abgeleiteten Spalten aus. Wenn Sie unter **Quelle** die **Vorhersagefunktion**ausgewählt haben, enthält diese Zelle eine Dropdownliste der für das ausgewählte Miningmodell verfügbaren Vorhersagefunktionen.  
  
 **Alias**  
 Der Name der vom Server zurückgegebenen Spalte.  
  
 **Anzeigen**  
 Wählen Sie aus, ob die Spalte zurückgegeben oder nur in der WHERE-Klausel verwendet werden soll.  
  
 **Gruppieren**  
 Wird mit der **Und/Oder** -Spalte verwendet, um Ausdrücke zu gruppieren. Beispielsweise (expr1 OR expr2) AND expr3.  
  
 **Und/Oder**  
 Wird zum Erstellen einer logischen Abfrage verwendet. Beispielsweise (expr1 OR expr2) AND expr3.  
  
 **Kriterium/Argument**  
 Geben Sie eine Bedingung oder einen benutzerdefinierten Ausdruck an, der auf die Spalte angewendet wird. Spalten können aus den das Miningmodell enthaltenden Tabellen und den Eingabespalten auf die Zelle gezogen werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [Data Mining-Erweiterungen &#40;DMX&#41; – Anweisungsreferenz](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  
