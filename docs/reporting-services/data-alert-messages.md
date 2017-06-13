---
title: Datenwarnmeldungen | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6819720c-d848-4b90-9b51-89501b4f4645
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1182111ce441c5a02417532cf4344ceb4ce7e44e
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="data-alert-messages"></a>Datenwarnmeldungen

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Datenwarnungen übermitteln zwei Typen von Datenwarnmeldungen per E-Mail: Meldungen mit Datenwarnungsergebnissen und Meldungen mit Fehlerbeschreibungen. Durch Meldungen mit Ergebnissen werden alle Empfänger über Änderungen der Berichtsdaten informiert, die von allgemeinem Interesse und wichtig für Geschäftsentscheidungen sind. Tritt aus einem unbestimmten Grund ein Fehler auf, und sind die Ergebnisse nicht verfügbar, wird stattdessen die Fehlermeldung gesendet.

Der Eigentümer der Datenwarnungsdefinition kann auch Informationen zur Datenwarnungsinstanz im Datenwarnungs-Manager anzeigen. Weitere Informationen finden Sie unter [Data Alert Manager for SharePoint Users](../reporting-services/data-alert-manager-for-sharepoint-users.md).  

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.
  
##  <a name="DataAlertMessages"></a> Datenwarnmeldungen  
 Die folgenden Bilder zeigen eine Datenwarnmeldung mit Ergebnissen und eine Warnmeldung mit einer Fehlerbeschreibung.  
  
 **Ergebnismeldung**  
  
 ![Daten-Warnungs-e-Mail-Nachricht mit Ergebnissen](../reporting-services/media/rs-alertmessageresults.gif "Daten-Warnungs-e-Mail-Nachricht mit Ergebnissen")  
  
 **Fehlermeldung**  
  
 ![Datenwarnmeldung mit Fehlermeldung](../reporting-services/media/rs-alertmessageerrror.gif "datenwarnmeldung mit Fehlermeldung")  
  
 Die Meldungen beinhalten die gleichen Informationstypen.  
  
1.  **Im Auftrag von** enthält den Namen des Erstellers der Datenwarnungsdefinition.  
  
2.  Haben Sie in der Warnungsdefinition eine Beschreibung angegeben, wird diese unterhalb von **Im Auftrag von**angezeigt.  
  
3.  **Warnungsergebnisse** zeigen die Zeilen im Berichtsdatenfeed, der die in der Warnungsdefinition angegebenen Regeln erfüllt, in einem Tabellenformat oder eine Fehlermeldung an. Die Anzahl der angezeigten Zeilen ist unbeschränkt.  
  
4.  **Gehe zu Bericht** ist ein Link zum Bericht, auf dem die Warnungsdefinition basiert. Wenn der Link nicht gültig ist, da der Bericht verschoben oder gelöscht wurde, wird eine Fehlermeldung angezeigt.  
  
5.  **Regel(n)** listet die Regeln und Klauseln in der Warnungsdefinition auf. Anhand dieser Informationen lassen sich die Warnungsergebnisse leichter überprüfen und verstehen. Des Weiteren lassen sich die Regeln in der Datenwarnungsdefinition identifizieren, die Sie ggf. zum Eingrenzen oder Erweitern der Ergebnisse ändern möchten.  
  
6.  **Berichtsparameter** listet die Parameter und Parameterwerte auf, mit denen der Bericht ausgeführt wurde. Parameter und Parameterwerte vereinfachen den Einblick in die Warnungsergebnisse.  
  
7.  **Kontextwerte** beinhalten die Namen und Werte von Berichtselementen, die sich außerhalb der Berichtsdatenbereiche befinden. Die Elemente sind in der Regel Textfelder. Es kann sich zum Beispiel um ein Textfeld mit einem konstanten Wert wie dem Betreff oder der Beschreibung eines Berichts handeln.  
  
 Der einzige Unterschied zwischen den zwei Meldungstypen ist Element 5, **Warnungsergebnisse**. Tritt bei der Erstellung einer Datenwarnungsinstanz oder Datenwarnmeldung ein Fehler auf, zeigt **Warnungsergebnisse** eine Fehlermeldung mit der Beschreibung des Problems an. Die Fehlermeldung wird an alle Empfänger gesendet und informiert diese, dass die erwarteten Warnungsergebnisse, die die Empfänger u. U. auch für Geschäftsentscheidungen benötigen, nicht verfügbar sind.  
  
  
##  <a name="HowTo"></a> Verwandte Aufgaben  
 Dieser Abschnitt listet Prozeduren zum Erstellen und Bearbeiten der Datenwarnungsdefinitionen auf, die viele der in den Datenwarnmeldungen angezeigten Informationen bieten.  
  
-   [Erstellen einer Datenwarnung im Datenwarnungs-Designer](../reporting-services/create-a-data-alert-in-data-alert-designer.md)  
  
-   [Bearbeiten einer Datenwarnung im Warnungs-Designer](../reporting-services/edit-a-data-alert-in-alert-designer.md)  

## <a name="see-also"></a>Siehe auch

[Datenwarnungs-Designer](../reporting-services/data-alert-designer.md)   
[Reporting Services-Datenwarnungen](../reporting-services/reporting-services-data-alerts.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
