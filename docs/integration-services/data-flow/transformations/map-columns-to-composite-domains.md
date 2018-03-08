---
title: "Zuordnen von Spalten zu Verbunddomänen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8fb2e38ea252928a84dfaa8404d1b29b0bb6f33
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="map-columns-to-composite-domains"></a>Zuordnen von Spalten zu Verbunddomänen
  Eine Verbunddomäne besteht aus mindestens zwei einzelnen Domänen. Sie können der Domäne mehrere Spalten oder eine einzelne Spalte mit durch Trennzeichen getrennten Werten zuordnen.  
  
 Bei Verwendung mehrerer Spalten müssen Sie jeder einzelnen Domäne in der Verbunddomäne eine Spalte zuordnen, um die Verbunddomänenregeln auf die Datenbereinigung anzuwenden. Sie wählen die einzelnen, in der Verbunddomäne enthaltenen Domänen im Data Quality-Client aus. Weitere Informationen finden Sie unter [Erstellen einer Verbunddomäne](../../../data-quality-services/create-a-composite-domain.md).  
  
 Bei Verwendung einer einzelnen Spalte mit durch Trennzeichen getrennten Werten müssen Sie die einzelne Spalte der Verbunddomäne zuordnen. Die Werte müssen dieselbe Reihenfolge wie die einzelnen Domänen in der Verbunddomäne aufweisen. Das Trennzeichen in der Datenquelle muss mit dem zum Analysieren der Verbunddomänenwerte verwendeten Trennzeichen übereinstimmen. Zum Auswählen des Trennzeichens für die Verbunddomäne sowie zum Festlegen anderer Eigenschaften verwenden Sie den Data Quality-Client. Weitere Informationen finden Sie unter [Erstellen einer Verbunddomäne](../../../data-quality-services/create-a-composite-domain.md).  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>So ordnen Sie einer Verbunddomäne mehrere Spalten zu  
  
1.  Klicken Sie mit der rechten Maustaste auf die Transformation für die DQS-Bereinigung, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Vergewissern Sie sich auf der Registerkarte **Verbindungs-Manager** , dass die Verbunddomäne in der Liste verfügbarer Domänen angezeigt wird.  
  
3.  Wählen Sie auf der Registerkarte **Zuordnung** die Spalten im Bereich **Verfügbare Eingabespalten** aus.  
  
4.  Wählen Sie für jede im Feld **Eingabespalte** aufgelistete Spalte eine einzelne Domäne im Feld **Domäne** aus. Wählen Sie nur einzelne Domänen aus, die in der Verbunddomäne enthalten sind.  
  
5.  Ändern Sie ggf. die Namen in den Feldern **Alias - Quelle**, **Alias - Ausgabe**und **Alias - Status** .  
  
6.  Legen Sie nach Bedarf Eigenschaften auf der Registerkarte **Erweitert** fest. Weitere Informationen zu den Eigenschaften finden Sie unter [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>So ordnen Sie einer Verbunddomäne eine Spalte mit durch Trennzeichen getrennten Werten zu  
  
1.  Klicken Sie mit der rechten Maustaste auf die Transformation für die DQS-Bereinigung, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Vergewissern Sie sich auf der Registerkarte **Verbindungs-Manager** , dass die Verbunddomäne in der Liste verfügbarer Domänen angezeigt wird.  
  
3.  Wählen Sie auf der Registerkarte **Zuordnung** die Spalte im Bereich **Verfügbare Eingabespalten** aus.  
  
4.  Wählen Sie für die im Feld **Eingabespalte** aufgelistete Spalte die Verbunddomäne im Feld **Domäne** aus.  
  
5.  Ändern Sie ggf. die Namen in den Feldern **Alias - Quelle**, **Alias - Ausgabe**und **Alias - Status** .  
  
6.  Legen Sie nach Bedarf Eigenschaften auf der Registerkarte **Erweitert** fest. Weitere Informationen zu den Eigenschaften finden Sie unter [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DQS-Bereinigungstransformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
