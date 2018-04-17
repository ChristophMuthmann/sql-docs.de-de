---
title: Datenquellen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data sources [ODBC]
- data sources [ODBC], about data sources
ms.assetid: 4ae44fa2-0b9b-4e19-ab45-c1dc93b68406
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b16699f67a74232730b2b96a2fdeeb4545d1fe46
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="data-sources"></a>Datenquellen
Ein *Datenquelle* ist einfach die Quelle der Daten. Sie können eine Datei, die eine bestimmte Datenbank auf einem DBMS oder sogar einem live-Datenfeed sein. Daten können sich auf demselben Computer wie das Programm oder auf einem anderen Computer an einer beliebigen Stelle in einem Netzwerk sein. Z. B. möglicherweise eine Datenquelle eine Oracle-DBMS, die unter einem Betriebssystem OS/2®, Novell® Netware zugreift; eine IBM DB2-DBMS erfolgt über ein Gateway; eine Auflistung von Xbase-Dateien in einem Serververzeichnis; oder eine lokale Microsoft® Access-Datenbankdatei.  
  
 Der Zweck einer Datenquelle gehört, das alle technischen Informationen benötigt Zugriff auf die Daten zu erfassen – der Treibername, Netzwerkadresse, Netzwerksoftware usw. – zu einem einzelnen platzieren, und blenden Sie es dem Benutzer. Der Benutzer sollte sein können betrachten Sie eine Liste, die Lohnbuchhaltung, Bestandsinformationen und Mitarbeiter enthält, Payroll aus der Liste auswählen und die Anwendung die Gehaltsdaten herstellen, ohne zu wissen, wo die Daten zu Gehältern befindet, oder wie die Anwendung darauf gelangt.  
  
 Der Begriff *Datenquelle* darf nicht mit ähnlichen Begriffe verwechselt werden. In diesem Handbuch *DBMS* oder *Datenbank* bezieht sich auf eine Datenbankprogramm oder Modul. Ein weiterer Unterschied besteht zwischen *Desktopdatenbanken,* entworfen auf PCs ausgeführt werden und häufig fehlen in vollständiges SQL und Unterstützung von Transaktionen und *Serverdatenbanken,* in einem Client ausgeführt / Server-Situation und gekennzeichnet durch ein eigenständiges Datenbankmodul und umfangreiche SQL und Unterstützung von Transaktionen. *Datenbank* bezieht sich auch auf eine bestimmte Sammlung von Daten, z. B. eine Auflistung von Xbase-Dateien in einem Verzeichnis oder eine Datenbank auf SQL Server. Dies entspricht im Allgemeinen der Begriff *Katalog* an anderer Stelle in diesem Handbuch oder der Begriff verwendet *Qualifizierer* in früheren Versionen von ODBC.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Typen von Datenquellen](../../odbc/reference/types-of-data-sources.md)  
  
-   [Verwenden von Datenquellen](../../odbc/reference/using-data-sources.md)  
  
-   [Beispiel für Datenquellen](../../odbc/reference/data-source-example.md)
