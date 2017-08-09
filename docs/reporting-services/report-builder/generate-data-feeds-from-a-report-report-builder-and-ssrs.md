---
title: Generieren von Datenfeeds aus einem Bericht (Berichts-Generator und SSRS) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b49b80de8516e14972b05d7ae91f4f72e765803a
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>Generieren von Datenfeeds aus einem Bericht (Berichts-Generator und SSRS)

Sie können Atom-kompatible Datenfeeds von paginierten Berichten generieren und verwenden Sie die Datenfeeds in Anwendungen, z. B. Power Pivot erstellt wurde, oder feeds Power BI, die Daten nutzen können.  
  
 Die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Atom-Renderingerweiterung generiert ein Atom-Dienstdokument, in dem die aus einem Bericht verfügbaren Datenfeeds aufgeführt sind. Im Dokument ist mindestens ein Datenfeed für jeden Datenbereich im Bericht enthalten. Abhängig vom Typ des Datenbereichs und den darin angezeigten Daten könnte [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mehrere Datenfeeds aus einem Datenbereich generieren.  
  
 Ein Atom-Dienstdokument enthält einen eindeutigen Bezeichner für jeden Datenfeed. Sie verwenden den Bezeichner in einer URL, um den Inhalt des Datenfeeds anzuzeigen.  
  
 Weitere Informationen finden Sie unter [Generieren von Datenfeeds aus Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>So generieren Sie ein Atom-Dienstdokument  
  
1.  Navigieren Sie im [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Webportal zu dem Bericht, für den Sie Datenfeeds erstellen möchten.  
  
2.  Klicken Sie auf den Bericht.  
  
     Der Bericht wird ausgeführt.  
  
3.  Klicken Sie auf der Symbolleiste auf das Symbol **In Datenfeed exportieren** .  
  
     Sie werden in einer Meldung gefragt, ob Sie das Atom-Dokument, das den Datenfeed enthält, speichern oder öffnen möchten.  
  
4.  Klicken Sie auf **Speichern** , um das Dokument im Dateisystem zu speichern, oder auf **Öffnen** , um den Dokumentinhalt vor dem Speichern anzuzeigen. **Das Dokument wird standardmäßig in einem Browser geöffnet.**  
  
5.  Navigieren Sie zum Speicherort, an dem das Dokument gespeichert werden soll.  
  
6.  Ändern Sie optional den Namen des Dokuments.  
  
    > [!NOTE]  
    >  Standardmäßig entspricht der Dokumentname dem Berichtsnamen.  
  
7.  Stellen Sie sicher, dass der Dokumenttyp einer **ATOMSVC-Datei**entspricht, und klicken Sie dann auf **Speichern**.  
  
8.  Öffnen Sie die ATOMSVC-Datei optional in einem Browser bzw. einem Text- oder XML-Editor.  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>So zeigen Sie einen Atom-kompatiblen Datenfeed an  
  
1.  Falls das Atom-Dienstdokument noch nicht geöffnet ist, suchen Sie es und öffnen das Dokument in einem Browser wie Internet Explorer.  
  
2.  Kopieren Sie die URL des Datenfeeds, den Sie anzeigen möchten, aus dem Atom-Dienstdokument in den Browser.  
  
     Die URL hat folgendes Format:  
  
     `http://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
3.  Drücken Sie die EINGABETASTE.  
  
     Sie werden in einer Meldung gefragt, ob Sie das Atom-Dokument, das den Datenfeed enthält, speichern oder öffnen möchten.  
  
4.  Klicken Sie auf **Speichern** , um das Dokument im Dateisystem zu speichern, oder auf **Öffnen** , um den Datenfeed vor dem Speichern anzuzeigen.  
  
5.  Navigieren Sie zum Speicherort, an dem das Dokument gespeichert werden soll.  
  
6.  Ändern Sie optional den Namen des Dokuments.  
  
    > [!NOTE]  
    >  Standardmäßig entspricht der Dokumentname dem Berichtsnamen. Wenn das Atom-Dienstdokument mehrere Feeds enthält, verwenden alle standardmäßig den gleichen Namen, und zwar den Berichtsnamen. Um zwischen den Datenfeeds zu unterscheiden, benennen Sie diese mit aussagekräftigen Namen um.  
  
7.  Stellen Sie sicher, dass der Dokumenttyp einer **ATOM-Datei**entspricht, und klicken Sie dann auf **Speichern**.  
  
8.  Öffnen Sie die ATOM-Datei optional in einem Browser bzw. Text-Editor oder XML-Editor.  

## <a name="next-steps"></a>Nächste Schritte

[Exportieren von Berichten](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
