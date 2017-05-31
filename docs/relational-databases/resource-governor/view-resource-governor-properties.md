---
title: Anzeigen der Eigenschaften der Ressourcenkontrolle | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e856286b6048e320481b5983685fbfcd4e838c1d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="view-resource-governor-properties"></a>Anzeigen der Eigenschaften der Ressourcenkontrolle
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Auf der Seite Eigenschaften der Ressourcenkontrolle in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]können Sie Ressourcenkontrollentitäten erstellen oder konfigurieren, z. B. Ressourcenpools und Arbeitsauslastungsgruppen.  
  
 ##  <a name="BeforeYouBegin"></a> Verwandte Themen 
 Neben dem Anzeigen der Eigenschaften von Ressourcenkontrollentitäten können Sie auf der Seite **Eigenschaften der Ressourcenkontrolle** mehrere Konfigurationstasks ausführen. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)  
  
-   [Deaktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/disable-resource-governor.md)  
  
-   [Erstellen eines Ressourcenpools](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [Erstellen einer Arbeitsauslastungsgruppe](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
-   [Ändern der Einstellungen für den Ressourcenpool](../../relational-databases/resource-governor/change-resource-pool-settings.md)  
  
-   [Ändern der Einstellungen von Arbeitsauslastungsgruppen](../../relational-databases/resource-governor/change-workload-group-settings.md)  
  
-   [Verschieben von Arbeitsauslastungsgruppen](../../relational-databases/resource-governor/move-a-workload-group.md)  
  
 Nachdem Sie eine Arbeitsauslastungsgruppe oder einen Ressourcenpool hinzugefügt, gelöscht oder verschoben haben, wird die Anweisung ALTER RESOURCE GOVERNOR RECONFIGURE ausgeführt, wenn Sie auf **OK** klicken.  
  
 Bei einem Fehler beim Erstellungs- oder Neukonfigurierungsvorgang für den Ressourcenpool oder die Arbeitsauslastungsgruppe wird unter dem Titel der Eigenschaftenseite eine zusammenfassende Fehlermeldung angezeigt. Klicken Sie auf den Abwärtspfeil an der Fehlermeldung, um eine ausführliche Fehlermeldung anzuzeigen.  
  
 Sie können feststellen, ob eine ausstehende Konfiguration vorliegt, indem Sie die dynamische Verwaltungssicht [sys.dm_resource_governor_configuration](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) abfragen, um den aktuellen Status von is_configuration_pending zu erhalten.  
  
##  <a name="Permissions"></a> Berechtigungen  
 Zum Anzeigen der Ressourcenkontrolleigenschaften ist die VIEW SERVER STATER-Berechtigung erforderlich. Für die Konfigurationstasks für die Ressourcenkontrolle ist die CONTROL SERVER-Berechtigung erforderlich.  
  
##  <a name="ViewRGProp"></a> Seite „Eigenschaften von Resource Governor“  
 **So zeigen Sie Resource Governor-Eigenschaften auf der Seite „Eigenschaften von Resource Governor“ in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den Objekt-Explorer, und erweitern Sie den Knoten **Verwaltung** rekursiv, bis **Ressourcenkontrolle**angezeigt wird.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Resource Governor** , und klicken Sie dann auf **Eigenschaften**. Damit öffnen Sie die Seite **Eigenschaften der Resource Governor** .  
  
3.  Beschreibungen der Felder auf der Seite finden Sie unter [Eigenschaften der Ressourcenkontrolle](#RGProp).  
  
4.  Klicken Sie auf **OK**, um Änderungen zu speichern.  
  
##  <a name="RGProp"></a> Resource Governor properties  
 **Der Name der Klassifizierungsfunktion**  
 Geben Sie die Klassifizierungsfunktion durch Auswahl aus der Liste an.  
  
 **Aktivieren der Ressourcenkontrolle**  
 Aktivieren oder deaktivieren Sie die Ressourcenkontrolle, indem Sie das Kontrollkästchen aktivieren oder deaktivieren.  
  
 **Ressourcenpools**  
 Erstellen oder ändern Sie die Konfiguration von Ressourcenpools und externen Ressourcenpools mithilfe des vorhandenen Rasters. Dieses Raster wird mit Informationen für die vordefinierten internen Pools und Standardpools ausgefüllt. Wählen Sie einen Pool aus, mit dem Sie arbeiten möchten, indem Sie auf die erste Spalte in der Zeile für den Pool klicken. Klicken Sie zur Erstellung eines neuen Ressourcenpools auf die Zeile, der ein Sternchen (**\***) vorangestellt ist.  
  
 **Name**  
 Geben Sie den Namen des Ressourcenpools an.  
  
 **Minimaler CPU-Prozentsatz**  
 Geben Sie die garantierte durchschnittliche CPU-Bandbreite für alle Anforderungen im Ressourcenpool an, wenn CPU-Konflikte bestehen. Der Bereich liegt zwischen 0 und 100.  
  
 **Maximaler CPU-Prozentsatz**  
 Geben Sie die maximale durchschnittliche CPU-Bandbreite an, die allen Anforderungen im Ressourcenpool zugewiesen wird, wenn CPU-Konflikte bestehen. Der Bereich liegt zwischen 0 und 100. Die Standardeinstellung ist 100.  
  
 **Minimaler Arbeitsspeicherprozentsatz**  
 Geben Sie den Mindestarbeitsspeicher an, der für diesen Ressourcenpool reserviert ist und nicht gemeinsam mit anderen Ressourcenpools verwendet werden kann. Der Bereich liegt zwischen 0 und 100.  
  
 **Maximaler Arbeitsspeicherprozentsatz**  
 Geben Sie den gesamten Serverspeicher an, der für Anforderungen in diesem Ressourcenpool verwendet werden kann. Der Bereich liegt zwischen 0 und 100. Die Standardeinstellung ist 100.  
  
 Weitere Informationen finden Sie unter [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md) und unter [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  
 **Arbeitsauslastungsgruppen für Ressourcenpool**  
 Erstellen oder ändern Sie die Konfiguration von Arbeitsauslastungsgruppen mithilfe des vorhandenen Rasters. Dieses Raster wird mit Informationen für die vordefinierten internen Gruppen und Standardgruppen ausgefüllt. Wählen Sie eine Gruppe aus, mit der Sie arbeiten möchten, indem Sie auf die erste Spalte in der Zeile für den Pool klicken. Klicken Sie zur Erstellung einer neuen Arbeitsauslastungsgruppe auf die Zeile, der ein Sternchen (**\***) vorangestellt ist.  
  
 **Name**  
 Geben Sie den Namen der Arbeitsauslastungsgruppe an.  
  
 **Wichtigkeit**  
 Geben Sie die relative Wichtigkeit einer Anforderung in der Arbeitsauslastungsgruppe an. Die verfügbaren Einstellungen lauten Niedrig, Mittel und Hoch.  
  
 **Maximale Anforderungen**  
 Geben Sie die maximale Anzahl gleichzeitiger Anforderungen an, die in der Arbeitsauslastungsgruppe ausgeführt werden können. Dieser Wert muss 0 (null) oder eine positive Ganzzahl sein.  
  
 **CPU-Zeit (Sek.)**  
 Geben Sie die maximale CPU-Zeit für eine Anforderung an. Dieser Wert muss 0 (null) oder eine positive Ganzzahl sein. Bei 0 ist die Zeit unbegrenzt.  
  
 **Arbeitsspeicherzuweisung (%)**  
 Geben Sie die Höchstmenge an Arbeitsspeicher an, die eine einzelne Anforderung vom Pool in Anspruch nehmen kann. Der Bereich liegt zwischen 0 und 100.  
  
 **Timeout für Arbeitsspeicherzuweisung (Sek)**  
 Geben Sie die maximale Zeit in Sekunden an, die eine Abfrage auf das Freiwerden einer Ressource wartet, bevor die Abfrage fehlschlägt. Dieser Wert muss 0 (null) oder eine positive Ganzzahl sein.  
  
 **Grad der Parallelität**  
 Geben Sie den maximalen Grad der Parallelität (DOP) für parallele Anforderungen an. Der Bereich liegt zwischen 0 und 64.  
  
 Weitere Informationen finden Sie unter [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## <a name="view-resource-governor-properties-using-transact-sql"></a>Anzeigen von Resource Governor-Eigenschaften mit Transact-SQL  
 **Anzeigen von Eigenschaften der Ressourcenkontrolle mit Transact-SQL**  
  
1.  Um die Definitionen von Resource Governor-Entitäten anzuzeigen, verwenden Sie die [Katalogsichten des Resource Governors &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
2.  Um die aktuelle Konfiguration von Resource Governor-Entitäten anzuzeigen, verwenden Sie die [dynamischen Verwaltungssichten in Verbindung mit dem Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
## <a name="more-information"></a>Weitere Informationen
 [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md)   
 [Aktivieren der Ressourcenkontrolle](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Ressourcenpool für die Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Arbeitsauslastungsgruppe der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Klassifizierungsfunktion der Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor-classifier-function.md)  
  
  

