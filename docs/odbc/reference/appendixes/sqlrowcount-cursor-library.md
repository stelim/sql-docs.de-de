---
title: SQLRowCount (Cursor Library) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2125d299570c3e5b381a6bfa5500b5b5e61636f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772028"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (Cursorbibliothek)
> [!IMPORTANT]  
>  Dieses Feature wird in einer zukünftigen Version von Windows entfernt werden. Zu vermeiden Sie, verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Änderung von Anwendungen, die derzeit auf dieses Feature verwenden möchten. Microsoft empfiehlt die Verwendung von Cursor-Funktionalität des Treibers.  
  
 In diesem Thema erläutert die Verwendung von der **SQLRowCount** -Funktion in der Cursorbibliothek. Allgemeine Informationen zur **SQLRowCount**, finden Sie unter [SQLRowCount-Funktion](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Wenn eine Anwendung ruft **SQLRowCount** mit der Anweisung, die dem Cursor zugeordnet wird, gibt die Cursorbibliothek die Anzahl der Zeilen mit Daten, die er, aus dem Treiber abgerufen hat.  
  
 Wenn eine Anwendung ruft **SQLRowCount** mit der Anweisung ein positioniertes Update oder Delete-Anweisung zugeordnet ist, gibt die Cursorbibliothek die Anzahl der Zeilen, die von der Anweisung betroffen sind.  
  
 Wenn eine Anwendung ruft **SQLRowCount** nach einer **auswählen** -Anweisung, die Cursorbibliothek gibt-1 zurück.
