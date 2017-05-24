---
title: "Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA) | Microsoft Dokumentation"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e465c19541d7577b19eef3b875697ba843cba000
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>Empfehlungen für Columnstore-Index im Datenbankoptimierungsratgeber (DTA)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 
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

## <a name="see-also"></a>Siehe auch
[Beschreibung von Columnstore-Indizes](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[Datenbankoptimierungsratgeber](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[Tutorial: Datenbankoptimierungsratgeber](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)



  


