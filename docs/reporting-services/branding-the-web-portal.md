---
title: Branding des Webportals | Microsoft Docs
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6dac97f7-02a6-4711-81a3-e850a6b40bf1
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 19742f59b104d18633a954dc2f8bc9824b58ef21
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---

# <a name="branding-the-web-portal"></a>Branding des Webportals

[!INCLUDE[ssrs-appliesto-sql2016-preview](../includes/ssrs-appliesto-sql2016-preview.md)]

Sie können die Darstellung des Webportals ändern, indem Sie es an das eigene Unternehmen anpassen. Dies erfolgt über ein Markenpaket. Das Markenpaket wurde entwickelt, damit Sie keine umfassenden Kenntnisse über das Cascading Stylesheet (CSS) benötigen, um es zu erstellen.  
  
<iframe width="560" height="315" src="https://www.youtube.com/embed/m08kLuofwFA?list=PLv2BtOtLblH3F--8WmK9QcLbx6dV_lVkL" frameborder="0" allowfullscreen></iframe>  
   
## <a name="creating-the-brand-package"></a>Erstellen des Markenpakets  
  
Ein Markenpaket für Reporting Services besteht aus drei Elementen und wird als ZIP-Datei verpackt.   
  
- color.json  
- metadata.xml  
- logo.png (optional)  
  
Die Dateien müssen die oben aufgeführten Namen aufweisen. Die ZIP-Datei kann jedoch beliebig benannt werden.  
  
### <a name="metadataxml"></a>metadata.xml  
  
Mit der Datei „metadata.xml“ können Sie den Namen des Markenpakets festlegen. Sie verfügt ebenso jeweils über einen Verweis auf Ihre „colors.json“- und „logo.png“-Dateien.  
  
Um den Namen des Markenpakets zu ändern, ändern Sie das Attribut **Name** des Elements **SystemResourcePackage** .  
  
    name="Multicolored example brand"  
  
Sie können optional ein Logobild in Ihr Markenpaket einschließen. Dieses Element wird innerhalb des Elements „Inhalt“ aufgelistet.  
  
Beispiel ohne eine Logodatei.  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
    </Contents>  
  
Beispiel mit einer Logodatei.  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
      <Item key="logo" path="logo.png" />  
    </Contents>  
  
### <a name="colorsjson"></a>Colors.json  
  
Wenn das Markenpaket hochgeladen wird, extrahiert der Server die entsprechenden Name/Wert-Paare aus der „colors.json“-Datei und verbindet sie mit dem LESS-Masterstylesheet „brand.less“. Diese LESS-Datei wird verarbeitet, und die resultierende CSS-Datei an den Client übermittelt. Alle Farben im Stylesheet folgen der hexadezimalen Darstellung einer Farbe mit sechs Zeichen.  
  
Das LESS-Stylesheet enthält Blöcke, die auf einige vordefinierte LESS-Variablen wie die folgenden verweisen.  
  
    /* primary buttons */   
    .btn-primary {   
        color:@primaryButtonColor;   
        background-color:@primaryButtonBg;   
    }  
  
Obwohl dies der CSS-Syntax ähnelt, das die Farbwerte anzeigt, mit dem Präfix der @symbol, sind eindeutig für LESS. Sie sind Variablen, deren Werte von der JSON-Datei festgelegt werden.  
  
Wenn beispielsweise die colors.json-Datei die folgenden Werte hätte.  
  
    "primary":"#009900",   
    "primaryContrast":"#ffffff"   
  
Die verarbeitete Ausgabe wird die **@primaryButtonBg** LESS-Variable aufrufen und sicherstellen, dass sie der JSON-Eigenschaft, genannt **primary**, zugeordnet wird, die in diesem Beispiel #009900 ist. Daher würde die richtige CSS ausgegeben werden.  
  
    .btn-primary {   
        color:#ffffff;   
        background-color:#009900;   
    }  
  
Alle primären Schaltflächen würden dunkelgrün mit weißem Text gerendert werden.  
  
Die Datei colors.json für Reporting Services ist in zwei Hauptkategorien unterteilt, deren Elemente gruppiert sind.  
  
- **Schnittstelle**: enthält Elemente, die für das Reporting Services-Webportal spezifisch sind.  
- **Design**: enthält Elemente, die für von Ihnen erstellte mobile Berichte spezifisch sind.  
  
Der Schnittstellen-Abschnitt ist in folgenden Gruppierungen unterteilt.  
  
|Abschnitt|Description|  
|---|---|  
|primary|Schaltflächen- und Hoverfarben.|  
|Secondary|Titelleiste, Suchleiste, linkes Menü (sofern angezeigt) und die Textfarbe für diese Elemente|  
|Neutral Primary|Hintergründe für Startseiten- und Berichtsbereich.|  
|Neutral Secondary|Hintergründe für Textfeld- und Ordneroptionen sowie das Menü „Einstellungen“.|  
|Neutral Tertiary|Hintergründe für Siteeinstellungen.|  
|Gefahr-/Warn-/Erfolgsmeldungen|Farben für diese Meldungen.|  
|KPI|Steuert die Farben für eine gute (1), neutrale (0), neutrale (-1) und keine.|  
  
Wenn Sie sich zum ersten Mal mit Mobile Report Publisher auf einem Server anmelden, der über ein bereitgestelltes Markenpaket verfügt, wird das Design den verfügbaren Designs zugeordnet, die Sie im oberen rechten Menü der App verwenden können.  
  
![Branding des SSRS-Publishers für mobile Berichte](../reporting-services/media/ssrsbrandingmobilereportpublisher.png)  
  
Dann können Sie dieses Design für alle mobilen Berichte verwenden, die Sie erstellen, auch wenn sie nicht für den gleichen Server vorgesehen sind, auf dem Sie das Design bereitgestellt haben.   
  
### <a name="using-a-logo"></a>Das Verwenden eines Logos  
  
Wenn Sie ein Logo mit Ihrem Markenpaket einschließen, wird es im Webportal anstelle des Namens angezeigt, den Sie für das Webportal im Menü "Einstellungen" festgelegt haben.  
  
Die Datei, die Sie für das Logo einschließen, muss im PNG-Dateiformat vorliegen. Die Dateidimensionen werden skaliert, sobald sie auf den Server hochgeladen werden. Er sollten auf ungefähr 290px x 60px skalieren.  
   
## <a name="applying-the-brand-package-to-the-web-portal"></a>Anwenden des Markenpakets auf das Webportal  
  
Um ein Markenpaket hinzuzufügen, herunterzuladen oder zu entfernen, können Sie Folgendes tun:  
  
1.  Wählen Sie das **Zahnradsymbol** in der oberen rechten Ecke aus.  
  
2.  Wählen Sie **Siteeinstellungen**aus.  
  
    ![SSR-Menü nach Klick auf Zahnradsymbol](../reporting-services/media/ssrsgearmenu.png)  
  
3.  Wählen Sie **Branding**aus.  
  
    ![SSRS-Branding](../reporting-services/media/ssrsbranding.png)  
  
**Zurzeit installiertes Markenpaket** zeigt entweder den Namen des Pakets an, das hochgeladen wurde, oder es zeigt „Keines“ an.  
  
**Markenpaket hochladen** übernimmt das Paket für das Webportal. Sie werden sehen, dass dies sofort wirksam wird.  
  
Sie können das Paket auch **Herunterladen** oder **Entfernen** . Das Entfernen des Pakets führt zum sofortigen Zurücksetzen des Webportals auf das Standardbranding.  
  
## <a name="metadataxml-example"></a>metadata.xml-Beispiel  
  
    \<?xml version="1.0" encoding="utf-8"?>  
    <SystemResourcePackage xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/systemresourcepackagemetadata"  
        type="UniversalBrand"  
        version="2.0.2"  
        name="Multicolored example brand"  
        >  
        <Contents>  
            <Item key="colors" path="colors.json" />  
            <Item key="logo" path="logo.png" />  
        </Contents>  
    </SystemResourcePackage>  
   
## <a name="colorsjson-example"></a>colors.json-Beispiel  
  
    {  
        "name":"Multicolored example brand",  
        "version":"1.0",  
        "interface":{  
            "primary":"#b31e1e",  
            "primaryAlt":"#ca0806",  
            "primaryAlt2":"#621013",  
            "primaryAlt3":"#e40000",  
            "primaryAlt4":"#e14e50",  
            "primaryContrast":"#fff",  
  
            "secondary":"#042200",  
            "secondaryAlt":"#0f4400",  
            "secondaryAlt2":"#155500",  
            "secondaryAlt3":"#217700",  
            "secondaryContrast":"#49e63c",  
  
            "neutralPrimary":"#d8edff",  
            "neutralPrimaryAlt":"#c9e6ff",  
            "neutralPrimaryAlt2":"#aedaff",  
            "neutralPrimaryAlt3":"#88c8ff",  
            "neutralPrimaryContrast":"#0a2b4c",  
  
            "neutralSecondary":"#e9d8eb",  
            "neutralSecondaryAlt":"#d9badc",  
            "neutralSecondaryAlt2":"#b06cb5",  
            "neutralSecondaryAlt3":"#a75bac",  
            "neutralSecondaryContrast":"#250a26",  
  
            "neutralTertiary":"#f79220",  
            "neutralTertiaryAlt":"#f8a54b",  
            "neutralTertiaryAlt2":"#facc9b",  
            "neutralTertiaryAlt3":"#fce3c7",  
            "neutralTertiaryContrast":"#391d00",  
  
            "danger":"#ff0000",  
            "success":"#00ff00",  
            "warning":"#ff8800",  
            "info":"#00ff",  
            "dangerContrast":"#fff",  
            "successContrast":"#fff",  
            "warningContrast":"#fff",  
            "infoContrast":"#fff",  
  
            "kpiGood":"#4fb443",  
            "kpiBad":"#de061a",  
            "kpiNeutral":"#d9b42c",  
            "kpiNone":"#333",  
            "kpiGoodContrast":"#fff",  
            "kpiBadContrast":"#fff",  
            "kpiNeutralContrast":"#fff",  
            "kpiNoneContrast":"#fff"  
           },  
           "theme":{  
            "dataPoints":[  
                "#0072c6",  
                "#f68c1f",  
                "#269657",  
                "#dd5900",  
                "#5b3573",  
                "#22bdef",  
                "#b4009e",  
                "#008274",  
                "#fdc336",  
                "#ea3c00",  
                "#00188f",  
                "#9f9f9f"  
            ],  
  
            "good":"#85ba00",  
            "bad":"#e90000",  
            "neutral":"#edb327",  
            "none":"#333",  
  
            "background":"#fff",  
            "foreground":"#222",  
            "mapBase":"#00aeef",  
            "panelBackground":"#f6f6f6",  
            "panelForeground":"#222",  
            "panelAccent":"#00aeef",  
            "tableAccent":"#00aeef",  
  
            "altBackground":"#f6f6f6",  
            "altForeground":"#000",  
            "altMapBase":"#f68c1f",  
            "altPanelBackground":"#235378",  
            "altPanelForeground":"#fff",  
            "altPanelAccent":"#fdc336",  
            "altTableAccent":"#fdc336"  
        }  
    }  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
