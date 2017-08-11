---
title: "Erstellen eines verknüpften Berichts | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linked reports [Reporting Services], creating
ms.assetid: 12be8341-cb57-45e8-a421-2bf66b50234d
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 232e24ef08c24d5c6a2c9799094fc492305eea46
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-linked-report"></a>Erstellen eines verknüpften Berichts
  Ein verknüpfter Bericht ist ein Berichtsserverelement, das einen Zugriffspunkt auf einen vorhandenen Bericht bereitstellt. Grundsätzlich ist er mit einer Programmverknüpfung vergleichbar, die Sie verwenden, um ein Programm auszuführen oder eine Datei zu öffnen.  
  
 Ein verknüpfter Bericht wird von einem vorhandenen Bericht abgeleitet und behält die Berichtsdefinition des Originals bei. Ein verknüpfter Bericht erbt immer das Berichtslayout und die Datenquelleneigenschaften des ursprünglichen Berichts. Alle anderen Eigenschaften und Einstellungen können sich von denen des ursprünglichen Berichts unterscheiden, einschließlich Sicherheit, Parameter, Speicherort, Abonnements und Zeitpläne.  
  
 Sie können einen verknüpften Bericht erstellen, wenn Sie zusätzliche Versionen eines vorhandenen Berichts erstellen möchten. Beispielsweise könnten Sie einen einzelnen regionalen Vertriebsbericht verwenden, um regionsspezifische Berichte für alle Vertriebsgebiete zu erstellen.  
  
 Obwohl verknüpfte Berichte in der Regel auf parametrisierten Berichten basieren, ist kein parametrisierter Bericht erforderlich. Sie können immer dann verknüpfte Berichte erstellen, wenn Sie einen vorhandenen Bericht mit anderen Einstellungen bereitstellen möchten.  
  
### <a name="to-create-a-linked-report"></a>So erstellen Sie einen verknüpften Bericht  
  
1.  Navigieren Sie im Berichts-Manager zum Ordner, der den Bericht enthält, zu dem Sie einen Link erstellen möchten, und öffnen Sie dann das Menü Optionen und klicken Sie auf **Verknüpften Bericht erstellen**.  
  
2.  Geben Sie einen Namen für den neuen verknüpften Bericht ein. Geben Sie optional eine Beschreibung ein.  
  
3.  Um einen anderen Ordner für den Bericht auszuwählen, klicken Sie auf **Speicherort ändern**. Klicken Sie auf den Ordner, den Sie verwenden möchten, oder geben Sie den Ordnernamen im Feld **Speicherort** ein. [!INCLUDE[clickOK](../../includes/clickok-md.md)]Wenn Sie einen anderen Ordner nicht auswählen, wird der verknüpfte Bericht im aktuellen Ordner erstellt (in dem der Bericht basiert auf werden gespeichert ist).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]Der verknüpfte Bericht wird geöffnet.  
  
     Das Symbol für einen verknüpften Bericht unterscheidet sich von anderen Elementen, die von einem Berichtsserver verwaltet werden. Das folgende Symbol steht für einen verknüpften Bericht:  
  
     ![Symbol verknüpfte Berichte](../../reporting-services/report-server/media/hlp-16linked.gif "Linked report icon")  
  
## <a name="see-also"></a>Siehe auch  
 [Öffnen Sie und schließen Sie eines Berichts &#40; Berichts-Manager &#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Seite "Neuer verknüpfter Bericht" &#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/fefb46e8-6901-4d50-a3f8-7c49ad72e7b1)   
 [Wählen Sie die Seite "Speicherort" Element &#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/4a53a1a8-d1e1-47ef-b1fc-63352ece7d3c)   
 [Allgemeine Eigenschaftenseite, Berichte &#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/66c99d28-ab41-45f0-bf02-ed560293595d)   
 [Reporting Services-Konzepte &#40; SSRS &#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Berichts-Manager &#40; SSRS im einheitlichen Modus &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
