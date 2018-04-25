---
title: Kenntnisse der Unterschiede von Datentypen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf10944059322a159de43ccee2a7e4d8ed1d8526
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-data-type-differences"></a>Grundlegendes zu den Unterschieden von Datentypen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Es gibt eine Reihe von Unterschieden zwischen den Java-Datentypen und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Datentypen. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] berücksichtigt diese Unterschiede durch verschiedenartige Konvertierungen.  
  
## <a name="character-types"></a>Zeichentypen  
 Der JDBC-Zeichenfolgentypen werden **CHAR**, **VARCHAR**, und **LONGVARCHAR**. Der JDBC-Treiber unterstützt die JDBC 4.0-API. In JDBC 4.0 sind auch die JDBC-Zeichenfolgentypen sein können **NCHAR**, **NVARCHAR**, und **LONGNVARCHAR**. Diese neuen Zeichenfolgentypen verwalten die systemeigenen Java-Zeichentypen im Unicode-Format, sodass keine Konvertierung von ANSI nach Unicode und Unicode nach ANSI mehr erforderlich ist.  
  
|Typ|Description|  
|----------|-----------------|  
|Feste Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Char** und **Nchar** Datentypen zugeordnet werden, direkt an den JDBC **CHAR** und **NCHAR** Typen. Diese Typen weisen eine feste Länge auf und werden vom Server mit Leerstellen aufgefüllt, wenn für die Spalte SET ANSI_PADDING ON festgelegt wurde. Die Auffüllung mit Leerstellen ist für **immer aktiviert. Bei** fügt der JDBC-Treiber die Leerstellen jedoch nur hinzu, wenn die char-Spalten des Servers nicht aufgefüllt wurden.|  
|Variable Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varchar** und **Nvarchar** Typen sind direkt den JDBC **VARCHAR** und **NVARCHAR** bzw. die Argumenttypen.|  
|Long|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Text** und **Ntext** Typen zuordnen, um die JDBC **LONGVARCHAR** und **LONGNVARCHAR** vom Typ. Diese sind als veraltet markierte Typen ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], weshalb Sie große Werttypen verwenden sollten **varchar(max)** oder **nvarchar(max)**, stattdessen.<br /><br /> Verwenden das Update\<numerischen Typ > und [UpdateObject (Int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) -Methode treten für **Text** und **Ntext** -Serverspalten. Allerdings wird die Verwendung der setObject[-Methode mit Angabe eines Zeichenkonvertierungstyps für ](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)- und **-Serverspalten unterstützt.|  
  
## <a name="binary-string-types"></a>Binäre Zeichenfolgetypen  
 Die binären JDBC-Zeichenfolgentypen werden **BINÄRE**, **VARBINARY**, und **"LONGVARBINARY"**.  
  
|Typ|Description|  
|----------|-----------------|  
|Feste Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **binäre** geben Zuordnungen direkt an den JDBC **BINÄRE** Typ. Dieser Typ weist eine feste Länge auf und wird vom Server mit Leerstellen aufgefüllt, wenn für die Spalte SET ANSI_PADDING ON eingestellt wurde. Wenn die Zeichenspalten des Servers nicht mit Leerstellen aufgefüllt sind, fügt der JDBC-Treiber die Leerstellen hinzu.<br /><br /> Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Zeitstempel** Typ ist ein JDBC **BINÄRE** Typ mit einer festen Länge von 8 Bytes.|  
|Variable Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varbinary** geben Zuordnungen in der JDBC **VARBINARY** Typ.<br /><br /> Die **Udt** Geben Sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in JDBC ordnet eine **VARBINARY** Typ.|  
|Long|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Image** geben Zuordnungen in der JDBC **"LONGVARBINARY"** Typ. Dieser Typ ist ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] veraltet, sodass Sie stattdessen einen Typ mit umfangreichen Werten, d. h. **, verwenden sollten.|  
  
## <a name="exact-numeric-types"></a>Exakte numerische Typen  
 Die exakten numerischen JDBC-Typen sind direkt den entsprechenden SQL Server-Typen zugeordnet.  
  
|Typ|Description|  
|----------|-----------------|  
|BIT|Der JDBC-Typ ** stellt ein Bit dar, das 0 oder 1 sein kann. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Bit** Typ.|  
|TINYINT|Der JDBC-Typ ** stellt ein einzelnes Byte dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"tinyint"** Typ.|  
|SMALLINT|Der JDBC-Typ ** stellt eine 16-Bit-Ganzzahl mit Vorzeichen dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"smallint"** Typ.|  
|INTEGER|Der JDBC-Typ ** stellt eine 32-Bit-Ganzzahl mit Vorzeichen dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Int** Typ.|  
|bigint|Der JDBC-Typ ** stellt eine 64-Bit-Ganzzahl mit Vorzeichen dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"bigint"** Typ.|  
|NUMERIC|Der JDBC-Typ ** stellt einen Dezimalwert fester Genauigkeit dar, der Werte mit identischer Genauigkeit enthält. Die **numerischen** Typ ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **numerischen** Typ.|  
|DECIMAL|Der JDBC-Typ ** stellt einen Dezimalwert fester Genauigkeit dar, der Werte mit mindestens der angegebenen Genauigkeit enthält. Die **DECIMAL** Typ ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **decimal** Typ.<br /><br /> Der JDBC-Typ **ist außerdem den**-Typen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und ** zugeordnet. Dabei handelt es sich um spezielle Dezimaltypen fester Genauigkeit, die in 8 bzw. 4 Bytes gespeichert werden.|  
  
## <a name="approximate-numeric-types"></a>Angenäherte numerische Typen  
 Die angenäherten numerischen JDBC-Typen sind **echte**, **doppelte**, und **FLOAT**.  
  
|Typ|Description|  
|----------|-----------------|  
|real|Der JDBC-Typ **weist sieben Ziffern für die Genauigkeit auf (einfache Genauigkeit) und ist dem**-Typ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] zugeordnet.|  
|DOUBLE|Der JDBC-Typ **weist 15 Ziffern für die Genauigkeit auf (doppelte Genauigkeit) und ist dem**-Typ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] zugeordnet. Der JDBC **FLOAT** Typ ist ein Synonym für **doppelte**. Da zwischen Verwechslungen **FLOAT** und **doppelte**, **doppelte** wird bevorzugt.|  
  
## <a name="datetime-types"></a>Datum-/Zeittypen  
 Der JDBC **Zeitstempel** Typ ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"DateTime"** und **Smalldatetime** Typen. Der **-Typ wird in zwei integer-Werten mit einer Länge von 4 Byte gespeichert. Der **-Typ enthält die gleichen Informationen (Datum und Uhrzeit), allerdings mit geringerer Genauigkeit in zwei integer-Werten mit einer Länge von 2 Byte.  
  
> [!NOTE]  
>  Bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Typ ** handelt es sich um einen binären Zeichenfolgetyp mit fester Länge. Es ist nicht an ein beliebiges der JDBC-Typen zugeordnet: **Datum**, **Zeit**, oder **Zeitstempel**.  
  
## <a name="custom-type-mapping"></a>Benutzerdefinierte Typzuordnung  
 Die Zuordnungsfunktion für benutzerdefinierte Typen von JDBC, die die -Schnittstellen für die erweiterten JDBC-Typen (UDTs, Struct usw.) verwendet, ist im JDBC-Treiber nicht implementiert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
