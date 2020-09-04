
<h1 align="center">Weather</h1>

<p align="center">基于高德开放平台的 PHP 天气信息组件。</p>

## 安装

```sh
$ composer require lanxr/weather -vvv
```

## 配置

在使用本扩展之前，你需要去 [高德开放平台](https://lbs.amap.com/dev/id/newuser) 注册账号，然后创建应用，获取应用的 API Key。


## 使用

```php
use Lanxr\Weather\Weather;

$key = 'xxxxxxxxxxxxxxxxxxxxxx';

$weather = new Weather($key);
```

###  获取实时天气

```php
$response = $weather->getLiveWeather('贵阳');
```
示例：

```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "贵州",
            "city": "贵阳市",
            "adcode": "520100",
            "weather": "多云",
            "temperature": "23",
            "winddirection": "北",
            "windpower": "≤3",
            "humidity": "78",
            "reporttime": "2020-09-02 21:53:26"
        }
    ]
}
```

### 获取近期天气预报

```php
$response = $weather->getForecastsWeather('贵阳');
```
示例：

```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "forecasts": [
        {
            "city": "贵阳市",
            "adcode": "520100",
            "province": "贵州",
            "reporttime": "2020-09-02 21:53:26",
            "casts": [
                {
                    "date": "2020-09-02",
                    "week": "3",
                    "dayweather": "多云",
                    "nightweather": "多云",
                    "daytemp": "31",
                    "nighttemp": "20",
                    "daywind": "东北",
                    "nightwind": "东北",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2020-09-03",
                    "week": "4",
                    "dayweather": "中雨",
                    "nightweather": "阵雨",
                    "daytemp": "29",
                    "nighttemp": "20",
                    "daywind": "东",
                    "nightwind": "东",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2020-09-04",
                    "week": "5",
                    "dayweather": "多云",
                    "nightweather": "阵雨",
                    "daytemp": "29",
                    "nighttemp": "21",
                    "daywind": "南",
                    "nightwind": "南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                },
                {
                    "date": "2020-09-05",
                    "week": "6",
                    "dayweather": "阵雨",
                    "nightweather": "阵雨",
                    "daytemp": "27",
                    "nighttemp": "20",
                    "daywind": "南",
                    "nightwind": "南",
                    "daypower": "≤3",
                    "nightpower": "≤3"
                }
            ]
        }
    ]
}
```

### 获取 XML 格式返回值

以上两个方法第二个参数为返回值类型，可选 `json` 与 `xml`，默认 `json`：

```php
$response = $weather->getLiveWeather('贵阳', 'xml');
```

示例：

```xml
<response>
    <status>1</status>
    <count>1</count>
    <info>OK</info>
    <infocode>10000</infocode>
    <lives type="list">
        <live>
            <province>贵州</province>
            <city>贵阳市</city>
            <adcode>520100</adcode>
            <weather>多云</weather>
            <temperature>23</temperature>
            <winddirection>北</winddirection>
            <windpower>≤3</windpower>
            <humidity>78</humidity>
            <reporttime>2020-09-02 21:53:26</reporttime>
        </live>
    </lives>
</response>
```

### 参数说明

```
array | string getLiveWeather(string $city, string $format = 'json')
array | string getForecastsWeather(string $city, string $format = 'json')
```

> - `$city` - 城市名/[高德地址位置 adcode](https://lbs.amap.com/api/webservice/guide/api/district)，比如：“贵阳” 或者（adcode：520100）；
> - `$format` - 输出的数据格式，默认为 json 格式，当 output 设置为 “`xml`” 时，输出的为 XML 格式的数据。


### 在 Laravel 中使用

在 Laravel 中使用也是同样的安装方式，配置写在 `config/services.php` 中：

```php
    .
    .
    .
     'weather' => [
        'key' => env('WEATHER_API_KEY'),
    ],
```

然后在 `.env` 中配置 `WEATHER_API_KEY` ：

```env
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxx
```

可以用两种方式来获取 `Lanxr\Weather\Weather` 实例：

#### 方法参数注入

```php
    .
    .
    .
    public function show(Weather $weather) 
    {
        $response = $weather->getLiveWeather('贵阳');
    }
    .
    .
    .
```

#### 服务名访问

```php
    .
    .
    .
    public function show() 
    {
        $response = app('weather')->getLiveWeather('贵阳');
    }
    .
    .
    .

```

## 参考

- [高德开放平台天气接口](https://lbs.amap.com/api/webservice/guide/api/weatherinfo/)

## License

MIT
