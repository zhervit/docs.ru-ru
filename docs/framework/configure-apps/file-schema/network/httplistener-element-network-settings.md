---
title: Элемент <httpListener> (параметры сети)
ms.date: 03/30/2017
ms.assetid: 62f121fd-3f2e-4033-bb39-48ae996bfbd9
ms.openlocfilehash: 0054be3d2002e4ea5247f25d8094386ac7242422
ms.sourcegitcommit: 7f8eeef060ddeb2cabfa52843776faf652c5a1f5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2019
ms.locfileid: "74088380"
---
# <a name="httplistener-element-network-settings"></a>Элемент \<httpListener > (параметры сети)
Настраивает параметры, используемые классом <xref:System.Net.HttpListener>.  

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System. net >** ](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<** ](settings-element-network-settings.md) >\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<httpListener >**

## <a name="syntax"></a>Синтаксис  
  
```xml  
<httpListener  
  unescapeRequestUrl="true|false"  
/>  
```  
  
## <a name="type"></a>Type  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|унескаперекуестурл|Логическое значение, указывающее, использует ли экземпляр <xref:System.Net.HttpListener> Необработанный универсальный код ресурса (URI) без экранирования вместо преобразованного URI.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|**Элемент**|**Описание**|  
|-----------------|---------------------|  
|[Параметры](settings-element-network-settings.md)|Настраивает основные параметры сети для пространства имен <xref:System.Net>.|  
  
## <a name="remarks"></a>Заметки  
 Атрибут **унескаперекуестурл** указывает, использует ли <xref:System.Net.HttpListener> необработанный неэкранированный универсальный код ресурса (URI) вместо преобразованного универсального кода ресурса (URI), в котором преобразовываются все значения в кодировке% и выполняются другие действия нормализации.  
  
 Когда экземпляр <xref:System.Net.HttpListener> получает запрос через службу `http.sys`, он создает экземпляр строки URI, предоставленный `http.sys`, и предоставляет его в качестве свойства <xref:System.Net.HttpListenerRequest.Url%2A?displayProperty=nameWithType>.  
  
 Служба `http.sys` предоставляет две строки URI запроса:  
  
- Необработанный URI  
  
- Преобразованный URI  
  
 Необработанный URI является <xref:System.Uri?displayProperty=nameWithType>, указанным в строке запроса HTTP-запроса:  
  
 `GET /path/`  
  
 `Host: www.contoso.com`  
  
 Необработанный URI, предоставленный `http.sys` для запроса, указанного выше, — "/Пас/". Представляет строку, следующую за HTTP-командой в том виде, в котором она была отправлена по сети.  
  
 Служба `http.sys` создает преобразованный универсальный код ресурса (URI) из информации, предоставленной в запросе, используя URI, указанный в строке запроса HTTP, и заголовок узла для определения сервера-источника, на который должен быть перенаправлен запрос. Это делается путем сравнения информации из запроса с набором зарегистрированных префиксов URI. В документации по пакету SDK для HTTP-сервера этот преобразованный универсальный код ресурса (URI) называется структурой HTTP_COOKED_URL.  
  
 Чтобы иметь возможность сравнить запрос с зарегистрированными префиксами URI, необходимо выполнить некоторую нормализацию запроса. Для примера выше преобразованный URI будет выглядеть следующим образом:  
  
 `http://www.contoso.com/path/`  
  
 Служба `http.sys` объединяет значение свойства <xref:System.Uri.Host%2A?displayProperty=nameWithType> и строку в строке запроса для создания преобразованного универсального кода ресурса (URI). Кроме того, `http.sys` и класс <xref:System.Uri?displayProperty=nameWithType> также выполняет следующие действия:  
  
- Отменяет экранирование всех закодированных в процентах значений.  
  
- Преобразует символы, не входящие в набор ASCII, в кодировку UTF-16 в символьное представление. Обратите внимание, что символы UTF-8 и ANSI/DBCS поддерживаются, а также символы Юникода (Кодировка Юникода с использованием формата% Укскскскс).  
  
- Выполняет другие шаги нормализации, например сжатие пути.  
  
 Поскольку запрос не содержит никаких сведений о кодировке, используемой для значений, закодированных в процентах, возможно, вам не удастся определить правильную кодировку путем анализа значений, закодированных в процентах.  
  
 Поэтому `http.sys` предоставляет два раздела реестра для изменения процесса:  
  
|Раздел реестра .|Значение по умолчанию|Описание|  
|------------------|-------------------|-----------------|  
|EnableNonUTF8|1|Если значение равно нулю, `http.sys` принимает только URL-адреса в кодировке UTF-8.<br /><br /> Если не равен нулю, `http.sys` также принимает в запросах URL-адреса в кодировке ANSI или в кодировке DBCS.|  
|FavorUTF8|1|Если не равен нулю, `http.sys` всегда пытается декодировать URL-адрес как UTF-8. Если преобразование завершается неудачно и EnableNonUTF8 имеет ненулевое значение, HTTP. sys пытается декодировать его как ANSI или DBCS.<br /><br /> Если ноль (и EnableNonUTF8 не равен нулю), `http.sys` пытается декодировать его как ANSI или DBCS; Если это не удалось, то пытается выполнить преобразование UTF-8.|  
  
 Когда <xref:System.Net.HttpListener> получает запрос, он использует преобразованный универсальный код ресурса (URI) из `http.sys` в качестве входных данных для свойства <xref:System.Net.HttpListenerRequest.Url%2A>.  
  
 Есть необходимость в поддержке символов помимо символов и чисел в URI. Примером является следующий универсальный код ресурса (URI), который используется для получения сведений о клиенте для номера клиента «1/3812»:  
  
 `http://www.contoso.com/Customer('1%2F3812')/`  
  
 Обратите внимание на косую черту в формате URI (% 2F). Это необходимо, поскольку в данном случае символ косой черты представляет данные, а не разделитель пути.  
  
 Передача строки в конструктор URI приводит к следующему URI:  
  
 `http://www.contoso.com/Customer('1/3812')/`  
  
 Разделение пути на сегменты приведет к следующим элементам:  
  
 `Customer('1`  
  
 `3812')`  
  
 Это не цель отправителя запроса.  
  
 Если атрибут **унескаперекуестурл** имеет значение **false**, то когда <xref:System.Net.HttpListener> получает запрос, он использует необработанный универсальный код ресурса (URI) вместо преобразованного URI из `http.sys` в качестве входных данных для свойства <xref:System.Net.HttpListenerRequest.Url%2A>.  
  
 Значение по умолчанию для атрибута **унескаперекуестурл** — **true**.  
  
 Свойство <xref:System.Net.Configuration.HttpListenerElement.UnescapeRequestUrl%2A> можно использовать для получения текущего значения атрибута **унескаперекуестурл** из применимых файлов конфигурации.  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как настроить класс <xref:System.Net.HttpListener> при получении запроса на использование необработанного URI вместо преобразованного универсального кода ресурса (URI) из `http.sys` в качестве входных данных для свойства <xref:System.Net.HttpListenerRequest.Url%2A>.  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpListener  
        unescapeRequestUrl="false"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="element-information"></a>Сведения об элементе  
  
|||
|-|-|  
|Пространство имен|System.Net|  
|Имя схемы||  
|Файл проверки||  
|Может быть пустым||  
  
## <a name="see-also"></a>См. также

- <xref:System.Net.Configuration.HttpListenerElement>
- <xref:System.Net.HttpListener>
- <xref:System.Net.HttpListenerRequest.Url%2A>
- [Схема параметров сети](index.md)
