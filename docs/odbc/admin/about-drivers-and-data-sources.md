---
title: Informationen zu Treibern und Datenquellen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79ae9e95ce31df371366e9073cb36f88c5bd9ece
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="about-drivers-and-data-sources"></a>Informationen zu Treibern und Datenquellen
*Treiber* sind die Komponenten, die ODBC-Anforderungen zu verarbeiten und Daten an die Anwendung zurückgegeben. Ggf. ändern, Treiber die Anforderung einer Anwendung in ein Formular, das von der Datenquelle im Klaren sind. Sie müssen den Treiber-Setup-Programm verwenden, hinzufügen oder Löschen einen Treiber von Ihrem Computer.  
  
 *Datenquellen* Datenbanken oder Dateien, die von einem Treiber zugegriffen werden und werden durch einen Datenquellennamen (DSN) identifiziert. Verwenden Sie die ODBC-Datenquellen-Administrator hinzufügen, konfigurieren und Löschen von Datenquellen aus dem System. Die Typen von Datenquellen, die verwendet werden können, werden in der folgenden Tabelle beschrieben.  
  
|Datenquelle|Description|  
|-----------------|-----------------|  
|Benutzer|Benutzer-DSNs werden lokal auf einem Computer und können nur vom aktuellen Benutzer verwendet werden. Sie werden in der HKEY_CURRENT_USER-Registrierungsunterstruktur registriert.|  
|System|System-DSNs werden lokal auf einem Computer statt einem Benutzer zugeordnet. Das System oder jeder Benutzer mit Berechtigungen können eine Datenquelle mit einer System-DSN einrichten. System-DSNs werden in der HKEY_LOCAL_MACHINE-Unterstruktur der Registrierung registriert.|  
|File|Datei-DSNs werden dateibasierte Datenquellen, die für alle Benutzer, die die gleichen Treiber installiert wurden freigegeben werden können und daher haben Zugriff auf die Datenbank. Diese Datenquellen müssen nicht ausschließlich für einen Benutzer noch lokal auf einem Computer. Datei-Datenquellennamen von dedizierten Registrierungseinträge nicht erkannt; Stattdessen werden sie durch einen Dateinamen mit der Erweiterung DSN identifiziert.|  
  
 Benutzer und System-Datenquellen werden zusammenfassend als bezeichnet *Computer* -Datenquellen, da sie lokal auf einem Computer befinden.  
  
 Jede dieser Datenquellen verfügt über eine Registerkarte der **ODBC-Datenquellenadministrator** (Dialogfeld). Weitere Informationen zu Datenquellen finden Sie unter [Datenquellen](../../odbc/reference/data-sources.md).

