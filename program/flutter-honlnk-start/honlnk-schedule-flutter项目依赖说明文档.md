# Flutter 第三方库依赖文档

> 本文档记录了从 Vue.js 项目迁移到 Flutter 项目时的第三方库映射关系和使用指南

## 📋 库映射关系

### Vue → Flutter 依赖库对照表

| Vue.js 库 | Flutter 对应库 | 版本 | 功能描述 |
|-----------|---------------|------|----------|
| `axios` | `dio` | ^5.9.0 | HTTP 网络请求库 |
| `dayjs` | `intl` | ^0.20.2 | 日期时间格式化和国际化 |
| `element-plus` | `Flutter Material Design` | 内置 | UI 组件库 |
| `@element-plus/icons-vue` | `flutter_svg` + `cupertino_icons` | ^2.2.1 + ^1.0.8 | 图标库 |
| `pinia` | `flutter_riverpod` | ^3.0.0 | 状态管理库 |
| `pinia-plugin-persistedstate` | `shared_preferences` | ^2.5.3 | 本地数据持久化 |
| `vue-router` | `go_router` | ^16.2.1 | 路由管理 |

## 🔧 已安装的依赖库详情

### 1. dio - HTTP 网络请求库
**替代**: axios
```yaml
dio: ^5.9.0
```

**主要功能**:
- HTTP 请求/响应拦截器
- FormData 和文件上传下载
- 请求取消和超时设置
- 全局配置和实例化

**基本用法**:
```dart
import 'package:dio/dio.dart';

final dio = Dio();

// GET 请求
Response response = await dio.get('/users');

// POST 请求
Response response = await dio.post('/users', data: {'name': 'John'});
```

### 2. intl - 国际化和日期时间处理
**替代**: dayjs
```yaml
intl: ^0.20.2
```

**主要功能**:
- 日期时间格式化
- 数字格式化
- 多语言支持
- 本地化处理

**基本用法**:
```dart
import 'package:intl/intl.dart';

// 日期格式化
final formatter = DateFormat('yyyy-MM-dd HH:mm:ss');
String formattedDate = formatter.format(DateTime.now());

// 数字格式化
final numberFormat = NumberFormat('#,###');
String formattedNumber = numberFormat.format(1234567);
```

### 3. Flutter Material Design - UI 组件库
**替代**: element-plus
```yaml
# Flutter 内置，无需额外安装
```

**主要功能**:
- Material Design 组件
- 主题系统
- 响应式布局
- 动画效果

**基本用法**:
```dart
import 'package:flutter/material.dart';

// 使用 Material 组件
ElevatedButton(
  onPressed: () {},
  child: Text('按钮'),
)

AppBar(
  title: Text('标题'),
)

Card(
  child: ListTile(
    leading: Icon(Icons.person),
    title: Text('用户'),
  ),
)
```

### 4. flutter_svg - SVG 图标支持
**替代**: @element-plus/icons-vue
```yaml
flutter_svg: ^2.2.1
cupertino_icons: ^1.0.8
```

**主要功能**:
- SVG 矢量图形渲染
- 图标主题化
- 动画支持

**基本用法**:
```dart
import 'package:flutter_svg/flutter_svg.dart';

// 使用 SVG 图标
SvgPicture.asset(
  'assets/icons/user.svg',
  width: 24,
  height: 24,
)

// 使用内置图标
Icon(Icons.home)
Icon(CupertinoIcons.heart)
```

### 5. flutter_riverpod - 状态管理
**替代**: pinia
```yaml
flutter_riverpod: ^3.0.0
```

**主要功能**:
- 类型安全的状态管理
- 自动依赖追踪
- 测试友好
- 编译时安全检查

**基本用法**:
```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

// 定义 Provider
final counterProvider = StateProvider<int>((ref) => 0);

// 在 Widget 中使用
class CounterWidget extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final count = ref.watch(counterProvider);
    
    return Text('Count: $count');
  }
}
```

### 6. shared_preferences - 本地数据持久化
**替代**: pinia-plugin-persistedstate
```yaml
shared_preferences: ^2.5.3
```

**主要功能**:
- 键值对存储
- 跨平台支持
- 异步 API
- 类型安全

**基本用法**:
```dart
import 'package:shared_preferences/shared_preferences.dart';

// 保存数据
final prefs = await SharedPreferences.getInstance();
await prefs.setString('username', 'john_doe');
await prefs.setInt('userId', 123);

// 读取数据
String? username = prefs.getString('username');
int? userId = prefs.getInt('userId');
```

### 7. go_router - 路由管理
**替代**: vue-router
```yaml
go_router: ^16.2.1
```

**主要功能**:
- 声明式路由配置
- 类型安全的路由
- 深度链接支持
- 路由守卫和中间件

**基本用法**:
```dart
import 'package:go_router/go_router.dart';

final router = GoRouter(
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => HomePage(),
    ),
    GoRoute(
      path: '/profile/:userId',
      builder: (context, state) {
        final userId = state.params['userId'];
        return ProfilePage(userId: userId);
      },
    ),
  ],
);

// 导航
context.go('/profile/123');
context.push('/settings');
```

## 🚀 使用建议

### 学习优先级
1. **Flutter Material Design** - 熟悉基础 UI 组件
2. **dio** - 掌握网络请求
3. **flutter_riverpod** - 学习状态管理模式
4. **go_router** - 理解路由导航
5. **shared_preferences** - 学习数据持久化
6. **intl** - 掌握国际化和格式化

### 项目结构建议
```
lib/
├── main.dart                 # 应用入口
├── providers/               # Riverpod providers
├── models/                  # 数据模型
├── services/               # 网络服务 (dio)
├── utils/                  # 工具类 (intl)
├── widgets/                # 可复用组件
└── pages/                  # 页面组件
```

### 最佳实践
- 使用 `dio` 时配置全局拦截器处理错误和认证
- 使用 `flutter_riverpod` 时遵循单一职责原则
- 使用 `go_router` 时定义清晰的路由结构
- 使用 `shared_preferences` 时注意数据类型转换
- 使用 `intl` 时考虑多语言支持

## 📝 变更记录

### 2025年9月16日
- ✅ 初始化 Flutter 项目
- ✅ 安装 dio ^5.9.0 (替代 axios)
- ✅ 安装 intl ^0.20.2 (替代 dayjs)
- ✅ 安装 flutter_svg ^2.2.1 (替代 @element-plus/icons-vue)
- ✅ 安装 flutter_riverpod ^3.0.0 (替代 pinia)
- ✅ 安装 shared_preferences ^2.5.3 (替代 pinia-plugin-persistedstate)
- ✅ 安装 go_router ^16.2.1 (替代 vue-router)
- ✅ 所有依赖库通过代码分析检查

## 🔗 相关链接

- [Flutter 官方文档](https://flutter.dev/docs)
- [Dio 文档](https://pub.dev/packages/dio)
- [Riverpod 文档](https://riverpod.dev/)
- [Go Router 文档](https://pub.dev/packages/go_router)
- [Material Design 组件](https://flutter.dev/docs/development/ui/widgets/material)
- [Intl 文档](https://pub.dev/packages/intl)
- [Shared Preferences 文档](https://pub.dev/packages/shared_preferences)