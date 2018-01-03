---
title: Hardwarekonfigurationen (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Das Analytics Platform System (APS) Hardware basiert skalierbare Einheiten, damit Sie die richtige Menge an Verarbeitungs- und Ihren geschäftsanforderungen entsprechend erwerben."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: f95945b7-97ae-4ab9-bae5-c792a516acea
caps.latest.revision: "9"
ms.openlocfilehash: 6762775fdec3cd3a01a372ed5c16fbc4a93c1426
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="hardware-configurations"></a>Hardwarekonfigurationen
Das Analytics Platform System (APS) Hardware basiert skalierbare Einheiten, damit Sie die richtige Menge an Verarbeitungs- und Ihren geschäftsanforderungen entsprechend erwerben. Die Appliance skaliert Speicher für SQL Server Parallel Data Wareouse (PDW) aus wenigen Terabytes auf mehr als 6 Petabytes Daten.  
  
## <a name="contents"></a>Inhalt  
  
-   [One-Rack-Konfigurationen](#section1)  
  
-   [Multi-Rack-Konfigurationen](#section2)  

  
## <a name="section1"></a>One-Rack-Konfigurationen  
Das erste Rack in der Einheit enthält die erforderlichen Komponenten für PDW ausführen. Die minimale Einheitenkonfiguration ist ein Rack und Netzwerk sowie eine Basis-Skalierungseinheit. Diese Diagramme zeigen die Weise, dass das erste Rack der Appliance konfiguriert werden kann. Sie können zwischen 2 und 9 Serverknoten in das erste Rack, je nach Hardwarehersteller verwenden.  
  
### <a name="first-rack-configurations---dell"></a>Zuerst – Konfigurationen – DELL Rack  
Mindestkonfiguration für eine DELL-Anwendung verfügt über 3 Serverknoten. Sie können das erste Rack für insgesamt 9 Serverknoten bis zu 2 Daten Skalierungseinheiten hinzufügen.  
  
![Dell erste Rack Konfigurationen](media/first-rack-configurations-dell.png "Dell erste Rack Konfigurationen")  
  
### <a name="first-rack-configurations---hpe"></a>Zuerst Rack-Konfigurationen - HPE  
Mindestkonfiguration für eine Einheit HPE hat 2 Serverknoten. Sie können das erste Rack für insgesamt 8 Serverknoten bis zu 3 Daten Skalierungseinheiten hinzufügen.  
  
![HPE rack zuerst die Konfigurationen für HPE](media/first-rack-configurations-hpe.png "HPE zuerst rack-Konfigurationen")  
  
## <a name="section2"></a>Multi-Rack-Konfigurationen  
Funktionen mit PDW runbookverarbeitung können Sie Daten Skalierungseinheiten, zusammen mit zusätzlichen Rack & Netzwerk Komponenten nach Bedarf, um die richtige Leistungsfähigkeit bereitzustellen hinzufügen, die durch das Netzwerk und rack-Infrastruktur. Jede zusätzliche Rack & Netzwerk ist ein passiven Host erforderlich.  
  
Jede Hardwarehersteller gibt die Anzahl Daten Skalierungseinheiten, die Sie hinzufügen, können die Kapazität Ihrer Appliance angegeben. Es wird empfohlen, ausreichend Daten Skalierungseinheiten um mindestens eine Aufwertung 20 Prozent bei der Leistung finden Sie unter hinzufügen. Angenommen, kommen eine Skalierung von Daten hinzufügen Einheit in einer Anwendung, die bereits von Skalierungseinheiten 20 Daten einer unerheblich Leistungssteigerung. Der Reingewinn wäre nicht zu den Kosten und Aufwand.  
  
### <a name="scale-out-example---hpe"></a>Beispiel: HPE skalieren  
Dieses Diagramm zeigt eine 3 Rack HP-Anwendung, die 20 Serverknoten enthält.  
  
![HPE Appliance mit 20 Serverknoten](media/scale-out-hpe.png "HPE Appliance mit 20 Serverknoten")  
  
### <a name="scale-out-example--dell-quanta"></a>Beispiel – DELL, Quanta Dezentrales Skalieren  
Dieses Diagramm zeigt eine 3 Rack DELL oder Quanta Appliance, die 21 Serverknoten enthält.  
  
![Dell-Einheit mit 21 Serverknoten](media/scale-out-dell.png "Dell-Einheit mit 21 Serverknoten")  
 
