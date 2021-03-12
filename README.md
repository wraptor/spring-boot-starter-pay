# spring-boot-starter-pay

集成支付接口

- payJs

## spring boot starter依赖

```xml
<dependency>
  <groupId>com.seepine</groupId>
  <artifactId>spring-boot-starter-pay</artifactId>
  <version>0.0.1</version>
</dependency>
```

## 使用配置

### 1.配置文件
application.yml
```
pay-js:
  m-ch-id: ${your mChId}
  secret: ${your secret}
  notify-url: ${your notifyUrl}
```

### 2.代码使用
注入template
```java
@Autowire
private PayJsTemplate payJsTemplate;
```

## 方法介绍
### 1.native支付（返回支付二维码）
默认回调地址
```java
PayJsRes payRes = payJsTemplate.pay(String subject, //商品标题
        String outTradeNo, //已方生成订单号
        Double amount); //金额，单位元
```
手动填写回调地址
```java
PayJsRes payRes = payJsTemplate.pay(String subject, //商品标题
        String outTradeNo, //已方生成订单号
        Double amount, //金额，单位元
        String notifyUrl); //异步通知回调地址
```
### 2.异步通知回调验签
```java
    @ResponseBody
    @PostMapping(value = "notify")
    public Object fallback(PayJsReq payJsReq){
        Boolean isSign = payJsTemplate.checkSign(payJsReq);
        //业务逻辑...
    }
```