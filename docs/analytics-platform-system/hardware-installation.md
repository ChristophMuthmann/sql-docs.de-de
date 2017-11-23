---
title: Hardwareinstallation (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4f612b9-f320-4391-952b-d3696cfbe2e2
caps.latest.revision: "17"
ms.openlocfilehash: 9eb9fc0c1249c63550c33f09ac357c519d93bd7f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="hardware-installation"></a>Hardwareinstallation
Dieses Thema beschreibt, wie verschieben, entpacken und die Hardware für die SQL Server PDW Appliance zu installieren. In diesem Thema dient nur zu Informationszwecken und soll Ihnen helfen, den Prozess zu verstehen. Ihre Anwendung sollte entpackt, installiert werden, und überprüft, bevor sie Ihnen über aktiviert ist. Kunden die Teilnahme ist erforderlich, damit Elemente wie z. B. Daten zugreifen, Stromversorgung und Ethernet-Verbindungen zu zentrieren.  
  
## <a name="BeforeMoving"></a>Bevor Sie alle Komponenten von der Ladestation verschieben  
Führen Sie die folgenden Aufgaben aus, bevor Sie verschieben, entpacken oder rack Appliance-Komponenten.  
  
|Task|Description|  
|--------|---------------|  
|Stellen Sie sicher, dass alle Komponenten angekommen sind|Verwenden Sie die Rechnung von Materialien (BOM), um sicherzustellen, dass alle Komponenten angekommen und befinden sich auf ihre Paletten am empfangenden Dock für Ihr Datencenter.|  
|Stellen Sie sicher, dass das Rechenzentrum alle für das Gerät erfüllt|Starten Sie diesen Task, indem Hardwarespezifikationen überprüfen und Verkabelung Diagramme, die von Ihrem IHV bereitstellen. Die nächsten Schritte finden Sie Einzelheiten zu Rack erforderliche Speicherplatz und Konnektivität.|  
|Stellen Sie sicher, dass das Rechenzentrum ordnungsgemäße Rack Speicherplatz verfügt|Stellen Sie sicher, dass das Rechenzentrum genügend Speicherplatz für alle von der Einheit Racks verfügt.<br /><br />Stellen Sie sicher, dass das Gestell Platz leer sind und für die Appliance Racks den Empfang bereit ist.|  
|Stellen Sie sicher, dass das Rechenzentrum Konnektivität erfüllt|Stellen Sie sicher, dass das Rechenzentrum die Verkabelung in den Diagrammen Verkabelung erfüllt.<br /><br />Stellen Sie sicher, dass sich Platz für alle Kabel und Netzkabel nach Appliance Knoten eingerichtet werden.|  
|Überprüft, ob die Etagen zwischen Docks und den Regalen Gewichtung Anforderungen erfüllen|Stellen Sie sicher, dass alle Material zwischen Paletten und den Regalen die Gewichtung der Knoten Appliance, besonders in Rechenzentren mit ausgelöste Etagen unterstützen kann.<br /><br />Wenden Sie sich an Ihrem IHV Informationen für die Gewichtung der einzelnen Komponenten.|  
|Sichern Sie das Rechenzentrum Gestell|Sichern Sie das Rechenzentrum Rack über zusätzliche Geräte nach Bedarf für Ihre rechenzentrumstandorts, z. B. Erdbeben Schultergurte in geografischen Bereichen anfällig für Erdbeben durchgeführt.|  
|Unterstützung für das Transportieren von Komponenten vorbereiten|Im Voraus bestimmen Sie, welche um Unterstützung zu erhalten, Geräte und Tools, die jede Komponente auf sichere Weise und ohne dass Schäden verursacht behandelt werden sollen.|  
  
## <a name="Moving"></a>Verschieben Sie die Regalen von der Ladestation in das Rechenzentrum  
Jede Palette enthält alle Komponenten für eine Einheit Rack, einschließlich der Knoten, Kabel, Kabel usw. an.  
  
Verwenden Sie die folgende Checkliste, um jedes Rack Einheit aus der Palette an der Ladestation an ihrem Speicherort Rack im Datencenter zu verschieben. Verschieben Sie zunächst das Gestell Steuerelement, und verschieben Sie die Appliance Daten Racks.  
  
> [!WARNING]  
> Um diese Schritte genau wie beschrieben ausführen kann Bestimmung Schäden, Schäden an der SQL Server PDW Appliance oder anderen Problemen kommen.  
>   
> Nie Versuch, heben oder ein Knoten Appliance oder andere starker Komponente ohne Unterstützung nach "oder mit einem richtigen Gerät zu verschieben. Wenden Sie sich an Ihrem IHV Informationen für die Gewichtung der einzelnen Komponenten, damit Sie im Voraus ermitteln können, welche um Unterstützung zu erhalten, Geräte und Tools, die jede Komponente auf sichere Weise und ohne dass Schäden verursacht behandelt werden sollen.  
  
|Task|Description|  
|--------|---------------|  
|Stellen Sie sicher, dass die Palette Ebene ist.|Bevor Sie beginnen, zu verschieben, oder Entpacken die Palette, achten Sie darauf, dass er sich auf Ebene Ground befindet.|  
|Unbolt einen Knoten aus der Palette|Starten oben auf der Palette, unbolt den obersten Knoten aus der Palette.|  
|Verschieben Sie den Knoten zu einem Nachläuferachse oder der Einkaufswagen, die die Gewichtung unterstützen kann|Verwenden Sie Rampen und Techniken für den richtigen Aufhebung/verschieben, verschieben den Knoten zu einem Nachläuferachse oder der Einkaufswagen, die die Gewichtung unterstützen kann.|  
|Den Knoten in dem Rechenzentrum Transport|Verwenden Sie ordnungsgemäße Aufhebung/verschieben-Techniken, um die Knoten in der Position in der Data Center Gestell verschoben werden.|  
|Sichern Sie den Knoten im Rechenzentrum Gestell|Sichern Sie den Knoten direkt in das Rechenzentrum Gestell.|  
|Wiederholen Sie diese Schritte für den nächsten Knoten oder Komponente|Wiederholen Sie diese Schritte aus, um den nächsten Knoten oder eine andere Einheit-Komponente in das Rechenzentrum zu verschieben.|  
  
## <a name="AfterMoving"></a>Weitere Komponenten installieren  
Verwenden Sie die folgende Checkliste, um die zusätzlichen Komponenten zu installieren.  
  
|Task|Description||  
|--------|---------------|-|  
|Entpacken und rack-Netzwerkswitches und PDUs|Verwenden Sie die Rack Diagramme, um die Netzwerkswitches und PDUs am richtigen Speicherort in das Gestell einzufügen.||  
|Verbinden Sie die Infiniband und Ethernet-Kabel gemäß der Kabel Bezeichnungen|Betrachten Sie hierzu die Verkabelung Diagramm. Jedes Kabel hat die Bezeichnung an jedem Ende, der angibt, in denen er verbunden sein muss.||  
|Schließen Sie alle Netzkabel|Betrachten Sie hierzu die Verkabelung Diagramm.||  
|Aktivieren Sie die Stromversorgung erneut mit den Regalen und die PDUs|Verbinden Sie die Stromversorgung erneut mit den Regalen und aus den Regalen an die PDUs. **Schalten Sie nicht auf einem anderen Gerät Komponenten zu diesem Zeitpunkt.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
