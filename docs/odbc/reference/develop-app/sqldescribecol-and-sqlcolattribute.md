---
title: SQLDescribeCol und SQLColAttribute | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e569e51540cbaa5612b158abdacac5faae77f940
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722628"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol und SQLColAttribute
**SQLDescribeCol** und **SQLColAttribute** werden verwendet, um die resultsetmetadaten abzurufen. Der Unterschied zwischen diesen beiden Funktionen besteht darin, die **SQLDescribeCol** gibt immer die gleichen fünf Angaben (eines Spaltenwerts Namen, Datentyp, Genauigkeit, Dezimalstellen und NULL-Zulässigkeit), während **SQLColAttribute** gibt ein einzelnes Stück von der Anwendung angeforderten Informationen. Allerdings **SQLColAttribute** kann eine viel umfangreichere Auswahl von Metadaten, einschließlich eines Spaltenwerts Groß-/Kleinschreibung zurückgegeben, Größe, aktualisierbarkeit und Auffindbarkeit anzuzeigen.  
  
 Viele Anwendungen, vor allem solche, die Daten nur anzeigen erfordern, nur die Metadaten, die vom **SQLDescribeCol**. Für diese Anwendungen wird schneller verwenden **SQLDescribeCol** als **SQLColAttribute** da die Informationen in einem einzelnen Aufruf zurückgegeben wird. Andere Anwendungen, vor allem solche, die Daten zu aktualisieren, benötigen die zusätzliche Metadaten, die vom **SQLColAttribute** und daher beide Funktionen verwenden. Darüber hinaus **SQLColAttribute** unterstützt der Treiber-spezifische Metadaten; Weitere Informationen finden Sie unter [treiberspezifische Datentypen, Deskriptortypen, Informationstypen, Diagnosetypen und Attribute](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Eine Anwendung kann die resultsetmetadaten abrufen, zu einem beliebigen Zeitpunkt, nachdem eine Anweisung vorbereitet oder ausgeführt wurde und bevor Sie den Cursor über das Ergebnis Satz geschlossen ist. Nur sehr wenige Anwendungen erfordern Ergebnis Metadaten festzulegen, nachdem die Anweisung vorbereitet wurde und bevor er ausgeführt wird. Wenn möglich, sollten Anwendungen zum Abrufen von Metadaten erst, nachdem die Anweisung ausgeführt wird, da einige Datenquellen können keine Metadaten für vorbereitete Anweisungen zurückgeben und Emulieren von dieser Funktion in der Treiber häufig als langwieriger Prozess wird, warten. Zum Beispiel generiert der Treiber kann ein Resultset von 0 (null) Zeilen durch Ersetzen der **, in dem** -Klausel eine **auswählen** Anweisung mit der Klausel **WHERE 1 = 2** und Ausführen von der ergibt sich folgende Anweisung.  
  
 Metadaten sind häufig kostspielig aus der Datenquelle abgerufen werden. Aus diesem Grund sollte Treiber Metadaten zwischenspeichern, sie vom Server abzurufen, und halten, dass es während der Cursor über das Ergebnis geöffnet ist. Darüber hinaus sollten Anwendungen nur die Metadaten anfordern, unbedingt benötigten.
