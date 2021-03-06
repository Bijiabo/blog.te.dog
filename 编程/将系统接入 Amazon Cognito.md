最近工作忙的要死要活，原本的计划是要找找时间完善一下自己那个小 SaaS 系统的登录注册机制，奈何天天忙成狗（其实不如狗），于是看下大 AWS 有什么现成的服务呢，无非是交钱嘛。于是，喵到了 Cognito。

Cognito 提供了各个开发平台的 SDK 和接口，而且连 React Native  也有专门的 SDK 和文档支持，看起来很棒的说。大致浏览了一下文档，根据了解到的信息，大致是以下步骤：

1. 移动端集成 Amazon Cognito for React Native SDK，使用自己开发的 UI 界面（风格相对统一可控），调用接口实现用户在 Cognito 中注册和登录账户，包括一些短信、邮件验证机制
2. 用户登录后，移动端拿到 Cognito 的相关 Token，进行业务逻辑请求时，请求头携带特定标记的 token 信息提交给云端
3. 云端收到请求后，解析请求头，分析是否为来自从 Cognito 注册用户的请求信息，若是，则进入下一步，若不是，则走正常的验证流程
4. 解析 token 相关数据，检测是否有注册过对应账户，若无，则进行注册，最终返回识别到的用户信息（对应到系统内）

在 github 搜索，找到了 `django-cognito-jwt` 这个库，第一眼看过去，它应该是可以完全满足我的需求的。但是实际使用过程中，遇到一些问题，卡了很久，基本上从昨晚睡前到今天晚饭。遇到的问题点大致如下，总之文档的不完善是一个大坑。

1. `COGNITO_AUDIENCE` 一开始没有搞明白是什么意思，后来搜索了一下，发现应该是对应 Cognito 后台的 App Client id
2. App 如何传递数据给云端，理论上应该是与  JWT auth 的传输方式一样，但是似乎一直卡住，后来查看 issuse 和源代码才知到，请求头中 Authorization 的起始字符需要修改为 `bearer ` 而非 `JWT `
3. token 一直解析失败，这个问题是昨晚睡前一直困扰着我的，感谢有前人在 stackoverflow 上提出过类似问题，问题在于提交的 token 应该是 Cognito 返回的 `idToken` 而非 `accessToken`，尝试修改了一下立即成功了
4. 验证用户若没有，需要自动注册并返回 user，这一步需要添加 `User.objects.get_or_create_for_cognito` 方法，我的系统先前没用使用自己的  User Model 代替 Django 本身的，所以也没有自定义 UserManager，如果因为要添加这一个方法做诸如此类的改动，感觉是没有必要的，蛮纠结的。先直接修改包的源代码调通，感觉这个地方的设计需要考虑到兼容使用者的各种应用场景，不然会有和我一样的人踩坑的

当然，也感谢 `django-cognito-jwt` 这个库文档的不完善，让我查阅了不少资料，学习到了很多知识，若不是因为遇到这个问题，可能我还一直不知道 jwt token 三段分别是代表什么意思，含义如何呢。接下来，我想也许需要修改源代码，提交一个新的 Pull Request 了。

简单修改代码，本地测试 OK，顺便改进一下文档，应该会被 merge 进去吧，[Pull Request 地址](https://github.com/LabD/django-cognito-jwt/pull/5)

## 参考文档
- [将令牌与用户池结合使用](https://docs.aws.amazon.com/zh_cn/cognito/latest/developerguide/amazon-cognito-user-pools-using-tokens-with-identity-providers.html)