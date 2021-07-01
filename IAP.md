# IAP 内购

## 内购支付流程

1. 根据商品ID查询商品
2. 用查询到的商品发起IAP支付
3. 支付成功，获取App Receipt票据，服务端验证
4. 验证通过，给用户充值虚拟货币并回调给 App

    *IAP支付的机制，每次支付行为或每笔交易被认为是一个SKPaymentTransation，只有当SKPaymentTransation被finishTransaction:，这次支付（交易）行为才算是正常结束了。即使这次支付途中被中断，其实也并没有丢失。假设支付没有完成 App 就退出了（比如崩溃），那么当下次 App 重启之后，只要设置了监听addTransactionObserver:，之前被中断的支付就会接着进行。*

## 掉单可能会出现在哪些环节

1. IAP 支付过程中
2. 服务端验签过程中

    *针对第一种情况，可以在 App 一启动就设置监听，如果有未完成的支付，则会回调- (void)paymentQueue:(SKPaymentQueue *)queue updatedTransactions:(NSArray *)transactions;这个方法，在这个方法里调用接口充值。*

    *至于第二种情况，App 端需要做接口重试，设置一个重试的逻辑。，本地缓存订单状态，完成后修改*


## 参考文章

- [iOS—处理苹果内购(IAP)掉单的坑](https://www.jianshu.com/p/d8bf952a023a/)