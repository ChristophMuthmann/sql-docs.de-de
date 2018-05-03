---
title: Definieren einer Datenquelle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5a3e83c9-8788-431e-85b0-a68c79377ff3
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: dfeaa3291327ab2ee848acf30db017a60c4b3258
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-2---defining-a-data-source"></a>Lektion 1-2: Definieren einer Datenquelle
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Nach dem Erstellen eines [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Projekts beginnen Sie im Allgemeinen die Arbeit an dem Projekt, indem Sie mindestens eine Datenquelle definieren, die vom Projekt verwendet wird. Wenn Sie eine Datenquelle definieren, definieren Sie die Verbindungszeichenfolgeinformationen, die zum Verbinden der Datenquelle verwendet werden. Weitere Informationen finden Sie unter [Erstellen einer Datenquelle &#40;SSAS – mehrdimensional&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
In der folgenden Aufgabe definieren Sie die AdventureWorksDWSQLServer2012-Beispieldatenbank als Datenquelle für das [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial-Projekt. Während sich diese Datenbank für die Zwecke dieses Lernprogramms auf Ihrem lokalen Computer befindet, werden Quelldatenbanken häufig auf mindestens einem Remotecomputer gehostet.  
  
### <a name="to-define-a-new-data-source"></a>So definieren Sie eine neue Datenquelle  
  
1.  Klicken Sie im Projektmappen-Explorer (auf der rechten Seite des Microsoft Visual Studio-Fensters) mit der rechten Maustaste auf **Datenquellen**und anschließend auf **Neue Datenquelle**.  
  
2.  Klicken Sie auf der Seite **Willkommen beim Datenquellen-Assistenten** des **Datenquellen-Assistenten**auf **Weiter** , um die Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** zu öffnen.  
  
3.  Auf der Seite **Wählen Sie aus, wie die Verbindung definiert werden soll** können Sie eine Datenquelle basierend auf einer neuen Verbindung, basierend auf einer vorhandenen Verbindung oder basierend auf einem vorher definierten Datenquellenobjekt definieren. Im Rahmen dieses Lernprogramms definieren Sie eine Datenquelle auf der Basis einer neuen Verbindung. Überprüfen Sie, ob die Option **Eine neue Datenquelle basierend auf einer vorhandenen oder neuen Verbindung erstellen** ausgewählt ist, und klicken Sie anschließend auf **Neu**.  
  
4.  Im Dialogfeld **Verbindungs-Manager** definieren Sie Verbindungseigenschaften für die Datenquelle. Überprüfen Sie im Listenfeld **Anbieter** , ob **Native OLE DB\SQL Server Native Client 11.0** ausgewählt ist.  
  
    [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt auch andere Anbieter, die in der **Anbieter** -Liste angezeigt werden.  
  
5.  Geben Sie im Textfeld **Servername** die Eingabe **localhost**ein.  
  
    Um eine Verbindung mit einer benannten Instanz auf Ihrem lokalen Computer herzustellen, geben Sie **localhost\\<instance name>**. Geben Sie den Computernamen oder die IP-Adresse ein, um eine Verbindung zu einem spezifischen Computer statt zum lokalen Computer herzustellen.  
  
6.  Überprüfen Sie, ob **Windows-Authentifizierung verwenden** ausgewählt ist. Wählen Sie im Listenfeld **Datenbanknamen eingeben oder auswählen** den Eintrag **AdventureWorksDW2012**aus.  
  
7.  Klicken Sie auf **Verbindung testen** , um die Verbindung zur Datenbank zu testen.  
  
8.  Klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
9. Auf der Seite **Identitätswechselinformationen** des Assistenten definieren Sie die Sicherheitsinformationen für [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] zur Verbindungsherstellung mit der Datenquelle. Der Identitätswechsel wirkt sich auf das Windows-Konto aus, das zum Herstellen der Verbindung mit der Datenquelle verwendet wird, wenn die Windows-Authentifizierung ausgewählt ist. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] unterstützt keinen Identitätswechsel für die Verarbeitung von OLAP-Objekten. Wählen Sie **Dienstkonto verwenden**aus, und klicken Sie anschließend auf **Weiter**.  
  
10. Bestätigen Sie auf der Seite **Assistenten abschließen** den Standardnamen **Adventure Works DW 2012**, und klicken Sie anschließend auf **Fertig stellen** , um die neue Datenquelle zu erstellen.  
  
> [!NOTE]  
> Wenn Sie die Eigenschaften einer Datenquelle nach dem Erstellen ändern möchten, doppelklicken Sie im Ordner **Datenquellen** auf die Datenquelle, um die Eigenschaften der Datenquelle im **Datenquellen-Designer**anzuzeigen.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Definieren einer Datenquellensicht](../analysis-services/lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen einer Datenquelle &#40;SSAS – mehrdimensional&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
