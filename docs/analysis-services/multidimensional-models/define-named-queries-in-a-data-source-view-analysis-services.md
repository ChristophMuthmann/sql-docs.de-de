---
title: Definieren von benannten Abfragen in einer Datenquellensicht (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ea1c777a0e7d03b5b85148e1158d1f428bd4f38
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="define-named-queries-in-a-data-source-view-analysis-services"></a>Definieren von benannten Abfragen in einer Datenquellensicht (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Bei einer benannten Abfrage handelt es sich um einen SQL-Ausdruck, der als Tabelle dargestellt wird. In einer benannten Abfrage können Sie einen SQL-Ausdruck angeben, um Zeilen und Spalten auszuwählen, die aus mindestens einer Tabelle in mindestens einer Datenquelle zurückgegeben wurden. Eine benannte Abfrage verhält sich wie alle anderen Tabellen in einer Datenquellensicht (Data Source View, DSV) mit Zeilen und Beziehungen. Der einzige Unterschied besteht darin, dass eine benannte Abfrage auf einem Ausdruck basiert.  
  
 Mit einer benannten Abfrage können Sie das relationale Schema vorhandener Tabellen in einer Datenquellensicht ohne Ändern der zugrunde liegenden Datenquelle erweitern. Sie können z. B. mithilfe einer Reihe benannter Abfragen eine komplexe Dimensionstabelle in kleinere einfachere Dimensionstabellen aufteilen, die in Datenbankdimensionen verwendet werden sollen. Eine benannte Abfrage kann auch zum Verknüpfen mehrerer Datenbanktabellen von mindestens einer Datenquelle in einer einzelnen Tabelle für die Datenquellensicht verwendet werden.  
  
## <a name="creating-a-named-query"></a>Erstellen einer benannten Abfrage  
  
> [!NOTE]  
>  Sie können einer benannten Abfrage keine benannte Berechnung hinzufügen. Die benannte Abfrage darf auch nicht auf einer Tabelle basieren, die eine benannte Berechnung enthält.  
  
 Geben Sie beim Erstellen einer benannten Abfrage einen Namen, die SQL-Abfrage, die Spalten und Daten für die Tabelle zurückgibt, und optional eine Beschreibung für die benannte Abfrage an. Der SQL-Ausdruck kann auf andere Tabellen in der Datenquellensicht verweisen. Nach dem definieren der benannten Abfrage wird die SQL-Abfrage in einer benannten Abfrage an den Anbieter für die Datenquelle gesendet und als Ganzes überprüft. Wenn der Anbieter keine Fehler in der SQL-Abfrage findet, wird die Spalte der Tabelle hinzugefügt.  
  
 Tabelle und Spalten, auf die in der SQL-Abfrage verwiesen wird, sollten nicht qualifiziert oder nur durch den Tabellennamen qualifiziert sein. Wenn Sie z. B. auf die SaleAmount-Spalte in einer Tabelle verweisen möchten, ist `SaleAmount` oder `Sales.SaleAmount` gültig, aber `dbo.Sales.SaleAmount` generiert einen Fehler.  
  
 **Hinweis** Wenn eine benannte Abfrage definiert wird, mit der eine [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] - oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0-Datenquelle abgefragt wird, treten für eine benannte Abfrage, die eine korrelierte Unterabfrage und eine GROUP BY-Klausel enthält, Fehler auf. Weitere Informationen finden Sie unter [Interner Fehler für SELECT-Anweisung mit korrelierter Unterabfrage und GROUP BY](http://support.microsoft.com/kb/274729) in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
## <a name="add-or-edit-a-named-query"></a>Hinzufügen oder Bearbeiten einer benannten Abfrage  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das Projekt, bzw. stellen Sie eine Verbindung mit der Datenbank her, das bzw. die die Datenquellensicht enthält, der Sie eine benannte Abfrage hinzufügen möchten.  
  
2.  Erweitern Sie im Projektmappen-Explorer den Ordner **Datenquellensichten** , und doppelklicken Sie anschließend auf die Datenquellensicht.  
  
3.  Klicken Sie im Bereich **Tabellen** oder **Diagramm** mit der rechten Maustaste auf einen geöffneten Bereich, und klicken Sie anschließend auf **Neue benannte Abfrage**.  
  
4.  Führen Sie im Dialogfeld **Benannte Abfrage erstellen** die folgenden Schritte aus:  
  
    1.  Geben Sie im Textfeld **Name** einen Abfragenamen ein.  
  
    2.  Geben Sie optional im Textfeld **Beschreibung** eine Beschreibung für die Abfrage ein.  
  
    3.  Wählen Sie im Listenfeld **Datenquelle** die Datenquelle aus, für die die benannte Abfrage ausgeführt werden soll.  
  
    4.  Geben Sie im unteren Bereich die Abfrage ein, oder verwenden Sie die grafischen Tools zum Erstellen von Abfragen, um eine Abfrage zu erstellen.  
  
    > [!NOTE]  
    >  Die Benutzeroberfläche zum Erstellen der Abfrage hängt von der Datenquelle ab. Anstelle einer grafischen Benutzeroberfläche erhalten Sie unter Umständen eine allgemeine textbasierte Benutzeroberfläche. Zwar erreichen Sie dasselbe mit diesen unterschiedlichen Benutzeroberflächen, die Vorgehensweise ist jedoch jeweils anders. Weitere Informationen finden Sie unter [Benannte Abfrage erstellen oder bearbeiten &#40;Dialogfeld, Analysis Services – mehrdimensionale Daten&#41;](http://msdn.microsoft.com/library/8e192ad6-a0b1-4e21-bb3f-087c93e62941).  
  
5.  Klicken Sie auf **OK**. Ein Symbol mit zwei überlappenden Tabellen wird im Tabellenkopf angezeigt. Dieses Symbol bedeutet, dass die Tabelle durch eine benannte Abfrage ersetzt wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellsichten in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Definieren von benannten Berechnungen in einer Datenquellensicht & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
