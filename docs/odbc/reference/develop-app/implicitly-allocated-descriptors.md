---
title: Implizit reserviert Deskriptoren | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d805b110453c5fe0bb5be8c8df067c09ff8146e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="implicitly-allocated-descriptors"></a>Implizit zugeordneten Deskriptoren
Wenn ein Anweisungshandle zugeordnet ist, weist die Anwendung implizit einen Satz von vier Deskriptoren. Die Anwendung erhalten die Handles dieser Deskriptoren implizit als Attribute des Anweisungshandles zugeordnet. Wenn die Anwendung das Anweisungshandle frei, gibt der Treiber alle implizit zugeordnete Deskriptoren auf dieses Handle frei.
