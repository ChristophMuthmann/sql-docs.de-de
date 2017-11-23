---
title: "Festlegen des Partitionsspeichers (Analysis Services – mehrdimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- low latency MOLAP
- standard storage [Analysis Services]
- hybrid OLAP
- automatic MOLAP
- relational OLAP
- multidimensional OLAP
- scheduled MOLAP [Analysis Services]
- partitions [Analysis Services], storage
- HOLAP
- MOLAP
- real time ROLAP
- real time HOLAP
- ROLAP
- medium latency MOLAP
ms.assetid: e525e708-f719-4905-a4cc-20f6a9a3edcd
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4610c996aa58fc71090c5a724447cfe733ede5d7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="set-partition-storage-analysis-services---multidimensional"></a>Festlegen des Partitionsspeichers (Analysis Services – Mehrdimensional)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt mehrere Standardspeicherkonfigurationen für Speichermodi und Zwischenspeicherungsoptionen bereit. Diese stellen häufig genutzte Konfigurationen zur Updatebenachrichtigung, Latenzzeit und Neuerstellung von Daten bereit.  
  
 Sie können den Partitionsspeicher auf der Registerkarte Partitionen des Cubes [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]oder auf der Seite mit der Partitionseigenschaft in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]angeben.  
  
## <a name="guidelines-for-choosing-a-storage-mode"></a>Richtlinien zur Auswahl eines Speichermodus  
 Bei einer großen Measuregruppe empfiehlt es sich, den Speicher für die verschiedenen Partitionen unterschiedlich zu konfigurieren. Beachten Sie die folgenden Richtlinien:  
  
-   Verwenden Sie Echtzeit-ROLAP für aktuelle Daten, die fortwährend aktualisiert werden.  
  
-   Verwenden Sie die proaktive Zwischenspeicherung mit niedrigerer oder mittlerer Latenzzeit für Partitionen, die auf weniger häufig aktualisierten Datenquellen basieren.  
  
-   Verwenden Sie automatische MOLAP für Datenquellen, bei denen die Latenzzeit der Daten weniger wichtig ist als eine hohe Leistungsfähigkeit.  
  
-   Verwenden Sie geplante MOLAP für Datenquellen, bei denen die Benutzer einen kontinuierlichen Zugriff auf die Daten benötigen, Änderungen jedoch nur in regelmäßigen Abständen angezeigt werden müssen.  
  
-   Verwenden Sie die MOLAP-Speicherung ohne proaktive Zwischenspeicherung für Partitionen, die sich selten oder überhaupt nicht ändern, für Partitionen, bei denen die Benutzer nicht die aktuellsten Daten durchsuchen müssen. Verwenden Sie sie auch, wenn die Daten nicht kontinuierlich während notwendiger Updates oder einer erforderlichen Verarbeitung für Benutzer verfügbar sein müssen.  
  
 Das sind allgemeine Richtlinien. Zum Entwickeln des optimalen Speicherschemas für Ihre Daten sind möglicherweise eine sorgfältige Analyse und Tests erforderlich. Darüber hinaus können Sie die Speichereinstellungen für eine Partition manuell konfigurieren, wenn keine der Standardkonfigurationen Ihre Anforderungen erfüllt.  
  
## <a name="storage-settings-descriptions"></a>Beschreibungen der Speichereinstellungen  
  
|Standardspeichereinstellung|Description|  
|------------------------------|-----------------|  
|Echtzeit-ROLAP|OLAP wird in Echtzeit ausgeführt. Detaildaten und Aggregationen werden im relationalen Format gespeichert. Der Server überwacht Benachrichtigungen, wenn Daten geändert werden und alle Abfragen den aktuellen Status der Daten wiedergeben (keine Latenzzeit).<br /><br /> Diese Einstellung wird normalerweise für eine Datenquelle mit sehr häufigen und fortlaufenden Updates verwendet, wenn Benutzer immer die letzten Daten benötigen. Abhängig von den Abfragetypen, die von den Clientanwendungen generiert wurden, sind bei dieser Methode die Antwortzeiten wahrscheinlich am langsamsten.|  
|Echtzeit-HOLAP|OLAP wird in Echtzeit ausgeführt. Detaildaten werden im relationalen Format und Aggregationen werden in einem mehrdimensionalen Format gespeichert. Der Server überwacht Benachrichtigungen, wenn Daten geändert werden und aktualisiert die mehrdimensionalen OLAP-Aggregationen (MOLAP) bei Bedarf. Ein MOLAP-Cache wird nicht erstellt. Bei jedem Update der Datenquelle wechselt der Server zur relationalen Echtzeit-OLAP (ROLAP), bis die Aggregationen aktualisiert werden. Alle Abfragen geben den aktuellen Status der Daten (keine Latenzzeit) wieder.<br /><br /> Diese Einstellung wird in der Regel für eine Datenquelle mit häufigen und fortlaufenden Updates (aber nicht so häufig, dass Echtzeit-ROLAP erforderlich wäre) verwendet, und von den Benutzern werden immer die letzten Daten benötigt. Bei dieser Methode ist normalerweise die Gesamtleistung besser als bei der ROLAP-Speicherung. Wenn die Datenquelle lange genug still ist, können Benutzer mit dieser Einstellung MOLAP-Leistung bekommen.|  
|MOLAP mit niedriger Latenzzeit|Detaildaten und Aggregationen werden im mehrdimensionalen Format gespeichert. Der Server überwacht Benachrichtigungen in Bezug auf Datenänderungen und wechselt zu Echtzeit-ROLAP, während MOLAP-Objekte in einem Cache erneut verarbeitet werden. Vor einem Update des Caches ist ein Ruheintervall von wenigstens 10 Sekunden erforderlich. Wenn das Ruheintervall nicht erreicht wird, gibt es ein Überschreibungsintervall von 10 Minuten. Die Verarbeitung geschieht automatisch bei Änderungen an den Daten. Nach der ersten Änderung beträgt die Latenzzeit 30 Minuten.<br /><br /> Diese Einstellung wird normalerweise für eine Datenquelle mit häufigen Updates verwendet, wenn die Abfrageleistung in gewisser Hinsicht wichtiger ist, als immer die aktuellsten Daten bereitzustellen. Bei dieser Einstellung werden MOLAP-Objekte immer dann automatisch verarbeitet, wenn dies nach dem Latenzzeitintervall erforderlich ist. Während der Neuverarbeitung von MOLAP-Objekten ist die Leistung langsamer.|  
|MOLAP mit mittlerer Latenzzeit|Detaildaten und Aggregationen werden im mehrdimensionalen Format gespeichert. Der Server überwacht Benachrichtigungen in Bezug auf Datenänderungen und wechselt zu Echtzeit-ROLAP, während MOLAP-Objekte im Cache erneut verarbeitet werden. Vor einem Update des Caches ist ein Ruheintervall von wenigstens 10 Sekunden erforderlich. Wenn das Ruheintervall nicht erreicht wird, gibt es ein Überschreibungsintervall von 10 Minuten. Bei Datenänderungen wird die Verarbeitung mit einer Ziellatenzzeit von vier Stunden automatisch durchgeführt.<br /><br /> Diese Einstellung wird normalerweise für eine Datenquelle mit häufigen (oder weniger häufigen) Updates verwendet, wenn die Abfrageleistung wichtiger ist, als immer die aktuellsten Daten bereitzustellen. Bei dieser Einstellung werden MOLAP-Objekte immer dann automatisch verarbeitet, wenn dies nach dem Latenzzeitintervall erforderlich ist. Während der Neuverarbeitung von MOLAP-Objekten ist die Leistung langsamer.|  
|Automatische MOLAP|Detaildaten und Aggregationen werden im mehrdimensionalen Format gespeichert. Der Server überwacht Benachrichtigungen, behält aber den aktuellen MOLAP-Cache bei, während ein neuer erstellt wird. Der Server wechselt nicht zu Echtzeit-OLAP, und während der neue Cache erstellt wird, sind Abfragen möglicherweise veraltet.<br /><br /> Vor dem Erstellen des neuen MOLAP-Cache ist ein Ruheintervall von wenigstens 10 Sekunden erforderlich. Wenn das Ruheintervall nicht erreicht wird, gibt es ein Überschreibungsintervall von 10 Minuten. Bei Datenänderungen wird die Verarbeitung mit einer Ziellatenzzeit von zwei Stunden automatisch durchgeführt.<br /><br /> Diese Einstellung wird normalerweise für Datenquellen verwendet, wenn die Abfrageleistung der wichtigste Faktor ist. Bei dieser Einstellung werden MOLAP-Objekte immer dann automatisch verarbeitet, wenn dies nach dem Latenzzeitintervall erforderlich ist. Abfragen geben nicht die aktuellsten Daten zurück, während der neue Cache erstellt und verarbeitet wird.|  
|Geplante MOLAP|Detaildaten und Aggregationen werden in einem mehrdimensionalen Format gespeichert. Der Server empfängt keine Benachrichtigungen bei Datenänderungen. Die Verarbeitung wird automatisch alle 24 Stunden durchgeführt.<br /><br /> Diese Einstellung wird normalerweise für Datenquellen verwendet, bei denen nur ein tägliches Update erforderlich ist. Abfragen werden immer mit den Daten im MOLAP-Cache ausgeführt, der erst verworfen wird, wenn ein neuer Cache erstellt und die darin befindlichen Objekte verarbeitet wurden.|  
|MOLAP|Proaktives Zwischenspeichern ist nicht aktiviert. Detaildaten und Aggregationen werden im mehrdimensionalen Format gespeichert. Der Server empfängt keine Benachrichtigungen bei Datenänderungen. Die Verarbeitung muss entweder geplant oder manuell ausgeführt werden.<br /><br /> Diese Einstellung wird normalerweise für Datenquellen verwendet, bei denen regelmäßige Updates für die Clientanwendungen nicht erforderlich sind, bei denen jedoch eine hohe Leistung wichtig ist.<br /><br /> Die MOLAP-Speicherung ohne proaktives Zwischenspeichern stellt die bestmögliche Leistung bereit, wenn die Anwendungen nicht die aktuellsten Daten benötigen. Das Verarbeiten von aktualisierten Objekten erfordert Downtime, auch wenn die Downtime durch Aktualisieren und Verarbeiten von Cubes auf einem Stagingserver und durch Verwenden der Datenbanksynchronisierung zum Kopieren der aktualisierten und verarbeiteten MOLAP-Objekte auf dem Produktionsserver auf ein Minimum beschränkt werden kann.|  
  
## <a name="custom-storage-options"></a>Benutzerdefinierte Speicheroptionen  
 Statt eine der Standardspeichereinstellungen zu verwenden, können Sie das Speichern und proaktive Zwischenspeichern manuell konfigurieren. Bevor Sie benutzerdefinierte Speichereinstellungen erstellen, sollten Sie zunächst auf die Option **Standardeinstellung** klicken, und den Schieberegler zu der Standardeinstellung verschieben, die der Konfiguration am ähnlichsten ist, die Sie verwenden möchten. Um anschließend eine benutzerdefinierte Konfiguration zu erstellen, klicken Sie auf die Option **Benutzerdefinierte Einstellungen** und dann auf **Optionen**.  
  
-   Sie können angeben, ob Änderungen in der Datenquelle Updates des Caches auslösen. Um die Belastung durch das Speichern auf ein akzeptables Maß zu begrenzen, können Sie ein Ruheintervall mit einer Mindestdauer angeben, das nach den Updates der Datenquelle eingehalten wird. Sie können ein Ruheintervall auch so angeben, dass der Cache nach einer bestimmten Zeit aktualisiert wird, wenn das Intervall zwischen den Änderungen der Datenquelle nie das Minimum erreicht.  
  
-   Sie können angeben, ob der veraltete Cacheinhalt bei Updates gelöscht werden soll. Bei Auswahl dieser Option geschieht Folgendes: Wenn die festgelegte Latenzzeit überschritten wird, schaltet der Server zu relationaler OLAP (ROLAP) in Echtzeit um, während er den Cache aktualisiert. Wenn Sie diese Option nicht auswählen, fährt der Server fort, den veralteten mehrdimensionalen OLAP-Cache (MOLAP) abzufragen, während ein neuer erstellt wird.  
  
     Sie können die Länge des Latenzzeitintervalls angeben, das zwischen dem Ändern und Löschen des veralteten Caches liegen soll. Das ist die Zeit, während der Benutzer den veralteten Cache noch durchsuchen können, bevor er gelöscht wird. Wenn Änderungen auftreten, während der Cache aktualisiert oder am Ende dieses Intervalls verarbeitet wird, werden Abfragen an ROLAP umgeleitet.  
  
-   Sie können erzwungene Updates des Cache planen, wenn Sie die zwischengespeicherten MOLAP-Objekte unabhängig von den Änderungen der Datenquelle periodisch aktualisieren möchten. Echtzeit-OLAP-Vorteile variieren in Abhängigkeit der Größe der Datenbank und der Häufigkeit der durch Datenquellenänderungen zugeordneten Latenzzeitperiode. Benutzer sollen so oft wie möglich Abfragen an einen Cache und nicht an ROLAP schicken.  
  
 Wenn Sie das Kontrollkästchen **Einstellungen auf Dimensionen anwenden** aktivieren, werden dieselben Speichereinstellungen auf die mit der Measuregruppe verknüpften Dimensionen angewendet. Die Dimensionswerte sind zu Beginn identisch mit den Partitionswerten.  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)  
  
  
