---
title: Ведение журналов с использованием эластичного стека
description: Ведение журналов с помощью эластичного стека, Logstash и Kibana
ms.date: 09/23/2019
ms.openlocfilehash: 989834925bc08541bf484e1a4567a56ac324872f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2019
ms.locfileid: "73841741"
---
# <a name="logging-with-elastic-stack"></a>Ведение журналов с использованием эластичного стека

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Существует множество хороших средств централизованного ведения журналов, которые изменяются по затратам от бесплатных средств с открытым исходным кодом до более дорогостоящих вариантов. Во многих случаях бесплатные инструменты должны быть как или более надежными, чем оплаченные предложения. Одним из таких инструментов является сочетание трех компонентов с открытым исходным кодом: Эластичный Поиск, Logstash и Kibana.
Вместе эти средства называются стеком эластичных баз данных или ELK.

## <a name="what-are-the-advantages-of-elastic-stack"></a>Каковы преимущества эластичного стека?

Эластичный стек обеспечивает централизованное ведение журналов с экономичным, масштабируемым и облачным способом. Его пользовательский интерфейс упрощает анализ данных, позволяя тратить время на получение ценных сведений из данных вместо борьбы с интерфейсом неуклюжим. Он поддерживает широкий спектр входных данных, так как распределенное приложение охватывает больше и разных типов служб, поэтому вы можете продолжать работать с данными журналов и метрик в системе. Эластичный стек также поддерживает быстрый поиск даже в больших наборах данных, что делает возможным даже для больших приложений запись подробных данных в журнал и по-прежнему иметь возможность видеть их в удобном для себя виде.

## <a name="logstash"></a>Logstash

Первый компонент — [Logstash](https://www.elastic.co/products/logstash). Это средство используется для сбора данных журнала из большого спектра различных источников. Например, Logstash может считывать журналы с диска, а также отправлять сообщения из библиотек ведения журналов, например [Serilog](https://serilog.net/). Logstash может выполнять некоторую базовую фильтрацию и расширение журналов по мере их поступления. Например, если журналы содержат IP-адреса, Logstash можно настроить для выполнения географического поиска и получения страны или даже города происхождения сообщения.

Serilog — это библиотека ведения журналов для языков .NET, позволяющая выполнять параметризованное ведение журнала. Вместо создания текстового сообщения журнала, включающего поля, параметры хранятся отдельно. Это обеспечивает более интеллектуальную фильтрацию и поиск. Пример конфигурации Serilog для записи в Logstash показан на рис. 7-2.

```csharp
var log = new LoggerConfiguration()
         .WriteTo.Http("http://localhost:8080")
         .CreateLogger();
```

**Рис. 7-2** Serilog config для записи сведений журнала непосредственно в logstash по протоколу HTTP

Logstash будет использовать конфигурацию, подобную показанной на рис. 7-3.

```
input {
    http {
        #default host 0.0.0.0:8080
        codec => json
    }
}

output {
    elasticsearch {
        hosts => "elasticsearch:9200"
        index=>"sales-%{+xxxx.ww}"
    }
}
```

**Рис. 7-3** . Конфигурация Logstash для использования журналов из Serilog

Для сценариев, в которых не требуется много операций с журналами, существует альтернатива [Logstash, известного как](https://www.elastic.co/products/beats)незначительное. Ритм — это семейство средств, которое может собирать разнообразные данные из журналов в данные сети и сведения о времени работы. Многие приложения будут использовать как Logstash, так и ритмы.

После того, как журналы собраны с помощью Logstash, им нужно поместить их в любое место. Хотя Logstash поддерживает множество различных выходов, одна из самых интересных — эластичный Поиск.

## <a name="elastic-search"></a>Эластичный Поиск

Эластичный Поиск — это мощная поисковая система, которая может индексировать журналы по мере их поступления. Он позволяет быстро выполнять запросы к журналам. Эластичный Поиск может обрабатывать огромные объемы журналов, и в крайних случаях их можно масштабировать на нескольких узлах.

Сообщения журнала, которые были созданы для хранения параметров или которых были разделены с помощью обработки Logstash, можно запрашивать напрямую, так как Elasticsearch сохраняет эти сведения.

Запрос, выполняющий поиск 10 первых страниц, посещенных `jill@example.com`, отображается на рис. 7-4.

```
"query": {
    "match": {
      "user": "jill@example.com"
    }
  },
  "aggregations": {
    "top_10_pages": {
      "terms": {
        "field": "page",
        "size": 10
      }
    }
  }
```

**Рис. 7-4** . запрос Elasticsearch для поиска 10 ведущих страниц, посещенных пользователем

## <a name="visualizing-information-with-kibana-web-dashboards"></a>Визуализация информации с помощью веб-панелей мониторинга Kibana

Последним компонентом стека является Kibana. Это средство используется для предоставления интерактивных визуализаций на веб-панели мониторинга. Панели мониторинга могут создаваться даже пользователями, которые не являются техническими. Большинство данных, находящихся в Elasticsearch индексе, могут быть добавлены на панели мониторинга Kibana. Отдельные пользователи могут иметь разную панель мониторинга, и Kibana обеспечивает эту настройку, позволяя пользователям просматривать панели мониторинга.

## <a name="installing-elastic-stack-on-azure"></a>Установка эластичного стека в Azure

Эластичный стек можно установить в Azure несколькими способами. Как всегда, можно [подготавливать виртуальные машины и устанавливать эластичный стек на них напрямую](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-elasticsearch). Этот вариант является предпочтительным для некоторых опытных пользователей, так как он обеспечивает наивысшую степень настройки. При развертывании на основе инфраструктуры в качестве службы вы узнаете о значительных затратах на управление, которые применяют этот путь, чтобы стать владельцем всех задач, связанных с инфраструктурой, таких как обеспечение безопасности компьютеров и обновление исправлений.

Параметр с меньшими издержками заключается в использовании одного из многих контейнеров DOCKER, для которых уже настроен эластичный стек. Эти контейнеры можно удалить в существующий кластер Kubernetes и запустить вместе с кодом приложения. Контейнер [себп/Elk](https://elk-docker.readthedocs.io/) — это хорошо документированный и протестированный контейнер эластичного стека.

Другой вариант — [недавно объявленное предложение Elk как услуга](https://devops.com/logz-io-unveils-azure-open-source-elk-monitoring-solution/).

## <a name="references"></a>Ссылки

- [Установка эластичного стека в Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-elasticsearch)

>[!div class="step-by-step"]
>[Назад](observability-patterns.md)
>[Вперед](monitoring-azure-kubernetes.md)
