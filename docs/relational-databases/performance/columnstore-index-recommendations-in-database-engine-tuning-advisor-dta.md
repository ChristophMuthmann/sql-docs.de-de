---
title: "Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA) | Microsoft Dokumentation"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 887b3134a4c8dee933e46b9501e7622f678325fc
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

 
  Data-Warehousing und analytische Arbeitsauslastungen können in hohem Maße von [Columnstore-Indizes](../../t-sql/statements/create-columnstore-index-transact-sql.md) sowie von herkömmlichen Rowstore-Indizes profitieren. Die Wahl der Rowstore und Columnstore-Indizes für die Erstellung Ihrer Datenbank, hängt von der Arbeitsauslastung Ihrer Anwendung ab. In SQL Server 2016 kann der [Database Engine Tuning Advisor (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) Ihre Arbeitsauslastung analysieren, und eine Empfehlung bestehend aus einer Kombination von Rowstore und Columnstore-Indizes zum Erstellen Ihrer Datenbank ausgeben. 
  
 Dieses Feature ist in SQL Server Management Studio, Version **16.4** oder höher verfügbar. 
  
## <a name="how-to-enable-columnstore-index-recommendations-in-database-engine-tuning-advisor-gui"></a>Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (GUI) ermöglichen

  
  1. Starten Sie den Datenbankoptimierungsratgeber, und öffnen Sie eine neue Optimierungssitzung.
  
  2. Wählen Sie eine oder mehrere Datenbanken und die Arbeitsauslastung für die Optimierung im Bereich **Allgemein** aus.
  
  3. Im Bereich „Optimierungsoptionen“ aktivieren Sie das Kontrollkästchen **Columnstore-Indizes empfehlen** (siehe Abbildung unten).
  ![DTA Columnstore-Indizes Optimierungsoption](../../relational-databases/performance/media/dta-columnstore-indexes-tuning-option.gif)
 
  4. Wählen Sie andere Optimierungsoptionen, und klicken Sie anschließend auf die Schaltfläche **Analyse starten**.
  
  5. Nach Abschluss der Optimierung zeigen Sie alle Empfehlungen, einschließlich aller Columnstore-Indizes im Bereich **Empfehlungen** an (siehe Abbildung unten).      
  ![DTA Columnstore-Indexempfehlung](../../relational-databases/performance/media/dta-columnstore-index-recommendation.gif)
  
  6. Klicken Sie auf den Link **Definition** zum Anzeigen der SQL (Data Definition Language, Datendefinitionssprache)-Anweisung, die den empfohlenen Index erstellen kann. DTA verwendet standardmäßig das Suffix **Col** im Namen des Columnestore-Index, um die Identifizierung von Columnstore-Indizes zu erleichtern (siehe Abbildung unten).
  ![Definition des DTA Columnstore-Index](../../relational-databases/performance/media/dta-columnstore-index-definition.gif) 
  
  
  ## <a name="how-to-enable-columnstore-index-recommendations-in-dtaexe-utility"></a>Aktivieren von Columnstore-Index-Empfehlungen im dta.exe-Hilfsprogramm

Verwenden Sie zum Aktivieren von Columnstore Empfehlungen bei Verwendung des Befehlszeilen-Hilfsprogramms „dta.exe“ die **-fc**-Befehlszeilenparameter.

Weitere Informationen zum Befehlszeilen-Hilfsprogramm „dta.exe“ finden Sie unter [Hilfsprogramm dta](../../tools/dta/dta-utility.md)

## <a name="see-also"></a>Weitere Informationen finden Sie unter
[Beschreibung von Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[Tutorial: Datenbankoptimierungsratgeber](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)



  

