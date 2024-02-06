geo_location_checker=http://ip-api.com/json/?lang=zh-CN, https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IP_API.js

http://ip-api.com/json/?lang=zh-CN 会自动获取节点的信息返回的数据格式为

```js
{
  "status": "success",  // 状态
  "country": "日本",     // 国家
  "countryCode": "JP",  // 国家对应的代码
  "region": "27",       // 地区
  "regionName": "Ōsaka", // 地区名称
  "city": "大阪市",      // 城市
  "zip": "",             
  "lat": 34.6937,          // 纬度
  "lon": 135.5022,         // 经度
  "timezone": "Asia/Tokyo", // 时区
  "isp": "xTom Limited", // 互联网服务供应商
  "org": "Xtom",         
  "as": "AS4785 xTom",
  "query": "45.8.220.56" // ip
}
```

逗号后面的这一串https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IP_API.js，表示解析前面接口获取的数据