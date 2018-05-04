---
title: WMI-Anbieter für Serverereignisse Klassen und Eigenschaften | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- event classes [WMI]
- WMI Provider for Server Events, events listed
- classes [WMI]
ms.assetid: e2916cd7-a3ed-41e6-97b4-2ee060754cbe
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3514bd676b6b84436141cdcf669cc6c8f33598e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="wmi-provider-for-server-events-classes-and-properties"></a>Klassen und Eigenschaften für den WMI-Anbieter für Serverereignisse
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Die folgenden Serverereignisse bilden das Programmiermodell für den WMI-Anbieter für Serverereignisse. Es gibt zwei Hauptkategorien von Ereignissen, die durch Absetzen von WQL-Abfragen an den Anbieter abgefragt werden können: DDL-Ereignisse (Data Definition Language) und Ablaufverfolgungsereignisse. Auch die Service Broker-Ereignisse QUEUE_ACTIVATION und BROKER_QUEUE_DISABLED können abgefragt werden. Beachten Sie den inklusiven Charakter der folgenden Strukturdiagramme. Das DDL_ASSEMBLY_EVENTS-Ereignis schließt z. B. beliebige Ereignisse vom Typ ALTER_ASSEMBLY, CREATE_ASSEMBLY und DROP_ASSEMBLY ein. Analog dazu schließt das TRC_FULL_TEXT-Ereignis beliebige Ereignisse vom Typ FT_CRAWL_ABORTED, FT_CRAWL_STARTED und FT_CRAWL_STOPPED ein. ALL_EVENTS deckt alle DDL-Ereignisse, Ablaufverfolgungsereignisse, QUEUE_ACTIVATION und BROKER_QUEUE_DISABLED ab.  
  
 Um zu ermitteln, welche Eigenschaften aus einem Ereignis oder einer Ereignisgruppe abgefragt werden können, konsultieren Sie das Ereignisschema. Standardmäßig wird das Ereignisschema im folgenden Verzeichnis installiert: [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] Tools\Binn\schemas\sqlserver\2006\11\events\events .xsd.  
  
 Sie können alternativ finden Sie in auf veröffentlichte Ereignisschema [ http://schemas.microsoft.com/sqlserver ](http://go.microsoft.com/fwlink/?linkid=43100).  
  
 Z. B. durch einen Verweis auf das ALTER_DATABASE-Ereignis, erfahren Sie, dass das übergeordnete Ereignis DDL_SERVER_LEVEL_EVENTS ist und seine Eigenschaften werden **TSQLCommand** und **DatabaseName**. Das Ereignis erbt auch die Eigenschaften **%SQLInstance**, **PostTime**, **ComputerName**, **SPID**, und **LoginName** . Das Ereignis verfügt über keinen untergeordneten Ereignisse.  
  
> [!NOTE]  
>  Gespeicherte Systemprozeduren, die DDL-ähnliche Vorgänge ausführen, können auch Ereignisbenachrichtigungen auslösen. Testen Sie die Ereignisbenachrichtigungen, um ihre Reaktion auf gespeicherte Systemprozeduren, die ausgeführt werden, zu bestimmen. Beispielsweise die CREATE TYPE-Anweisung und **Sp_addtype** gespeicherten Prozedur werden beide auslösen eine ereignisbenachrichtigung, die für ein CREATE_TYPE-Ereignis erstellt wird. Weitere Informationen finden Sie unter[DDL-Ereignisse](../../relational-databases/triggers/ddl-events.md).  
  
 **Data Definition Language-Ereignisse und Ereignisgruppen**  
  
 ![WMI-Anbieter für Serverereignisse-Ereignisstruktur](../../relational-databases/wmi-provider-server-events/media/sql-wmi-ddl-events-ktm.gif "WMI-Anbieter für Serverereignisse-Ereignisstruktur")  
  
 **Ablaufverfolgungsereignisse und Ereignisgruppen**  
  
 ![Verfolgen Sie Ereignisse und Ereignisgruppen](../../relational-databases/wmi-provider-server-events/media/sql-wmi-trc-all-events.gif "Ablaufverfolgungsinformationen Ereignisse und Ereignisgruppen")  
  
## <a name="see-also"></a>Siehe auch  
 [WMI-Anbieter für Server-Ereignisse-Konzepte](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)   
 [Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](../../relational-databases/wmi-provider-server-events/using-wql-with-the-wmi-provider-for-server-events.md)  
  
  
