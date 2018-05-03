---
title: Erstellen ein vertrauenswürdiges Speicherorts für Power Pivot-Websites in der Zentraladministration | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3dabb6a62434ce2956a0c11a62f3b383104df698
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-trusted-location-for-power-pivot-sites-in-central-administration"></a>Erstellen eines vertrauenswürdigen Speicherorts für PowerPivot-Websites in der Zentraladministration
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In Excel Services können Sie angeben, welche Speicherorte gültige Repositorys für Arbeitsmappen sind, die Sie auf einem SharePoint-Server öffnen. Diese Speicherorte werden als 'vertrauenswürdige Speicherorte' bezeichnet, und Sie können unterschiedliche Konfigurationseinstellungen für jeden vertrauenswürdigen Speicherort verwenden, den Sie erstellen. Bei einer Bereitstellung von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint sollten Sie erwägen, einen vertrauenswürdigen Speicherort für Websites zu erstellen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten, sodass Sie die Einstellungen anwenden können, die optimal für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff geeignet sind, aber gleichzeitig die Standardeinstellungen für den Rest der Farm beibehalten können.  
  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 Sie müssen Farm- oder Dienstadministrator sein, um eine URL als vertrauenswürdigen Speicherort festzulegen.  
  
 Sie müssen die URL-Adresse der SharePoint-Website kennen, die den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog oder eine andere Bibliothek enthält, in der die Arbeitsmappen gespeichert sind. Sie erhalten die Adresse, indem Sie die Website öffnen, die die Bibliothek enthält, mit der rechten Maustaste auf **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog**klicken, **Eigenschaften**auswählen und anschließend den ersten Teil der Adresse (URL) kopieren, der den Servernamen und den Websitepfad enthält.  
  
##  <a name="overview"></a> Übersicht  
 Erste Installationen von Excel Services geben 'http://' als vertrauenswürdigen Speicherort an, was bedeutet, dass Arbeitsmappen von jeder beliebigen Website in der Farm auf dem Server geöffnet werden können. Wenn Sie eine bessere Kontrolle darüber benötigen, welche Speicherorte als vertrauenswürdig angesehen werden, können Sie neue, vertrauenswürdige Speicherorte erstellen, die bestimmten Websites in der Farm zugeordnet sind, und dann die Einstellungen und Berechtigungen für jede einzelne variieren.  
  
 Wenn Sie für den übrigen Teil der Farm Standardwerte beibehalten, gleichzeitig aber andere Einstellungen anwenden möchten, die optimal für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff geeignet sind, empfiehlt es sich, einen neuen vertrauenswürdigen Speicherort für Websites zu erstellen, die als Host für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen dienen. Ein vertrauenswürdiger Speicherort, der für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen optimiert ist, kann z.B. eine maximale Arbeitsmappengröße von 50 MB haben, während der Rest der Farm den Standardwert 10 MB verwendet.  
  
 Das Erstellen eines vertrauenswürdigen Speicherorts wird empfohlen, wenn Sie [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalogbibliotheken verwenden, um eine Vorschau veröffentlichter Arbeitsmappen anzuzeigen, und anstelle des erwarteten Vorschaubilds Datenaktualisierungswarnungen angezeigt werden. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Der Katalog rendert Miniaturbilder von Berichten und Arbeitsmappen unter Verwendung von Daten und Präsentationsinformationen innerhalb des Dokuments. Wenn „Beim Aktualisieren warnen“ für einen vertrauenswürdigen Speicherort aktiviert ist, verfügt der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog möglicherweise nicht über ausreichende Berechtigungen zum Ausführen der Aktualisierung, sodass anstelle des Miniaturbilds ein Fehler angezeigt wird. Das Hinzufügen einer Website als neuer vertrauenswürdiger Speicherort, die den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog enthält, kann dieses Problem ausschließen.  
  
##  <a name="create"></a> Erstellen eines vertrauenswürdigen Speicherorts für den Power Pivot-Datenzugriff  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf die Excel Services-Dienstanwendung.  
  
3.  Klicken Sie auf **Vertrauenswürdige Dateispeicherorte**.  
  
4.  Klicken Sie auf **Vertrauenswürdigen Dateispeicherort hinzufügen**.  
  
5.  Geben Sie die URL einer Website ein, in der eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalogbibliothek enthalten ist.  
  
6.  Wählen Sie als Speicherorttyp **Microsoft SharePoint Foundation**aus.  
  
    > [!IMPORTANT]  
    >  UNC- und HTTP-Speicherorttypen werden beim [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff nicht unterstützt.  
  
7.  Akzeptieren Sie die Standardeinstellungen für sämtliche Eigenschaften unter Sitzungsverwaltung, Arbeitsmappeneigenschaften und Berechnungsverhalten.  
  
8.  Legen Sie in Arbeitsmappeneigenschaften die Option **Maximale Arbeitsmappengröße** auf **50**fest. Dadurch wird die Obergrenze der Arbeitsmappendateigröße auf die Obergrenze für Dateiuploads in die übergeordnete Webanwendung eingestellt. Wenn die Arbeitsmappen größer als 50 MB sind, müssen Sie die maximale Dateigröße weiter erhöhen. Weitere Informationen finden Sie unter [Konfigurieren der maximalen Dateiuploadgröße &#40;PowerPivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).  
  
9. Überprüfen Sie in „Externe Daten“, ob „Externe Daten zulassen“ auf **Vertrauenswürdige Datenverbindungsbibliotheken und eingebettete Verbindungen** festgelegt ist. Diese Einstellung ist für den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datenzugriff in einer Arbeitsmappe erforderlich.  
  
10. Deaktivieren Sie in „Externe Daten“ für „Beim Aktualisieren warnen“ auch das Kontrollkästchen **Aktualisierungswarnung aktiviert**. Wenn Sie das Kontrollkästchen deaktivieren, kann der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Katalog Routinewarnmeldungen umgehen und stattdessen Vorschaubilder einer Arbeitsmappe anzeigen.  
  
11. Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Power Pivot-Katalog](http://msdn.microsoft.com/library/2a0db616-e08e-4062-aac8-979f8cad7794)   
 [Erstellen und Anpassen von Power Pivot-Katalogs](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)   
 [Verwenden des Power Pivot-Katalogs](../../analysis-services/power-pivot-sharepoint/use-power-pivot-gallery.md)  
  
  
