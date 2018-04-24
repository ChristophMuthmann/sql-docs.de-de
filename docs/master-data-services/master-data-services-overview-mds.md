---
title: Übersicht über Master Data Services (MDS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
keywords:
- Was ist Master Data
helpviewer_keywords:
- Master Data Services, overview
- Master Data Services
ms.assetid: 8a4c28b1-6061-4850-80b6-132438b8c156
caps.latest.revision: 28
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8702bafc6b62d4c75d9dc76a32931e16dbe84e76
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="master-data-services-overview-mds"></a>Übersicht über Master Data Services (MDS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 In diesem Thema werden die Organisations- und Verwaltungsfunktionen von Schlüsseldaten in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]beschrieben. 
  
 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] ermöglicht es Ihnen, einen Mastersatz der Daten Ihrer Organisation zu verwalten. Sie können die Daten in Modellen organisieren, Regeln für das Aktualisieren der Daten erstellen und steuern, wer die Daten aktualisiert. Mit Excel können Sie den Masterdatensatz für andere Personen in Ihrer Organisation freigeben. 
  
 >  Eine Beschreibung der [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] -Architektur finden Sie im Artikel [Master Data Services – The Basics](https://www.simple-talk.com/sql/database-delivery/master-data-services-basics) auf „simple-talk.com“. Informationen zu den neuen Funktionen in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] finden Sie unter [Neues in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
   **Weitere Informationen zur Installation von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], der Einrichtung der Datenbank und Website und der Bereitstellung der Beispielmodelle finden Sie unter** [Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md).  
  
 In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]ist das Modell der Container auf der höchsten Ebene in der Struktur Ihrer Masterdataen. Ein Modell wird zum Verwalten von Gruppen ähnlicher Daten erstellt, z. B. von Onlineproduktdaten. Ein Modell enthält eine oder mehrere Entitäten, und Entitäten enthalten Elemente, die ihrerseits die Datensätze darstellen. Eine Entität ist ähnlich einer Tabelle.  
  
 Ihr Onlineproduktmodell kann beispielsweise Entitäten wie „Produkt“, „Farbe“ und „Stil“ beinhalten. Die Entität „Farbe“ kann bestimmte Elemente für die Farben Rot, Silber und Schwarz enthalten.  
  
 ![Color-Entität](../master-data-services/media/mds-productmodel-colorentity-composite.png "Color entity")  
  
 Modelle enthalten außerdem Attribute, die innerhalb von Entitäten definiert sind. Ein Attribut enthält Werte, die das Beschreiben der Entitätselemente unterstützen. Es gibt Freiformattribute und domänenbasierte Attribute.  Ein domänenbasiertes Attribut enthält Werte, die von Mitgliedern aus einer Entität aufgefüllt werden und als Attributwerte für andere Entitäten verwendet werden können.  
  
 Beispielsweise kann die Entität „Produkt“ über Freiformattribute für Kosten und Gewicht verfügen. Es gibt außerdem ein domänenbasiertes Attribut für Farbe ![Nummer 1](../master-data-services/media/mds-number1.png "Number 1"), dessen Werte aus den Elementen der Color-Entität stammen. Diese Hauptliste der Farben liefert die Attributwerte für die Product-Entität ![Nummer 2](../master-data-services/media/mds-number2.png "Number 2").  
  
 ![Domänenbasiertes Attribut für die Farbe](../master-data-services/media/mds-productentity-color-domainattribute.png "Domain-based attribute for color")  
  
 Abgeleitete Hierarchien stammen aus den Beziehungen zwischen Entitäten in einem Modell. Hierbei handelt es sich um domänenbasierte Attributbeziehungen. Im Produktmodell kann z.B. eine aus der Farbe abgeleitete Hierarchie ![Nummer 1](../master-data-services/media/mds-number1.png "Number 1") verwendet werden, die auf der Beziehung zwischen den Color-![Nummer 2](../master-data-services/media/mds-number2.png "Number 2") und Product-Entitäten ![Nummer 3](../master-data-services/media/mds-number3.png "Number 3") basiert.  
  
 ![Von Color abgeleitete Hierarchie](../master-data-services/media/mds-derivedhierarchy.png "Color derived hierarchy")  
  
 Sobald Sie eine grundlegende Struktur für Ihre Daten definiert haben, können Sie damit beginnen, Datensätze (Elementen) mithilfe der Importfunktion hinzuzufügen. Sie laden Daten in Stagingtabellen, überprüfen sie mithilfe von Geschäftsregeln, und laden die Daten in MDS-Tabellen.  Geschäftsregeln können auch zum Festlegen von Attributwerden verwendet werden.  
  
 Die folgende Tabelle beschreibt die wichtigsten Aufgaben in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] in Grundzügen. Wenn nichts anderes angegeben ist, müssen Sie für alle nachfolgenden Prozeduren Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)zuzugreifen.  
  
> [!NOTE]  
>  Sie können die folgenden Tasks in einer Testumgebung ausführen und die bei der Installation von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]bereitgestellten Beispieldaten verwenden. Weitere Informationen finden Sie unter [Bereitstellen von Modellen &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md).  
  
|Aktion|Details|Verwandte Themen|  
|------------|-------------|--------------------|  
|Erstellen eines Modells|Wenn Sie ein Modell erstellen, gilt dieses als VERSION_1.|[Modelle &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)<br /><br /> [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md)|  
|Erstellen von Entitäten|Sie können so viele Entitäten erstellen, wie Sie für die Elemente benötigen.|[Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)<br /><br /> [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md)|  
|Erstellen von Entitäten, die als domänenbasierte Attribute verwendet werden|Um ein domänenbasiertes Attribut zu erstellen, müssen Sie zunächst die Entität zum Auffüllen der Attributwertliste erstellen.|[Domänenbasierte Attribute &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)<br /><br /> [Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|Erstellen von Attributen für die Entitäten|Erstellen Sie Attribute, um die Elemente zu beschreiben. Ein Name-Attribut und ein Code-Attribut ist automatisch in jeder Entität enthalten und können nicht entfernt werden. Bei Bedarf können Sie weitere Freiformattribute für Text, Datumsangaben, Zahlen oder Dateien erstellen.|[Attribute &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)<br /><br /> [Erstellen eines Textattributs &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)<br /><br /> [Erstellen eines numerischen Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)<br /><br /> [Erstellen eines Datenattributs &#40;Master Data Services&#41;](../master-data-services/create-a-date-attribute-master-data-services.md)<br /><br /> [Erstellen eines Linkattributs &#40;Master Data Services&#41;](../master-data-services/create-a-link-attribute-master-data-services.md)<br /><br /> [Erstellen eines Dateiattributs &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|Erstellen von Attributgruppen|Wenn Sie über mehr als vier oder fünf Attribute für eine Entität verfügen, empfiehlt sich die Erstellung von Attributgruppen. Diese Gruppen werden als Registerkarten oberhalb des Rasters in **Explorer** dargestellt und vereinfachen die Navigation, indem Attribute auf einzelnen Registerkarten gruppiert werden.|[Attributgruppen &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)<br /><br /> [Erstellen einer Attributgruppe &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Importieren von Elementen für die unterstützenden Entitäten|Importieren Sie die Daten für die unterstützenden Entitäten mithilfe des Stagingprozesses. Für das Product-Modell kann dies bedeuten, dass Sie Farben oder Größen importieren. Sie können Elemente auch manuell erstellen.<br /><br /> <br /><br /> Hinweis: Benutzer können Elemente in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] erstellen, wenn sie mindestens über die Berechtigung **Aktualisieren** für das Blattmodellobjekt einer Entität und über Zugriff auf den Funktionsbereich **Explorer** verfügen.|[Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)<br /><br /> [Erstellen eines Blattelements &#40;Master Data Services&#41;](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|Erstellen und Anwenden von Geschäftsregeln zum Sicherstellen der Datenqualität|Erstellen und veröffentlichen Sie Geschäftsregeln, um die Genauigkeit der Daten sicherzustellen. Sie können Geschäftsregeln für folgende Aufgaben verwenden:<br /><br /> Legen Sie Standardwerte für Attribute fest.<br /><br /> Ändern Sie Attributwerte.<br /><br /> Senden Sie E-Mail-Benachrichtigungen, wenn Daten die Geschäftsregelüberprüfung nicht bestanden haben.|[Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)<br /><br /> [Erstellen und Veröffentlichen einer Geschäftsregel &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)<br /><br /> [Überprüfen von bestimmten Elementen auf Geschäftsregeln (Master Data Services)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)<br /><br /> [Konfigurieren von E-Mail-Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)<br /><br /> [Konfigurieren von Geschäftsregeln für das Senden von Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Importieren von Elementen für die primären Entitäten und Anwenden von Geschäftsregeln|Importieren Sie die Elemente für die primären Entitäten mithilfe des Stagingprozesses. Überprüfen Sie anschließend die Version, die Geschäftsregeln auf alle Elemente in der Modellversion anwendet.<br /><br /> Anschließend können Sie alle Probleme bei der Geschäftsregelüberprüfung korrigieren.|[Überprüfung &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md)<br /><br /> [Überprüfen einer Version anhand von Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)<br /><br /> [Gespeicherte Überprüfungsprozedur &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)|  
|Erstellen abgeleiteter Hierarchien|Abgeleitete Hierarchien können aktualisiert werden, wenn sich die Geschäftsanforderungen ändern, und stellen sicher, dass alle Elemente auf der entsprechenden Ebene berücksichtigt werden.|[Abgeleitete Hierarchien &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)<br /><br /> [Erstellen einer abgeleiteten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Erstellen expliziter Hierarchien (bei Bedarf)|Wenn Sie Hierarchien erstellen möchten, die nicht ebenenbasiert sind und Elemente aus einer einzelnen Entität enthalten, können Sie explizite Hierarchien erstellen.|[Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)<br /><br /> [Erstellen einer expliziten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Erstellen von Auflistungen (bei Bedarf)|Erstellen Sie eine Auflistung, wenn Sie unterschiedliche Gruppierungen der Elemente zu Berichts- oder Analysezwecken anzeigen möchten und keine vollständige Hierarchie benötigen.<br /><br /> <br /><br /> Hinweis: Benutzer können Auflistungen in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] erstellen, wenn sie mindestens über die Berechtigung **Aktualisieren** für das Auflistmodellobjekt und über Zugriff auf den Funktionsbereich **Explorer** verfügen.|[Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)<br /><br /> [Erstellen einer Sammlung &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|Erstellen von benutzerdefinierten Metadaten|Fügen Sie dem Modell benutzerdefinierte Metadaten hinzu, um die Modellobjekte zu beschreiben. Die Metadaten könnten den Besitzer eines Objekts oder die Quelle der Daten enthalten.||  
|Sperren einer Version des Modells und Zuweisen eines Versionsflags|Sperren Sie eine Version des Modells, so dass nur Administratoren Änderungen an den Elementen vornehmen können. Wenn die Daten der Version erfolgreich mit den Geschäftsregeln angeglichen wurden, können Sie einen Commit für die Version ausführen. So wird verhindert, dass Benutzer Änderungen an Elementen vornehmen.<br /><br /> Erstellen Sie ein Versionsflag und weisen Sie es dem Modell zu. Anhand von Flags können Benutzer und Abonnementsysteme erkennen, welche Modellversion verwendet werden soll.|[Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)<br /><br /> [Sperren einer Version &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)<br /><br /> [Erstellen eines Versionsflags &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)|  
|Erstellen von Abonnementsichten|Damit die Abonnementsysteme die Masterdaten nutzen können, müssen Sie Abonnementsichten erstellen, durch die in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank Standardsichten erstellt werden.|[Übersicht: Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)<br /><br /> [Erstellen einer Abonnementsicht zum Exportieren von Daten &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Konfigurieren von Benutzer- und Gruppenberechtigungen|Sie können keine Benutzer- und Gruppenberechtigungen aus einer Test- in eine Produktionsumgebung kopieren. Sie können jedoch anhand der Testumgebung die Sicherheit bestimmen, die in der Produktionsumgebung verwendet werden soll.|[Sicherheit &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)<br /><br /> [Hinzufügen einer Gruppe &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)<br /><br /> [Hinzufügen eines Benutzers &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)|  
  
 Anschließend können Sie das Modell mit oder ohne Daten in der Produktionsumgebung bereitstellen. Weitere Informationen finden Sie unter [Bereitstellen von Modellen &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md).  
  
  

