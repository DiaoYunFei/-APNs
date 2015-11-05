-APNs
APNs : Apple Push No-fica-on server 苹果推送通知服务
苹果的APNs允许设备和苹果的推送通知服务 器保持连接,支持开发者推送消息给用户设 备对应的应用程序。
常见用途
常常用于消息的订阅 
1、电商:我有新品发布啦!我的某某产品在搞活动,五折优惠! 
2、新闻媒体:今天又有新鲜事发生了!
3、社交:某某给你留言了! 某某对你的文章发表评论了!

实现消息推送的步骤 
1、注册:为应用程序申请消息推送服务。此时你的设备会向APNs服务器发送注册请求。 
2、APNs服务器接收请求,并将deviceToken返给你设备上的应用程序 
3、客户端应用程序将deviceToken发送给后台服务器程序,后台接收并储存。 
4、后台服务器向APNs服务器发送推送消息
5、APNs服务器将消息发给deviceToken对应设 备上的应用程序

UIApplica-on与UIApplica-onDelegate UIApplica-on的核心作用是提供IOS程序运行期间的控制和协作工作。
UIApplica-on的实例会被赋予一个代理对象 (UIApplica-onDelegate),以处理应用程序 的生命周期事件,系统事件。

远程消息注册 //注册远程消息推送
[applica-on registerForRemoteNo-fica-onTypes:
UIRemoteNo-fica-onTypeAlert | UIRemoteNo-fica-onTypeBadge | UIRemoteNo-fica-onTypeSound];


iOS8 注册推送
[applica-on registerUserNo-fica-onSeKngs: [UIUserNo-fica-onSeKngs seKngsForTypes: 
    (UIUserNo-fica-onTypeSound | UIUserNo-fica-onTypeAlert | UIUserNo-fica-onTypeBadge) categories:nil]];
[applica-on registerForRemoteNo-fica-ons];


注册成功
-(void)applica-on:(UIApplica-on *)applica-on didRegisterForRemoteNo-fica-onsWithDeviceT oken:(NSData *)deviceToken;
1、注册成功会弹出提示框征求用户的同意 
2、当用户选择允许之后会在这个方法里取得设备的deviceToken,然后发送给服务器
3、测试环境与发布环境所连接的服务器地址 是不同的,所获取到的deviceToken值也是不 同的。deviceToken与应用无关。

注册失败
-  (void)applica-on:(UIApplica-on *)applica-on didFailToRegisterForRemoteNo-fica-onsWith Error:(NSError *)error;
失败原因: 
1、当用户选择不允许的时候会执行此方法 
2、当使用模拟器的时候会执行此方法 
3、证书问题

收到远程消息
-  (void)applica-on:(UIApplica-on *)applica-on didReceiveRemoteNo-fica-on:(NSDic-onary *)userInfo;
想要收到推送消息,就必须要有后台服务器 向APNs服务器发请求。
1、公司自己开发后台服务器程序
2、采用第三方的后台服务程序,比如:百度 云推送
