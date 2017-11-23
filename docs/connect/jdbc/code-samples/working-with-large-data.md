---
title: Arbeiten mit umfangreichen Daten | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: c8195decee231a628599e42d2f44109ff0452ed8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="working-with-large-data"></a>Arbeiten mit umfangreichen Daten
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Der JDBC-Treiber bietet Unterstützung für die adaptive Pufferung, mit der Sie beliebige Daten mit umfangreichen Werten ohne den Aufwand von Servercursorn abrufen können. Mit adaptiver Pufferung der [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] ruft Ergebnisse aus der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ab, wenn die Anwendung benötigt, anstatt alle auf einmal abzurufen. Der Treiber verwirft außerdem die Ergebnisse, sobald die Anwendung nicht mehr auf sie zugreifen kann.  
  
 In der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] JDBC Driver, Version 1.2, war der pufferungsmodus "**vollständige**" standardmäßig. Wenn Ihre Anwendung die Verbindungseigenschaft "ResponseBuffering" nicht, um festgelegt haben "**adaptive**" in den Verbindungseigenschaften oder mit der [SetResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) Methode der [ SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) -Objekt, das der Treiber unterstützt beim Lesen des gesamten Resultsets auf einmal vom Server. Um das Verhalten der adaptiven Pufferung, Ihre Anwendung musste "ResponseBuffering"-Verbindungseigenschaft auf setzen "**adaptive**" explizit.  
  
 Die **adaptive** Wert ist der standardpuffermodus und der JDBC-Treiber puffert wenig Daten wie möglichen bei Bedarf. Weitere Informationen zum Verwenden der adaptiven Pufferung finden Sie unter [mithilfe der adaptiven Pufferung](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Die Themen in diesem Abschnitt beschreiben verschiedene Möglichkeiten, die Sie verwenden können, zum Abrufen von Daten mit umfangreichen Werten aus einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datenbank.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Beispiel zum Lesen umfangreicher Daten](../../../connect/jdbc/reading-large-data-sample.md)|Beschreibt die Verwendung einer SQL-Anweisung zum Abrufen von Daten mit umfangreichen Werten.|  
|[Beispiel zum Lesen umfangreicher Daten mit gespeicherten Prozeduren](../../../connect/jdbc/reading-large-data-with-stored-procedures-sample.md)|Beschreibt das Abrufen eines umfangreichen CallableStatement OUT-Parameterwerts.|  
|[Beispiel zum Aktualisieren umfangreicher Daten](../../../connect/jdbc/updating-large-data-sample.md)|Beschreibt das Aktualisieren von Daten mit umfangreichen Werten in einer Datenbank.|  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiele für JDBC-Treiberanwendungen](../../../connect/jdbc/sample-jdbc-driver-applications.md)  
  
  
